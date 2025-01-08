原文地址：https://www.tecmint.com/linux-commands-for-sysadmins/



# 50 Must-Know Linux Commands: From Newbie to SysAdmin Pro



For someone new to **Linux**, using it can still feel challenging, even with [user-friendly distributions](https://www.tecmint.com/top-most-popular-linux-distributions/) like **Ubuntu** and **Mint**.

While these distributions simplify many tasks, some manual configuration is often required, but fully harnessing the power of Linux, understanding basic commands is essential.

In **Linux**, commands are the primary way to interact with the system and allow users to perform tasks, configure settings, and manage the system efficiently.

This guide introduces 60 essential Linux commands, providing a foundation for beginners and a pathway to becoming a skilled system administrator. These commands cover a wide range of functions, from navigating directories and managing files to performing advanced system operations.

Whether you’re just starting out or aiming to deepen your expertise, these commands will help you unlock the full potential of Linux.

## Basic Linux Commands and Examples for Newbies



Whether you’re a beginner or an advanced user, [mastering basic Linux commands](https://www.tecmint.com/useful-linux-commands-for-newbies/) is essential for navigating and controlling the operating system.

Below are some [commonly used Linux commands](https://www.tecmint.com/most-used-linux-commands/) along with their descriptions and examples:

### 1. View the Contents of a Directory

The [ls command](https://www.tecmint.com/ls-command-in-linux/) is used to view the files and directories within a specified directory, it can display both visible and hidden files (files starting with `.` are hidden by default).

Additional options can provide detailed information like file permissions, ownership, size, and modification dates.

```
ls -la
```

### 2. Viewing Blocks, HDD Partition, External HDD

The [lsblk command](https://www.tecmint.com/commands-to-collect-system-and-hardware-information-in-linux/) displays information about block devices such as hard drives, partitions, and external drives in a tree-like format.

```
lsblk
```

### 3. Checking the Integrity of Downloaded/Transferred Packages

The `sha256sum` or `md5sum` commands generate and verify cryptographic hash values for files, which ensures the file’s integrity after downloading or transferring.

```
sha256sum file.tar.gz
```

### 4. Converting and Copying a File

The [dd command](https://www.tecmint.com/dd-command-examples/) is used for low-level file copying and conversion, which is often employed to [create bootable USB drives](https://www.tecmint.com/linux-bootable-usb-creators/) or [clone disk images](https://www.tecmint.com/clone-linux-partitions/).

```
dd if=input.img of=output.img bs=4M status=progress
```

### 5. Know Your Machine Name, OS, and Kernel



The [uname command](https://www.tecmint.com/check-linux-os-version/) provides system information, including the kernel version, system architecture, and hostname.

```
uname -a
```

### 6. Viewing History of Commands

The [history command](https://www.tecmint.com/history-command-examples/) lists previously executed commands, allowing you to recall or reuse them.

```
history
```

### 7. Run Commands as Root User

The [sudo command](https://www.tecmint.com/sudo-command-linux/) allows users to execute commands with administrative privileges. Use `sudo -i` to switch to a root shell.

```
sudo -i
```

### 8. Make a New Directory

The [mkdir command](https://www.tecmint.com/mkdir-command-examples/) creates a new directory with the specified name in the current location.

```
mkdir my_folder
```

### 9. Create or Update File Timestamps

The [touch command](https://www.tecmint.com/8-pratical-examples-of-linux-touch-command/) creates empty files or updates the timestamp of existing ones.

```
touch my_file.txt
```

### 10. Changing the File Permission

The `chmod` command changes file permissions, controlling who can read, write, or execute a file.

```
chmod 644 my_file.txt
```

### 11. Change File Ownership



The [chown command](https://www.tecmint.com/chown-command-examples/) changes file ownership and group ownership.

```
sudo chown user:group my_file.txt
```

### 12. Install, Update, and Maintain Packages

The [apt command](https://www.tecmint.com/apt-command-in-linux/) manages software packages on [Debian-based systems](https://www.tecmint.com/debian-based-linux-distributions/).

```
sudo apt update && sudo apt install package_name
```

### 13. Uncompressing a Tar File

The [tar command](https://www.tecmint.com/tar-command-examples-linux/) extracts compressed files.

```
tar -xvzf file.tar.gz
```

### 14. See Current Date, Time, and Calendar

The [date](https://www.tecmint.com/change-linux-system-date-and-time/) and `cal` commands display the current date, time, and calendar.

```
date
cal
```

### 15. Print Contents of a File

The [cat command](https://www.tecmint.com/cat-command-linux/) prints the contents of a file to the terminal.

```
cat my_file.txt
```

### 16. Copy and Move Files

The [cp](https://www.tecmint.com/cp-command-examples/) and [mv](https://www.tecmint.com/mv-command-linux-examples/) commands copy and move files, respectively.

```
cp source.txt destination.txt
mv old_name.txt new_name.txt
```

### 17. See the Working Directory for Easy Navigation



The [pwd command](https://www.tecmint.com/pwd-command-examples/) prints the current directory path.

```
pwd
```

### 18. Change the Working Directory

The [cd command](https://www.tecmint.com/cd-command-in-linux/) navigates between directories.

```
cd /path/to/directory
```

## Advanced Linux Commands for Intermediate Users

Once you’ve mastered the basic Linux commands, it’s time to dive deeper into [more advanced commands](https://www.tecmint.com/20-advanced-commands-for-middle-level-linux-users/) that will help you manage and optimize your system more efficiently.

### 19. Finding a File in a Given Directory

The [find command](https://www.tecmint.com/35-practical-examples-of-linux-find-command/) is used to search for files and directories within a specified directory or across the entire file system.

```
find /path/to/directory -name "filename"
```

### 20. Searching a File with the Given Keywords

The [grep command](https://www.tecmint.com/12-practical-examples-of-linux-grep-command/) is used to search for specific patterns (keywords) within files, which is highly useful when you want to find specific information inside a file or a set of files.

```
grep "keyword" filename
```

### 21. Finding Online Documentation

The [man command](https://www.tecmint.com/linux-man-pages/) displays the manual or help documentation for a specific command, which provides detailed information about how to use a command, its options, and its syntax.

```
man ls
```

### 22. List Current Running Processes



The [ps command](https://www.tecmint.com/ps-command-examples-for-linux-process-monitoring/) shows a snapshot of the current processes running on your system with details like process IDs (PIDs), memory usage, and CPU usage.

```
ps aux
```

To list all processes related to **Firefox**, using `grep` to filter the output.

```
ps aux | grep firefox
```

### 23. Kill a Running Process

The [kill command](https://www.tecmint.com/how-to-kill-a-process-in-linux/) is used to terminate a running process by specifying the process ID (PID) of the process you want to terminate.

```
kill 1234
```

### 24. See the Location of Installed Binaries

The `which` command helps locate the path of executables in your system’s PATH by searching through the directories listed in the PATH environment variable and returns the location of the executable.

```
which python3
```

### 25. Starting, Ending, Restarting a Service

The [systemctl command](https://www.tecmint.com/manage-services-using-systemd-and-systemctl-in-linux/) is used to manage system services (also known as **daemons**) on systems using **systemd**.

```
systemctl start service_name
systemctl stop service_name
systemctl restart service_name
```

### 26. Creating and Removing Command Aliases

Aliases are shortcuts for commands, which can save time by reducing the amount of typing and the [alias command](https://www.tecmint.com/create-alias-in-linux/) creates a shortcut, while unalias remove it.

```
alias shortcut_name='command'
unalias shortcut_name
```



You can create an alias for a command with a custom name.

```
alias ll='ls -l'
unalias ll
```

This creates an alias `ll` for the `ls -l` command, which lists directory contents in a long format.

### 27. View Disk and Space Usage

The [df command](https://www.tecmint.com/how-to-check-disk-space-in-linux/) shows disk space usage for all mounted file systems by providing information about the total space, used space, and available space.

```
df -h
```

### 28. Removing a File and/or Directory

The [rm command](https://www.tecmint.com/remove-directory-linux/) is used to remove files and directories. You can use the `-r` option to remove directories and their contents recursively.

```
rm filename
rm -r directory_name
```

### 29. Print/Echo a Custom Output on Standard Output

The [echo command](https://www.tecmint.com/echo-command-in-linux/) is used to print text or the value of a variable to the terminal.

```
echo "Custom Message"
```

### 30. Changing Password in Linux

The `passwd` command is used to change passwords for the current user or other users (if you are the root user).

```
passwd username
```

### 31. View Printing Queue



The `lpq` command shows the status of the printing queue, including any pending or completed print jobs.

```
lpq
```

### 32. Compare Two Files

The [diff command](https://www.tecmint.com/best-linux-file-diff-tools-comparison/) compares two files line by line and displays the differences between them.

```
diff file1 file2
```

### 33. Download a File, the Linux Way (wget)

The [wget command](https://www.tecmint.com/10-wget-command-examples-in-linux/) is used to download files from the internet, it supports HTTP, HTTPS, and FTP protocols.

```
wget https://example.com/file.zip
```

### 34. Mount a Block/Partition/External HDD

The `mount` command is used to attach a block device (e.g., a hard drive or USB drive) to a directory in the filesystem.

```
mount /dev/sdX /mnt
```

### 35. Compile and Run C, C++, and Java Code

To compile and run code in `C`, `C++`, and `Java`, you use the respective compilers and runtimes.

- **C**: `gcc` is used to compile C programs.c.
- **C++**: `g++` is used to compile C++ programs.
- **Java**: `javac` is used to compile Java programs, and java is used to run them.

To compile and run `C` code:

```
gcc -o outputfile sourcefile.c
./outputfile
```



To compile and run `C++` code:

```
g++ -o outputfile sourcefile.cpp
./outputfile
```

To compile and run `Java` code:

```
javac filename.java
java filename
```

## Advance Linux Commands for Linux Sysadmins

In the last section of this series, we tried to cover the [commands that needed to administer](https://www.tecmint.com/20-advanced-commands-for-linux-experts/) a Linux server.

### 36. Configuring Network Interface

The [ifconfig command](https://www.tecmint.com/ifconfig-command-examples/) is used to allow you to set up, manage, and display network interface parameters, which is typically used to assign IP addresses, configure network interfaces, and troubleshoot network issues.

```
sudo ifconfig eth0 192.168.1.100 netmask 255.255.255.0 up
```

This command assigns the IP address `192.168.1.100` to the `eth0` interface and brings it up.

### 37. Viewing Custom Network-Related Information

The [netstat command](https://www.tecmint.com/install-netstat-in-linux/) provides detailed information about network connections, routing tables, interface statistics, and more.

```
netstat -tuln
```

### 38. Fetching Data with curl



The [curl command](https://www.tecmint.com/linux-curl-command-examples/) is used to transfer data from or to a server. It supports various protocols, including HTTP, FTP, and more. You can use it to fetch data from a web server or test server responses.

```
curl -I https://www.example.com
```

### 39. Checking DNS Information

The [dig command](https://www.tecmint.com/dig-command-examples/) is a DNS lookup utility that provides detailed information about DNS records, which is commonly used for troubleshooting DNS issues.

```
dig example.com
```

### 40. Knowing Your System Uptime

The [uptime command](https://www.tecmint.com/linux-uptime-command-examples/) shows how long the system has been running, the number of users logged in, and the system load averages for the past 1, 5, and 15 minutes.

```
uptime
```

### 41. Broadcast Messages to Logged-in Users

The `wall` command is used to send messages to all users currently logged into the system.

```
echo "System Maintenance in 10 minutes" | wall
```

### 42. Send Text Messages Directly to a User

The `write` command allows you to send a message to another logged-in user.

```
write username
```

### 43. Piping Commands Together

You can combine multiple commands using pipes `(|)` to pass the output of one command to another.

```
ps aux | grep firefox
```

### 44. Seeing the Processes of a CPU



The [top command](https://www.tecmint.com/12-top-command-examples-in-linux/) displays a dynamic, real-time view of system processes, including CPU and memory usage.

```
top
```

### 45. Creating a Newly Formatted ext4 Partition

The `mkfs.ext4` command is used to create an ext4 file system on a partition.

```
sudo mkfs.ext4 /dev/sdb1
```

### 46. Editing Files with vi, emacs, and nano

In Linux, there are [several text editors](https://www.tecmint.com/best-open-source-linux-text-editors/) available for editing files directly from the command line. Among the most popular are [vi](https://www.tecmint.com/vi-editor-usage/), [emacs](https://www.tecmint.com/emacs-text-editor/), and [nano](https://www.tecmint.com/learn-nano-text-editor-in-linux/).

To edit files with `vi`:

```
vi filename.txt
```

To edit files with `emacs`:

```
emacs myfile.txt
```

To edit files with `nano`:

```
nano myfile.txt
```

### 47. Copying a Large File/Folder with Progress Bar



The [rsync command](https://www.tecmint.com/rsync-local-remote-file-synchronization-commands/) is used to copy files and directories. With the `--progress` option, it shows a progress bar.

```
rsync -avh --progress source_directory/ destination_directory/
```

### 48. Check Available Memory

The [free command](https://www.tecmint.com/check-memory-usage-in-linux/) shows the amount of free and used memory in the system.

```
free -h
```

### 49. Backing Up a MySQL Database

The [mysqldump command](https://www.tecmint.com/mysql-backup-and-restore-commands-for-database-administration/) is used to create backups of MySQL databases.

```
mysqldump -u root -p database_name > backup.sql
```

### 50. Generate a Random Password

The `openssl` command can generate a random password.

```
openssl rand -base64 12
```

### 51. Merge Two Text Files

The `cat` command can be used to concatenate two text files into one.

```
cat file1.txt file2.txt > mergedfile.txt
```

### 52. List of All the Opened Files

The [lsof command](https://www.tecmint.com/10-lsof-command-examples-in-linux/) lists all open files and the processes that opened them.

```
lsof
```



These commands are fundamental tools for system administrators and users to interact with Linux systems efficiently.
