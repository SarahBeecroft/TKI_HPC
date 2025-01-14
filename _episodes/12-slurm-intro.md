---
title: "Basics of Interacting with SLURM Scheduler"
teaching: 5
exercises: 10
questions:
objectives:
- Submit a job to the queue
- Query the SLURM job queue
- Cancel a submitted job
keypoints:
- SLURM manages the allocation and resourcing of all submitted jobs
- Being able to check the status of your job is useful
---
## Submitting sbatch scripts to the queue
Right now, we should all be working in the `/scratch` filesystem. We are all currently running on a Setonix login node by default. 

That's nice, but how about we submit a job script to the queue with `sbatch` and see what happens? Do you remember how to submit an SBATCH script to SLURM? Let's go through it now:

### Looking at the test sbatch script provided in the training materials
What is inside the script we have provided?

```bash
cat test.sh
```
```output
#!/bin/bash -l
#SBATCH --account=courses01
#SBATCH --nodes=1
#SBATCH --ntasks-per-node=1
#SBATCH --cpus-per-task=1
#SBATCH --mem=100M
#SBATCH --time=00:05:00
#SBATCH --partition=work

echo 'I am a test job'
echo 'sleeping for 5 minutes'
srun sleep 5m
```

So this script follows the syntax we learned about. It then prints out some info and goes to sleep for 5 mins. 

A recap on the sbatch syntax:

- The `#SBATCH` lines specify to SLURM the computational resources/specifications we want for our job. It is also important to note that SLURM job scripts start with `#!/bin/bash` because they are essentially bash scripts.  
- The `--account` flag tells the system which allocation to 'charge' for the compute time.  
- The `--nodes` flag specifies how many nodes you want to use.  
- The `--ntasks-per-node` flag specifies how many tasks per node you want to run.  
- The `--cpus-per-task` flag specifies how many CPUs (cores) per task you need. 
- The `--mem` flag specifies how much memory to use per job.
- The `--time` flag sets the maximum allowable time for your job to run (i.e. the wall-clock limit). This job is set to get cut-off by SLURM at the 5 minute mark.  


Let's submit it to the queue! 

### Submitting a job to the queue using sbatch
```bash
sbatch test.sh
```
Each job gets a unique identifier (Job ID)

Can you see your job running in the queue? What is the job ID?
```bash
squeue -u $USER
```

## Cancelling a submitted job using scancel
Sometimes you will want to cancel a job. Maybe you were just testing the script, or maybe you realised you made a mistake! 

To cancel your specific job
```bash
scancel jobID
```

You can also cancel all jobs under your name with 
```bash
scancel -u $USER
```
