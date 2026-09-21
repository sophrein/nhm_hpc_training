---
title: Installing tools
layout: default
nav_order: 6
---

# Installing tools

Bioinformatics work usually depends on a range of specialised software. On a shared HPC system you normally **cannot** install software system-wide (you don't have administrator rights), so instead you install tools into your own space or run them in self-contained environments. This page gives a generalised overview of the three most common approaches. The exact commands vary slightly between clusters, so always check the documentation for the system you are using.

{: .note }
> For step-by-step, NHM-specific instructions — including installing Conda, building Singularity images, and using the shared software area — see the [Installing software](04_accessing_hpc_resources/nhm_hpc.md#installing-software) section of the NHM HPC guide.

## 1. Conda (package and environment manager)

[Conda](https://docs.conda.io/en/latest/) is the most common way to install bioinformatics software without needing administrator rights. It downloads pre-built packages and manages **environments** — isolated collections of software packages — so that different projects can use different tools and versions without conflicting.

### Installing Conda

Conda may already be available on the cluster you are using so check the relevant documentation. On the NHM HPC, documentation on how to install Conda is here [NHM HPC guide](04_accessing_hpc_resources/nhm_hpc.md#installing-conda).

Downloading and installing [Miniconda](https://www.anaconda.com/docs/getting-started/concepts/anaconda-or-miniconda#miniconda) (a lightweight version of Conda):

```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```

Follow the prompts, then restart your terminal or run:

```bash
source ~/.bashrc
```

Verify the installation with:

```bash
conda --version
```

### Typical workflow:

Create an environment and install some tools into it:

```bash
conda create -n myproject <tool1> <tool2>
```

Activate your conda environment to use the packages installed:

```bash
conda activate myproject
```

Leave the environment when finished:

```bash
conda deactivate
```

Bioconda is a channel for the conda package manager that specialises in bioinformatics software. Many tools are distributed through [Bioconda](https://bioconda.github.io/), this allows you to install them with a single `conda install` command rather than compiling from source.


**Good for:** quickly installing tools that are available as Conda packages; personal use.

## 2. Singularity / Apptainer (containers)

[Singularity](https://apptainer.org/documentation/) (also known as Apptainer) lets you run software inside a **container** — a self-contained image that bundles a tool together with all of its dependencies. Containers are portable (you can move the same image between your computer and different clusters), reproducible, and shareable with colleagues. Singularity is preferred over Docker on HPC systems because it can be run without administrator rights.

### Installing Singularity

Installation requires administrator rights, so on an HPC cluster Singularity/Apptainer is usually already installed. Check with your system administrator or the cluster documentation.

If you need to install it on your own Linux machine, follow the official [Singularity/Apptainer installation guide](https://apptainer.org/docs/admin/main/installation.html).

On the NHM HPC, see the [NHM HPC guide](04_accessing_hpc_resources/nhm_hpc.md#singularityapptainer) for how to access Singularity/Apptainer.

You can verify it is available with:

```bash
apptainer --version
```

### Typical workflow:

pull an existing image from a container registry:

```bash
singularity pull docker://biocontainers/samtools
```
By default, the container cannot see files outside of it — use --bind to make a directory (with data you want to reference) visible inside the container, then run your command:

```bash
singularity run --bind /path/to/data samtools_latest.sif <your command> /path/to/data/<yourfile>
```

**Good for:** complex software with awkward dependencies; reproducible pipelines; sharing a fixed environment with others.

## 3. Environment modules (Lmod)

Most HPC clusters pre-install commonly used software and make it available through **environment modules**, usually via the `module` (or `ml`) command. This lets you load a specific tool and version into your session without installing anything yourself.

### Typical workflow:

List the software available on the cluster:

```bash
ml avail
```
Load a specific tool and version:

```bash
ml samtools/1.10
```

List what you currently have loaded:

```bash
ml list
```

To unload a module:

```bash
ml -samtools/1.10
```
To unload all modules at once:

```bash
ml purge
```

**Good for:** software the cluster administrators have already installed and maintained.

## Which should I use?

| Approach | Use it when |
|----------|-------------|
| Conda | The tool is available as a Conda/Bioconda package and you just need it in your own space. |
| Singularity/Apptainer | You need a reproducible, portable environment, or the software is hard to install directly. |
| Environment modules | The software is already provided and maintained on the cluster. |

These approaches are not mutually exclusive — it is common, for example, to load a module for one tool while using a Conda environment for another.