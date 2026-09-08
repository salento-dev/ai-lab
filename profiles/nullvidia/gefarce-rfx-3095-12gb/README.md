# Nullvidia GeFarce RFX 3095 · 6 GB system RAM

Fictional example hardware. All specs and performance below are jokes, not measurements or compatibility claims.

| Spec | Value |
| --- | --- |
| Memory | 12 GB GDDR6X |
| Cores | 13,337 |
| Tensor cores | 404 |
| Ray cores | 69 |
| Memory bus | 384-bit |
| TDP | 420 W |
| Interface | PCIe 4.0 x16 |
| Backend | “CUDA-compatible-ish” |
| Throughput | 42 tok/s |
| Load temperature | yes |

## Example setups

- [LLM / llama.cpp](llm/llama-cpp/6gb-ram/): illustrative Compose setup; bring a real GPU and model.
- [Diffusion / ComfyUI](diffusion/comfyui/6gb-ram/): manual recipe for rendering the cooling system we deserve.
- [Audio / whisper.cpp](audio/whisper-cpp/6gb-ram/): transcribe speech, or the fan's resignation letter.
- [Vision / Ollama](vision/ollama/6gb-ram/): image descriptions with Gemma 3 4B.
- [Embeddings / TEI](embeddings/tei/6gb-ram/): semantic vectors for search and RAG.

The examples target Linux with 6 GB installed system RAM and a real supported NVIDIA GPU with 12 GB VRAM in place of Nullvidia. GPU setups require a compatible driver and NVIDIA Container Toolkit for Docker. Run one stack at a time; stop servers before switching. Memory consumption and performance are unmeasured. Image/model tags are illustrative defaults; record exact versions after testing.

Use this profile as a starting point for your own hardware setup. It is not runnable as-is. This temporary example will be removed once real setups populate the catalog.
