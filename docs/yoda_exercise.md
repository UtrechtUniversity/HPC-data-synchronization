# Exercise

This short exercise is designed for beginning users to get familiar with the `iget` and `iput` commands for copying single files between Yoda and HPC platforms.

Log in to yoda via the web portal, or go to the mounted network drive on your working station.

Make a text file, called `test.txt`

In your ssh session to the HPC system, find the Yoda folder where the file has be created using the `icd` and `ils` commands. When you have navigated to the folder where the text file is located using `icd`, collect the text file with the `iget` command. 

```
iget test.txt .  
```
The command needs the following arguments:

```
iget <source> <destination>
```

Source should provide the filename (and if necessary the path to the file).
Destination should provide the destination directory on the HPC system (and if necessary and alternative filename).

E.g:

``` 
iget my_yoda_folder/myfile ./my_hpc_folder/myalternativefile
```

To copy a file to yoda, use the `iput` command. This command works similar to `iget`.

```
iput <source> <destination>
iput ./my_hpc_folder/myfile my_yoda_folder/myalternativefile
```

Copy the created text file back to Yoda and give a different name:

```
iput ./test.txt test2.txt  
```

Go back to the [Synchronization manual](./Yoda.md).