# GeFarce audio department

Speech-to-text with whisper.cpp. Example target: Linux x86_64, 6 GB system RAM, a real NVIDIA CUDA GPU and NVIDIA Container Toolkit. Nullvidia is fictional; usage and performance are unmeasured.

## Run

Download `ggml-base.bin` from [the upstream model collection](https://huggingface.co/ggerganov/whisper.cpp/tree/main) into `models/`. This is multilingual Whisper base in GGML format, not GGUF.

```bash
cp .env.example .env
mkdir -p models input
# Put your model in models/ and your own audio at input/recording.mp3.
ffmpeg -i input/recording.mp3 -ar 16000 -ac 1 -c:a pcm_s16le input/desk-fan.wav
docker compose --env-file .env run --rm transcribe
```

Requires Docker Compose and host FFmpeg. The transcript appears in the terminal. If all you recorded was a fan, do not expect a TED talk.

Settings: automatic language detection, four CPU threads, CUDA offload, original model precision. The input is 16 kHz mono PCM16 WAV. Edit filenames and language in `.env`.

The image tag moves; pin a verified digest when recording your real setup. No measured RAM/VRAM requirement is claimed.

[Upstream usage and Docker images](https://github.com/ggml-org/whisper.cpp).
