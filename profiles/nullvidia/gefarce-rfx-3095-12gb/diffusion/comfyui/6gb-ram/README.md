# GeFarce diffusion department

Manual setup for the fictional [RFX 3095](../../../README.md): Linux, 6 GB installed system RAM, a real NVIDIA GPU and compatible CUDA PyTorch. Not hardware-tested; no measured memory requirement.

## Start

Install ComfyUI outside this repository using the [official manual guide](https://docs.comfy.org/installation/manual_install), including its Python environment, CUDA PyTorch and requirements. This runtime uses Python; repository validation does not.

Download `v1-5-pruned-emaonly.safetensors` from the [SD 1.5 model repository](https://huggingface.co/stable-diffusion-v1-5/stable-diffusion-v1-5) into the ComfyUI installation's `models/checkpoints/`.

From that installation, with its environment active:

```bash
python main.py --listen 127.0.0.1 --port 8188
```

Open http://localhost:8188. Load a basic SD 1.5 text-to-image workflow from [Templates](https://docs.comfy.org/interface/features/template), select the downloaded checkpoint and use the settings below. Queue one image; check the output preview and terminal for errors. No custom nodes needed.

## Imaginary text-to-image recipe

| Setting | Example |
| --- | --- |
| Checkpoint | `v1-5-pruned-emaonly.safetensors` |
| Resolution | 512 × 512 |
| Steps | 20 |
| Sampler / scheduler | Euler / normal |
| CFG | 7 |
| Batch size | 1 |
| Seed | 13337 |
| Prompt | A GPU cooled by a tiny desk fan, dramatic product photography |
| Negative prompt | fire, smoke, melted PCIe slot |
| Precision / offload | ComfyUI defaults; inspect startup logs for actual choices |
| Generation time / memory usage | Not measured |

For a real contribution, record the ComfyUI commit and PyTorch/driver versions and export the workflow JSON. Keep checkpoints and generated images local. Load temperature remains: yes.
