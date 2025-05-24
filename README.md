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