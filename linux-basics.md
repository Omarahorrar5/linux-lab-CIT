# 🚀 Linux Lab — Filesystem, Users, Groups & Permissions

## 🎯 Objectives

By the end of this lab, students will be able to:

* Understand the Linux filesystem hierarchy.
* Use essential file and directory commands.
* Manage users and groups.
* Configure permissions (`rwx`), ownership, and access control.
* Apply all concepts through hands-on exercises.

Works on **Ubuntu (VMware)**.

---

# 🗂️ 1. The Linux Filesystem

Linux is a **tree structure** with `/` (root) as the top.

### 📁 Important directories

| Directory          | Description                                |
| ------------------ | ------------------------------------------ |
| `/`                | The root of everything                     |
| `/home`            | User home directories                      |
| `/etc`             | System config files (passwords, services…) |
| `/var`             | Changing data (logs, caches, websites…)    |
| `/tmp`             | Temporary files cleared sometimes          |
| `/opt`             | Optional / external software               |
| `/bin`, `/usr/bin` | Executable programs                        |
| `/dev`             | Devices (USB, disks…)                      |

🔎 **Example**:
`/home/omar/Documents/file.txt` → `file.txt` is inside the Documents folder of user "omar".

---

# 📘 2. Basic File Commands

Each command includes **what it does** + **short examples**.

---

## 🔍 Listing files — `ls`

```
ls             # list files
ls -l          # detailed list (permissions, size)
ls -lh         # size in KB, MB, GB
ls -a          # show hidden files (starting with .)
ls -la         # detailed + hidden
```

Hidden files example:
`.bashrc`, `.config/`

---

## 📄 Creating files

```
touch file.txt          # create an empty file
nano file.txt           # open text editor in terminal (gedit, vim, nvim are other text editor alternatives)
cat file.txt            # show file content
echo "Hello" > file.txt # write text to file
```

Example:

```
echo "My first Linux file" > note.txt
cat note.txt
```

---

## 📂 Creating directories — `mkdir`

```
mkdir test
mkdir -p project/src    # create nested directories
```

The `-p` option makes parent folders if they don’t exist.

---

## 🧭 Navigation — `cd`, `pwd`

```
pwd           # show current directory
cd /etc       # go to /etc
cd ~          # go to home
cd ..         # go up one directory
cd -          # go back to previous directory
```

---

## 📑 Copy & Move — `cp`, `mv`

```
cp file.txt backup.txt              # copy file
cp -r folder folder_backup          # copy folder
mv file1.txt /tmp/                  # move file
mv oldname.txt newname.txt          # rename
```

Example:

```
mv notes/ old_notes/
```

---

## 🗑️ Delete — `rm`

```
rm file.txt
rm -r folder
rm -rf folder   # force delete (DANGEROUS)
```

⚠️ `rm -rf /` destroys the system — NEVER run it.

---

## 📦 File information — `stat`, `file`

```
stat file.txt   # full details (size, timestamps)
file file.txt   # tells what kind of file
```

---

## 🔎 Search — `find`

```
find . -name "*.txt"             # find text files
find /var -type f -size +5M      # files larger than 5MB
```

---

## 💾 Disk usage — `du`, `df`

```
du -sh .        # size of current directory
df -h           # disk space remaining
```

Example:

```
du -sh Downloads
```

---

# 🛠️ 3. File Permissions (rwx)

Every file has:

* **Owner**
* **Group**
* **Others**

Example output:

```
-rw-r--r-- 1 omar omar 1200 Jan 28 file.txt
```

Breakdown:

* `rw-` → owner: read + write
* `r--` → group: read
* `r--` → others: read

---

## ✏️ Changing permissions — `chmod`

```
chmod 755 script.sh
chmod u+rwx,g+rx,o-r file.txt
```

### Numeric mode

| rwx | Value |
| --- | ----- |
| r   | 4     |
| w   | 2     |
| x   | 1     |

Examples:

```
chmod 644 file.txt   # rw- r-- r--
chmod 700 secret/    # full access for owner only
chmod 770 project/   # owner + group, no others
```

---

## 🧑‍🤝‍🧑 Change owner & group — `chown`

```
sudo chown omar file.txt
sudo chown omar:admins file.txt
```

Example: give "devs" group ownership of /app:

```
sudo chown root:devs /app
```

---

# 👥 4. Users & Groups

---

## 👤 Create a user — `adduser`

```
sudo adduser student1
sudo passwd student1
```

Example:
Password prompt will appear — choose a simple password for lab.

---

## 👥 Create a group — `groupadd`

```
sudo groupadd devs
sudo usermod -aG devs student1
```

Meaning:
Add `student1` to group `devs` **without removing their existing groups** (`-aG`).

---

## 🔄 Switch user — `su`

```
su - student1
```

`-` loads the user's environment.

---

## 🔍 User information

```
whoami           # current user
id student1      # uid, gid, groups
groups student1
```

---

## 🧷 Sudo privileges

```
sudo command
sudo -l     # list allowed commands
```

---

# 🔒 5. Ownership & Access Examples

### Example 1 — Shared project directory

Goal: Only developers can modify `/project`.

```
sudo mkdir /project
sudo groupadd devs
sudo chown root:devs /project
sudo chmod 770 /project
```

Now:

* root → full access
* devs → full access
* others → no access

---

### Example 2 — Public read-only folder

```
sudo mkdir /public
sudo chmod 755 /public
```

Everyone can read, only owner can modify.

---

# 🧪 6. Complete Lab Exercises

## 📚 Lab 1 — Files & Directories

1. Create folder:

   ```
   mkdir linux_lab
   ```
2. Inside it create:

   ```
   touch a.txt b.txt c.txt
   ```
3. Write text:

   ```
   echo "hello world" > a.txt
   ```
4. Copy `a.txt`:

   ```
   cp a.txt backup.txt
   ```
5. Move `c.txt`:

   ```
   mkdir docs
   mv c.txt docs/
   ```
6. Human-readable listing:

   ```
   ls -lh
   ```
7. Find `.txt` files:

   ```
   find . -name "*.txt"
   ```
8. Show statistics:

   ```
   stat b.txt
   ```
9. Create 5MB file:

   ```
   dd if=/dev/zero of=bigfile bs=1M count=5
   du -sh bigfile
   ```
10. Explain hard link vs symbolic link (symlink):

* Hard link = another name for same file
* Symlink = shortcut pointing to original file

Create examples:

```
ln a.txt hardlink_a
ln -s a.txt symlink_a
```

---

## 📚 Lab 2 — Users & Groups

1. Create user:

   ```
   sudo adduser labuser
   ```
2. Create group:

   ```
   sudo groupadd labgroup
   ```
3. Add user to group:

   ```
   sudo usermod -aG labgroup labuser
   ```
4. Create directory:

   ```
   sudo mkdir /labfolder
   ```
5. Change ownership:

   ```
   sudo chown root:labgroup /labfolder
   ```
6. Set permissions:

   ```
   sudo chmod 750 /labfolder
   ```
7. Switch user:

   ```
   su - labuser
   ```
8. Try creating a file:

   ```
   touch /labfolder/test.txt
   ```

   → Permission denied (labuser cannot write)

---

## 📚 Lab 3 — Permissions

Given: `secret.txt`

1. Owner read-write:

   ```
   chmod u=rw secret.txt
   ```
2. Group read-only:

   ```
   chmod g=r secret.txt
   ```
3. Others no access:

   ```
   chmod o= secret.txt
   ```
4. Numeric mode:
   `rw- r-- ---` → **640**

```
chmod 640 secret.txt
```

---

# 📝 7. Cheat Sheet (Quick Summary)

### Files

```
ls, cd, pwd, mkdir, touch, cp, mv, rm, nano, cat, echo
```

### Permissions

```
chmod, chown, chgrp, stat
```

### Users

```
sudo adduser, sudo groupadd, usermod, passwd, su -, id, groups
```

### Search

```
find, du, df
```

---

# 🎉 End of Lab

Congrats!
This lab teaches the real skills used daily by **Cloud Engineers, DevOps Engineers, SysAdmins, and Security Engineers**.
