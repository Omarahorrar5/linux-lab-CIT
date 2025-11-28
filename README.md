# 🚀 Linux Lab — Filesystem, Users, Groups & Permissions

## 🎯 Objectives

By the end of this lab, students will be able to:

* Understand the Linux filesystem hierarchy.
* Use essential file and directory commands.
* Manage users and groups.
* Configure permissions (rwx), ownership, and access control.
* Apply all concepts through hands-on exercises.

All commands work on **Ubuntu** (VMware).

---

# 🗂️ 1. The Linux Filesystem

Linux is organized as a **single tree structure** starting from `/` (root).

### 📁 Important directories

| Directory          | Description                   |
| ------------------ | ----------------------------- |
| `/`                | Root of the filesystem        |
| `/home`            | Home directories for users    |
| `/etc`             | System configuration files    |
| `/var`             | Variable files (logs, cache…) |
| `/opt`             | Optional software             |
| `/tmp`             | Temporary files               |
| `/bin`, `/usr/bin` | User commands and binaries    |
| `/dev`             | Hardware devices              |

---

# 📘 2. Basic File Commands

### 🔍 Listing files

```
ls
ls -l      # long format
ls -lh     # human-readable sizes
ls -a      # show hidden files
ls -la
```

### 📄 Creating files

```
touch file.txt
nano file.txt   # edit file (gedit, vim, nvim are other text editor alternatives)
cat file.txt    # display file content
```

### 📂 Creating directories

```
mkdir test
mkdir -p project/src  # create nested folders
```

### 🧭 Navigation

```
pwd
cd /etc
cd ~        # go to home directory
cd ..       # go up one directory
```

### 📑 Copy & Move

```
cp file.txt backup.txt
cp -r folder folder_backup

mv file1.txt /tmp/
mv oldname.txt newname.txt
```

### 🗑️ Delete

```
rm file.txt
rm -r folder
rm -rf folder   # force delete (dangerous!)
```

### 📦 File information

```
stat file.txt
file file.txt
```

### 🔎 Search

```
find . -name "*.txt"
find /var -type f -size +5M
```

### 💾 Disk usage

```
du -sh .
df -h
```

---

# 🛠️ 3. File Permissions (rwx)

Each file has **owner**, **group**, and **others** permissions.
Example:

```
-rw-r--r-- 1 omar omar  1200 Jan 28 file.txt
```

Meaning:

* Owner: `rw-`
* Group: `r--`
* Others: `r--`

### Change permissions

```
chmod 755 script.sh
chmod u+rwx,g+rx,o-r file.txt
```

### Using numeric mode

| rwx | Value |
| --- | ----- |
| r   | 4     |
| w   | 2     |
| x   | 1     |

Examples:

```
chmod 644 file.txt   # rw- r-- r--
chmod 700 secret/    # owner only
```

### Change owner and group

```
sudo chown omar file.txt
sudo chown omar:admins file.txt
```

---

# 👥 4. Users & Groups

### Create a user

```
sudo adduser student1
sudo passwd student1
```

### Create a group

```
sudo groupadd devs
sudo usermod -aG devs student1
```

### Switch user

```
su - student1
```

### Show user info

```
whoami
id student1
groups student1
```

### Sudo privileges

```
sudo command
sudo -l        # list allowed commands
```

---

# 🔒 5. Ownership & Access Examples

### Example: give a developer group access to a project folder

```
sudo mkdir /project
sudo chown root:devs /project
sudo chmod 770 /project
```

Now only:

* root → full access
* devs → full access
* others → no access

---

# 🧪 6. Complete Lab Exercises

Students should **open a terminal** and follow tasks.

## 📚 Lab 1 — Files & Directories

1. Create a folder: `linux_lab`
2. Inside it, create 3 files: `a.txt`, `b.txt`, `c.txt`
3. Write text into `a.txt` using `echo`.
4. Copy `a.txt` to `backup.txt`.
5. Move `c.txt` to a new directory `docs/`.
6. List all files with size in human-readable format.
7. Find all `.txt` files using `find`.
8. Show statistics of `b.txt` using `stat`.
9. Create a 5MB file and check its size using `du`.
10. Explain the difference between a **hard link** and **symbolic link**.

Commands you will need:

```
mkdir, touch, echo, cat, ls, cp, mv, rm, find, du, stat, ln
```

## 📚 Lab 2 — Users & Groups

1. Create user `labuser`.
2. Create group `labgroup`.
3. Add `labuser` to `labgroup`.
4. Create directory `/labfolder`.
5. Set owner = root, group = labgroup.
6. Give: owner=rwx, group=rx, others=none.
7. Switch to labuser and test access.
8. Try creating a file inside `/labfolder` — what happens and why?

Commands you will use:

```
sudo adduser
sudo groupadd
sudo usermod -aG
sudo chown
chmod
su -
```

## 📚 Lab 3 — Permissions

Given a file `secret.txt`:

1. Give owner read-write.
2. Give group read-only.
3. Deny all permissions for others.
4. Convert the permissions to numeric mode.

---

# 📝 7. Cheat Sheet (Quick Summary)

### Files

```
ls, cd, pwd, mkdir, cp, mv, rm, touch, nano
```

### Permissions

```
chmod, chown, chgrp, stat
```

### Users

```
sudo adduser, usermod, passwd, su -, id, groups
```

### Search

```
find, du, df
```

---

# 🎉 End of Lab

You now have a working environment to practice Linux fundamentals, the same skills used in DevOps, Cloud, Security, and all backend work.
