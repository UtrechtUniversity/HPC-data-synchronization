## Instructions for synchronization of data on Cloud storage platforms and HPC 

To synchronize data between the Data Archive and Lisa is very easy. When you have an account for the Data Archive, you can access the Data Archive directly from Lisa via the following path:

```
/archive/<username>
```
Hence, transfering data can be done using standard Unix commands (`cp`, `mv`, `rsync`)

To synchronize a directory use the following command:

```
rsync <source> <destination>
```
E.g:

```
rsync -rPv ~/mylisafolder/ /archive/myusername/myarchivefolder/
```
`-rPv` means the following flags (options) are used:  
`-r` recursive - store the whole folder including subdirectories  
`-P` report progress of transfer  
`-v` verbose; increase the amount of information in the logs  

Note that the contents of the folder are now in the staging area of the Archive. They will tranfer automatically to tape after a while.
You can also issue a commands to do this. Read [this page](https://userinfo.surfsara.nl/systems/shared/software/dmf) for more info about these commands.
Check the status of your files using the following command:

```
dmls -l /archive/<username>
```
This will list your files and folders in Archive and their status. The status values are:
```
* REG: Regular files are user files residing only on disk
* MIG: Migrating files are files which are being copied from disk to tape
* DUL: Dual-state files whose data resides both online and offline
* OFL: Offline files whose data is no longer on disk
* UNM: Unmigrating files are files which are being copied from tape to disk
```

When you want to copy in opposite direction, first check whether the data is present in the staging area (REG).
When a file is offline it may take a while before it will transfer back.

To synchronize data from Archive to Lisa, issue the following command:

```
rsync -rPv ~/mylisafolder/ /archive/myusername/myarchivefolder/
```

>Try to store files of significant size (> 1 GB) as much as possible. Smaller files will always be accepted, but will lower the performance of restoring your files from tape.
If you have many small files, make sure to pack them using a file archiving tool like tar or dmftar.


## Job scripts
The above commands can be used in job scripts to transfer input data and scripts from the storage platform to the HPC cluster at the start of a job, and transfer the output back to the storage when the job has finished (and thereby clean up the HPC workspace).

Further documentation about jobscripts and example scripts can be found in [this section](./jobs.md).

Previous: [Evaluation of transfer options](./Evaluation.md)

