### **1. What is Linux?**

- **Definition**: Linux is an operating system kernel at its core. It is the foundation of many operating systems, often referred to as "Linux distributions" or "distros."
- **History**: Created by Linus Torvalds in 1991, Linux is a key part of the open-source movement.
- **Popular Distributions**: Ubuntu, CentOS, Fedora, Debian, Arch Linux, and more.
- **Comparison with Other OS**: Unlike Windows and macOS, Linux is free, open-source, and highly customizable.

---

### **2. Why Learn Linux?**

- **Use Cases**: Linux powers servers, cloud platforms, DevOps environments, supercomputers, and embedded systems.
- **Real-World Applications**: Hosting websites, running Android, IoT devices, and even smart home systems.
- **Benefits**: Free to use, customizable, secure, and lightweight.

---
### **3. Linux Ecosystem and Architecture**
- **Components of Linux**:
    - **Kernel**: The core of the OS that interacts with hardware.
    - **Shell**: A command interpreter (e.g., Bash, Zsh, fish) to communicate with the kernel.
    - **File System**: Organizes files in directories.
    - **Applications**: Software running on Linux.
- **Booting Process**: Basic understanding of how Linux starts up.

---
### **4. Open-Source Philosophy**

- **Definition**: Open-source software allows anyone to view, modify, and distribute the code.
- **Linux Community**: Maintained and updated by contributors worldwide.
- **Licensing**: Governed by the GNU General Public License (GPL).

---
### **5. Linux File System Basics**

![[Pasted image 20250108182458.png]]

- **Structure**:
    - `/` (root directory): The top-level directory.
    - Key directories: `/home` (user files), `/etc` (config files), `/var` (logs), `/bin` (basic commands), `/usr` (user applications), `/tmp` (temporary files).
- **Paths**:
    - **Absolute Path**: Starts from `/` (e.g., `/home/user/documents`).
    - **Relative Path**: Relative to the current directory (e.g., `documents` from `/home/user`).

---

### **6. Key Linux Terms**

- **Distribution**: Different flavors of Linux tailored for various use cases.
- **Package Manager**: Tools like `apt` (Ubuntu/Debian), `yum` or `dnf` (Red Hat/CentOS), and `pacman` (Arch Linux) to manage software.
- **Shell vs Terminal**: Shell is the command interpreter; the terminal is the tool to access it.
- **CLI vs GUI**: Command-line interface vs graphical user interface.

---

### **7. Linux Desktop Environments**

- Examples: GNOME, KDE, Xfce.
- These provide graphical interfaces for Linux systems.
- Demonstrate how Linux can look and feel different based on the desktop environment.

---

### **8. Setting Up Linux**

- **Options to Try Linux**:
    - Dual Boot: Install Linux alongside another OS.
    - Virtual Machine: Use tools like VirtualBox or VMware.
    - Live USB: Run Linux directly from a USB drive.
    - WSL: Windows Subsystem for Linux allows running Linux on Windows.

---

### **9. Security and Permissions**

- **User Roles**:
    - Root (superuser): Has complete control over the system.
    - Regular users: Limited permissions.
    - Groups: Logical grouping of users for shared access.
- **File Permissions**:
    - **Read** (r), **Write** (w), **Execute** (x).
    - Ownership concepts: Files have owners and associated groups.

---

### **10. Preparing for the Terminal**

- **Why the Terminal?**
    - Powerful and flexible for system management.
    - Efficient for automating tasks and scripting.
- **Beginner Tips**:
    - Use **man pages** (`man <command>`) for command help.
    - Leverage **tab completion** to save typing effort.
    - Explore Linux cheat sheets and online documentation for guidance.


---

# Getting started with GNU/Linux

## Section 1.1: Useful shortcuts

## Cursor Movement

| Shortcut | Action                                                 |
| -------- | ------------------------------------------------------ |
| Ctrl + A | Go to the beginning of the current line.               |
| Ctrl + E | Go to the end of the current line.                     |
| Ctrl + X | Move between the beginning of the line and the cursor. |
| Alt + F  | Move cursor forward one word.                          |
| Alt + B  | Move cursor backward one word.                         |
| Ctrl + F | Move cursor forward one character.                     |
| Ctrl + B | Move cursor backward one character.                    |


## Text Manipulation

| Shortcut       | Action                                                                     |
|-----------------|-----------------------------------------------------------------------------|
| Ctrl + U        | Cut the line from the current position to the beginning (entire line if at end), adding to clipboard. |
| Ctrl + K        | Cut the line from the current position to the end (entire line if at beginning), adding to clipboard. |
| Ctrl + W        | Delete the word before the cursor, adding it to the clipboard.             |
| Ctrl + Y        | Paste the last cut item from the clipboard (undo last delete).            |
| Alt + T         | Swap the last two words before the cursor.                              |
| Alt + L         | Make lowercase from cursor to end of word.                               |
| Alt + U         | Make uppercase from cursor to end of word.                               |
| Alt + C         | Capitalize to end of word starting at cursor (whole word if at beginning). |
| Alt + D         | Delete to end of word starting at cursor (whole word if at beginning).     |
| Alt + .         | Prints the last word written in the previous command.                     |
| Ctrl + T        | Swap the last two characters before the cursor.                           |

## History Access

| Shortcut       | Action                                                                  |
|-----------------|--------------------------------------------------------------------------|
| Ctrl + R        | Search through previously used commands.                               |
| Ctrl + G        | Leave history searching mode without running a command.                 |
| Ctrl + J        | Copy current matched command to command line without running it.         |
| Alt + R         | Revert changes to a command pulled from history (if edited).            |
| Ctrl + P        | Show last executed command (similar to up arrow).                       |
| Ctrl + N        | Show next executed command (similar to down arrow).                      |

## Terminal Control

| Shortcut       | Action                                                                           |
| -------------- | -------------------------------------------------------------------------------- |
| Ctrl + L       | Clear the screen (similar to `clear` command).                                   |
| Ctrl + S       | Stop all output to the screen (doesn't stop the command).                        |
| Ctrl + Q       | Resume output to the screen after stopping with Ctrl+S.                          |
| Ctrl + C       | End currently running process.                                                   |
| Ctrl + D       | Log out of the current shell session (similar to `exit` or `logout`).            |
| Ctrl + Z       | Suspend currently running foreground process.  Use `bg`, `fg`, `jobs` to manage. |
| Tab            | Auto-complete files and directory names.                                         |
| Tab (repeated) | Show all possibilities when typed characters don't uniquely match.               |

## Special Characters

| Shortcut | Action                      |
| -------- | --------------------------- |
| Ctrl + H | Same as Backspace           |
| Ctrl + J | Same as Return (Line Feed)  |
| Esc      | Deadkey (equivalent to Alt) |

## Closing the Terminal

| Shortcut             | Action                     |
|----------------------|-----------------------------|
| Ctrl + Shift + W      | Close terminal tab          |
| Ctrl + Shift + Q      | Close entire terminal       |


## Section 1.2: File Management Commands

### Directory Navigation

| Command                | Utility                                                 | Example                   |
| ---------------------- | ------------------------------------------------------- | ------------------------- |
| `pwd`                  | Print the full path of the current working directory.   | `pwd`                     |
| `cd -`                 | Navigate to the last working directory.                 | `cd -`                    |
| `cd ~`                 | or `cd`  Navigate to the current user's home directory. | `cd` or `cd ~`            |
| `cd ..`                | Go to the parent directory.                             | `cd ..`                   |
| `cd path/to/directory` | Navigate to a specific directory.                       | `cd /home/user/documents` |

### Listing Files and Directories

| Command      | Utility                                                                                          | Example              |         |
| ------------ | ------------------------------------------------------------------------------------------------ | -------------------- | ------- |
| `ls -l`      | List files and directories in long (table) format. Recommended for readability.                  | `ls -l`              |         |
| `ls -ld dir` | List information about the directory `dir` itself, not its contents.                             | `ls -ld mydirectory` |         |
| `ls -a`      | List all files, including hidden ones (those starting with a dot ".").                           | `ls -a`              |         |
| `ls -F`      | Appends a symbol to filenames indicating their type (*executable, /directory, @symlink, =socket, | pipe, >door).        | `ls -F` |
| `ls -lt`     | List files sorted by last modified time (most recent first).  `-l` provides long format.         | `ls -lt`             |         |
| `ls -lh`     | List files with human-readable file sizes (e.g., KB, MB, GB).                                    | `ls -lh`             |         |
| `ls -lR`     | List files recursively, showing all subdirectories.                                              | `ls -lR`             |         |



### File/Directory Creation, Copying, and Removal

| Command                     | Utility                                                                                        | Example                            |                                       |
| --------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------- | ------------------------------------- |
| `cp -p source dest`         | Copy a file, preserving attributes (owner, timestamp, permissions, etc.).                      | `cp -p file1.txt file2.txt`        |                                       |
| `cp -R source_dir dest_dir` | Recursively copy a directory and its contents.                                                 | `cp -R mydir /backup/`             |                                       |
| `mv file1 file2`            | Move (rename) a file.                                                                          | `mv oldname.txt newname.txt`       |                                       |
| `rm -i filename`            | Remove files, prompting for confirmation before each removal (**recommended for beginners**).  | `rm -i file1.txt file2.txt`        |                                       |
| `rm -R dir`                 | Recursively remove a directory and its contents (**use with extreme caution!**).               | `rm -R mydirectory`                |                                       |
| `rm -rf dir`                | Recursively remove a directory and its contents, without prompting (**extremely dangerous!**). | `rm -rf mydirectory`               | **(Use only if absolutely certain!)** |
| `rmdir dir`                 | Remove an empty directory.                                                                     | `rmdir emptydir`                   |                                       |
| `mkdir dir`                 | Create a directory.                                                                            | `mkdir newdirectory`               |                                       |
| `mkdir -p dir1/dir2/dir3`   | Create a directory hierarchy, creating parent directories as needed.                           | `mkdir -p myproject/src/main/java` |                                       |
| `touch filename`            | Create an empty file if it doesn't exist, or update its timestamp if it does.                  | `touch myfile.txt`                 |                                       |


### File/Directory Permissions and Groups

Linux permissions and groups play a crucial role in managing access to files and directories. Every file and directory in Linux has an associated set of permissions and ownership, which determine who can read, write, or execute them. These permissions are managed for three categories: user (u), group (g), and others (o).

---

### **Understanding Permissions**

- **Read (r)**: Allows viewing the content of a file or listing the contents of a directory.
- **Write (w)**: Permits modifying the content of a file or creating/deleting files within a directory.
- **Execute (x)**: Enables executing a file as a program or accessing a directory.

Each file or directory has three sets of these permissions:

1. **User (u)**: The owner of the file.
2. **Group (g)**: A group of users who share the same permissions.
3. **Others (o)**: All other users.

---

### **Managing Permissions with Commands**

Below is a table summarizing key commands for managing file and directory permissions and groups in Linux:

| Command                 | Utility                                                                            | Example                         |
| ----------------------- | ---------------------------------------------------------------------------------- | ------------------------------- |
| `chmod <spec> filename` | Change file permissions. `<spec>` uses u(user), g(group), o(other), +, -, r, w, x. | `chmod u+x myprogram`           |
| `chmod -R <spec> dir`   | Recursively change permissions of a directory and its contents.                    | `chmod -R g+rw myproject`       |
| `chmod go=+r myfile`    | Add read permission for group and others.                                          | `chmod go=+r myfile`            |
| `chmod a+rwx myfile`    | Allow all users (a) read, write, and execute permissions.                          | `chmod a+rwx myfile`            |
| `chmod go-r myfile`     | Remove read permission from group and others.                                      | `chmod go-r myfile`             |
| `chown owner filename`  | Change the file owner.                                                             | `chown john myfile`             |
| `chgrp group filename`  | Change the file's primary group.                                                   | `chgrp developers myfile`       |
| `chgrp -R group dir`    | Recursively change the primary group of a directory and its contents.              | `chgrp -R developers myproject` |

---

### **Ownership in Linux**

Each file and directory in Linux has an associated:

1. **Owner**: Typically the user who created the file. The owner has special privileges to manage the file.
2. **Group**: A logical grouping of users. Users in the group share the same access permissions for the file or directory.

#### Commands to Manage Ownership

- `chown owner filename`: Change the owner of a file.
    - Example: `chown alice report.txt` assigns ownership of `report.txt` to user `alice`.
- `chgrp group filename`: Change the primary group of a file.
    - Example: `chgrp admins report.txt` assigns `admins` as the group for `report.txt`.
- `chgrp -R group dir`: Recursively change the group ownership for a directory and its contents.
    - Example: `chgrp -R developers project/` updates the group ownership of all files in `project`.

---

### **Tips for Working with Permissions and Groups**
- **Recursive Changes**: Use `-R` with `chmod` or `chgrp` to apply changes to a directory and its contents.
- **Avoid Over-Permissive Settings**: Grant only necessary permissions to maintain system security.
- **Verify Changes**: Use `ls -l` to list files with their permissions and ownership to confirm changes.


## Section 1.3: Hello World

**Command:**

```bash
echo "Hello World"
```

**Output:**

```
Hello World
```

## Section 1.4: Basic Linux Utilities

**Getting Help in Linux:**

| Command                        | Usability                                                                       |
| ------------------------------ | ------------------------------------------------------------------------------- |
| `man <name>`                   | Read the manual page of `<name>`.                                               |
| `apropos <editor>`             | Output all applications whose one-line description matches the word `<editor>`. |
| `help`                         | When not able to recall the application name, use this command.                 |
| `help <name>`                  | In Bash shell, this will display the info about the `<name>` bash command.      |
| `info <name>`                  | View all the information about `<name>`.                                        |
| `dpkg -l`                      | Output a list of all installed packages on a Debian-based system.               |
| `dpkg -L packageName`          | List files installed and path details for a given package on Debian.            |
| `less /var/lib/dpkg/available` | Return descriptions of all available packages.                                  |
| `whatis cp`                    | List a one-line description of cp.                                              |


**User Identification:**

| Command       | Usability                                                                                                     |
| ------------- | ------------------------------------------------------------------------------------------------------------- |
| `hostname`    | Display hostname of the system.                                                                               |
| `hostname -f` | Displays Fully Qualified Domain Name (FQDN) of the system.                                                    |
| `passwd`      | Change password of current user.                                                                              |
| `whoami`      | Username of the user logged in at the terminal.                                                               |
| `who`         | List of all users currently logged in.                                                                        |
| `w`           | Display current system status, time, duration, list of users currently logged in, and other user information. |
| `last`        | Who recently used the system.                                                                                 |
| `last root`   | When was the last time root logged in.                                                                        |
| `lastb`       | Shows all bad login attempts into the system.                                                                 |

**Process Related Information:**

| Command      | Usability                                                                                                                            |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------ |
| `top`        | List all processes sorted by their current system resource usage. Continuously updated display (3 seconds default). Use `q` to exit. |
| `ps`         | List processes currently running on current shell session.                                                                           |
| `ps -u root` | List all processes and commands root is running.                                                                                     |
| `ps -aux`    | List all processes by all users on the current system.                                                                               |

## Section 1.5: Searching for Files by Patterns

**Find Files by Name:**

```bash
find /var/www -name '*.css'
```

**Find Files Containing Text:**

```bash
grep font /var/www/html/style.css
```

## Section 1.6: File Manipulation

| Command                         | Description                                          |
| ------------------------------- | ---------------------------------------------------- |
| `touch myFile`                  | Create an empty text file called `myFile`.           |
| `mv myFile myFirstFile`         | Rename `myFile` to `myFirstFile`.                    |
| `cat myFirstFile`               | View the contents of a file.                         |
| `less myFirstFile`              | View the content of a file with pager.               |
| `head myFirstFile`              | View the first several lines of a file.              |
| `tail myFirstFile`              | View the last several lines of a file.               |
| `vi myFirstFile`                | Edit a file.                                         |
| `mkdir myFirstDirectory`        | Create an empty directory called `myFirstDirectory`. |
| `mkdir -p src/myFirstDirectory` | Create multi-path directory.                         |


## Chapter 2: Detecting Linux Distribution Name and Version, Kernel and Shell

**Section 2.1: Detect Debian-based Distribution**

The primary method to determine the Debian-based distribution and its version is using the command `lsb_release -a`.

**Example Output:**

**On Debian:**

```bash
$ lsb_release -a
No LSB modules are available.
Distributor ID:	Debian
Description:	Debian GNU/Linux testing (stretch)
Release:	testing
Codename:	stretch
```


**Alternative Method (if `lsb_release` is not installed):**

If the `lsb_release` command is unavailable, a less reliable but often helpful method is to examine the `/etc/issue` file.  This file often contains information about the distribution.

**Example:**

On Ubuntu:

```bash
$ cat /etc/issue
Ubuntu 12.04.5 LTS \n \l
```

**Important Note:** The `/etc/issue` file's contents can vary significantly between distributions and versions, making it a less robust method than `lsb_release -a`.  The `lsb_release` command is preferred whenever possible.

OR
```
cat /etc/os-release
```

Running Kernel
```
uname -a
```

Shell
```
chsh -l
echo $SHELL
history
```


# Chapter 3: Manage Files

| Command         | Description                                                                                               | Options                                        | Output Example                                                                                   |
| --------------- | --------------------------------------------------------------------------------------------------------- | ---------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| `df -h`         | Displays disk space usage for file systems in human-readable format.                                      | `-h` (human-readable)                          | `Filesystem      Size  Used Avail Use% Mounted on`<br>`/dev/sda1        20G   12G   6.5G  65% /` |
| `du`            | Reports on disk usage of files and directories.                                                           | `-s`, `-h`, `-S`, `-t size`, `-d depth`        | Varies greatly depending on options and arguments.                                               |
| `du -s`         | Displays only the total disk usage for each argument (file or directory).                                 | `-s` (summarize)                               | `4K     ./file1`<br>`12K    ./directory1`                                                        |
| `du -h`         | Displays disk usage in human-readable format for the current directory and its subdirectories.            | `-h` (human-readable)                          | `4.0K    ./file1`<br>`12K    ./directory1`                                                       |
| `du -Sh`        | Displays the size of each directory (recursively) in human-readable format, excluding subdirectory sizes. | `-S` (summarize, exclude subdirectories), `-h` | `12K    ./directory1`<br>`4.0K    ./file2`                                                       |
| `du -Sh -t 10M` | Displays size of each directory (recursively) in human-readable format, showing only those > 10MB.        | `-S`, `-h`, `-t size` (threshold)              | Only directories larger than 10MB are shown.                                                     |
| `du -d 1`       | Displays the size of the current directory and its immediate subdirectories, not recursing further.       | `-d depth` (depth of recursion)                | Only one level of subdirectories is shown.                                                       |

# Chapter 4: Getting System Information

| Command             | Description                                                      | Options                          | Output Example                                                                     | Requires Root? |
| ------------------- | ---------------------------------------------------------------- | -------------------------------- | ---------------------------------------------------------------------------------- | -------------- |
| `free -h`           | Displays memory usage statistics in human-readable format.       | `-h` (human-readable)            | Table showing total, used, free, shared, buffers, cache, and available memory.     | No             |
| `netstat -ntlp`     | Shows open TCP listening sockets and their associated processes. | `-n`, `-t`, `-l`, `-p`           | List of TCP listening sockets with PIDs and process names.                         | No             |
| `netstat -nulp`     | Shows open UDP listening sockets and their associated processes. | `-n`, `-u`, `-l`, `-p`           | List of UDP listening sockets with PIDs and process names.                         | No             |
| `netstat -nxlp`     | Shows open Unix domain sockets and their associated processes.   | `-n`, `-x`, `-l`, `-p`           | List of Unix domain sockets with PIDs and process names.                           | No             |
| `sudo iftop`        | Displays real-time network bandwidth usage.                      | None                             | Dynamic display showing network traffic per connection.                            | Yes            |
| `lsusb`             | Lists USB devices connected to the system.                       | `-t` (tree view), `-v` (verbose) | List of connected USB devices.                                                     | No             |
| `lsusb -tv`         | Lists USB devices in a tree view with verbose information.       | `-t`, `-v`                       | Hierarchical tree view of USB devices with detailed information.                   | No             |
| `lscpu`             | Provides a summary of CPU architecture information.              | None                             | Table summarizing CPU architecture, model, cores, frequency, cache, etc.           | No             |
| `cat /proc/cpuinfo` | Displays detailed CPU information from the `/proc/cpuinfo` file. | None                             | Detailed, less structured information about CPU cores and other low-level details. | No             |

# Chapter 5: Services

### Listing Services

| Command                               | Description                                    |
| ------------------------------------- | ---------------------------------------------- |
| `systemctl`                           | Lists all services (active, inactive, failed). |
| `systemctl list-units`                | Lists all units (services, targets, etc.).     |
| `systemctl list-units --type=service` | Lists only service units.                      |
| `systemctl --failed`                  | Lists services that have failed to start.      |
| `systemctl --failed --type=service`   | Lists failed service units.                    |
| `systemctl status <service-name>`     | shows details on a specific service status.    |

### Managing Targets (Similar to Runlevels in SysV)

Targets in systemd are similar to runlevels in the older SysV init system. They define the system's state (e.g., graphical desktop, multi-user text mode).

| Command                     | Description                                           |
|------------------------------|-------------------------------------------------------|
| `systemctl get-default`      | Shows the current default target.                     |
| `systemctl set-default <target-name>` | Sets a new default target.  `<target-name>` examples: `multi-user.target`, `graphical.target` |


### Managing Services at Runtime

| Command                 | Description                                                   |
|--------------------------|---------------------------------------------------------------|
| `systemctl start <service-name>` | Starts a service.                                         |
| `systemctl stop <service-name>`  | Stops a service.                                          |
| `systemctl restart <service-name>` | Restarts a service.                                       |
| `systemctl reload <service-name>` | Reloads the service's configuration without restarting it. |
| `systemctl status <service-name>` | Shows the current status of a service.                    |


### Managing Autostart of Services (Enabling/Disabling on Boot)

| Command                     | Description                                               |
|------------------------------|-----------------------------------------------------------|
| `systemctl is-enabled <service-name>` | Checks if a service is enabled to start at boot.           |
| `systemctl is-active <service-name>`  | Checks if a service is currently running.                 |
| `systemctl enable <service-name>`   | Enables a service to start at boot.                     |
| `systemctl disable <service-name>`  | Disables a service from starting at boot.                |

### Restarting systemd

| Command                   | Description                                                                             |
| ------------------------- | --------------------------------------------------------------------------------------- |
| `systemctl daemon-reload` | Reloads systemd's configuration files.  Use this after making changes to service files. |

# Chapter 6: Managing Services


**Systemd-based Systems (Fedora ≥ 15, Ubuntu ≥ 15.04, RHEL/CentOS ≥ 7):**

| Command                              | Description                                                                                                |
| ------------------------------------ | ---------------------------------------------------------------------------------------------------------- |
| `systemctl status <service-name>`    | Shows the basic status and recent errors for a service.                                                    |
| `journalctl -xe`                     | Displays the last 1000 log entries in a pager (like `less`), jumping to the end.                           |
| `journalctl -f`                      | Follows log messages as they are added.                                                                    |
| `journalctl -f -t <service-name>`    | Follows log messages specifically for a given service.                                                     |
| `journalctl -p <priority> -S <date>` | Filters log entries by priority (e.g., `err`, `warn`, `info`, `debug`) and start date (e.g., `yesterday`). |


**If `journalctl` is unavailable or for services not using the system journal:**

| Command                   | Description                                                                              |
|----------------------------|------------------------------------------------------------------------------------------|
| `tail -f /var/log/messages` | Displays the last lines of the system log, continuously updating (`-f` for "follow").   |
| `tail -f /var/log/secure`  | Displays the last lines of the secure log (for privileged services), continuously updating. |
| `tail -f <service-specific-log-file>` | Monitors a service's specific log file if one exists (often within `/var/log/`).      |


# Chapter 7: Secure Shell (SSH)

```
ssh -p port user@server-address
```

To generate ssh
```
ssh-keygen -t rsa -b 4096 - C myemail@email.com
```

```
ssh -i ~/my.ssh/id_rsa username@ip
```

```
ssh -L 7474:localhost:7474 username@ip
```

To download from server

```
scp username@ip:server_file localpath
```

Upload to Server

```
scp localfile username@ip:server_path
```


# Chapter 8: Network 

### **1. Checking the IP Address**

#### Command: `ip` or `ifconfig`

- **Usage**: Display the IP addresses and network interface details.
- **Examples**:
    - `ip addr show`: Displays details of all network interfaces.
    - `ifconfig`: Displays network configuration (older tool, may not be available by default).

Note: public IP: `curl ifconfig.me`

---

### **2. Ping a Host**

#### Command: `ping`

- **Usage**: Test connectivity to a specific host by sending ICMP echo requests.
- **Examples**:
    - `ping google.com`: Sends continuous ICMP requests to `google.com`.
    - `ping -c 4 google.com`: Sends only 4 packets to `google.com`.

---

### **3. Testing HTTP/HTTPS Requests**

#### Command: `curl`

- **Usage**: Send HTTP/HTTPS requests to a server and display the response.
- **Examples**:
    - `curl http://example.com`: Fetches the content of `example.com`.
    - `curl -I http://example.com`: Displays HTTP headers of `example.com`.
    - `curl -X POST -d 'key=value' http://example.com`: Sends a POST request with data to `example.com`.

---

### **4. Trace the Route to a Host**

#### Command: `traceroute`

- **Usage**: Show the route packets take to reach a destination.
- **Examples**:
    - `traceroute google.com`: Displays the network path to `google.com`.
    - `traceroute -n google.com`: Displays the route with IP addresses only (no DNS resolution).

> **Note**: If `traceroute` is not installed, use `sudo apt install traceroute` or the equivalent for your distro.

---

### **5. Display Routing Table**

#### Command: `route` or `ip route`

- **Usage**: View or manipulate the system’s routing table.
- **Examples**:
    - `route -n`: Displays the routing table without resolving hostnames.
    - `ip route`: Displays the current routing table.

---

### **6. Query DNS Information**

#### Command: `dig` or `nslookup`

- **Usage**: Retrieve DNS information for a specific domain.
- **Examples**:
    - `dig google.com`: Fetches DNS records for `google.com`.
    - `dig +short google.com`: Displays concise DNS information.
    - `nslookup google.com`: Fetches DNS information (simpler alternative to `dig`).

---

### **7. Network Statistics**

#### Command: `netstat` or `ss`

- **Usage**: Display network connections, routing tables, and interface statistics.
- **Examples**:
    - `netstat -tuln`: Displays active TCP and UDP connections.
    - `ss -tuln`: Faster alternative to `netstat` for viewing open ports.

---

### **8. Checking Open Ports**

#### Command: `nmap`

- **Usage**: Scan networks and identify open ports.
- **Examples**:
    - `nmap localhost`: Scans for open ports on the local machine.
    - `nmap -p 22 192.168.1.1`: Checks if port 22 (SSH) is open on a specific host.

> **Note**: If `nmap` is not installed, use `sudo apt install nmap` or the equivalent for your distro.

---

### **9. Viewing Active Connections**

#### Command: `lsof` or `netstat`

- **Usage**: List open files and network connections.
- **Examples**:
    - `lsof -i`: Displays all active network connections.
    - `netstat -anp`: Lists all active connections with their associated processes.
