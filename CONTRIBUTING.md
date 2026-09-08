# Contributing

Got a local AI setup working? Share the configuration and explain how to use it. Fixes and README improvements are welcome too. No benchmarks or PR template required.

## Where it goes

```text
profiles/<vendor>/<device>/<workload>/<runtime-or-stack>/[<system-profile>/]
```

Use lowercase kebab-case names, including accelerator memory when useful. Add a variant such as `6gb-ram` only if it changes the setup. Choose the workload by task using the [root README](README.md). Other workloads can follow real contributions. Create only necessary directories. Keep model details in the README.

The temporary [Nullvidia profile](profiles/nullvidia/gefarce-rfx-3095-12gb/) shows the idea. Replace the jokes and placeholders with your actual setup.

## What to include

Give each setup a short `README.md` with:

- Hardware, installed RAM and VRAM/unified memory, OS, and relevant driver/runtime versions used.
- External model source and exact file or revision, with format/quantization when relevant.
- Installation, startup, important settings, and a quick way to check that it works.
- What you tried, limitations, and anything unverified.

Include configuration files needed to reproduce it. For Compose, keep `compose.yaml` and a safe `.env.example` alongside the README. Native installs and other launch methods are fine.

For LLMs, mention context size and GPU offload. For diffusion, mention resolution, steps, sampler and batch size when relevant. A few lines or a small table are enough.

For audio, mention STT/TTS, language, sample rate and precision. For vision, describe the task and image input. For embeddings, include vector dimensions, input limits and batch settings. Document RAM/VRAM requirements if known; do not turn guesses into requirements.

Performance measurements are optional. If shared, explain how you obtained them and distinguish installed memory from observed usage. Unknown values can stay unknown.

Link new setups from the root README. Describe what changed and what you tried in the PR, in your own words.

## Keep out of Git

Do not commit weights, checkpoints, datasets, caches, generated media, secrets, credentials, or private data. Ignored local `.env` and model directories are fine.

Only share material you have permission to contribute. Preserve licenses and attribution; do not include unauthorized content or instructions for bypassing access restrictions. For sensitive issues, see [SECURITY.md](SECURITY.md).

## Quick checks

For Compose, run from the setup directory:

```bash
docker compose --env-file .env.example -f compose.yaml config --quiet
```

If installed, `yamllint .` can catch YAML mistakes. Check links and files proposed for Git. CI checks Compose syntax, not GPU compatibility.
