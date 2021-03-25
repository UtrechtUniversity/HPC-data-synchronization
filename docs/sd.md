## Rclone interactive menu instructions for Surfdrive

The following instructions will guide you through the Rclone interactive menu to make a config file for Surfdrive.
After you have typed `rclone config` (as instructed on previous page), you will see a short list of options:

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

2.  Type a name for the remote storage, e.g. `surfdrive` or `SD`.

A list appears with different storage types:

3.  Type `34` and press enter for 'webdav'

4.	Fill in the URL. You can look this up via the web portal of surfdrive. In the top right corner click your account name. Go to settings. In the left panel, click security. At the very bottom of the page there will be a section WebDAV passwords. There is also an URL, something like: https://surfdrive.surf.nl/files/remote.php/nonshib-webdav Use this URL.

5.	Before you continue with the Rclone menu, first perform the following step via the web portal of surfdrive. Fill in an app name (e.g. lisa) on the security settings page (same page as previous step) and click “create new app password”. The page will show a username and a password. You will need these in the following steps of the Rclone menu.

6.	Select the type of webdav storage system. Type: `2` for Owncloud.
6.	Type in your user name from surfdrive (this is the username found in the web portal (step 5))
7.	Select: y) Yes type in my own password
8.	Type in your password from the web portal and type it in again for confirmation. 
9.  Skip the Bearer token option by pressing enter.
9.	Confirm your settings by typing `y`.

Go back to the [main instructions page](./surfdrive.md).
