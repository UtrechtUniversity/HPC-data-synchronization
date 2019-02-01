## Rclone interactive menu instructions for Data Archive

The following instructions will guide you through the Rclone interactive menu to make a config file for the Data Archive.
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

2.  Type a name for the remote storage, e.g. `Archive`.

A list appears with different storage types:

3.  Type `23` and press enter for 'sftp'

4.	Host> Fill in the host URL: `archive.surfsara.nl`

5.	User name> Type in your archive user name
6.  Port> press return for default
7.	Password> Type: n (leave this optional password blank)
8.	Key file> press return to leave blank
9.  Use_insecure_cipher> press return to leave blank
10. advanced options> no
11.	Confirm your settings by typing `y`.

Go back to the [main instructions page](./ArchiveUBC.md).