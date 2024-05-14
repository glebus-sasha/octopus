# octopus_nf

This repository contains a Nextflow variant calling pipeline for analyzing Next-Generation Sequencing (NGS) data using octopus (https://github.com/luntergroup/octopus).

```mermaid
%%{init: {'theme':'base'}}%%
flowchart TB
    subgraph "input"
    v0["reads"]
    v1["reference"]
    end
    v2([REFINDEX])
    v3([QCONTROL])
    subgraph "output"
    v4["quality report"]
    v14["VCF"]
    end
    v6([ALIGN])
    v8([PREPARE])
    v10([VARCALL])
    v13([ANNOTATE])
    v0 --> v3
    v1 --> v2
    v2 --> v6
    v3 --> v6
    v3 --> v4
    v1 --> v6
    v6 --> v8
    v6 --> v10
    v1 --> v8
    v8 --> v10
    v1 --> v10
    v10 --> v13
    v13 --> v14
```

## Description

The pipeline is implemented in Nextflow and includes several stages for NGS data analysis:

1. **REFINDEX:** Index creation using BWA (Burrows-Wheeler Aligner).
2. **QCONTROL:** Data preprocessing using Fastp.
3. **ALIGN:** Sequence alignment using BWA mem.
4. **PREPARE:** File processing and preparation using Samtools.
5. **VARCALL:** Variant calling using Octopus.
6. **ANNOTATE:** Annotation using vep.

## Usage

### Quick Start

To quickly run the pipeline, use the following command:

```bash
nextflow run glebus-sasha/octopus_nf \
-profile <docker/singularity> \
--reference <path-to-reference> \
--reads "<path-to-reads-folder>/*[rR]{1,2}*.fastq*" \ # quotes are important
--outdir results
```

### Requirements

- Nextflow (https://www.nextflow.io/docs/latest/install.html)
- Docker (https://docs.docker.com/engine/install/) or
- Singularity (https://github.com/sylabs/singularity/blob/main/INSTALL.md)

### Running the Pipeline

1. Install all the necessary dependencies such as Nextflow, Singularity.
3. Clone this repository: `git clone https://github.com/glebus-sasha/octopus.git`
4. Navigate to the pipeline directory: `cd octopus_nf`
5. Edit the `nextflow.config` file to set the required parameters, if necessary.
6. Run the pipeline, setting the required parameters, for example:

```bash
nextflow run main.nf
```

## License

This project is licensed under the [MIT License](LICENSE).
