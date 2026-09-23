---
title: Crop Diversity
layout: default
parent: Accessing HPC resources
nav_order: 3
---

# Crop Diversity

Crop Diversity is a High Performance Computing cluster run and maintained by the James Hutton Institute's Information & Computational Sciences (ICS) Research Computing team, together with the Scientific Computing section of NIAB's IT team. It supports researchers from six UK institutions, including the Natural History Museum, and uses a SLURM job scheduler. The cluster's head node (the server you log into) is called **gruffalo**.

The Crop Diversity team maintain excellent, detailed documentation. This page gives a short overview to get you started, but the definitive reference is the official documentation landing page:

[**Crop Diversity HPC documentation**](https://help.cropdiversity.ac.uk/index.html)

## Requesting an account

Before you can use the cluster, you need to request an account:

- [Request an account for the Crop Diversity cluster](https://help.cropdiversity.ac.uk/user-accounts.html).

## Connecting to the cluster

Once you have an account, you can [get connected](https://help.cropdiversity.ac.uk/ssh.html) to gruffalo using either a terminal-based or a graphical SSH client. Supported clients include MobaXterm, WSL (Windows 10+ only), Cygwin/mintty and PuTTY.

How you connect depends on where you are:

- **On site or on your institution's VPN** - if you are at a [supported institution](https://help.cropdiversity.ac.uk/organizations.html), you can connect directly using your password, either via the [terminal](https://help.cropdiversity.ac.uk/ssh-terminal-pw.html) or a [graphical client](https://help.cropdiversity.ac.uk/ssh-graphical-pw.html).
- **Off site** - you must use key authentication with an `ssh` key pair and 2FA, either via the [terminal](https://help.cropdiversity.ac.uk/ssh-terminal-keys.html) or a [graphical client](https://help.cropdiversity.ac.uk/ssh-graphical-keys.html).

## Storage

Crop Diversity has storage quotas, so it is worth being aware of how much space you are using. See the [storage documentation](https://help.cropdiversity.ac.uk/data-storage.html) for details on quotas and where to store your data.

## Useful Features

### Database mirrors

Crop Diversity maintains mirrors of several popular bioinformatics databases, such as NCBI's nucleotide and protein databases (used for sequence searching with tools like BLAST). These are stored on the cluster's high-performance storage and are accessible from any node, meaning you do not need to download these large databases yourself. See the [database mirrors](https://help.cropdiversity.ac.uk/database-mirrors.html#database-mirrors) documentation for details.

## Getting help

Crop Diversity is used by a large community of researchers, and the [cropdiversity-hpc Slack channel](https://cropdiversity-hpc.slack.com) is usually the best place to ask for help with issues related to the cluster.