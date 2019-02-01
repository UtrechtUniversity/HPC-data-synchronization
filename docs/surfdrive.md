
## Instructions for synchronization of data on Cloud storage platforms and HPC 

To synchronize data between Cloud storage platforms and HPC using Rclone, follow these steps (steps are elaborated below):

1. Install Rclone
2. Make a config file
3. Submit Synchronization commands

Step 1 only needs to be performed once. Step 2 is performed once for each storage platform that you want to connect to. Every subsequent HPC session you can directly start using Rclone for synchronization.

### Step 1: Install Rclone (first time only)

Before installing Rclone, first check whether Rclone is already installed on the HPC system. Type:

```
rclone version
```

The response is either:

```
rclone: command not found
```
or,

```
rclone v<version number>
```
If there is a version of rclone installed, it may be an old version. Compare the version number with the most current version on [this website](https://rclone.org/downloads/).

At the moment of writing Rclone version v1.35 is installed on Lisa, and the most current version is v1.45.

To download and install the most current version of rclone type (or copy-paste) the following three commands:

```
wget https://downloads.rclone.org/rclone-current-linux-amd64.zip
unzip rclone-current-linux-amd64.zip
```

check the version number in name of the the unzipped folder with `ls` and replace <version number> with the right number in the command below:

```
export PATH=${HOME}/rclone-v<version number>-linux-amd64/:${PATH}
```


### Step 2:  Make a config file (perform once for every storage platform)

Rclone has an interactive menu to generate a config file for you. You need to complete this menu once for each storage platform that you want to connect to. You can use Rclone for many different types of storage platforms: check the [homepage](https://rclone.org/) for a list. Surfdrive and Research drive are based on Owncloud software. Many platforms (including Yoda, Data Archive or the U: network drive of UU student and employees) are accessible via the WebDAV protocol which is also in the list. 

To start the interactive menu, type:

```
rclone config
```

You will enter an interactive menu. On separate pages, we provide instructions for completing the interactive menu for different storage options:

[Config file surfdrive](./sd.md)  
[Config file research drive](./rd.md)  
[Config file U: network drive](./udrive)  

When you have completed the menu, the config file named 'rclone.conf' resides in the folder .config/rclone/ by default.

Check whether the connection works by listing the directories of the storage platform.

```
rclone lsd <chosen name>:
```
E.g.

```
rclone lsd surfdrive:
```

### Step 3: Submit Synchronization commands

Each time you login to the HPC system you need to run the following command from step 1 to append the path to the rclone software.

```
export PATH=${HOME}/rclone-v<version number>-linux-amd64/:${PATH}
```

> Warning! Synchronization with Rclone makes the destination folder equal to the source folder and deletes files and folders in he destination folder that are not present in the source folder. Therefore it is wise to use the --dry-run flag to see what will be copied and deleted. 

```
rclone sync <source> <destination> --dry-run
```
E.g:
```
rclone sync surfdrive:Mysharedfolder ./Mysharedfolder --dry-run
```
When you are sure you would like to proceed, remove the `--dry-run` flag and run the command again.

```
rclone sync surfdrive:Mysharedfolder ./Mysharedfolder -cPv
```
`-cPv` means the following flags (options) are used:  
`-c` skip files that are already present (compared using checksums)  
`-P` report progress of transfer  
`-v` verbose; increase the amount of information in the logs  

By default, multiple files are transferred in parallel. You can control the number of parallel threads as well as the number of checkers that calculate the checksums (to check whether the copied files are equal on both ends). Use the following commands:
```
--checkers=16 --transfers=16
```
E.g:
```
rclone sync surfdrive:Mysharedfolder ./Mysharedfolder -c --checkers=16 --transfers=16 -Pv
```

To synchronize in opposite direction: 

```
rclone sync ./Mysharedfolder surfdrive:Mysharedfolder -cPv
```
>It is recommended to create separate input and output folders on your HPC system. An input folder for files that are sent from storage to HPC before running a job and output for files that are sent from HPC to storage. You can consider creating bash scripts for the synchronization commands in these folder to reduce the propability of mixing up sources and destinations, which would result in data loss.

## Job scripts
The above commands can be used in job scripts to transfer input data and scripts from the storage platform to the HPC cluster at the start of a job, and transfer the output back to the storage when the job has finished (and thereby clean up the HPC workspace).

Further documentation about jobscripts and example scripts can be found in [this section](./jobs.md).

Previous: [Evaluation of transfer options](./Evaluation.md)

