# 🐧 Linux Commands Cheat Sheet

A practical collection of commonly used Linux commands for **DevOps, Linux Administration, Cloud, Docker, Jenkins, Ansible, Kubernetes, and interview preparation**.

---
# 1. 📁 File & Directory Management

| Command                 | Description                                               |
| ----------------------- | --------------------------------------------------------- |
| `ls`                    | Lists files and directories                               |
| `ls -l`                 | Displays detailed information about files and directories |
| `cd directory`          | Changes to the specified directory                        |
| `cd`                    | Returns to the user's home directory                      |
| `mkdir directory`       | Creates a new directory                                   |
| `touch file.txt`        | Creates a new empty file                                  |
| `cp source destination` | Copies a file or directory                                |
| `rm file`               | Removes a file                                            |
| `rm -rf directory`      | Recursively removes a directory and its contents          |
| `tree`                  | Displays files and directories in a tree structure        |

### Examples

```bash
ls
cd infosys/
mkdir flipkart
touch flipkart/login.txt
cp login.tar.gz infosys/
rm -rf *
tree
```

> ⚠️ `rm -rf` permanently deletes files/directories. Use it carefully.

---

# 2. 📦 Archive & Compression

## TAR Commands

| Command                          | Description                         |
| -------------------------------- | ----------------------------------- |
| `tar -cvf archive.tar files`     | Creates a TAR archive               |
| `tar -tvf archive.tar`           | Lists the contents of a TAR archive |
| `tar -xvf archive.tar`           | Extracts a TAR archive              |
| `tar -zcvf archive.tar.gz files` | Creates a compressed TAR.GZ archive |
| `tar -zxvf archive.tar.gz`       | Extracts a TAR.GZ archive           |

### Example

```bash
tar -zcvf login.tar.gz a.js b.js c.js d.js
```

Extract:

```bash
tar -zxvf login.tar.gz
```

---

## ZIP Commands

| Command                      | Description                         |
| ---------------------------- | ----------------------------------- |
| `zip file.zip files`         | Creates a ZIP archive               |
| `zip -r file.zip directory/` | Compresses a directory recursively  |
| `unzip file.zip`             | Extracts a ZIP archive              |
| `unzip -l file.zip`          | Lists the contents of a ZIP archive |

### Examples

```bash
zip login.zip a.js b.js
zip -r project.zip project/
unzip login.zip
unzip -l login.zip
```

---

## GZIP Commands

| Command           | Description                  |
| ----------------- | ---------------------------- |
| `gzip file`       | Compresses a file using GZIP |
| `gzip -d file.gz` | Decompresses a GZIP file     |
| `gunzip file.gz`  | Decompresses a GZIP file     |

### Examples

```bash
gzip login.txt
gzip -d login.txt.gz
gunzip login.txt.gz
```

---

# 3. 👤 User Management

| Command                            | Description                                         |
| ---------------------------------- | --------------------------------------------------- |
| `whoami`                           | Displays the current logged-in username             |
| `useradd username`                 | Creates a new user                                  |
| `useradd -m -s /bin/bash username` | Creates a user with a home directory and Bash shell |
| `passwd username`                  | Sets or changes a user's password                   |
| `su - username`                    | Switches to another user                            |
| `exit`                             | Exits the current shell/session                     |
| `userdel username`                 | Deletes a user                                      |
| `cat /etc/passwd`                  | Displays information about system users             |

### Examples

Create a user:

```bash
useradd -m -s /bin/bash sony
```

Set password:

```bash
passwd sony
```

Switch user:

```bash
su - sony
```

Check current user:

```bash
whoami
```

Delete user:

```bash
userdel sony
```

View users:

```bash
cat /etc/passwd
```

---

# 4. 👥 Group Management

| Command                  | Description                              |
| ------------------------ | ---------------------------------------- |
| `groupadd groupname`     | Creates a new group                      |
| `groupdel groupname`     | Deletes a group                          |
| `cat /etc/group`         | Displays information about system groups |
| `usermod -aG group user` | Adds a user to a supplementary group     |
| `groups username`        | Displays the groups a user belongs to    |
| `gpasswd -d user group`  | Removes a user from a group              |

### Example

Create a group:

```bash
groupadd docker
```

Create a user:

```bash
useradd -m -s /bin/bash ansible
```

Add user to group:

```bash
usermod -aG docker ansible
```

Check user's groups:

```bash
groups ansible
```

Remove user from group:

```bash
gpasswd -d ansible docker
```

Delete group:

```bash
groupdel docker
```

### Important

```bash
groups ansible
```

is used to check **which groups the user `ansible` belongs to**.

```bash
groups docker
```

does **not** check the `docker` group. `groups` expects a username.

---

# 5. 📖 File Viewing Commands

| Command          | Description                              |
| ---------------- | ---------------------------------------- |
| `cat file`       | Displays the complete contents of a file |
| `head file`      | Displays the first 10 lines              |
| `head -n 5 file` | Displays the first 5 lines               |
| `head -3 file`   | Displays the first 3 lines               |
| `tail file`      | Displays the last 10 lines               |
| `tail -n 3 file` | Displays the last 3 lines                |
| `tail -5 file`   | Displays the last 5 lines                |

### Examples

```bash
cat sam.txt
head sam.txt
head -n 5 sam.txt
tail sam.txt
tail -n 3 sam.txt
```

---

# 6. 🔤 Sorting & Duplicate Handling

## sort

| Command        | Description                    |
| -------------- | ------------------------------ |
| `sort file`    | Sorts lines in ascending order |
| `sort -r file` | Sorts lines in reverse order   |

Example:

```bash
sort sam.txt
```

Reverse:

```bash
sort -r sam.txt
```

---

## uniq

`uniq` is used to handle **consecutive duplicate lines**.

| Command         | Description                               |
| --------------- | ----------------------------------------- |
| `uniq file`     | Removes consecutive duplicate lines       |
| `uniq -d file`  | Displays only duplicate consecutive lines |
| `uniq -u file`  | Displays only unique consecutive lines    |
| `uniq -c file`  | Counts consecutive occurrences            |
| `uniq -uc file` | Displays unique lines with counts         |
| `uniq -dc file` | Displays duplicate lines with counts      |

### Example

```bash
uniq sam.txt
```

Show duplicates:

```bash
uniq -d sam.txt
```

Count duplicates:

```bash
uniq -c sam.txt
```

### Important

`uniq` checks **adjacent/consecutive duplicates**.

To identify duplicates throughout a file, a common approach is:

```bash
sort file.txt | uniq
```

---

# 7. 🔎 File Searching

The `find` command is used to search for files and directories.

| Command                           | Description                          |
| --------------------------------- | ------------------------------------ |
| `find -name filename`             | Searches for a file by name          |
| `find ./ -name filename`          | Searches from the current directory  |
| `find ./directory -name filename` | Searches inside a specific directory |

### Examples

```bash
find -name sam.txt
```

```bash
find ./ -name sam.txt
```

```bash
find ./flipkart -name login.txt
```

---

# 8. 🔍 Text Searching

The `grep` command searches for text or patterns inside files.

| Command                            | Description                                     |
| ---------------------------------- | ----------------------------------------------- |
| `grep "text" file`                 | Searches for text in a file                     |
| `grep -r "text" directory/`        | Recursively searches files in a directory       |
| `grep -r "text" ./`                | Recursively searches from the current directory |
| `grep -rE "pattern1\|pattern2" ./` | Searches for multiple patterns                  |

### Examples

Search for `error`:

```bash
grep "error" sam.txt
```

Search recursively:

```bash
grep -r "error" flipkart/
```

Search the current directory:

```bash
grep -r "error" ./
```

Search for `error` OR `warning`:

```bash
grep -rE "error|warning" ./
```

### DevOps Use Case

`grep` is frequently used to search **application logs** for errors, warnings, exceptions, and specific events.

Example:

```bash
grep "error" application.log
```

---

# 9. 📊 File Statistics

The `wc` command counts lines, words, and bytes.

| Command      | Description                      |
| ------------ | -------------------------------- |
| `wc file`    | Displays lines, words, and bytes |
| `wc -c file` | Counts bytes                     |
| `wc -l file` | Counts lines                     |
| `wc -w file` | Counts words                     |

### Examples

```bash
wc sam.txt
```

Count lines:

```bash
wc -l sam.txt
```

Count words:

```bash
wc -w sam.txt
```

Count bytes:

```bash
wc -c sam.txt
```

---

# 10. ✏️ Text Editor

## vi

`vi` is a command-line text editor used to create and edit files.

```bash
vi sam.txt
```

Open another file:

```bash
vi flipkart/login.txt
```

---

# 11. 📦 Package Management

On Ubuntu/Debian-based systems, `apt` is used to manage packages.

| Command               | Description                 |
| --------------------- | --------------------------- |
| `apt update`          | Updates package information |
| `apt install package` | Installs a package          |

### Example

```bash
apt update
```

Install `tree`:

```bash
apt install tree
```

---

# 12. 🐚 Shell Scripting

Shell scripts contain a series of Linux commands that can be executed together.

Example script:

```bash
#!/bin/bash

echo "Welcome to Shell Scripting"
whoami
pwd
date
```

Run using `sh`:

```bash
sh sam.sh
```

Run using Bash:

```bash
bash sam.sh
```

Give execute permission:

```bash
chmod +x sam.sh
```

Execute directly:

```bash
./sam.sh
```

### Common commands used inside scripts

```bash
echo
whoami
pwd
hostnamectl
uptime
ps
uname -a
date
```

---

# 13. 🖥️ System Information

| Command       | Description                                    |
| ------------- | ---------------------------------------------- |
| `hostnamectl` | Displays hostname and system information       |
| `uptime`      | Shows how long the system has been running     |
| `ps`          | Displays running processes                     |
| `uname -a`    | Displays kernel and system information         |
| `date`        | Displays current date and time                 |
| `free -h`     | Displays memory usage in human-readable format |

### Examples

```bash
hostnamectl
uptime
ps
uname -a
date
free -h
```

---

# 14. 🌐 Networking

## nslookup

Used to query DNS information for a domain.

```bash
nslookup flipkart.com
```

It can show the DNS server being used and the IP address associated with the domain.

---

# 15. 🕘 Command History

## history

Displays previously executed commands.

```bash
history
```

This is useful for reviewing commands used during troubleshooting or administration.

---

# 🚀 Linux Commands for DevOps

These commands are especially useful when working with:

* 🐧 Linux Administration
* 🐳 Docker
* ☸️ Kubernetes
* 🔧 Jenkins
* 🤖 Ansible
* 🏗️ Terraform
* ☁️ AWS
* 🐚 Shell Scripting
* 📊 Monitoring & Troubleshooting
* 🔍 Log Analysis

---

## 🎯 Quick DevOps Reference

```text
Files & Directories  → ls, cd, mkdir, touch, cp, rm, tree
Archives             → tar, zip, unzip, gzip, gunzip
Users                → useradd, passwd, su, userdel, whoami
Groups               → groupadd, groupdel, usermod, groups, gpasswd
Viewing              → cat, head, tail
Sorting              → sort
Duplicates           → uniq
File Search          → find
Text Search          → grep
Statistics           → wc
Editing              → vi
Packages             → apt
Shell Scripting      → sh, bash, chmod
System Information   → hostnamectl, uptime, ps, uname, free
Networking           → nslookup
History              → history
```

---

## 📚 Learning Goal

This cheat sheet is created as part of my **Linux and DevOps practice**, covering commonly used commands for system administration, troubleshooting, automation, and DevOps environments.

> **Practice → Understand → Automate → Apply in real projects**

---

### 👨‍💻 DevOps Learning

**Linux | Git | Docker | Jenkins | Ansible | Terraform | AWS | Kubernetes**
