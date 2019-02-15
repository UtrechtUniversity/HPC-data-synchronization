## Creating a job script data synchronization

A synchronization command can be incorporated in a shell script or a job script to take care of the transfer of input and output data directly to and from the remote storage platforms. This can help to keep your HPC working environment clean and your data in one place. On this page we provide instructions how to setup job scripts on the Lisa cluster. 

### Lisa

If you work with data volumes of a few of Gigabytes or less, and reading and writing of data is not a main task in your workflow, you can transfer the data to the 'home file system' of Lisa. This is the file system you have available upon login at Lisa. However, when working with large data volumes and reading and writing of data becomes a significant part of your workflow it may be better to use the scratch file system on the compute nodes. More info about the filesystems on Lisa can be found [here](https://userinfo.surfsara.nl/systems/lisa/filesystems). Examples of these 2 methods are provided below.

**Home file system**

Below an example job script using Surfdrive and Rclone.

```
#! /bin/bash

#SBATCH -N 1              # 1 node
#SBATCH --mem=32G         # with 32 GB memory
#SBATCH -t 00:10:00       # for 5 minutes
#SBATCH --mail-type=BEGIN,END
#SBATCH --mail-user=<email address of user>

    # When a node is available, the system logins at that node as the user who has submitted this batch script
    # The following commands will be executed on behalf of the user
    
# MAIN BODY    
# Synchronize input data to HPC

mkdir input  # make a folder where all input data is stored

export PATH=${HOME}/rclone-v1.45-linux-amd64/:${PATH}  # set path to newest rclone version
rclone version

rclone sync surfdrive:myinputfolder  ./input -cv  # one-way sync folders

echo Transfer input done

# Perform tasks

mkdir output
cp ./input/* ./output/

sleep 10

# Synchronize output data back to storage

rclone sync ./output surfdrive:myoutputfolder -cv

echo End of Job
```

> In the above script:
>1. fill in your email address on the indicated place.
>2. check whether the rclone version is the same as the version you installed (see [this manual](./surfdrive))
>3. if necessary, change the rclone paths to <name remote in rclone config>:<surfdrive folder>

When using Yoda or the Data Archive, the transfer commands in the above scripts need to be replaced by the appropriate commands for these platforms. Example scripts for using [Yoda](../scripts/transferjob_yoda) and [Archive](../scripts/transferjob_archive) can be found following the links. Note that when using 'icommands' for transferring data to and from Yoda, the `iinit` command needs to be issued at the command line to generate a password for connecting before submitting the job.

**Scratch file system**

When using the scratch file system, simply use the environment variable `"$TMPDIR"` before any local directory paths. This results in the following job script:


```
#! /bin/bash

#SBATCH -N 1              # 1 node
#SBATCH --mem=32G         # with 32 GB memory
#SBATCH -t 00:10:00       # for 5 minutes
#SBATCH --mail-type=BEGIN,END
#SBATCH --mail-user=<email address of user>

    # When a node is available, the system logins at that node as the user who has submitted this batch script
    # The following commands will be executed on behalf of the user
    
mkdir "$TMPDIR"/input  # make a folder where all input data is stored

# Synchronize input data to HPC
export PATH=${HOME}/rclone-v1.45-linux-amd64/:${PATH}  # set path to newest rclone version
rclone version

rclone sync surfdrive:myinputfolder "$TMPDIR"/input/ -cv

echo Transfer input done

# Perform tasks
mkdir "$TMPDIR"/output
cp "$TMPDIR"/input/* "$TMPDIR"/output/

sleep 10

# Synchronize output data back to storage
rclone sync "$TMPDIR"/output/ surfdrive:myoutputfolder

echo End of Job
```

### UBC

Job scripts for UBC are similar except for the first few lines:


```
#!/bin/bash

#$ -cwd       # execute the job from the current working directory.
#$ -M <email address of user>
#$ -m beas    # notify by e-mail in case of the following events: Begin, End, Abort, Suspend. 

# MAIN BODY    
# Synchronize input data to HPC

mkdir input  # make a folder where all input data is stored

export PATH=${HOME}/rclone-v1.45-linux-amd64/:${PATH}  # set path to newest rclone version
rclone version

rclone sync surfdrive:myinputfolder  ./input -cv  # one-way sync folders

echo Transfer input done

# Perform tasks

mkdir output
cp ./input/* ./output/

sleep 10

# Synchronize output data back to storage

rclone sync ./output surfdrive:myoutputfolder -cv

echo End of Job
```
> In the above script:
>1. fill in your email address on the indicated place.
>2. check whether the rclone version is the same as the version you installed (see [this manual](./surfdrive))
>3. if necessary, change the rclone paths to <name remote in rclone config>:<surfdrive folder>

When using Yoda or the Data Archive, the transfer commands in the above scripts need to be replaced by the appropriate commands for these platforms. Example scripts for using [Yoda](../scripts/transferjob_yoda) and [Archive](../scripts/transferjob_archive) can be found following the links. Note that when using 'icommands' for transferring data to and from Yoda, the `iinit` command needs to be issued at the command line to generate a password for connecting before submitting the job.

## Links

[Typical Workflow](./workflow.md)  
[Evaluation of data transfer](./Evaluation.md)  
[Transfer Instructions Yoda](./Yoda.md)  
[Transfer Instructions Cloud Storage](./surfdrive.md)  
[Transfer Instructions Data Archive](./Archive.md)  

