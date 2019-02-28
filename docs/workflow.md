# Typical HPC workflow

In order to keep a clear overview of the most recent versions of your data and scripts, it is recommended to use one 'central storage facility' in your workflow, such as YODA, Surfdrive, or a data archive. You can access the data from any working station (e.g. your own laptop) And when you do analyses on a HPC platform, you can transfer data from the storage facility to the HPC system and when your job is done you transfer the output back to storage. 

<img src="./pictures/example_workflow.png" alt="example" width="550" height="400">

## Storage
YODA (developed at the UU) is a data storage tool that can be used as 'central storage facility' (see figure). [Yoda](https://yoda.sites.uu.nl/home/introduction-to-yoda-2/) is built on state-of-the-art data storage and transfer technology and is suitable for a full range from researchers that just started working with large datasets and high performance computing to research groups that work with very large datasets. Yoda is not only a handy tool for long-term and secure storage of data; it is also possible to synchronize data to various platforms at very high transfer speeds. Alternatives are cloud storage platforms such as Surfdrive (SURFsara) and Google Drive (commercial), or Data-Archive (SURFsara).

## Data transfer and synchronization; ‘drag and drop’ versus command line tools
For users that are used to working with Windows or Apple computers, tools are available to connect to remote data storage as well as storage systems of HPC platforms from your working station. With these tools it is possible to manually transfer files using ‘drag and drop’ principles. Open source tools in this category are [Winscp](https://winscp.net/) and [Cyberduck](https://cyberduck.io/), or the more versatile [MobaXterm](https://mobaxterm.mobatek.net/), which can also be used for login in to HPC platforms. These tools are solid and intuitive for beginning users, but also somewhat slow which becomes relevant when you frequently need to transfer many gigabytes of data. When the number of files you work with increases, this also becomes a labour-intensive task. 
For users that are experienced with using command line interfaces and/or users that need to transfer large amounts of data, command line tools exist that are more efficient. The above-mentioned storage system YODA is typically accessed via ‘icommands’. Another very versatile tool that can be used in combination with many storage platforms is ‘Rclone’. These tools can be operated directly on the HPC platform and transfer commands can be incorporated in job scripts, which makes your work reproducible. 

Next: [Evaluation of storage and transfer tools](./Evaluation.md)  
Previous: [Introduction](../README.md)

Links:  
[Main page](../README.md)  
[Yoda staging](./Yoda.md)  
[Surfdrive staging](./surfdrive.md)  
[Archive staging](./Archive.md)  
[Glossary](./Glossary.md)

