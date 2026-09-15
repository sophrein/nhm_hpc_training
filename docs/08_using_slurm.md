'---
title: Using SLURM
layout: default
nav_order: 5
---

# Using SLURM

On a shared HPC cluster, many people are running large analyses at the same time. To share the available computing resources fairly, clusters use a **job scheduler**. SLURM (Simple Linux Utility for Resource Management) is one of the most widely used, and is the scheduler on both the NHM HPC and Crop Diversity.

The login node is a shared entry point for all users and is not meant for heavy computation, so instead of running a heavy analysis directly on the machine you log into, you describe your job in a small script — how much CPU, memory and time it needs, and the commands to run — and **submit** it to SLURM. SLURM then queues your job and runs it on a compute node when suitable resources are free.

{: .note }
> This page is a general introduction to SLURM. For detailed, worked examples on the NHM HPC — including Conda, shared software and GPU jobs — see the [Using the job scheduler (Slurm)](04_accessing_hpc_resources/nhm_hpc.md#using-the-job-scheduler-slurm) section of the NHM HPC guide.

## Key commands

A handful of commands cover most day-to-day use:

| Command | What it does |
|---------|--------------|
| `sbatch script.sh` | Submit a job script to the scheduler. |
| `squeue -u <username>` | See the status of your own jobs in the queue. |
| `scancel <job_id>` | Cancel a running or queued job. Your job ID is returned when you run `sbatch`, and is also shown in the output of `squeue`. |
| `sacct -j <job_id>` | View details of a currenlty running or finished job (including how much memory and time it actually used). |
| `sinfo` | Check the state of the cluster's nodes and partitions. |

## Partitions (queues)

Clusters divide their compute nodes into **partitions** (sometimes called queues), often based on how long a job is allowed to run — for example `hour`, `day`, `week` and `month` on the NHM HPC. As a general rule, shorter jobs are scheduled sooner. Choose the shortest partition that comfortably fits your job. You specify the partition in your job script with `#SBATCH --partition=<value>` OR `#SBATCH -p <value>`.

## A minimal job script

A SLURM job script is just a shell script with some `#SBATCH` directives at the top that request resources:

```
#!/bin/bash
#SBATCH -J my-job          # job name
#SBATCH -p day             # partition (queue)
#SBATCH -c 2               # number of CPUs
#SBATCH --mem=4GB          # memory

echo "Running on $SLURM_NODELIST"
# ...your commands here...
```

Submit it with `sbatch my_script.sh`. The exact options and partition names differ between clusters, so always check the local documentation.

By default, an output log file is written to slurm-<jobid>.out in the directory you submitted from, which will include any errors from running the script.

## Using SLURM etiquette

A cluster is a **shared** resource. Being a considerate user keeps the system responsive for everyone (including you), and helps the scheduler give your own jobs a fair share. Please keep the following do's and don'ts in mind.

### Do's

- **DO right-size your jobs.** Request only the CPUs and memory your job actually needs. After a job finishes, use `sacct` to see how much it really used, and adjust future requests accordingly. Over-requesting wastes resources and can lower your priority; under-requesting can cause your job to fail or run out of memory.
- **DO choose an appropriate partition.** Submit jobs to the shortest queue that fits — don't put a 10-minute job in the `month` queue, or a week-long job in the `hour` queue.
- **DO test on a small scale first.** Run a quick test with a small dataset (or an interactive session) before launching a large batch of jobs, to catch mistakes early.
- **DO clean up after yourself.** Remove temporary files from scratch space when your job is done, rather than waiting for auto-deletion.
- **DO cancel jobs you no longer need** with `scancel`, so they aren't holding resources unnecessarily.

### Don'ts

- **DON'T create congestion on the cluster.** Avoid submitting hundreds or thousands of jobs (for example, huge array jobs) all at once. This floods the queue and can crowd out other users. Submit in reasonable batches, or use the scheduler's throttling options (such as limiting the number of simultaneously running array tasks).
- **DON'T run heavy analyses on the login/head node.** The login node is for editing files, managing data and submitting jobs — not for computation. Always submit compute work through SLURM.
- **DON'T request far more resources "just in case."** Requesting many CPUs or huge amounts of memory that you don't use makes your jobs wait longer and reduces the resources available to others.
- **DON'T leave interactive sessions idle.** Interactive sessions hold resources for as long as they are open — close them when you have finished.

If in doubt about the right resources for a job, ask on your cluster's support channel (see [Getting help](07_getting_help.md)).
