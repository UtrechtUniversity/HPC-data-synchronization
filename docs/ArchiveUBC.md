## Instructions for synchronization of data on Cloud storage platforms and HPC 

To synchronize data between Cloud storage platforms and HPC using Rclone, follow these steps (steps are elaborated below):

1. Generate SSH keys
2. Install Rclone
3. Make a config file
4. Submit Synchronization commands

Step 1 and 2 only need to be performed once. Step 3 is performed once for each storage platform that you want to connect to. Every subsequent HPC session you can directly start using Rclone for synchronization.

### Step 1:  Generate SSH keys (perform once)

In your SSH sessio to UBC, enter the following commands to generate ssh keys and allow automatic login using an  ssh-agent. First enter:

```
ssh-keygen -t ed25519
```
You will be asked to enter a file name in which to save the key. Type: 
```
id_rsa
```
Then you will be asked to enter a passphrase. Fill in passphrase (Enter a sentence you can remember easy for the pass-phrase question).

Repeat passphrase.

Next, view the contents of id_rsa.pub with VIM.

```
vim ./.ssh/id_rsa.pub
```

Now, in a separate window, start an ssh session to the Data Archive.

In this ssh session to the Archive, create directory `.ssh`

```
mkdir .ssh
cd .ssh
```
In this folder, make a file called authorized_keys

```
vim authorized_keys
```
Now copy the contents of the id_rsa.pub file in the other ssh session (UBC) and paste this in the authorized_keys file on the archive.

Save and quit: `:wq`

Now you have arranged that you have to type in the pass-phrase only once for each login-session on UBC.

Type now (or after a new login)

```
ssh-agent bash
```
Next, type

```
ssh-add
```
Fill in the passphrase that you have typed above.

To test if everything is setup correctly, within your SSH session to the UBC cluster, make an SSH connection to the Data Archive 
```
ssh <username>@archive.surfsara.nl
```
If all is correct, you will login directly without password or passphrase.
Logout again from this ssh session from UBC to archive.

`logout`

### Step 2: Install Rclone (first time only)

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

### Step 3:  Make a config file (perform once)

Rclone has an interactive menu to generate a config file for you. You need to complete this menu once for each storage platform that you want to connect to. You can use Rclone for many different types of storage platforms: check the [homepage](https://rclone.org/) for a list. Surfdrive and Research drive are based on Owncloud software. Many platforms (including Yoda, Data Archive or the U: network drive of UU student and employees) are accessible via the WebDAV protocol which is also in the list. 

To start the interactive menu, type:

```
rclone config
```

You will enter an interactive menu. On [this page](./rclone_archive.md), we provide instructions for completing the interactive menu.

### Step 4: Submit Synchronization commands

Each time you login to the HPC system you need to run the following command from step 1 to append the path to the rclone software.

```
export PATH=${HOME}/rclone-v<version number>-linux-amd64/:${PATH}
```
You also need to initialize the ssh-agent each time you login.

```
ssh-agent bash
```
Next, type

```
ssh-add
```
Fill in the passphrase you have created when you generated the hpc keys (Above).

Now start synchronizing.

> Warning! Synchronization with Rclone makes the destination folder equal to the source folder and deletes files and folders in he destination folder that are not present in the source folder. Therefore it is wise to use the --dry-run flag to see what will be copied and deleted. 

```
rclone sync <source> <destination> --dry-run
```
E.g:
```
rclone sync /hpc/<usergroup>/<username>/Mysharedfolder Archive:Mysharedfolder --dry-run
```
When you are sure you would like to proceed, remove the `--dry-run` flag and run the command again.


```
rclone sync /hpc/<usergroup>/<username>/Mysharedfolder Archive:Mysharedfolder -cPv
```

`-cPv` means the following flags (options) are used:  
`-c` skip files that are already present (compared using checksums)  
`-P` report progress of transfer  
`-v` verbose; increase the amount of information in the logs  

Note that the contents of the folder are now in the staging area of the Archive. They will tranfer automatically to tape after a while.
You can also issue a commands to do this. Read [this page](https://userinfo.surfsara.nl/systems/shared/software/dmf) for more info about these commands.

Start an SSH session to archive. Check the status of your files using the following command:

```
dmls -l
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

To synchronize data from Archive to UBC, issue the following command in your SSH session to UBC:


```
rclone sync Archive:Mysharedfolder /hpc/<usergroup>/<username>/Mysharedfolder -cPv
```
By default, multiple files are transferred in parallel. You can control the number of parallel threads as well as the number of checkers that calculate the checksums (to check whether the copied files are equal on both ends). Use the following commands:
```
--checkers=16 --transfers=16
```
E.g:
```
rclone sync surfdrive:Mysharedfolder ./Mysharedfolder -c --checkers=16 --transfers=16 -Pv
```
>It is recommended to create separate input and output folders on your HPC system. An input folder for files that are sent from storage to HPC before running a job and output for files that are sent from HPC to storage. You can consider creating bash scripts for the synchronization commands in these folder to reduce the propability of mixing up sources and destinations, which would result in data loss.

## Job scripts
The above commands can be used in job scripts to transfer input data and scripts from the storage platform to the HPC cluster at the start of a job, and transfer the output back to the storage when the job has finished (and thereby clean up the HPC workspace).

Further documentation about jobscripts and example scripts can be found in [this section](./jobs.md).

Previous: [Evaluation of transfer options](./Evaluation.md)



