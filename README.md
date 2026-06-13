# Automatic Object Removal via Click-Based Inpainting

Computer Vision - Sapienza Università di Roma - A.A. 2025–2026
Omri Ben Zion · Johannes Erhard

Remove a person or object from a photo with a single click — no mask drawing, no prompt writing. The background fills in automatically.

## Pipeline

```
click → SAM (mask) → BLIP-2 (caption) → Improved RePaint on SD 1.5 → result
```

## Improved RePaint

We extend the RePaint resampling strategy with 8 refinements that recover quality on a small frozen SD 1.5 backbone, with no extra training:

- coherent noise
- selective resampling
- guidance ramp (CFG 5 → 9)
- progressive mask
- Laplacian pyramid blending
- SDEdit refinement pass
- deterministic VAE encoding
- default negative prompt

## Results

100 COCO 2017 val images (person), 3 seeds each.

| Pipeline | LPIPS ↓ | Mask-LPIPS ↓ | CLIP ↑ |
|---|---|---|---|
| Baseline (SD Inpaint) | 0.1598 | 0.3534 | 0.2405 |
| Vanilla RePaint | 0.0994 | 0.3382 | 0.2438 |
| **Improved RePaint (ours)** | **0.0905** | **0.3083** | 0.2425 |

## Run

Open `final_cv.ipynb` in Kaggle and run all cells (GPU required).

## References

- Rombach et al. — [High-Resolution Image Synthesis with Latent Diffusion Models](https://arxiv.org/abs/2112.10752)
- Lugmayr et al. — [RePaint: Inpainting using Denoising Diffusion Probabilistic Models](https://arxiv.org/abs/2201.09865)