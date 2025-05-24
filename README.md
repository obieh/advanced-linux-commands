# Advanced Linux commands
## This Project Demonstrates advanced linux commands and how to use them.

### Basic File Permissions
Linux assigns permissions to three types of users:

* Owner (User) – The user who created the file.

* Group – Users who are part of a specific group.

* Others (World) – All other users on the system.

### Each file/directory has three types of permissions:

* Read (r) – Allows viewing file contents or listing directory contents.

* Write (w) – Allows modifying file contents or creating/deleting files in a directory.

* Execute (x) – Allows running a file as a program or accessing a directory.

### Viewing Permissions

* Run `ls -l` to see permissions

![ls](./img/ls%20-l.png)

*-rw-r--r-- 1 user group 1024 May 25 10:00 file.txt*

* The first part (-rw-r--r--) shows permissions:

   *  = File type (- for file, d for directory).

  * rw- = Owner permissions (read, write).

  - r-- = Group permissions (read).

  - r-- = Others permissions (read).

  ### Changing Permissions with `chmod`

  #### Use chmod to modify permissions in two ways:

  **Symbolic Mode(u,g,o,a)**

  * u (user/owner), g (group), o (others), a (all).
  * +(add), - (remove), = (set exactly).

  #### Examples

  ```bash
  chmod u+x script.sh    # Add execute for owner
  chmod g-w file.txt     # Remove write for group
  chmod o=r-- file.txt   # Set others to read-only
  chmod a+rw file.txt    # Give read-write to all
  ```

#### Numeric Mode (Octal)
* Each permission has a number:
  - 4 = Read (r)

  - 2 = Write (w)

  - 1 = Execute (x) 

* Combine them (e.g., 7 = 4+2+1 for rwx).

#### Example:

```bash
chmod 755 script.sh    # rwxr-xr-x (Owner: rwx, Group/Others: r-x)
chmod 644 file.txt     # rw-r--r-- (Owner: rw-, Group/Others: r--)
```
### Changing Ownership with `chown` & `chgrp`
* **chown** changes the *owner* of a file:

```bash
chown user file.txt
chown user:group file.txt
```
* **chgrp** changes the *group*:
```bash
chgrp group file.txt
```

### Special Permissions
* Set User ID (SUID) (4) – Executes as the owner (e.g., **chmod 4755**).

* Set Group ID (SGID) (2) – Executes as the group (e.g., **chmod 2755**).

* Sticky Bit (1) – Only the owner can delete files in a directory (e.g., **/tmp**):

  - `chmod +t /shared_dir`

### Default Permissions (`umask`)

