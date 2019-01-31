
## Instructions for synchronization of Yoda and HPC folders

When you have a Yoda account and icommands are installed on the HPC system, you have to follow the following steps (steps are elaborated below) to synchronize data:

0. Make a config file
1. Load icommands
2. Initialize connection to iRODS
3. Submit Synchronization commands

Step 0 only needs to be performed once. The other steps need to be performed every HPC session.

### Step 0:  Make a config file (first time only)

You may need help from your datamanager or contact Yoda support to obtain the information needed for the config file.

In the home directory of your HPC system, make a directory called .irods

```
mkdir .irods
cd .irods
```

In this directory, make a file named `irods_environment.json`.

```
touch irods_environment.json
```

Edit the file using a linux text editor like 'vim' or (when working via e.g. MobaXterm) a windows text editor.
Copy and paste the text below to the file and fill in the fields marked with '< >'.

```
{
    "irods_host": "<your category>.data.uu.nl",
    "irods_port": <port number>,
    "irods_default_resource": "irodsResc",
    "irods_user_name": "<user name>",
    "irods_zone_name": "<zone name>",
    "irods_home": "/<zone name>/home",
    "irods_cwd": "/<zone name>/home",
    "irods_ssl_verify_server": "none",
    "irods_authentication_scheme": "pam"
}
```
Save and close the file.

### Step 1: Load icommands (not required at UBC cluster)

Load icommands on Lisa as follows:

```
module load icommands
```

### Step 2: Initialize connection to iRODS

Initialize the connection to the Yoda system as follows:

```
iinit
```
Type your Yoda password when requested.

Type `ils` to see whether the connection has been established. The output of the `ils` command will list the current Yoda folder and the folders that are located within the current folder.

`iinit` and `ils` are commands which can only be used when icommands is active. Some of these commands are very similar to standard unix commands. When icommands is active you can still operate the HPC system using normal unix commands. A complete list of all 'icommands' can be found [here](https://docs.irods.org/4.2.4/icommands/user/).

A short exercise can be found [here](./yoda_exercise.md).

### Step 3: Submit Synchronization commands

The irsync command is used to synchronize data between a Yoda folder and an HPC folder.
The command is used as follows.

```
irsync <source> <destination>
```

In contrary to the `iput` and `iget` commands, in `irsync` it is necessary to put  'i:' before the Yoda path. The Yoda path (directly after 'i:') to the folder that should be synchronized should be relative to the **current** Yoda folder (check with `ils`). 

E.g.

```
irsync -rKV i:myfolder /my_hpc_folder
```
`-rKV` means the following flags (options) are used:  
`-r` recursive - store the whole subdirectory  
`-K` Calculate and verify the checksum on the data  
`-V` Very verbose  

To synchronize in the opposite direction

```
irsync -rKV /my_hpc_folder/ i:myfolder
```
> note the '/' at the end of /my_hpc_folder/ that is not used in the command above.

### Parallel transfer
With icommands it is possible to transfer individual files in parallel using multiple ports. The flag `-N` can be used to control the number of parallel threads. When not specified the server decides the number of threads. For large files this number is 16 threads by default. 

At the time of writing, parallel transfer is not possible on Lisa. For this reason the flag `-N 0` should be included when transferring files to and from Lisa:

```
irsync -rKV -N 0 i:myfolder /my_hpc_folder
```

## Job scripts
The above commands can be used in job scripts to transfer input data and scripts from the storage platform to the HPC cluster at the start of a job, and transfer the output back to the storage when the job has finished (and thereby clean up the HPC workspace).

Further documentation about jobscripts and example scripts can be found in [this section](./jobs.md).

Previous: [Evaluation of transfer options](./Evaluation.md)
