## Rclone interactive menu instructions for U: drive

The following instructions will guide you through the Rclone interactive menu to make a config file for your U: drive. There is a [UU manual](https://handleidingen.uu.nl/en/handleiding/o-en-u-schijf-benaderen-via-webdav-onder-windows/) for connecting to the U: drive from your local working station via WebDAV. Connecting from HPC via Rclone requires the same information.

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

2.  Type a name for the remote storage, e.g. `udrive`.

A list appears with different storage types:

3.  Type `4` and press enter for 'other'

4.	Fill in the URL: https://webdav.uu.nl/users/<Solis-id> 

5.	As user name fill in your UU e-mail address.
7.	Select: y) Yes type in my own password
8.	Type in your (Solis) password and type it in again for confirmation. 
9.  Skip the Bearer token option by pressing enter.
9.	Confirm your settings by typing `y`.

Go back to the [main instructions page](./surfdrive.md).

