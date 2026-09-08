# ai-lab agent instructions

This is a community collection of local AI setups. Favor useful configurations and concise READMEs. Benchmarks are optional.

Paths below are relative to the repository root. Read CONTRIBUTING.md for contribution conventions.

## Add or update a setup

1. Use `profiles/<vendor>/<device>/<workload>/<runtime-or-stack>/[<system-profile>/]`. Create only necessary directories. The fictional Nullvidia profile lives in this same structure as a temporary example, to be removed once real setups populate the catalog.
2. Include a short README with hardware, environment, external model references, startup, settings, and limitations. Include Compose and a safe environment example only when used.
3. Describe what was actually tried. Never invent tests or measurements. Label fictional specs as jokes.
4. Link new real setups from the root README. Keep changes focused.

Workloads describe the task: `llm` for text generation, `diffusion` for image generation, `audio` for STT/TTS and audio, `vision` for image understanding, and `embeddings` for semantic vectors. A runtime can appear under different workloads. Other workloads should follow actual contributions.

## Soft repository review

When asked to review or before finishing changes:

- Inspect changed and new files: directory names, READMEs, links, and consistency with CONTRIBUTING.md.
- Look for accidentally included weights, datasets, generated media, secrets, and large artifacts in files proposed for Git. Ignored local models and `.env` files are allowed.
- For each changed Compose setup, run `docker compose --env-file .env.example -f compose.yaml config --quiet` from its directory.
- Run `yamllint .` if installed. Do not install tools solely for this optional check.
- Report concrete issues and checks not run. Missing performance data is fine; syntax does not prove hardware compatibility.

This workflow is guidance, not an automatic policy gate. Review requests do not authorize edits; when implementing changes, fix relevant issues within scope.

Keep secrets and model artifacts out of committed files and preserve licenses and attribution. When changing conventions, update affected documentation, examples, and CI together.
