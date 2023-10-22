---
title: "Azurecompute"
date: 2023-09-22T16:39:34Z
---
All about Azure compute
-----------------------

As it's a requirement for the DP-100 exam, I'm going to write a little about Azure compute.
Much like there are storage and compute resources in the wider Azure eco-system, Azure Machine Learning also has it's own storage and compute features.
Compute in Azure ML comes in 2 varieties, managed compute and unmanaged compute.
Managed compute, as the name suggests, are compute resources that are created and managed by Azure Machine learning.  These come in 3 types - 

Compute instances
Compute clusters
Serverless (which is in preview)

It's probably no surprise that unmanaged compute refers to compute that is created and managed outside of Azure machine learning, and attached to the workspace by you. This could refer to - 

Kubernetes clusters
Azure Databricks
HD Insight
Virtual Machine


Compute instances
-----------------
Azure ML compute instances are cloud based, managed workstations for data scientists, with useful packages pre-installed (e.g. numpy, scikit-learn, tensorflow, keras, etc), they are ideal for running notebooks in the exploration phase of a project and for development and testing. Any required packages which are not installed can be set up manually or by using set up scripts.

A notebook in a compute instance can be run within the Azure ML workspace, in VS code for web, and in VS code locally. To edit a notebook in VS code, web or local, the compute instance must be running.  From a quick play around, running in VS code web seems to be pretty much the same as using a github codespace.

As these are bascially Azure VM's, the costs could run away from you, so it would be wise to use the auto run and shutdown configuration that is available.

Where's all the data?
---------------------
Any software packages are stored on the OS disk of the compute instance which has a 128GB capacity.  Large files should be saved in the tmp directory, or the temporary drive mounted on mnt. The size of the temporary disk is determined by the VM size.


The default storage account of the workspace is used for storing notebooks and python scripts when working with a compute instance. This makes it easy to share these resources between different compute instances and preserves them when an instance is stopped or even deleted.

When started, the file share in the default storage account is mounted as a drive to the compute instance, and is the default working directory for any Jupyter notebooks, Jupyter labs, RStudio, and Posit Workbench. As you might expect, starting a different compute instance will mount the share to that instance and make the files available (what if you run 2 compute instances at the same time?).


Compute clusters
----------------
A compute cluster is similar to a compute instance, but works as an on demand cluster of compute nodes optimised for parallel computing. This can be useful as the training process is split between multiple nodes in the cluster. A compute cluster will scale automatically (and to zero) which makes them more suitable for production workloads than a compute instance.

Unlike a compute instance, you can't connect to a compute cluster directly and start running scripts and notebooks, what you can use it  for is to run jobs from automated ML, the ML designer, and pipeline jobs.


Serverless compute
------------------
Currently in preview. I like the look of this.  There are a lot of positives, my favorites - 

1. No more insufficient quota messages.  If you've done any work in Azure ML, you may have run into the issue of hitting the limits Microsoft sets on allowed resources in a subscription.  If you haven't ran into this, familiarize yourself with the "Usage + quotas" area of any Azure subscription and you might save yourself a headache later on.
2. Specify the required resources as you require them, or just let Azure pick the default.
3. No need to write blog posts about compute, just ignore all other types of compute and focus on the machine learning task.

Serverless compute can be used for Auto ML, ML pipelines, and the designer. Although it is in preview so you might need to enable it first.


Kubernetes Clusters
-------------------
Kubernetes clusters can be attached to the workspace to handle training or inference workloads.  The cluster will need the Azure ML extension installed before it can be attached.

Once this is set up it should be possible to select the cluster as a compute target. I say "should", as I had some real trouble with this and eventually ran out of time, so I'll circle back to this at a later date.  A look online suggests I'm not the only one who ran into issues, so that's somewhat comforting.

This is the end, I hope it's not too disappointing.