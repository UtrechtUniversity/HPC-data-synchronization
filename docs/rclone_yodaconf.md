## Rclone interactive menu instructions for Yoda

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

2.  Type a name for the remote storage, e.g. `Yoda`.

A list appears with different storage types:

3.  Type `24` and press enter for 'webdav'

4.	Fill in the URL. https://<your category>.data.uu.nl

5.	Select the type of webdav storage system. Type: `4` for 'other'.
6.	Type your Yoda user name, typically your uu mail address. 
7.	Select: y) Yes type in my own password
8.	Type in your Yoda password and type it in again for confirmation. 
9.  Skip the Bearer token option by pressing enter.
9.	Confirm your settings by typing `y`.

Go back to the [main instructions page](./rclone_yoda.md).
