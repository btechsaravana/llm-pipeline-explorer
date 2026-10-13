# LLM Pipeline Explorer

**An interactive, animated map of how a question becomes an answer from your own data.**
It runs from raw training text through the transformer, your document pipeline and retrieval, to the final streamed answer.

One self-contained HTML file. No build step, no dependencies, no backend.

<!-- After enabling GitHub Pages, put your link here:
**Live demo:** https://YOUR-USERNAME.github.io/YOUR-REPO/
-->

---

## What it shows

Three colour-coded paths, 25 clickable stages, one running example (e-Sevai invoices and the question *"How much did Murugan e-Sevai pay in March?"*).

| Path | Colour | Question it answers | Stages |
|---|---|---|---|
| **A · Model build** | Violet | How was the LLM itself made? | Raw data, tokenizer, embeddings and position, self-attention, next-token probabilities, pretraining, SFT, alignment |
| **B · Your data prep** | Teal | How is *my* data made searchable? | Parse, clean, chunk, metadata, embed, index (HNSW / BM25), store |
| **C · Question time** | Amber | What happens on each request? | Question, rewrite, embed query, retrieve, hybrid merge and filter, rerank, prompt, prefill and KV cache, decode and sampling, answer |

A's trained model is what runs in C8–C9. B's vectors and index are what C3–C5 search.

## Features

- **Animated journey.** Press *Play* and a dot travels A → B → C while a caption shows how the example data changes at every stage.
- **A live lab at every stage.** Sliders and toggles for the parameters that matter, with results recomputed in the page:
  - tokenizer on your own text (including Tamil)
  - attention heatmap with a causal-mask toggle
  - learning-rate loss curve and training-compute estimate
  - chunk size, overlap and structure-aware splitting
  - HNSW search animation and BM25 inverted index
  - dense, BM25, hybrid (alpha), metadata filters and reranking, side by side
  - prompt token budget, KV-cache memory and GPU sizing
  - temperature, top-p and top-k sampling
- **Type your own question** in stage C1 and watch every later stage change. Ask something the documents cannot answer and the system refuses instead of guessing.
- **Per-stage notes:** what happens, parameters that matter (typical values and effects), and system-level concerns.
- Deep links to any stage, e.g. `index.html#C4`. Keyboard arrows move between stages.
- Light and dark themes, phone-friendly, respects reduced-motion settings.

## Run it

Open `index.html` in any modern browser. That is all.

Fonts load from Google Fonts. Offline, the page falls back to system fonts and still works.

## Host it free (GitHub Pages)

1. Push this repository to GitHub.
2. **Settings → Pages → Build and deployment → Deploy from a branch.**
3. Choose branch `main`, folder `/ (root)`, and save.
4. After about a minute the site is live at `https://<username>.github.io/<repo>/`.

## What is real and what is simulated

Computed live in the page:
cosine similarity, BM25, hybrid score fusion, metadata filtering, token-budget arithmetic, KV-cache and weight memory, training FLOPs and the softmax and sampling maths.

Simplified stand-ins, labelled in the page:
- the embedding is a toy 8-number vector with named dimensions (real models use 384–3,072 unnamed numbers)
- attention weights, the loss curve, the cross-encoder reranker and the final answer are small rule-based simulations, not real model output

Numbers such as GPU throughput are rough teaching estimates, not benchmarks.

## Project layout

```
.
├── index.html   # the whole app: markup, styles and scripts
└── README.md
```

## Learn more

Good open-source starting points for each path:

- **A:** `karpathy/nn-zero-to-hero`, `karpathy/nanoGPT`, `rasbt/LLMs-from-scratch`
- **B and C:** `UKPLab/sentence-transformers`, `facebookresearch/faiss`, `pgvector/pgvector`, `NirDiamant/RAG_Techniques`
- **Serving and evaluation:** `vllm-project/vllm`, `explodinggradients/ragas`

## Contributing

Issues and pull requests are welcome, for example more stages, other example datasets or translations.

## License

Choose a licence before sharing widely, for example MIT. Add a `LICENSE` file to match.
