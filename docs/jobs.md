## Creating a job script data synchronization

A synchronization command can be incorporated in a shell script or a job script to take care of the transfer of input and output data directly to and from the remote storage platforms. This can help to keep your HPC working environment clean and your data in one place. On this page we provide instructions how to setup job scripts on the UBC cluster and the Lisa cluster. 

### Lisa

If you work with data volumes of a couple of Gigabytes or less, and reading and writing of data is not a main task in your workflow, you can transfer the data to your 'home file system'. This is the file system you have available upon login to Lisa. However, when working with large data volumes and reading and writing of data becomes a significant part of your workflow it may be better to use the scratch file system on the compute nodes. Examples of these 2 methods are provided below.

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
    
# Synchronize input data to HPC

mkdir input  # make a folder where all input data is stored

export PATH=${HOME}/rclone-v1.45-linux-amd64/:${PATH}  # set path to newest rclone version
rclone version

rclone sync surfdrive:myfolder  ./input -cv  # one-way sync folders

echo Transfer input done

# Perform tasks

mkdir output
cp ./input/* ./output/

sleep 10

# Synchronize output data back to storage

rclone sync ./output surfdrive:Transfer/Output -cv

echo End of Job
```

> In the above script:
1. fill in your email address on the indicated place.
2. check whether the rclone version is the same as the version you installed (see [this manual](./surfdrive))
3. if necessary, change the rclone paths to <name remote in rclone config>:<surfdrive folder>










    # Yoda option 
module load icommands
iinit
irsync i:myfolder  .
iget myfolder/myfile

    # Archive option
rsync <>  .
rclone

module load R             # load the R modules

cd $SLURM_SUBMIT_DIR      # go to the directory from which the job was submitted

cp -r $SLURM_SUBMIT_DIR/R "$TMPDIR"
cp -r $SLURM_SUBMIT_DIR/data "$TMPDIR"

cd "$TMPDIR"
mkdir ./output

            # The "&" at the end forces the R scripts to run in the background
            # Every script is started without waiting upon his predecessor.
            # If there are less tasks than cores in the node this will be fine.
            # Else the tasks (Rscripts) will compete with each other for the available cores
            # resulting in a longer lead time of the batch job

Rscript ./R/digits_svm_pl.R  &

            # Wait till all previous programs have ended, because we must copy all the
            # output files of the batch job back to the home space of the user
wait

