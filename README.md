# NHM bioinformatics training

Training material for linux accessing HPC resources at the NHM. 

The webpage is hosted [here](https://nhm-sequencing-facility.github.io/nhm_hpc_training/). 

The webpage is written in [just-the-docs](https://just-the-docs.com/) with all tutorial data in markdown format. 

## Contributing

Here are instructions on how to contribute training material. 


```
# clone repo
git clone https://github.com/nhm-sequencing-facility/nhm_hpc_training.git

# change directory
cd nhm_hpc_training

# create branch, replacing 'test_branch' with a relevant name for you
git checkout -b test_branch
```

Once you have your own copy of the repo and new branch, you can make changes to the file structure. 

When you have made your changes, stage and commit them:

```
# stage your changes
git add .

# commit with a descriptive message
git commit -m "brief description of your changes"

# push your branch to GitHub
git push origin your-branch-name
```

When finished, submit a pull request and the changes will be reviewed before uploading. 

## Adding new tutorials

If you would like to create your own tutorial, just create a new markdown file in the docs folder. If the tutorial requires multiple sections, you can create a subdirectory in the docs folder with multiple markdown files within it.

## Images

All images can be placed in the images directory.
