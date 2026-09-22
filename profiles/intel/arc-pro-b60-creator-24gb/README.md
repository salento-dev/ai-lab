# Intel Arc Pro B60 Creator · 24 GB

Real hardware profile: ASRock **Intel Arc Pro B60 Creator 24GB** workstation
GPU (Xe2-HPG "Battlemage"), running llama.cpp on the SYCL / oneAPI Level Zero
backend inside Docker, Linux host.

| Spec | Value |
| --- | --- |
| GPU die | Intel Arc Pro B60 (BMG-G21) |
| Memory | 24 GB GDDR6, 192-bit, ~456 GB/s |
| AI engines | 160 XMX |
| Clock | 2000 MHz base / 2400 MHz boost |
| Interface | PCIe 5.0 |
| Host RAM | 16 GB (system profile; confirm on your machine) |

Spec sources: [Intel spec page](https://www.intel.com/content/www/us/en/products/sku/243916/intel-arc-pro-b60-graphics/specifications.html),
[TechPowerUp](https://www.techpowerup.com/gpu-specs/arc-pro-b60.c4350),
[ASRock product page](https://www.asrock.com/Graphics-Card/Intel/Intel+Arc+Pro+B60+Creator+24GB/).

## Setups

Single-model variants of one llama-swap stack, one directory per model:

- [LLM / llama-swap — Qwen3.8 27B Intel-Arc-Tuned Q4_K](llm/llama-swap/16gb-ram/qwen3-8-27b-arc-tuned/)
- [LLM / llama-swap — Qwen3.5 27B Q4_K_M](llm/llama-swap/16gb-ram/qwen3-5-27b/)
- [LLM / llama-swap — Qwen3-Coder 30B A3B UD Q4_K_XL](llm/llama-swap/16gb-ram/qwen3-coder-30b-a3b/)
- [LLM / llama-swap — GPT-OSS 20B Q4_K_M](llm/llama-swap/16gb-ram/gpt-oss-20b/)
- [LLM / llama-swap — Qwen3.6 35B A3B UD Q3_K_XL](llm/llama-swap/16gb-ram/qwen3-6-35b-a3b/)
- [LLM / llama-swap — DeepSeek R1 Distill Qwen 32B Q4_K_M](llm/llama-swap/16gb-ram/deepseek-r1-distill-qwen-32b/)
- [LLM / llama-swap — Devstral Small 2 24B Instruct Q5_K_M](llm/llama-swap/16gb-ram/devstral-small-24b/)
- [LLM / llama-swap — Magistral Small 2506 Q5_K_M](llm/llama-swap/16gb-ram/magistral-small-2506/)
- [LLM / llama-swap — Qwen3 30B A3B Instruct 2507 Q4_K_M](llm/llama-swap/16gb-ram/qwen3-30b-a3b-instruct/)
- [LLM / llama-swap — Qwen3.6 35B A3B Uncensored Q4_K_M](llm/llama-swap/16gb-ram/qwen3-6-35b-a3b-uncensored/)
- [LLM / llama-swap — Gemma 4 26B A4B IT UD Q4_K_M](llm/llama-swap/16gb-ram/gemma-4-26b-a4b-it/)

## Runtime notes

- Image `ghcr.io/mostlygeek/llama-swap:intel` bundles llama.cpp built for
  Intel Arc. GPU access is via the SYCL / Level Zero backend
  (`ONEAPI_DEVICE_SELECTOR=level_zero:0`, `ZES_ENABLE_SYSMAN=1`) with
  `/dev/dri` passed into the container; `GGML_VK_VISIBLE_DEVICES=1` is kept
  from the original stack.
- `group_add` IDs (44 = render on many distros, 990 = custom) are host
  specific; check `/dev/dri` permissions on your machine and adjust.
- Each stack is standalone and exposes port `11434` (Ollama-compatible
  endpoint). The original multi-model stack also joined an external
  `ollama-network` and exposed port `5900` (purpose unknown); neither is
  reproduced here. Run one stack at a time.
- Configurations were transcribed from the owner's running 11-model stack;
  this repository has not re-verified them. GPU memory usage and throughput
  are unmeasured.
