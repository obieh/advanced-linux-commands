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
### Create a file, check and change permision

* Run `touch script.sh` to create the file
* Run `ls -latr script.sh` to check permission
* Run `chmod +x` to add execute permission
* Run `chmod 755` to add execute permission to user, group and others

![](./img/chmod755.png)

### Create a text file and check permissions
* Run `touch file.txt`
* Run `chmod 777 file.txt`
* Run `ls -latr note.txt`


![](./img/ls%20-l.png)

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
### Change ownership of script.sh to user named johndoe who is in developers group.
* Run `sudo chown johndoe:developers /home/ubuntu/script.sh`
![](./img/chmod-user&group.png)

### Super User privilleges
- The superuser, or we can say root, is a special user account used for system administration purposes on Linux. They have all rights on the files like read write execute. However, if you are the root user and want to perform administrative task, prefix the command with `sudo`
* Run `sudo -i` to switch account to root. Type `exit` to switch back to your user account.

![](./img/sudo-i.png)

### Create a new user account
* Run `sudo adduser johndoe` to create a user named johndoe

![](./img/johndoe.png)

* Run `sudo usermod -aG sudo johndoe` to add johndoe to sudo group which give johnedoe administrative privileges.

![](./img/sudo-john-doe.png)

## Connecting to ec2 instance as johndoe.
### Copy existing key Run the following commnads

```bash
sudo mkdir -p /home/johndoe/.ssh #Create .ssh folder in johndoes's home dir
sudo cp ~/.ssh/authorized_keys /home/johndoe/.ssh/ #Copy authorised key to johnedoe .ssh folder.
sudo chown -R johndoe:johndoe /home/johndoe/.ssh
sudo chmod 700 /home/johndoe/.ssh
sudo chmod 600 /home/johndoe/.ssh/authorized_keys
```
![](./img/chmod-4-john-doe.png)

* `chown` → "Change owner" (the command to modify ownership).
* `-R`→ Recursive, meaning it applies to
    - The specified directory and
    - All files/subdirectories inside it.

* `john:john` → Sets:
    - User owner = john
    - Group owner = john

* `/home/johndoe/.ssh` → The target director

### Now connect to the ec2 as john doe
* log out as user ubuntu
* Run `ssh -i /path/to/key.pem johndoe@ec2-18-209-60-216.compute-1.amazonaws.com`

![](./img/login-in-as%20johndoe.png)

![](./img/logged-in-as-johndoe.png)

* Run `echo ~` to see home directory of johndoe

![](./img/echo~johndoe.png)

* Run `cd /home/johndoe` to get to johndoe's home directory.

![](./img/cd-home-jdoe.png)

### Switch User Accounts
* Type 'exit' to leave johndoe account
* Run `su johndoe` to login as user johndoe, type password when prompted.

![](./img/login-new-pw-johndoe.png)

### Special Permissions
* Set User ID (SUID) (4) – Executes as the owner (e.g., **chmod 4755**).

* Set Group ID (SGID) (2) – Executes as the group (e.g., **chmod 2755**).

* Sticky Bit (1) – Only the owner can delete files in a directory (e.g., **/tmp**):

  - `chmod +t /shared_dir`

### Default Permissions (`umask`)

