# LuxTTS

Voice cloning in Google Colab — clone any voice from a short audio sample, generate speech from text, no local GPU required.

## Problem

Voice cloning typically requires expensive GPU hardware, complex setup, and ML expertise. The goal: make it accessible to anyone with a Google account. This guide walks through setting up LuxTTS in Colab, configuring the cloning parameters, and generating high-quality speech output — all in the browser.

## What You Get

- **Voice cloning** from a 5–20 second audio sample
- **Text-to-speech** generation in the cloned voice
- **Configurable output** — volume, speed, quality, smoothing
- **One-click download** of the generated audio

## Quick Start

1. Open [Google Colab](https://colab.research.google.com)
2. Paste the code from `Voice Clone Demo`
3. Upload a reference audio file (WAV or MP3)
4. Edit the text and settings
5. Run — download `output.wav` when done

## Pipeline

```
Reference audio → encode prompt → configure settings → generate speech → output.wav
```

| Step | What Happens | Time |
|------|-------------|------|
| Setup | Clone repo, install deps, K2 for CUDA | ~2 min |
| Model load | Load LuxTTS weights | 30–60 sec |
| Encode | Process reference audio into voice embedding | ~10 sec |
| Generate | Synthesise speech from text | 30 sec – 2 min |

## Configuration

| Parameter | Default | What It Does |
|-----------|---------|-------------|
| `rms` | 0.01 | Volume — increase for louder output |
| `t_shift` | 0.9 | Quality — higher = better quality |
| `num_steps` | 4 | Processing depth — 3–4 is fast, 6+ is high quality |
| `speed` | 1.0 | Speech rate — 0.5 (slow) to 2.0 (fast) |
| `return_smooth` | False | Smoothing — True = smoother, False = clearer |
| `ref_duration` | 10000 | Reference audio duration (ms) — lower = faster |

### Recommended Settings

| Goal | Settings |
|------|----------|
| Speed | `num_steps=3`, `ref_duration=5000` |
| Quality | `num_steps=6+`, `t_shift=0.95` |
| Clarity | `return_smooth=False`, `t_shift=0.85` |
| Smoothness | `return_smooth=True`, `t_shift=0.95` |

## Input/Output

| | Details |
|--|--------|
| **Input** | WAV or MP3, 5–20 seconds, clear audio preferred |
| **Output** | `output.wav`, 48kHz PCM, duration matches text length |

## Requirements

- Google account (for Colab)
- GPU runtime enabled in Colab (Runtime → Change runtime type → T4 GPU)
- A reference audio file

## Troubleshooting

| Problem | Fix |
|---------|-----|
| CUDA out of memory | Switch to `device='cpu'`, reduce `ref_duration` to 5000 |
| Audio has artifacts | Increase `ref_duration` to 15000, reduce `rms` to 0.005 |
| Output sounds robotic | Increase `num_steps` to 6+, set `return_smooth=True` |
| Poor cloning quality | Use cleaner reference audio (5+ seconds, no background noise) |

## Ethical Use

- Only clone voices with the speaker's consent
- Disclose when audio is AI-generated
- Don't use for impersonation or deception

## Tech Stack

- **LuxTTS** — voice cloning model ([ysharma3501/LuxTTS](https://github.com/ysharma3501/LuxTTS))
- **K2** — CUDA acceleration for faster inference
- **soundfile** — audio I/O
- **Google Colab** — free GPU environment

## References

- [LuxTTS repository](https://github.com/ysharma3501/LuxTTS)
- [LuxTTS on Hugging Face](https://huggingface.co/YatharthS/LuxTTS)

## License

MIT
