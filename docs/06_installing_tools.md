---
title: Installing tools
layout: default
nav_order: 6
---

# Installing tools

Bioinformatics work usually depends on a range of specialised software. On a shared HPC system you normally **cannot** install software system-wide (you don't have administrator rights), so instead you install tools into your own space or run them in self-contained environments. This page gives a cluster-agnostic overview of the three most common approaches. The exact commands vary slightly between clusters, so always check the documentation for the system you are using.

{: .note }
> For step-by-step, NHM-specific instructions — including installing Conda, building Singularity images, and using the shared software area — see the [Installing software](04_accessing_hpc_resources/nhm_hpc.html#installing-software) section of the NHM HPC guide.

## 1. Conda (package and environment manager)

[Conda](https://docs.conda.io/en/latest/) is the most common way to install bioinformatics software without needing administrator rights. It downloads pre-built packages and manages **environments** — isolated collections of software — so that different projects can use different tools and versions without conflicting.

Typical workflow:

```
# create an environment and install some tools into it
conda create -n myproject samtools bwa

# activate the environment
conda activate myproject

# ...do your work...

# leave the environment when finished
conda deactivate
```

Many bioinformatics tools are distributed through the [Bioconda](https://bioconda.github.io/) channel.

**Good for:** quickly installing tools that are available as Conda packages; personal use.

## 2. Singularity / Apptainer (containers)

[Singularity](https://apptainer.org/documentation/) (also known as Apptainer) lets you run software inside a **container** — a self-contained image that bundles a tool together with all of its dependencies. Containers are portable (you can move the same image between your computer and different clusters), reproducible, and shareable with colleagues. Singularity is preferred over Docker on HPC systems because it can be run without administrator rights.

Typical workflow:

```
# pull an existing image from a container registry
singularity pull docker://biocontainers/samtools

# run a command inside the container
singularity run samtools_latest.sif samtools --version
```

**Good for:** complex software with awkward dependencies; reproducible pipelines; sharing a fixed environment with others.

## 3. Environment modules (Lmod)

Most HPC clusters pre-install commonly used software and make it available through **environment modules**, usually via the `module` (or `ml`) command. This lets you load a specific tool and version into your session without installing anything yourself.

Typical workflow:

```
# list the software available on the cluster
ml avail

# load a specific tool and version
ml samtools/1.10

# list what you currently have loaded
ml list
```

**Good for:** software the cluster administrators have already installed and maintained.

## Which should I use?

| Approach | Use it when |
|----------|-------------|
| Conda | The tool is available as a Conda/Bioconda package and you just need it in your own space. |
| Singularity/Apptainer | You need a reproducible, portable environment, or the software is hard to install directly. |
| Environment modules | The software is already provided and maintained on the cluster. |

These approaches are not mutually exclusive — it is common, for example, to load a module for one tool while using a Conda environment for another.