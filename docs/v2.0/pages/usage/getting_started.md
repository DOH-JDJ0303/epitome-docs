---
title: Getting Started
layout: page
nav_order: 2
grand_parent: v2.0
parent: Usage Guide
permalink: /docs/v2.0/pages/usage/getting_started/
---

# {{ page.title }}
{: .no_toc}

1. TOC
{:toc}

# Dependencies
EPITOME is built using [Nextflow](https://www.nextflow.io/). Nextflow simplifies the development and execution of complex, scalable data analysis workflows by enabling reproducibility, portability across computing environments, and seamless integration with container technologies like Docker and Singularity.

The following are required to run EPITOME:
- [Nextflow](https://www.nextflow.io/docs/latest/install.html) (version 23.04.0 or higher)
- One of the following container engines: 
    - [Podman](https://podman.io/docs/installation) (recommended)
    - [Docker](https://docs.docker.com/engine/install/)
    - [Apptainer](https://apptainer.org/docs/admin/main/installation.html)
    - [Singularity](https://docs.sylabs.io/guides/3.0/user-guide/installation.html). 

{: .important}
EPITOME does not support Conda / Mamba. Please submit a [feature request](https://github.com/DOH-JDJ0303/EPITOME/issues) if this is essential for your lab.

# Nextflow Basics
Below are some general pointers for how to run Nextflow workflows.
## Specifying the workflow version
There are two general ways you can specify which version of EPITOME you want to run:
1. Tell Nextflow which version you want to use

    ```
    nextflow run doh-jdj0303/EPITOME \
        -r v1.0 \
        -profile docker \
        --input samplesheet.csv \
        --outdir results
    ```

2. Clone the workflow version manually
    ```
    git clone https://github.com/doh-jdj0303/EPITOME.git -b v1.0 
    ```
    ```
    nextflow run EPITOME/main.nf \
        -profile docker \
        --input samplesheet.csv \
        --outdir results
    ```

{: .tip}
Nextflow caches repos in ~/.nextflow/assets/ by default. Removing this cache can be helpful when running into version-related issues.

## Specifying resource limits
We recommend adjusting the maximum resource limits that Nextflow can use. Setting these limits too high will cause the workflow to fail. There are four general ways to achieve this:
1. Set limits via command-line parameters
    ```
    nextflow run doh-jdj0303/EPITOME \
        -r v2.0 \
        -profile docker \
        --input samplesheet.csv \
        --outdir results \
        --max_cpus 8 \
        --max_memory 12.GB 
    ```
2. Set limits in the [nextflow.config](https://github.com/DOH-JDJ0303/EPITOME/blob/main/nextflow.config) config file
    ```
        // Max resource options
        // Defaults only, expecting to be overwritten
        max_memory                 = '128.GB'
        max_cpus                   = 16
        max_time                   = '240.h'
    ```

3. Set limits via a custom config file
    `custom.config`
    ```
    process {
    // Default maximum resources allowed per process
    withName: '*' {
        maxCpus = 16         // set your desired max CPUs
        maxMemory = '64 GB'  // set your desired max memory
    }
    }
    ```
    ```
    nextflow run doh-jdj0303/EPITOME \
        -r v2.0 \
        -c custom.config \
        -profile docker \
        --input samplesheet.csv \
        --outdir results
    ```

{: .tip}
*All* parameters can be supplied via a custom config file, including `input` and `outdir`. This is generally best practice and should be used when possible.

---

## Resuming a run
Nextflow can resume a run. This comes in handy when a workflow fails or when you need to make small parameter adjustments. Below is an example of how you can resume a workflow run:
```
nextflow run doh-jdj0303/EPITOME \
    -r v2.0 \
    -profile docker \
    --input samplesheet.csv \
    --outdir results \
    -resume
```

# Testing EPITOME
Verify that EPITOME is running properly using the command below. Update `-profile` to your preferred container engine.
```
nextflow run doh-jdj0303/EPITOME \
    -r v2.0 \
    -profile (docker|podman|apptainer|singularity),test \
    --outdir EPITOME_test
```
You can learn more about how the test configuration [here](https://github.com/DOH-JDJ0303/EPITOME/blob/main/conf/test.config)

# Basic Usage
In-depth overviews of [inputs](../inputs) and [outputs](../outputs/) are available. All other questions / issues should be submitted via the EPITOME [GitHub issues](https://github.com/DOH-JDJ0303/EPITOME/issues) page or by [email](mailto:waphl-bioinformatics@doh.wa.gov).