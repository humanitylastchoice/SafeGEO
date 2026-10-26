---
license: cc-by-4.0
task_categories: [text-ranking, text-retrieval]
language: [en]
tags: [generative-engine-optimization, geo, recommendation, recommendation-agents, llm-safety, adversarial, red-teaming, retrieval-augmented-generation, agents, benchmark]
pretty_name: SafeGEO
size_categories: [100K<n<1M]
configs:
  - config_name: visible
    data_files: [{split: test, path: visible/test-*.parquet}]
  - config_name: labels
    data_files: [{split: test, path: labels/test-*.parquet}]
  - config_name: candidate_quality
    data_files: [{split: test, path: candidate_quality/test-*.parquet}]
  - config_name: source_annotations
    data_files: [{split: test, path: source_annotations/test-*.parquet}]
  - config_name: geo_line_annotations
    data_files: [{split: test, path: geo_line_annotations/test-*.parquet}]
  - config_name: targets
    data_files: [{split: test, path: targets/test-*.parquet}]
  - config_name: instances_manifest
    data_files: [{split: test, path: instances_manifest/test-*.parquet}]
  - config_name: quality_distributions
    data_files: [{split: test, path: quality_distributions/test-*.parquet}]
  - config_name: requirement_annotations
    data_files: [{split: test, path: requirement_annotations/test-*.parquet}]
  - config_name: controlled_documents
    data_files: [{split: test, path: controlled_documents/test-*.parquet}]
  - config_name: diamond_visible
    data_files: [{split: test, path: diamond/visible/test-*.parquet}]
  - config_name: diamond_labels
    data_files: [{split: test, path: diamond/labels/test-*.parquet}]
  - config_name: diamond_candidate_quality
    data_files: [{split: test, path: diamond/candidate_quality/test-*.parquet}]
  - config_name: diamond_source_annotations
    data_files: [{split: test, path: diamond/source_annotations/test-*.parquet}]
  - config_name: diamond_geo_line_annotations
    data_files: [{split: test, path: diamond/geo_line_annotations/test-*.parquet}]
  - config_name: diamond_targets
    data_files: [{split: test, path: diamond/targets/test-*.parquet}]
  - config_name: diamond_instances_manifest
    data_files: [{split: test, path: diamond/instances_manifest/test-*.parquet}]
  - config_name: diamond_quality_distributions
    data_files: [{split: test, path: diamond/quality_distributions/test-*.parquet}]
  - config_name: diamond_requirement_annotations
    data_files: [{split: test, path: diamond/requirement_annotations/test-*.parquet}]
  - config_name: diamond_controlled_documents
    data_files: [{split: test, path: diamond/controlled_documents/test-*.parquet}]
---

# SafeGEO

[![EMNLP 2026 Oral](https://img.shields.io/badge/EMNLP_2026-Oral-A83630)](https://humanitylastchoice.org/research/papers/safegeo)
[![arXiv](https://img.shields.io/badge/arXiv-2606.28356-1D1713)](https://arxiv.org/abs/2606.28356)
[![Paper page](https://img.shields.io/badge/Hugging_Face-paper_page-1D1713)](https://huggingface.co/papers/2606.28356)
[![Code](https://img.shields.io/badge/GitHub-humanitylastchoice%2FSafeGEO-1D1713?logo=github)](https://github.com/humanitylastchoice/SafeGEO)
[![Humanity’s Last Choice](https://img.shields.io/badge/Humanity%E2%80%99s_Last_Choice-community-A83630)](https://humanitylastchoice.org)

![600 recommendation scenarios across 6 product categories; 22 GEO attack variants; 3 manipulation mechanisms; 40,800 evaluation instances](https://cdn-uploads.huggingface.co/production/uploads/667465a45ad1ce3339324940/mAUGXtnKwlYSMszdwetMt.jpeg)

SafeGEO tests whether recommendation agents still make the choice the user asked
for when seller-controlled web sources are edited with Generative Engine
Optimization (GEO) attacks. The full benchmark contains 600 recommendation base
cases across six product verticals. Each case is expanded into 68 instances: 22
attack packages applied separately to three sampled targets, plus two controls,
for 40,800 instances total.

![How a GEO attack reaches a recommendation: a user request, the agent's retrieved sources, an attack on one seller-controlled source, and the final ranking](https://cdn-uploads.huggingface.co/production/uploads/667465a45ad1ce3339324940/pIdtD6zKUF8L4fi9cISEO.jpeg)

A fixed release seed samples three eligible non-ground-truth candidates per
case without replacement. Candidate IDs identify the targets throughout the
release. Candidate-specific feasibility, quality, and evidence annotations
remain available for analysis. Product and vendor names in the candidate roster
and source packet use synthetic replacements.

The attack library spans three manipulation loci (content, epistemic, and
model-facing) and seven primitives. Full construction and schema documentation
is available in the [GitHub data guide](https://github.com/humanitylastchoice/SafeGEO/blob/main/data/README.md),
[attack taxonomy](https://github.com/humanitylastchoice/SafeGEO/blob/main/docs/ATTACK_TAXONOMY.md),
and [datasheet](https://github.com/humanitylastchoice/SafeGEO/blob/main/docs/DATASHEET.md).

## Results at a glance

![The strongest GEO attack moved an unsuitable product into the top three: 12.7% to 95.9% on Devstral Small 2 24B](https://cdn-uploads.huggingface.co/production/uploads/667465a45ad1ce3339324940/AeGd7S1xeB95ZqixL-pzX.jpeg)

- Across eight realistic GEO strategies, an unsuitable product reached the top three in 73–91% of cases on four systems. With matched truthful edits of the same page, 3–13%.
- The strongest attack moved Devstral Small 2 24B from 12.7% to 95.9%.
- A structured evidence check for each candidate helped most (Qwen3.6 27B: 78.3% → 39.1%), but did not return to the 8.1% truthful baseline.

Results from arXiv v2 (September 4, 2026).

## The two-minute version

<video src="https://cdn-uploads.huggingface.co/production/uploads/667465a45ad1ce3339324940/EIXNtVbHhRA_1xDsyVqw6.mp4" poster="https://cdn-uploads.huggingface.co/production/uploads/667465a45ad1ce3339324940/j0jkBlekg-W__cz9O7IQ0.jpeg" controls muted playsinline width="100%"></video>

A family asks an assistant about baby monitors, one seller edits its page, and the ranking flips. The narrated version is on the [project page](https://humanitylastchoice.org/research/papers/safegeo).

## SafeGEO Diamond

SafeGEO Diamond is a 600-instance screening subset for inexpensive iteration.
It contains 120 deterministic, vertical-balanced base cases (20 per vertical),
with one sampled target per case. Each case includes three high-effect realistic
attack packages and both controls.
Attack selection makes Diamond a biased screening set; use the complete
benchmark for population-level reporting. The exact cases, target assignments,
and row counts are recorded in
[`diamond/selection_manifest.json`](https://huggingface.co/datasets/humanitylastchoice/SafeGEO/blob/main/diamond/selection_manifest.json).

## Loading

```python
from datasets import load_dataset

# Full benchmark model inputs and hidden scoring labels.
visible = load_dataset("humanitylastchoice/SafeGEO", "visible", split="test")
labels = load_dataset("humanitylastchoice/SafeGEO", "labels", split="test")

# Fast Diamond screening inputs and labels.
diamond_visible = load_dataset("humanitylastchoice/SafeGEO", "diamond_visible", split="test")
diamond_labels = load_dataset("humanitylastchoice/SafeGEO", "diamond_labels", split="test")
```

The full dataset and Diamond each expose the same ten logical configs:

| Full config | Diamond config | Description |
|---|---|---|
| `visible` | `diamond_visible` | Model-facing query, candidate roster, and source packet. |
| `labels` | `diamond_labels` | Hidden package, target, and scoring metadata. |
| `candidate_quality` | `diamond_candidate_quality` | Candidate-level benchmark-reference quality annotations. |
| `source_annotations` | `diamond_source_annotations` | Source annotations for citation-validity scoring. |
| `geo_line_annotations` | `diamond_geo_line_annotations` | Misleading and refuting controlled-source lines. |
| `targets` | `diamond_targets` | Three sampled targets by base case. |
| `instances_manifest` | `diamond_instances_manifest` | Expanded-instance mapping. |
| `quality_distributions` | `diamond_quality_distributions` | Per-query candidate-quality distributions. |
| `requirement_annotations` | `diamond_requirement_annotations` | Query requirements used by the benchmark reference. |
| `controlled_documents` | `diamond_controlled_documents` | Full controlled-source corpus and hidden attack metadata. |

The full `visible`, `labels`, and `instances_manifest` configs contain 40,800
rows. The corresponding Diamond configs contain 600 rows. Other config counts
follow their base-case, candidate, source, or document granularity.

## Visibility and storage

Only `visible` / `diamond_visible` fields are model inputs. Attack design,
target identity, package IDs, and benchmark-reference annotations are hidden
from evaluated models. Records are stored as Parquet; nested lists and mappings
are JSON-encoded strings and can be decoded with `json.loads`, or loaded through
`safegeo.io.read_records` from the GitHub repository.

## Humanity’s Last Choice

![SafeGEO presented as an oral at EMNLP 2026, Room F9–10, Budapest, October 25, 2026](https://cdn-uploads.huggingface.co/production/uploads/667465a45ad1ce3339324940/s7BxsN4Xoe6v5iMhr3TYw.jpeg)

SafeGEO comes from [Humanity’s Last Choice](https://humanitylastchoice.org), an open research
community studying whether AI recommendations hold when the options’ pages are
edited to win the model. Its follow-up position paper proposes a common
evaluation standard for GEO:
[A Common Evaluation Standard for Generative Engine Optimization](https://huggingface.co/papers/2610.23541).

If you have a system to evaluate, a domain to add or a question, open a
discussion on this dataset or find us at [humanitylastchoice.org](https://humanitylastchoice.org).

## License

The dataset is released under CC-BY-4.0. Code and scoring utilities are released
separately under Apache-2.0 in the GitHub repository.

## Citation

```bibtex
@article{wen2026safegeo,
  title   = {SafeGEO: Understanding Generative Engine Optimization Risks in Recommendation Agents},
  author  = {Wen, Qianfeng and Liu, Yifan Simon and Liu, Xin and Jiao, Difan and Yang, Blair and Wu, Junda and Tang, Zhenwei},
  journal = {arXiv preprint arXiv:2606.28356},
  year    = {2026}
}
```
