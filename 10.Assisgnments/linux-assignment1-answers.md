# Linux Assignment Questions and Answers

## Beginner Level

### Assignment 1: Basic Linux Navigation

#### Q1. Print current working directory.

```bash
pwd
```

#### Q2. Go to `/tmp`.

```bash
cd /tmp
```

#### Q3. Create folder `linux-practice`.

```bash
mkdir linux-practice
```

#### Q4. Go inside the folder.

```bash
cd linux-practice
```

#### Q5. Create files.

```bash
touch file1.txt file2.txt file3.log
```

#### Q6. List files in long format.

```bash
ls -l
```

#### Q7. List hidden files also.

```bash
ls -la
```

#### Q8. Create hidden file.

```bash
touch .secret
```

#### Q9. Show latest modified file at bottom.

```bash
ls -lrth
```

#### Q10. Delete `file2.txt`.

```bash
rm file2.txt
```

---

## Intermediate Level

### Assignment 2: User and Group Management

#### Q1. Create users.

```bash
sudo useradd -m -s /bin/bash devuser
sudo useradd -m -s /bin/bash qauser
sudo useradd -m -s /bin/bash opsuser
```

#### Q2. Create groups.

```bash
sudo groupadd dev
sudo groupadd qa
sudo groupadd ops
```

#### Q3. Add users to groups.

```bash
sudo usermod -aG dev devuser
sudo usermod -aG qa qauser
sudo usermod -aG ops opsuser
```

#### Q4. Set passwords.

```bash
sudo passwd devuser
sudo passwd qauser
sudo passwd opsuser
```

#### Q5. Check user details.

```bash
id devuser
id qauser
id opsuser
```

#### Q6. Check group membership.

```bash
groups devuser
groups qauser
groups opsuser
```

#### Q7. Lock user.

```bash
sudo passwd -l qauser
```

#### Q8. Unlock user.

```bash
sudo passwd -u qauser
```

---

## Intermediate Level

### Assignment 3: File Permissions

#### Q1. Create training folder and script.

```bash
sudo mkdir /training
sudo touch /training/demo.sh
```

#### Q2. Add content.

```bash
echo 'echo "Welcome to Linux Training"' | sudo tee /training/demo.sh
```

#### Q3. Give execute permission to owner.

```bash
sudo chmod u+x /training/demo.sh
```

#### Q4. Give read and execute to group.

```bash
sudo chmod g+rx /training/demo.sh
```

#### Q5. Remove write permission from others.

```bash
sudo chmod o-w /training/demo.sh
```

#### Q6. Change owner and group.

```bash
sudo chown devuser:dev /training/demo.sh
```

#### Q7. Verify.

```bash
ls -l /training/demo.sh
```

---

## Advanced Level

### Assignment 4: ACL Permission

#### Requirement

Only `student1` should get `rwx` access to trainer script. `student2` should not get access.

#### Commands

```bash
sudo useradd -m -s /bin/bash trainer
sudo useradd -m -s /bin/bash student1
sudo useradd -m -s /bin/bash student2

sudo mkdir -p /home/trainer/shared
echo 'echo "Hello from trainer script"' | sudo tee /home/trainer/shared/helloworld.sh

sudo chown -R trainer:trainer /home/trainer/shared
sudo chmod 700 /home/trainer
sudo chmod 700 /home/trainer/shared
sudo chmod 700 /home/trainer/shared/helloworld.sh
```

#### Give ACL permission only to `student1`

```bash
sudo setfacl -m u:student1:rx /home/trainer
sudo setfacl -m u:student1:rx /home/trainer/shared
sudo setfacl -m u:student1:rwx /home/trainer/shared/helloworld.sh
```

#### Verify ACL

```bash
getfacl /home/trainer/shared/helloworld.sh
```

#### Test as `student1`

```bash
su - student1
cat /home/trainer/shared/helloworld.sh
echo 'echo "Student1 updated file"' >> /home/trainer/shared/helloworld.sh
bash /home/trainer/shared/helloworld.sh
exit
```

#### Test as `student2`

```bash
su - student2
cat /home/trainer/shared/helloworld.sh
exit
```

Expected result:

```text
Permission denied
```

#### Remove ACL

```bash
sudo setfacl -x u:student1 /home/trainer
sudo setfacl -x u:student1 /home/trainer/shared
sudo setfacl -x u:student1 /home/trainer/shared/helloworld.sh
```

---

## Advanced Level

### Assignment 5: Shell Script for User and Group Creation

Create script:

```bash
vi create-users.sh
```

Script:

```bash
#!/bin/bash

echo "Creating groups..."

groupadd developers 2>/dev/null
groupadd testers 2>/dev/null
groupadd support 2>/dev/null

echo "Creating users..."

useradd -m -s /bin/bash alice 2>/dev/null
useradd -m -s /bin/bash bob 2>/dev/null
useradd -m -s /bin/bash charlie 2>/dev/null

echo "Adding users to groups..."

usermod -aG developers alice
usermod -aG testers bob
usermod -aG support charlie

echo "Setting temporary passwords..."

echo "alice:Welcome@123" | chpasswd
echo "bob:Welcome@123" | chpasswd
echo "charlie:Welcome@123" | chpasswd

echo "Force password change on first login..."

passwd -e alice
passwd -e bob
passwd -e charlie

echo "User details:"

id alice
id bob
id charlie

echo "User and group setup completed."
```

Run:

```bash
chmod +x create-users.sh
sudo ./create-users.sh
```

---

## Advanced Level

### Assignment 6: Shell Script for File Permission Setup

Create script:

```bash
vi setup-permission.sh
```

Script:

```bash
#!/bin/bash

echo "Creating company folders..."

mkdir -p /company/dev
mkdir -p /company/qa
mkdir -p /company/support

echo "Creating script files..."

echo 'echo "Dev script running"' > /company/dev/dev-script.sh
echo 'echo "QA script running"' > /company/qa/qa-script.sh
echo 'echo "Support script running"' > /company/support/support-script.sh

echo "Setting ownership..."

chown -R root:developers /company/dev
chown -R root:testers /company/qa
chown -R root:support /company/support

echo "Setting directory permissions..."

chmod 770 /company/dev
chmod 770 /company/qa
chmod 770 /company/support

echo "Setting script permissions..."

chmod 750 /company/dev/dev-script.sh
chmod 750 /company/qa/qa-script.sh
chmod 750 /company/support/support-script.sh

echo "Verifying permissions..."

ls -ld /company/dev /company/qa /company/support
ls -l /company/dev /company/qa /company/support

echo "Permission setup completed."
```

Run:

```bash
chmod +x setup-permission.sh
sudo ./setup-permission.sh
```

---

## Expert Level

### Assignment 7: Docker Linux Admin Lab

#### Step 1: Run Ubuntu container

```bash
docker run -dit \
  --name linux-admin-lab \
  --hostname linux-admin-lab \
  --cpus="2" \
  --memory="2g" \
  -p 8080:80 \
  ubuntu:22.04 /bin/bash
```

#### Step 2: Enter container

```bash
docker exec -it linux-admin-lab bash
```

#### Step 3: Install packages

```bash
apt update
apt install -y vim sudo acl procps net-tools iproute2 curl apache2 apache2-utils stress-ng lsof
```

#### Step 4: Start Apache service inside container

```bash
apachectl -D FOREGROUND &
```

#### Step 5: Verify Apache process

```bash
ps -ef | grep apache
```

#### Step 6: Check port

```bash
ss -tulnp
```

#### Step 7: Test Apache

```bash
curl http://localhost
```

From host machine:

```bash
curl http://localhost:8080
```

---

## Expert Level

### Assignment 8: CPU and Memory Load Testing

#### Check CPU and memory before load

```bash
top
free -h
uptime
```

#### Generate high CPU load

```bash
stress-ng --cpu 2 --timeout 120s --metrics-brief
```

#### Check high CPU process

```bash
top
```

or

```bash
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head
```

#### Generate memory load

```bash
stress-ng --vm 1 --vm-bytes 512M --timeout 120s --metrics-brief
```

#### Check high memory process

```bash
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head
```

#### Check memory

```bash
free -h
```

#### Stop stress process manually if needed

```bash
pkill stress-ng
```

---

## Expert Level

### Assignment 9: Apache Service Load Demo

#### Install Apache and Apache benchmark tool

```bash
apt update
apt install -y apache2 apache2-utils curl procps
```

#### Start Apache

```bash
apachectl -D FOREGROUND &
```

#### Generate traffic

```bash
ab -n 10000 -c 100 http://127.0.0.1/
```

Meaning:

```text
-n 10000 = total 10000 requests
-c 100   = 100 concurrent requests
```

#### Monitor Apache CPU usage

```bash
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head
```

#### Check Apache processes

```bash
ps -ef | grep apache
```

#### Check listening port

```bash
ss -tulnp | grep :80
```

#### Stop Apache

```bash
pkill apache2
```

Ready-to-Use Scripts for Your Repo

Create folder:

mkdir -p scripts
Script 1: User, Group, and Permission Setup

File name:

scripts/linux-user-permission-demo.sh
#!/bin/bash

set -e

echo "Creating groups..."

groupadd developers 2>/dev/null || true
groupadd testers 2>/dev/null || true
groupadd support 2>/dev/null || true

echo "Creating users..."

useradd -m -s /bin/bash alice 2>/dev/null || true
useradd -m -s /bin/bash bob 2>/dev/null || true
useradd -m -s /bin/bash charlie 2>/dev/null || true

echo "Adding users to groups..."

usermod -aG developers alice
usermod -aG testers bob
usermod -aG support charlie

echo "Setting passwords..."

echo "alice:Welcome@123" | chpasswd
echo "bob:Welcome@123" | chpasswd
echo "charlie:Welcome@123" | chpasswd

echo "Creating company folders..."

mkdir -p /company/dev
mkdir -p /company/qa
mkdir -p /company/support

echo "Creating scripts..."

echo 'echo "Dev script running"' > /company/dev/dev-script.sh
echo 'echo "QA script running"' > /company/qa/qa-script.sh
echo 'echo "Support script running"' > /company/support/support-script.sh

echo "Setting ownership..."

chown -R root:developers /company/dev
chown -R root:testers /company/qa
chown -R root:support /company/support

echo "Setting permissions..."

chmod 770 /company/dev /company/qa /company/support
chmod 750 /company/dev/dev-script.sh
chmod 750 /company/qa/qa-script.sh
chmod 750 /company/support/support-script.sh

echo "Verification..."

id alice
id bob
id charlie

ls -ld /company/dev /company/qa /company/support
ls -l /company/dev /company/qa /company/support

echo "Demo setup completed successfully."

Run:

chmod +x scripts/linux-user-permission-demo.sh
sudo ./scripts/linux-user-permission-demo.sh
Script 2: ACL Demo — Permission to One Single User

File name:

scripts/acl-single-user-demo.sh
#!/bin/bash

set -e

echo "Installing ACL package if missing..."

if ! command -v setfacl >/dev/null 2>&1; then
  apt update
  apt install -y acl
fi

echo "Creating users..."

useradd -m -s /bin/bash trainer 2>/dev/null || true
useradd -m -s /bin/bash student1 2>/dev/null || true
useradd -m -s /bin/bash student2 2>/dev/null || true

echo "Setting passwords..."

echo "trainer:Welcome@123" | chpasswd
echo "student1:Welcome@123" | chpasswd
echo "student2:Welcome@123" | chpasswd

echo "Creating trainer script..."

mkdir -p /home/trainer/shared
echo 'echo "Hello from trainer script"' > /home/trainer/shared/helloworld.sh

chown -R trainer:trainer /home/trainer/shared
chmod 700 /home/trainer
chmod 700 /home/trainer/shared
chmod 700 /home/trainer/shared/helloworld.sh

echo "Giving ACL access only to student1..."

setfacl -m u:student1:rx /home/trainer
setfacl -m u:student1:rx /home/trainer/shared
setfacl -m u:student1:rwx /home/trainer/shared/helloworld.sh

echo "ACL verification..."

getfacl /home/trainer/shared/helloworld.sh

echo "Test command for student1:"
echo "su - student1"
echo "cat /home/trainer/shared/helloworld.sh"
echo "echo 'echo updated by student1' >> /home/trainer/shared/helloworld.sh"
echo "bash /home/trainer/shared/helloworld.sh"

echo "Test command for student2:"
echo "su - student2"
echo "cat /home/trainer/shared/helloworld.sh"
echo "Expected: Permission denied"

echo "ACL demo setup completed."

Run:

chmod +x scripts/acl-single-user-demo.sh
sudo ./scripts/acl-single-user-demo.sh
Script 3: Docker CPU, Memory, and Apache Service Demo

File name:

scripts/docker-cpu-memory-service-demo.sh
#!/bin/bash

set -e

echo "Updating packages..."

apt update

echo "Installing required tools..."

apt install -y apache2 apache2-utils stress-ng procps curl net-tools iproute2 lsof

echo "Starting Apache service..."

apachectl -D FOREGROUND &

sleep 3

echo "Apache process details:"

ps -ef | grep apache | grep -v grep || true

echo "Listening ports:"

ss -tulnp || true

echo "Testing Apache locally..."

curl -I http://127.0.0.1 || true

echo "Current CPU and memory status:"

uptime
free -h
df -h

echo "Top CPU processes:"

ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head

echo "Top memory processes:"

ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head

echo "Generating Apache traffic for service load..."

ab -n 5000 -c 50 http://127.0.0.1/ || true

echo "Generating CPU load for 60 seconds..."

stress-ng --cpu 2 --timeout 60s --metrics-brief &

echo "Generating memory load for 60 seconds..."

stress-ng --vm 1 --vm-bytes 512M --timeout 60s --metrics-brief &

echo "Monitor using below commands in another terminal:"
echo "top"
echo "free -h"
echo "ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head"
echo "ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head"

wait

echo "Load test completed."

echo "Final CPU and memory status:"

uptime
free -h

echo "Demo completed successfully."

Run Ubuntu container:

docker run -dit \
  --name linux-admin-lab \
  --hostname linux-admin-lab \
  --cpus="2" \
  --memory="2g" \
  -p 8080:80 \
  ubuntu:22.04 /bin/bash

Enter container:

docker exec -it linux-admin-lab bash

Inside container, create and run the script:

mkdir -p scripts
vi scripts/docker-cpu-memory-service-demo.sh
chmod +x scripts/docker-cpu-memory-service-demo.sh
./scripts/docker-cpu-memory-service-demo.sh

From host machine, test Apache:

curl http://localhost:8080
4. Commands for CPU, Memory, and Service Monitoring

Use these during demo.

# CPU and load
top
uptime
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%cpu | head

# Memory
free -h
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head

# Disk
df -h
du -sh /*
lsblk

# Service/process
ps -ef | grep apache
pgrep apache2
ss -tulnp | grep :80

# Generate CPU high
stress-ng --cpu 2 --timeout 120s --metrics-brief

# Generate memory high
stress-ng --vm 1 --vm-bytes 512M --timeout 120s --metrics-brief

# Generate Apache service load
ab -n 10000 -c 100 http://127.0.0.1/

# Stop load
pkill stress-ng

# Stop Apache
pkill apache2
