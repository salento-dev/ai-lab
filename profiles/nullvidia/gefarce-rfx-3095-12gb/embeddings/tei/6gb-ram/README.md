# GeFarce embeddings department

Semantic vectors for search/RAG using Text Embeddings Inference (TEI). Example target: Linux x86_64, 6 GB system RAM, a real supported NVIDIA GPU and NVIDIA Container Toolkit. Nullvidia has no real CUDA capability; check [TEI hardware support](https://huggingface.co/docs/text-embeddings-inference/supported_models) when adapting this.

## Run

```bash
cp .env.example .env
docker compose --env-file .env up -d
docker compose logs --tail=30 embeddings
curl --fail http://localhost:8081/embed \
  -H 'Content-Type: application/json' \
  -d '{"inputs":["The GPU is warm.","The graphics card is hot."]}'
```

Wait for model loading before sending the request. Expect two numeric vectors.

[BAAI/bge-small-en-v1.5](https://huggingface.co/BAAI/bge-small-en-v1.5) is an English embedding model: 384 dimensions and a 512-token sequence limit. TEI runs it in float16; client batches are capped at eight. Model files download to a Docker volume.

This serves vectors, not a vector database or a complete RAG application. For retrieval, follow the model card's query instructions.

No memory or throughput measurements. The version tag and model revision are not immutable; record resolved artifacts after testing. Run examples separately to avoid competing for VRAM.

[TEI deployment and API](https://huggingface.co/docs/text-embeddings-inference/quick_tour).
