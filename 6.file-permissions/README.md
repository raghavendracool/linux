# File Permissions Management in Linux

## Introduction to File Permissions
Linux file permissions determine who can read, write, or execute files and directories. Each file and directory has three levels of permission:
- **Owner (User)**: The creator of the file.
- **Group**: Users belonging to the assigned group.
- **Others**: All other users on the system.

Permissions are represented as:
- **Read (`r` or `4`)** – View file contents.
- **Write (`w` or `2`)** – Modify file contents.
- **Execute (`x` or `1`)** – Run scripts or programs.

To check file permissions, use:
```bash
ls -l filename
```
Output example:
```bash
-rwxr--r-- 1 user group 1234 Mar 28 10:00 myfile.sh
```

## Changing Permissions with `chmod`
### Using Symbolic Mode
Modify permissions using symbols:
- Add (`+`), remove (`-`), or set (`=`) permissions.

Examples:
```bash
chmod u+x filename  # Add execute for user
chmod g-w filename  # Remove write for group
chmod o=r filename  # Set read-only for others
chmod u=rwx,g=rx,o= filename  # Set full access for user, read/execute for group, and no access for others
```

### Using Numeric (Octal) Mode
Each permission has a value:
- Read (`4`), Write (`2`), Execute (`1`).

Examples:
```bash
chmod 755 filename  # User (rwx), Group (r-x), Others (r-x)
chmod 644 filename  # User (rw-), Group (r--), Others (r--)
chmod 700 filename  # User (rwx), No access for others
```

## Steps: Trainer Creates Script → Student Gets RWX Access

### Step 1 — Login as `trainer`, create the script

```bash
su - trainer
# or open trainer's terminal

mkdir -p ~/shared
vim ~/shared/helloworld.sh
```

Add content, save and exit:

```bash
:wq
```

---

### Step 2 — Set directory permission

Student must be able to enter the directory.

```bash
chmod o+rx /home/trainer
chmod o+rx /home/trainer/shared
```

---

### Step 3 — Set file permissions

Give `rwx` permission to others, so the student can read, write, and execute the script.

```bash
chmod o+rwx /home/trainer/shared/helloworld.sh
```

Verify:

```bash
ls -l /home/trainer/shared/helloworld.sh
# should show: -rwxr-xrwx or similar with others = rwx
```

---

### Step 4 — Switch to `student` and test all 3 permissions

```bash
su - student

# 1. READ
cat /home/trainer/shared/helloworld.sh

# 2. WRITE
echo "echo Hello" >> /home/trainer/shared/helloworld.sh

# 3. EXECUTE
bash /home/trainer/shared/helloworld.sh
```

---

### Permission Meaning

```text
r = read
w = write
x = execute
```

```bash
chmod o+rwx /home/trainer/shared/helloworld.sh
```

Meaning:

```text
o = others
+rwx = add read, write, execute permission
```

So any other user, including `student`, can read, edit, and execute the script.


## Changing Ownership with `chown`
Modify file owner and group:
```bash
chown newuser filename  # Change owner
chown newuser:newgroup filename  # Change owner and group
chown :newgroup filename  # Change only group
```

Recursively change ownership:
```bash
chown -R newuser:newgroup directory/
```

## Changing Group Ownership with `chgrp`
```bash
chgrp newgroup filename  # Change group
chgrp -R newgroup directory/  # Change group recursively
```

## Special Permissions
### SetUID (`s` on user execute bit)
Allows users to run a file with the file owner's permissions.
```bash
chmod u+s filename
```
Example: `/usr/bin/passwd` allows users to change their passwords.

### SetGID (`s` on group execute bit)
Files: Users run the file with the group's permissions.
Directories: Files created inside inherit the group.
```bash
chmod g+s filename  # Set on file
chmod g+s directory/  # Set on directory
```

### Sticky Bit (`t` on others execute bit)
Used on directories to allow only the owner to delete their files.
```bash
chmod +t directory/
```
Example: `/tmp` directory.

## Default Permissions: `umask`
`umask` defines default permissions for new files and directories.
Check current umask:
```bash
umask
```
Set a new umask:
```bash
umask 022  # Default: 755 for directories, 644 for files
```

## Conclusion
Understanding file permissions is essential for system security and proper file management. Using `chmod`, `chown`, and `chgrp`, you can control access to files and directories efficiently.
