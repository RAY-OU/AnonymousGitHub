# GradHarmon — Supplementary Qualitative Results

We provide additional qualitative evidence to address the AC and reviewers' concerns regarding (1) the distinct visual roles of SGB and SPA, and (2) whether GradHarmon's texture improvements are genuine rather than noise or oversharpening.

---

## 1. Qualitative Ablation: SGB vs. SPA

**Setup.** Four-column comparisons on the same prompt: DMD2 baseline / +SGB only / +SPA only / Full GradHarmon. All models share the same base architecture (QwenImage) and training data; only the loss components differ.

![Qualitative Ablation](rebutall_ablation_p1.png)

**DMD2 baseline** (1st column) exhibits two coupled degradations from spectral collapse: fine textures are smoothed into featureless blobs (lion fur, Avatar skin paint, kangaroo hair all lack detail), and colors are pushed toward over-saturation (the lion's mane is unnaturally red, the sunset sky is overly orange).

**+SGB only** (2nd column) recovers texture detail — lion fur becomes strand-level, Avatar skin gains visible pores, kangaroo fur shows individual hairs — but colors remain over-saturated. This matches Table 2: SGB raises ELV from 0.0074→0.0118 and WER from 0.666→1.147 (texture metrics), while PickScore improves only modestly.

**+SPA only** (3rd column) corrects color distribution — the lion's red tones become natural, Avatar skin returns to balanced blue, sunset shows realistic gradients — but textures remain somewhat smooth. This matches Table 2: SPA improves PickScore from 0.2192→0.2238 and ImageReward from 1.2536→1.3562 (perceptual quality), while ELV gains are smaller than SGB's.

**Full GradHarmon** (4th column) combines both: natural colors with rich texture detail across all examples. Table 2 confirms the combination achieves the best results on every metric.

**Summary of each component's role across visual dimensions:**

| Aspect | SGB | SPA |
|---|---|---|
| Texture | Recovers fine-grained detail (fur strands, skin pores, fabric weaves) | Mild improvement |
| Color saturation | Not significantly affected | Corrects over-saturation to natural range |
| Semantic consistency | Not significantly affected | Improves global coherence via perceptual alignment |
| Spatial layout | Not affected (operates on gradient magnitude only) | Not affected (Gram loss is spatially invariant; spatial loss produces weak gradients when layouts differ) |
| Artifacts | Removes smoothing/blob artifacts from high-freq suppression | Removes unnatural color shifts |

---

## 2. More Qualitative Comparisons

**Setup.** Three-column comparisons: 40-step Teacher / DMD2 (4-step) / GradHarmon (4-step).

![More Results](rebuttal_more_results.pdf)

As shown above, DMD2 (4-step) suffers from texture smoothing (feather barbs flattened, fur collapsed into blobs, fabric wrinkles lost) and color over-saturation (Union Jack pushed to pure red/blue, emblem shifted to unnatural gold). GradHarmon addresses both through SGB (restoring fine-grained textures) and SPA (correcting color distribution), achieving visual quality on par with the 40-step teacher — preserving individual feather structures, strand-level fur detail, realistic color gradients, and three-dimensional material quality across all examples.

---

We will incorporate both the qualitative ablation and the expanded comparisons into the final version of the paper.
