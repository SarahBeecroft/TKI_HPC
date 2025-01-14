---
title: "Using Modules"
teaching: 5
exercises: 20
questions:
objectives:
- Explain what modules are
- List, load, unload modules
keypoints:
- Modules are a common way of managing software on HPC
- Make sure to load necessary modules in your job scripts 
---
## What are modules
The supercomputing admin staff make available many popular packages, so that users don't need to locally install common software. This is an efficient use of resources and time. Learning how to use modules is essential for getting the most out of HPC resources. 

## A worked example
For example, let's say that you want to use the container engine Singularity. Rather than having to find out how to locally install the software, you could check to see if  Singularity is supported as a module. Let's check! 
```bash
module avail singularity
```
 
```output
----------------- /software/setonix/2024.05/pawsey/modules --------------------------
   singularity/4.1.0-askap-gpu    singularity/4.1.0-mpi-gpu    singularity/4.1.0-nohost    singularity/4.1.0-slurm (D)
   singularity/4.1.0-askap        singularity/4.1.0-mpi        singularity/4.1.0-nompi

  Where:
   D:  Default Module

If the avail list is too long consider trying:

"module --default avail" or "ml -d av" to just list the default modules.
"module overview" or "ml ov" to display the number of modules for each name.

Use "module spider" to find all possible modules and extensions.
Use "module keyword key1 key2 ..." to search for all possible modules matching any of the "keys".

```

There lots of different versions to choose from. Each version of Singularity here has some tweaks to optimise it for particular use cases. We will use the `singularity/4.1.0-nompi` version. Let's load it. 

```bash
module load singularity/4.1.0-nompi
```

Then to see what modules you have loaded in your environment, use
```bash
module list
```
```output
Currently Loaded Modules:
  1) craype-x86-milan     4) perftools-base/23.09.0                 7) pawsey       10) craype/2.7.23      13) cray-libsci/23.09.1.1
  2) libfabric/1.15.2.0   5) xpmem/2.8.4-1.0_7.3__ga37cbd9.shasta   8) pawseytools  11) cray-dsmml/0.2.2   14) PrgEnv-gnu/8.4.0
  3) craype-network-ofi   6) pawseyenv/2024.05                      9) gcc/12.2.0   12) cray-mpich/8.1.27  15) singularity/4.1.0-nompi
```
 
You will notice that Singularity is loaded, but there are some other modules loaded too. These are loaded by default on Pawsey systems to ensure a smooth user experience.
To test that the singularity module is working, let's try a small command to get to the help page
```bash
singularity
```
```output
Usage:
  singularity [global options...] <command>

Available Commands:
  build       Build a Singularity image
  cache       Manage the local cache
  capability  Manage Linux capabilities for users and groups
  completion  Generate the autocompletion script for the specified shell
  config      Manage various singularity configuration (root user only)
  delete      Deletes requested image from the library
  exec        Run a command within a container
  inspect     Show metadata for an image
  instance    Manage containers running as services
  key         Manage OpenPGP keys
  keyserver   Manage singularity keyservers
  oci         Manage OCI containers
  overlay     Manage an EXT3 writable overlay image
  plugin      Manage Singularity plugins
  pull        Pull an image from a URI
  push        Upload image to the provided URI
  registry    Manage authentication to OCI/Docker registries
  remote      Manage singularity remote endpoints
  run         Run the user-defined default command within a container
  run-help    Show the user-defined help for an image
  search      Search a Container Library for images
  shell       Run a shell within a container
  sif         Manipulate Singularity Image Format (SIF) images
  sign        Add digital signature(s) to an image
  test        Run the user-defined tests within a container
  verify      Verify digital signature(s) within an image
  version     Show the version for Singularity
```
Ok, if we want to take the singularity module out of our environment, we can use
```bash
module unload singularity
# Let's check out list of loaded modules again
module list
```
```output
Currently Loaded Modules:
  1) craype-x86-milan     4) perftools-base/23.09.0                 7) pawsey       10) craype/2.7.23      13) cray-libsci/23.09.1.1
  2) libfabric/1.15.2.0   5) xpmem/2.8.4-1.0_7.3__ga37cbd9.shasta   8) pawseytools  11) cray-dsmml/0.2.2   14) PrgEnv-gnu/8.4.0
  3) craype-network-ofi   6) pawseyenv/2024.05                      9) gcc/12.2.0   12) cray-mpich/8.1.27
```

### What modules are available?

To view all of the available modules use

```bash
module avail
# press q to exit the avail screen
```

```output
# Output has been condensed for clarity

---------------------------------------------------------------------------------------------- /opt/cray/pe/lmod/modulefiles/mpi/gnu/8.0/ofi/1.0/cray-mpich/8.0 ----------------------------------------------------------------------------------------------
   cray-hdf5-parallel/1.12.2.1      craype-dl-plugin-ftr/22.06.1.2    craype-dl-plugin-py3/21.04.1      craype-dl-plugin-py3/22.08.1
   cray-parallel-netcdf/1.12.3.1    craype-dl-plugin-py3/21.02.1.3    craype-dl-plugin-py3/22.06.1.2    craype-dl-plugin-py3/22.09.1 (D)

------------------------------------------------------------------------------------------ /software/projects/pawsey0001/sbeecroft/setonix/modules/zen3/gcc/12.1.0 -------------------------------------------------------------------------------------------
   awscli/1.16.308-lsytfn3        py-botocore/1.13.44-4akvtdz    py-jmespath/0.10.0-edb6pk7    py-pyasn1/0.4.6-cz4oyjo             py-pyyaml/5.1.2-suqjcx3        py-setuptools-scm/6.3.2-ladffju    py-tomli/1.2.1-nd3pse5
   cmaq/5.3.1-ufxlpng             py-colorama/0.4.1-cqaqozz      py-packaging/21.0-ctswzg7     py-pyparsing/2.4.7-xyospqf          py-rsa/3.4.2-442zd47           py-setuptools/57.4.0-gai6cpk       py-urllib3/1.25.6-3kpilb4
   fastqc/0.11.9-3xczk4r   (D)    py-docutils/0.15.2-pskxmp2     py-pip/22.2.2-xhs7glf         py-python-dateutil/2.8.2-3x7ykix    py-s3transfer/0.2.1-vjwvdqz    py-six/1.16.0-vu2pa5f              python/3.9.9-iylvmfy

  Where:
   D:  Default Module
   L:  Module is loaded

```

## Getting help
To get a list of all the commands available with the `module` software, use the help function as below
```bash
module help
```

```output
Usage: module [options] sub-command [args ...]

Options:
  -h -? -H --help                   This help message
  -s availStyle --style=availStyle  Site controlled avail style: system (default: system)
  --regression_testing              Lmod regression testing
  -D                                Program tracing written to stderr
  --debug=dbglvl                    Program tracing written to stderr (where dbglvl is a number
                                    1,2,3)
  --pin_versions=pinVersions        When doing a restore use specified version, do not follow
                                    defaults
  -d --default                      List default modules only when used with avail
  -q --quiet                        Do not print out warnings
  --expert                          Expert mode
  -t --terse                        Write out in machine readable format for commands: list, avail,
                                    spider, savelist
  --initial_load                    loading Lmod for first time in a user shell
  --latest                          Load latest (ignore default)
  --ignore_cache                    Treat the cache file(s) as out-of-date
  --novice                          Turn off expert and quiet flag
  --raw                             Print modulefile in raw output when used with show
  -w twidth --width=twidth          Use this as max term width
  -v --version                      Print version info and quit
  -r --regexp                       use regular expression match
  --gitversion                      Dump git version in a machine readable way and quit
  --dumpversion                     Dump version in a machine readable way and quit
  --check_syntax --checkSyntax      Checking module command syntax: do not load
  --config                          Report Lmod Configuration
  --config_json                     Report Lmod Configuration in json format
  --mt                              Report Module Table State
  --timer                           report run times
  --force                           force removal of a sticky module or save an empty collection
  --redirect                        Send the output of list, avail, spider to stdout (not stderr)
  --no_redirect                     Force output of list, avail and spider to stderr
  --show_hidden                     Avail and spider will report hidden modules
  --spider_timeout=timeout          a timeout for spider
  -T --trace                        

[...]

```
