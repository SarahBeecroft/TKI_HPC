---
title: "Basics of Singularity"
teaching: 5
exercises: 10
questions:
objectives:
- Download container images
- Run commands from inside a container
keypoints:
- Execute commands in containers with `singularity exec`
- Download a container image in a selected location with `singularity pull`
---

## Let's ask for an interactive session on slurm

Since we are running this tutorial on a shared system, we should use one of the compute nodes rather than the login node. You can get this setup by using an interactive Slurm allocation:

```bash
salloc -n 1 -t 4:00:00 --account=courses01
module load singularity/4.1.0-nompi
```

```output
salloc: Granted job allocation 3453895
salloc: Waiting for resource configuration
salloc: Nodes z052 are ready for job
```

### Download and use images via SIF file names

Singularity is able to download and run Docker images, which are the defacto standard format. For these exercises, we're going to use a plain *Ubuntu* container image.  It's small and quick to download, and will allow use to get to know how containers work by using common Linux commands.  
Let's try and download a Ubuntu container from the [**Docker Hub**](https://hub.docker.com), *i.e.* the main registry for Docker containers:

```bash
singularity pull docker://ubuntu:16.04
```

```output
INFO:    Converting OCI blobs to SIF format
INFO:    Starting build...
Getting image source signatures
Copying blob sha256:22e816666fd6516bccd19765947232debc14a5baf2418b2202fd67b3807b6b91
 25.45 MiB / 25.45 MiB [====================================================] 1s
Copying blob sha256:079b6d2a1e53c648abc48222c63809de745146c2ee8322a1b9e93703318290d6
 34.54 KiB / 34.54 KiB [====================================================] 0s
Copying blob sha256:11048ebae90883c19c9b20f003d5dd2f5bbf5b48556dabf06c8ea5c871c8debe
 849 B / 849 B [============================================================] 0s
Copying blob sha256:c58094023a2e61ef9388e283026c5d6a4b6ff6d10d4f626e866d38f061e79bb9
 162 B / 162 B [============================================================] 0s
Copying config sha256:6cd71496ca4e0cb2f834ca21c9b2110b258e9cdf09be47b54172ebbcf8232d3d
 2.42 KiB / 2.42 KiB [======================================================] 0s
Writing manifest to image destination
Storing signatures
INFO:    Creating SIF file...
INFO:    Build complete: /data/singularity/.singularity/cache/oci-tmp/a7b8b7b33e44b123d7f997bd4d3d0a59fafc63e203d17efedf09ff3f6f516152/ubuntu_16.04.sif
```

Singularity has just downloaded a Ubuntu image from the online container repository to your working directory. This would be skipped if the image had been downloaded previously.

Container images have a **name** and a **tag**, in this case `ubuntu` and `16.04`.  The tag can be omitted, in which case Singularity will default to a tag named `latest`.

Note that, to point Singularity to Docker Hub, the prefix `docker://` is required.

Docker Hub organises images only by users (also called *repositories*), not by projects: `<repository>/<name>:<tag>`.  


By default, the image is saved in the current directory. Let's check it's there:

```bash
ls
```

```output
ubuntu_16.04.sif
```

Then you can use this image file by:

```bash
singularity exec ubuntu_16.04.sif echo "Hello World"
```

```output
Hello World
```

If the container isn't in your working directory, you can specify the path to the container location. For example:

```bash
singularity exec $MYSOFTWARE/ubuntu_16.04.sif echo "Hello World"
```

## Contextual help on Singularity commands
Use `singularity help`, optionally followed by a command name, to print help information on features and options.
