---
title: Outputs
layout: page
nav_order: 5
grand_parent: v2.0
parent: Usage Guide
permalink: /docs/v2.0/pages/usage/outputs/
---

# {{ page.title }}
{: .no_toc}

1. TOC
{:toc}

# Overview
Below is an overview of the standard outputs produced by EPITOME.
```
`${outdir}` 
├── `${taxon}`
│   ├── input
│   │   ├── `${taxon}`-wg.fa.gz
│   │   ├── `${taxon}`-wg.metadata.jsonl.gz
│   │   ├── manifest.csv
│   │   └── versions.yml
│   └── wg
│       ├── `${taxon}`-wg.centroid.jsonl.gz
│       ├── `${taxon}`-wg.clusters.jsonl.gz
│       ├── `${taxon}`-wg.condensed.jsonl.gz
│       ├── `${taxon}`-wg.consensus.jsonl.gz
│       ├── `${taxon}`-wg.qc.jsonl.gz
│       └── alignments
│           └── `${taxon}`-wg-`${variant}`.mafft.fa
└── pipeline_info
```