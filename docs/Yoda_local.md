# Data transfer between Yoda and your local workingstation

To run analysis on your local working station (e.g. laptop) with data that is stored in Yoda, you can map yoda as a network drive on your working station (find instructions [here](https://yoda.sites.uu.nl/home/how-to-quick-guide/create-a-network-share/)). This drive can be accessed via a file explorer or directly within your analysis software. In some cases, it may be that accessing your data directly from your network drive with analysis software is not suitable for your use case (e.g. when performing large operations on big data files). Creating a local copy of your data may help to solve this problem.

Transferring data between Yoda and your local working station can be done in several ways. We describe three methods: using a mapped network drive, using the command line tool icommands, or manual synchronization using cyberduck. These three options differ in terms of transfer speed and intuitiveness. 

## Network drive

Simply browse to the file location on the network drive and copy-paste it to a local folder. This method is intuitive but may also be tedious when you need many files, and can be prone to user errors.

## Icommands

Icommands is the standard tool for transferring data to and from Yoda using a command line interface. On linux you can install icommands using the instructions on [this page](./install_icommands.md).

On Mac an Windows it is only possible to use icommands via a linux subsystem or a virtual machine.

In recent windows versions, it is possible to install a "Windows Subsystem for Linux" (or WSL). In order to do this, one has to turn on WSL. Open PowerShell and issue the following command:

```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```
Restart your system after you have activated WSL.

Next, open Start and search for `bash.exe` and press Enter. 

If bash is already installed, you will enter bash command line, where you can issue bash commands to install icommands (go to [this page](./install_icommands.md) for installation instructions).

If bash is not installed you will be asked to type `y` and press Enter to download and install Bash from the Windows Store.

Next you need to create a default UNIX user account. Type the username that you would like to use. 

When you succesfully installed bash, start the bash command line and install icommands using the instructions on [this page](./install_icommands.md). From there, continue with configuration of the icommands [instructions here](./Yoda.md).


## Cyberduck
Cyberduck is a handy open source tool for file transfer between remote platforms (such as Yoda and High Performance Computing platforms) and your local working station.

The instructions for using Cyberduck in combination with Yoda below are adapted from https://irods.org/2015/09/howtocyberduck/.

1. Download the installer for your platform via https://cyberduck.io/download/.
2. Locate the downloaded file and double click to begin installation. 
3. Go through the installation process. 

Next, configure Cyberduck for use with Yoda.
To connect Cyberduck to Yoda, you must first bookmark the connection using a `.cyberduckprofile` Connection Profile file.

1. Click [this link](http://people.renci.org/~danb/FOR_DEMOS/cyberduck/irods.cyberduckprofile) to download a Connection Profile template, which contains preconfigured settings for using Cyberduck with iRODS repositories.

2. Use a text editor to edit the contents of the Connection Profile.

3. Change the field below "Hostname" to your yoda host address (see example below)

4. Change the field below "Region" to your iRODS Zone name and default resource according to the format `tempZone:demoResc`. If you don't know this information, consult your data manager or RDM support.

5. Add the lines  
`<key>Authorization</key>`  
`<string>PAM</string>`
at the bottom of the file (see the example below).

6. Save the updated Connection Profile in the profiles folder of your Cyberduck directory (e.g. C:\Program Files (x86)\Cyberduck\profiles ). Make sure the file has a `.cyberduckprofile` extension.


### Example cyberduck profile
```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>Protocol</key>
        <string>irods</string>
        <key>Vendor</key>
        <string>iRODS</string>
        <key>Description</key>
        <string>iRODS Cyberduck Bookmark</string>
        <key>Hostname Configurable</key>
        <true/>
        <key>Port Configurable</key>
        <true/>
        <key>Default Hostname</key>
        <string>its.data.uu.nl</string>
        <key>Region</key>
        <string>nluu12p:irodsResc</string>
        <key>Default Port</key>
        <string>1247</string>
        <key>Username Placeholder</key>
        <string>Yoda Username</string>
        <key>Password Placeholder</key>
        <string>Yoda password</string>
        <key>Authorization</key>
        <string>PAM</string>
    </dict>
</plist>
```

Double click the updated irods.cyberduckprofile file to open it as a Cyberduck bookmark. The profile will open so you can edit the defaults.

1. Update the Cyberduck bookmark.
2. Update the Nickname field with an appropriate name to identify the bookmark.
3. Update the Username field with your iRODS user name.
4. In the More Options section, update the "Transfer Files" setting, selecting "Open multiple connections".
5. Close the bookmark window.
6. Now under the 'bookmarks' tab, double click the created bookmark to start the connection. Right click a folder you want to work on 


The steps above describe the configuration process on a windows pc. It is also possible to use use cyberduck on other operating systems or via windows command line. 

Check the [instructions page](https://trac.cyberduck.io/wiki/help/en/howto/cli) of Cyberduck to find specific installation and operation instructions.
The operating system specific paths for installation of the cyberduck profiles can be found [here](https://trac.cyberduck.io/wiki/help/en/howto/cli#Profiles).

Other options for transfer include: webdav connection using [Rclone](https://rclone.org/) or manual drag-and-drop transfer using [Winscp](https://winscp.net/).

## Links
[Back to evaluation of storage and transfer tools](./Evaluation.md)

