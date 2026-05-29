# Linux Assignment Questions

## Beginner Level

### Assignment 1: Basic Linux Navigation

1. Print your current working directory.
2. Go to `/tmp` directory.
3. Create a folder named `linux-practice`.
4. Go inside `linux-practice`.
5. Create three files: `file1.txt`, `file2.txt`, and `file3.log`.
6. List all files in long format.
7. List hidden files also.
8. Create one hidden file named `.secret`.
9. Show the latest modified file at the bottom.
10. Delete `file2.txt`.

---

### Assignment 2: File Viewing and Editing

1. Create a file named `students.txt`.
2. Add five student names inside the file using `echo`.
3. View the file using `cat`.
4. View the first 3 lines using `head`.
5. View the last 2 lines using `tail`.
6. Open the file using `vi`.
7. Add one more student name.
8. Save and exit from vi.
9. Display the file content in reverse order.
10. Copy `students.txt` to `students_backup.txt`.

---

### Assignment 3: Directory and File Management

1. Create the below directory structure:

```text
/project
/project/dev
/project/qa
/project/prod
```

2. Create one file inside each folder.
3. Rename `dev` folder to `development`.
4. Copy the `qa` folder to `/tmp`.
5. Move the `prod` folder to `/opt`.
6. Remove the copied `qa` folder from `/tmp`.
7. Show the full directory tree using command.
8. Check size of `/project`.
9. Check disk usage using `df -h`.
10. Check folder usage using `du -sh`.

---

## Intermediate Level

### Assignment 4: User and Group Management

1. Create three users:
   - `devuser`
   - `qauser`
   - `opsuser`

2. Create three groups:
   - `dev`
   - `qa`
   - `ops`

3. Add `devuser` to `dev` group.
4. Add `qauser` to `qa` group.
5. Add `opsuser` to `ops` group.
6. Set password for all users.
7. Check user details using `id`.
8. Check group membership using `groups`.
9. Lock `qauser`.
10. Unlock `qauser`.

---

### Assignment 5: File Permissions

1. Create folder `/training`.
2. Create file `/training/demo.sh`.
3. Add below content in `demo.sh`:

```bash
echo "Welcome to Linux Training"
```

4. Give execute permission to owner only.
5. Run the script.
6. Give read and execute permission to group.
7. Remove write permission from others.
8. Change owner of file to `devuser`.
9. Change group of file to `dev`.
10. Verify permission using `ls -l`.

---

### Assignment 6: ACL Permission

1. Create users:
   - `trainer`
   - `student1`
   - `student2`

2. Create folder `/home/trainer/shared`.
3. Create file `/home/trainer/shared/helloworld.sh`.
4. Give only `student1` read, write, and execute access using ACL.
5. Do not give access to `student2`.
6. Verify ACL using `getfacl`.
7. Login as `student1` and test read/write/execute.
8. Login as `student2` and verify access is denied.
9. Remove ACL permission for `student1`.
10. Verify again.

---

## Advanced Level

### Assignment 7: Shell Script for User and Group Creation

Write a shell script named `create-users.sh` that performs the below tasks:

1. Create groups:
   - `developers`
   - `testers`
   - `support`

2. Create users:
   - `alice`
   - `bob`
   - `charlie`

3. Add:
   - `alice` to `developers`
   - `bob` to `testers`
   - `charlie` to `support`

4. Create home directory for each user.
5. Set default shell as `/bin/bash`.
6. Set temporary password for each user.
7. Force password change on first login.
8. Display user details using `id`.

---

### Assignment 8: Shell Script for File Permission Setup

Write a shell script named `setup-permission.sh` that performs below tasks:

1. Create `/company`.
2. Create subfolders:
   - `/company/dev`
   - `/company/qa`
   - `/company/support`

3. Create one file inside each folder:
   - `dev-script.sh`
   - `qa-script.sh`
   - `support-script.sh`

4. Set ownership:
   - `/company/dev` should belong to group `developers`
   - `/company/qa` should belong to group `testers`
   - `/company/support` should belong to group `support`

5. Set folder permission as `770`.
6. Set script permission as `750`.
7. Verify using `ls -l`.

---

### Assignment 9: Process Management

1. Start a background process using `sleep 500`.
2. Find the process using `ps`.
3. Find the process using `pgrep`.
4. Kill the process using `kill`.
5. Start another process.
6. Kill it using `pkill`.
7. Run `top`.
8. Run `free -h`.
9. Check load average using `uptime`.
10. Find top CPU consuming process.

---

### Assignment 10: Monitoring and Troubleshooting

1. Check CPU usage.
2. Check memory usage.
3. Check disk usage.
4. Check running processes.
5. Check listening ports.
6. Install Apache service.
7. Start Apache service.
8. Check Apache process.
9. Generate CPU load.
10. Generate memory load.
11. Identify high CPU process.
12. Identify high memory process.
13. Stop the load process.
14. Verify CPU and memory become normal.

---

## Expert Level

### Assignment 11: Docker-Based Linux Admin Lab

Create a Docker container and perform below tasks:

1. Run Ubuntu container.
2. Install required packages:
   - `vim`
   - `sudo`
   - `acl`
   - `procps`
   - `net-tools`
   - `iproute2`
   - `apache2`
   - `apache2-utils`
   - `stress-ng`

3. Create users and groups using shell script.
4. Create file permissions using shell script.
5. Install and run Apache service.
6. Generate Apache traffic using `ab`.
7. Generate CPU load using `stress-ng`.
8. Generate memory load using `stress-ng`.
9. Monitor using `top`, `ps`, `free`, `df`, and `ss`.
10. Stop all load and verify system is normal.

---

### Assignment 12: Real-Time Admin Scenario

Scenario:

A trainer created a script in `/home/trainer/shared/helloworld.sh`.

Requirement:

1. Only `student1` should read, write, and execute the script.
2. `student2` should not access the script.
3. The trainer should remain owner of the file.
4. Permission should be given without changing file owner or group.
5. Use ACL to solve this.
6. Verify with `getfacl`.
7. Test with both users.
8. Remove ACL permission after testing.
