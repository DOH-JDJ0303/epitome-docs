---
title: Inputs
layout: page
nav_order: 4
grand_parent: v2.0
parent: Usage Guide
permalink: /docs/v2.0/pages/usage/inputs/
---

# {{ page.title }}
{: .no_toc}

1. TOC
{:toc}

# Overview
Pipeline parameters can be adjusted using the following methods:

1. At the command line using `--{parameter_name}` (e.g., `--input`)
2. In the `nextflow.config` file
3. In a JSON file via the `-params-file` parameter

# Input Options
## `--input`
Path to the samplesheet. 

### Example samplesheet
`samplesheet.csv`:
```csv
taxon
Alphainfluenzavirus
```
### Samplesheet columns

|Column Name|Description|
|:-|:-|
|`taxon`|Taxonomy name, as it appears in NCBI (if using NCBI)|
|`segmented`|Whether or not the taxon has a segmented genome (true or false (not case sensitive))|
|`assembly`|Path to a multi-FASTA file containing sequences associated with the specifed taxon|
|`metadata`|Path to CSV file containing information about each sequence in the supplied assembly|
|`exclusions`|Path to CSV file containing sequence accessions that should be excluded|

### Metadata columns

|Column Name|Description|
|:-|:-|
|`acession`|Sequence accession that matches the sequence header in the multi-FASTA|
|`taxon`|Taxonomy name|
|`species`|Species name (optional)|
|`segment`|Species name (optional)|

{: .note}
You can add whatever columns you want to the metadata and they will be carried through to the final reference set

### Exclusions

|Column Name|Description|
|:-|:-|
|`acession`|Sequence accession|

## `--len_threshold`
The sequence length threshold used to filter input sequences: `length +- len_threshold*mean(length)`

- Options: `0...1`
- Default: `0.20`

## `--amb_threshold`
The ratio of ambiguous bases (`N`) allowed in a sequence.

- Options: `0...1`
- Default: `0.02`

# Subworkflow

## `--ncbi`
Automatically pull down sequences from NCBI

- Options: `true` or `false`
- Default: `true`

## `--create`
Create a reference set from the input sequences

- Options: `true` or `false`
- Default: `true`

# Clustering Options
## `--dist_threshold`
Create a reference set from the input sequences

- Options: `0...1`
- Default: `0.02`

## `--max_cluster`
Maximum number of sequences to include in hierarchal clustering.

- Options: `0...Inf`
- Default: `1000`

{: .caution}
Increasing this value can _significantly_ increase run time and may cause the pipeline to fail.

    ksize                      = 31
    scaled                     = 100
    window_size                = 8000

## `--ksize`
K-mer size used when calculating average nucleotide identity using Sourmash (for clustering and condensing).

- Options: `?...?`
- Default: `31`

> Options are whatever Sourmash allows 🙈

## `--scaled`
Scaled value used by Sourmash when calculating average nucleotide identity (for clustering and condensing).

- Options: `0...?`
- Default: `100`

> Options are whatever Sourmash allows 🙈

## `--window_size`
Sequence window size to use when determining pairwise distances. 

- Options: `0...Inf`
- Default: `8000`

# Reference Options
## `--consensus`
Create references using consensus mode.

- Options: `true` or `false`
- Default: `true`

## `--centroid`
Create references using centroid mode.

- Options: `true` or `false`
- Default: `true`

## `--max_align`
Maximum number of sequences to include in an alignment.

- Options: `0...Inf`
- Default: `1000`

> Sequences are randomly subsampled to this value within each cluster.

{: .caution}
Increasing this value can _significantly_ increase run time and may cause the pipeline to fail.