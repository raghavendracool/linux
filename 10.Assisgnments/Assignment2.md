# Shell Scripting Assignment - Questions Only

## Assignment 1: Basic System Information Script

Write a shell script named `system-info.sh`.

Requirements:

1. Print current date and time.
2. Print hostname.
3. Print current logged-in user.
4. Print current working directory.
5. Print system uptime.

---

## Assignment 2: File and Directory Check Script

Write a shell script named `file-dir-check.sh`.

Requirements:

1. Ask user to enter a file name.
2. Check whether the file exists or not.
3. If file exists, print `File exists`.
4. If file does not exist, create the file.
5. Ask user to enter a directory name.
6. Check whether the directory exists or not.
7. If directory does not exist, create it.

---

## Assignment 3: User and Group Creation Script

Write a shell script named `user-group-create.sh`.

Requirements:

1. Create groups:
   - `dev`
   - `qa`
   - `support`

2. Create users:
   - `devuser`
   - `qauser`
   - `supportuser`

3. Add users to their respective groups.
4. Set default shell as `/bin/bash`.
5. Create home directory for all users.
6. Set temporary password as `Welcome@123`.
7. Verify using `id` and `groups`.

---

## Assignment 4: File Permission Script

Write a shell script named `permission-setup.sh`.

Requirements:

1. Create directory `/training`.
2. Create file `/training/hello.sh`.
3. Add below content:

```bash
echo "Welcome to Linux Training"
```

4. Give execute permission to owner.
5. Give read and execute permission to group.
6. Remove all permission from others.
7. Verify using `ls -l`.

---

## Assignment 5: ACL Single User Permission Script

Write a shell script named `acl-demo.sh`.

Requirements:

1. Create users:
   - `trainer`
   - `student1`
   - `student2`

2. Create file:

```bash
/home/trainer/shared/helloworld.sh
```

3. Give only `student1` read, write, and execute permission using ACL.
4. Do not give access to `student2`.
5. Verify using `getfacl`.

---

## Assignment 6: Apache/Tomcat Service Check Script

Write a shell script named `service-check.sh`.

Requirements:

1. Check whether Apache or Tomcat process is running.
2. If service is running, print:

```text
Service is running
```

3. If service is not running, start the service.
4. Print:

```text
Service started successfully
```

---

## Assignment 7: Memory Usage Script

Write a shell script named `memory-check.sh`.

Requirements:

1. Check memory usage on the machine.
2. Print current memory usage in percentage.
3. Print top memory consuming process.
4. Print PID of top memory consuming process.

---

## Assignment 8: CPU Usage Script

Write a shell script named `cpu-check.sh`.

Requirements:

1. Check CPU usage on the machine.
2. Print current CPU usage in percentage.
3. Print top CPU consuming process.
4. Print PID of top CPU consuming process.

---

## Assignment 9: Live Monitoring Script

Write a shell script named `live-monitor.sh`.

Requirements:

1. Script should run continuously.
2. Every 10 seconds, it should print:
   - Date and time
   - CPU usage percentage
   - Memory usage percentage
   - Disk usage percentage
   - Top CPU consuming process with PID
   - Top memory consuming process with PID

3. Screen should refresh every 10 seconds.
4. User should stop script using `CTRL + C`.

---

## Assignment 10: Docker CPU and Memory Load Demo

Write a shell script named `docker-load-demo.sh`.

Requirements:

1. Install required packages:
   - `apache2`
   - `apache2-utils`
   - `stress-ng`
   - `procps`
   - `curl`

2. Start Apache service.
3. Generate Apache traffic using `ab`.
4. Generate CPU load using `stress-ng`.
5. Generate memory load using `stress-ng`.
6. Print top CPU and memory processes.
