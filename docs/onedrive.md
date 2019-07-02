## Rclone interactive menu instructions for OneDrive

Setting up synchronization between onedrive and HPC with Rclone is a complicated process and requires quite a few steps.  
You need a web browser for authentication, but a browser is generally not available on Lisa and UBC.
To be able to authenticate via a browser one has to install Rclone on a local working station, and to make it even more complicated, when working on Windows, one has to install a Windows Subsystem for Linux, to be able to install and operate Rclone.
The upside is that this procedure has to be performed once (and potentially renewed when passwords expire), after which Onedrive works quite fluently.

The following instructions will guide you through the process of making a config file for Onedrive.

## Steps

### Step 0 Install Ubuntu (on Windows systems only)

When working on a Windows system, you have to enable Windows Subsystem for Linux (WSL).

To do this: Open Windows PowerShell and issue the following command:
```
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

Restart your system after you have activated WSL.

Next, open Start and search for `Ubuntu` and press Enter to open or install Ubuntu.

Alternatively, Install Ubuntu from the Microsoft App Store.

### Step 1 Install Rclone


**Using linux or Ubuntu under Windows**

Install Rclone with the following commands:

```
$    wget https://downloads.rclone.org/rclone-current-linux-amd64.zip
$    unzip rclone-current-linux-amd64.zip
```
Use the `ls` command to check which version of rclone you have. Use this version number in the command below (i.e. change 1.48 in the command below to your version number if you have a different version). 

```
$    export PATH=${HOME}/rclone-v1.48-linux-amd64/:${PATH}
```


**Using mac**  

Follow instructions [here](https://rclone.org/downloads/).


### Step 2 Getting your own Client ID and Key

Next, generate your own Client ID and Key for Onedrive by following the steps below:

1.	Open https://apps.dev.microsoft.com/#/appList, then click Add an app (Choose Converged applications if applicable)  

2.	Enter a name for your app, and click continue. Copy and keep the Application Id under the app name for later use.  

3.	Under section Application Secrets, click Generate New Password. Copy and keep that password for later use.  

4.	Under section Platforms, click Add platform, then Web. Enter http://localhost:53682/ in Redirect URLs.  

5.	Under section Microsoft Graph Permissions, Add these delegated permissions: Files.Read, Files.ReadWrite, Files.Read.All, Files.ReadWrite.All, offline_access, User.Read.  

6.	Scroll to the bottom and click Save.  

Now the application is complete.  

### Step 3 Generate a config file on your remote machine

In your ssh session to your HPC system: type `rclone config` and press enter.

After you have typed `rclone config`, you will see a short list of options:

```
e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
```
You will see similar lists later on in this menu. You select an option by typing the character in front and press enter.

1.	Type `n` for new remote and press enter

2.  Type a name for the remote storage, e.g. `onedrive` or `OD`.

A list appears with different storage types:

3.  Type `18` and press enter for 'onedrive'

4.	Copy and paste the app ID (step 2) as Client ID  

5.	Copy and paste the password (step 2) as Secret  

5.	Edit advanced config? Type ‘n’  

6.	Use auto config? Type ‘n’  

**Now you will receive a command for authorization.
The command will look something like this:
rclone authorize "onedrive" "<Client ID>" "<password>"**

7.  Copy and paste the command to your **local command line session** (e.g. Ubuntu under Windows)
    
8.	In your local command line session, you will be asked to navigate to `http://127.0.0.1:53682/auth` with your browser. Type the address in your internet browser.

9.	You will see a Microsoft page, where you can select (or you have to login to) your Microsoft account. When everything went correct, you will see the message: “Success! Please go back to Rclone”

10.	Go back to your **local command line session**. You will see that a token has been generated that has to be copied to your **remote machine** (Lisa/UBC/etc.). Go to your remote machine and paste the token behind: `result>` and press Enter.

11. Next you will see:  
`Choose a number from below, or type in an existing value:`  
    Type `1`
    
12.	If all went correct, you will see: 
```
Found 1 drives, please select the one you want to use: 
0: OneDrive
```  
Type `0`

13.	Type `y` and `y` for the next two questions to finish the menu.



Go back to the [main instructions page](./surfdrive.md).
