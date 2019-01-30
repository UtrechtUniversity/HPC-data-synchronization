
ways to work with your Dropbox content across the cluster.
rclone
We were looking for a product that:
•	didn’t need to run as a service (always on), like the Dropbox client. These are extremely ‘expensive’ when used by many users on a multi-user system, and Dropbox was one of the most expensive around.
•	would be able to sync to and from not just Dropbox, but some other vendors, too, particularly: 
o	Amazon S3
o	Box
o	Google Drive
o	Microsoft OneDrive
•	would be simple to set up, and easy to implement into cluster workflow
•	could run from anywhere on the cluster, not just the login nodes!
Enter rclone! Spend a few minutes configuring your ‘remotes’ on the cluster via the ‘rclone config’ command (see full instructions here!!), then you’re ready to sync, copy, etc to and from whichever 3rd party cloud storage system you like, all using the same command structure, which is really useful. So I can change my 3rd party cloud storage solution from Dropbox to Box, but still use the same commands to move / sync files, just changing the remote I’m connecting to. Neat!




## Job scripts
The above commands can be used in job scripts to transfer input data and scripts from the storage platform to the HPC cluster at the start of a job, and transfer the output back to the storage when the job has finished (and thereby clean up the HPC workspace).

Further documentation about jobscripts and example scripts can be found in [this section](./jobs.md).

