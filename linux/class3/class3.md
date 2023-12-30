## Linux Command use flow
##### Bellow shows some Linux commands with a description.

## 20. Use `kill`

The `kill` command in Unix-like operating systems is used to terminate or send signals to processes. Here are some common use cases:

```
kill PID

kill 5704
```
- Firefox `kill`.
- To terminate a process with PID(5704)

```
kill -SIGTERM 5678
```
- To send the `SIGTERM` signal to a process with `PID` 5678:

### Common Signals:

- SIGTERM (15): Termination signal. This is the default signal sent by `kill` if no signal is specified.
- SIGKILL (9): Unconditionally kills the process. It cannot be caught or ignored.
- SIGHUP (1): Hangup signal, often used to instruct a process to reload its configuration.

### Conditional Option
```
kill -9 PID
```
- This forcefully terminates the process with the specified PID.
```
kill -15 PID
```
- This sends a termination signal, allowing the process to perform cleanup 

```
kill -l
```
- This lists all available signal names and their corresponding numbers.

## 21. Use `less`
### View a file one page at a time using `less/more`

```
$ less class3.md
```
- Use the arrow keys or the `j` and `k` keys to scroll up and down.
- To move forward one page, press the Spacebar or the Page Down key.
- To move back one page, press `b` or the Page Up key.
- To quit less, press the `q` key.
- Search text within the file by pressing `'/',` the insert `text` press `enter`. 

## 22.  Use `more`

```
$ more class3.md
```
- `more` is similar to `less` but has `less` functionality


#### `less` is more versatile and allows you to scroll in both directions, search for text, and provides a more interactive experience

### Display the beginning or end of a file- `head/tail`

`head` and `tail` are command-line utilities used to display the beginning (head) and end (tail) of text files, respectively. They are commonly used to view a portion of a file, often for the purpose of previewing its contents or monitoring log files.

## 23.  Use `head`
```
$ head class3.md
```
- By default, `head` displays the first 10 lines.
```
$ head -n 20 class3.md
```
- This displays the first 20 lines of `class3.md` using `-n`.

## 24.  Use `tail`

To view the end of a file, you can use the `tail` command in a similar manner to `head`. By default, `tail` displays the last 10 lines of a file

```
$ tail class3.md

$ tail -n 20 class3.md

$ tail -f logfile
```
- If you want to continuously monitor a file, such as a log file, you can use the `-f` option.


## 25.  Use `nano/vi` 
#### Text editors for creating and editing files- `nano/vi`

```
$ nano filename
$ vi filename
```
## 26.  Use `grap` default

### Use `grap` (Search for text in files.)

It seems like you meant to refer to the grep command, which is a powerful tool for searching and manipulating text in Linux and Unix-like operating systems. grep allows you to search for specific text patterns within files or the output of other commands.

```
$ grep 'searching' class3.md
```
- This will show full sentence with bold searching(`searching`) word.

```
$ grep - n 'searching' class3.md
```
- This will show full sentences with bold searching(`monitor`) words.

```
$ grep -n 'monitor' class3.md
```
- This will show the lines containing "monitor" along with their corresponding line numbers.

```
$ grep -n -A 1 -B 2 'searching' class3.md
```
- This will show the lines containing "searching" along with their corresponding line numbers.
- `-n` will show line number
- `-A` 1 will show 1 line after the matching line.
- `-B` 2 will show 2 lines before the matching line.

```
$ grep -n '.*searching.*' class3.md
```
- This will show you all lines in the file that contain the word `searching`.

## 27. Use `find`

The `find` command is a powerful tool in Linux operating systems for searching and locating files and directories based on various criteria. Here are some common use cases:

```
$ find . -name "*.txt"
```
- Finds all files with the `.txt` extension.

```
$ find . -type d
```
- This will list all directories under the current directory.

```
$ find . -type f
```
- This will list all files under the current directory.

### Searching with Specific Criteria:

```
$ find . -mtime -1
```
- The `-mtime -1` option means modified within the last 24 hours.

```
$ find . -size +100k
```
- Files larger than 100 kilobytes.

### Combining Multiple Criteria:

You can combine multiple criteria using logical operators (`-and`, `-or`, `-not`).

```
$ find . -name "*.txt" -mtime -7
```
- To find all `.txt` files modified within the last 7 days

```
$ find . -name "*.log" -size +1M
```
- To find all .log files larger than 1 megabyte

### Executing Commands on Found Items:

```
$ find . -name "*.tmp" -delete
```
- To find and delete all `.tmp` files

```
$ find . -name "*.jpg" -exec mv {} /path/to/destination \;
$ find . -name "*.tmp" -exec mv {} `sample/` \;
```
- To find and move all `.jpg` files to a different directory

## 28.  Use `ps` (List running processes)

```
$ ps
```
- This command shows a snapshot of processes for the current user.

```
$ ps aux
```
- This displays detailed information for all processes running on the system, including those of other users.

```
$ ps -eo pid,ppid,cmd,%mem,%cpu
```
- This command customizes the output to show specific information such as process ID, parent process ID, command, memory usage, and CPU usage.
```
$ ps -ejH
```
- This shows processes in a tree structure, displaying the hierarchy of parent and child processes.


### Common Options `ps`:
- e: Display information about every process.
- f: Display full-format listing.
- l: Long format.
- u: Display information for a specific user.
- a: Display information about all processes on a terminal, including those without a controlling terminal.

## 29. Use `watch`

The `watch` command is used to execute a command periodically and display the output in the terminal. It's a handy tool for monitoring changes or updates in real-time. Here's how you can use the `watch` command:

```
$ watch -n 1 'ps aux'
$ watch -n 1 'commend'
```
- This uses the `watch` command to repeatedly execute `ps aux` every 1 second, providing real-time updates on process information.
- Actually watch auto run given command on given time
- By default, watch refreshes every 2 seconds.
- `-n 5` to run command every 5 seconds

```
$ watch free -m
```
- Monitor the system's free memory every 2 seconds, user/you can use.

```
$ watch df -h
```
- This will show the disk usage statistics in human-readable format.

```
$ watch tail /var/log/syslog
```
- This will display the last few lines of the system log file and update every 2 seconds.

```
$ watch netstat -an
```
- This will continuously display network connections.

```
$ watch -n 1 'top -b -n 1 | head -n 15'
```
- This will run the `top` command every second and display the top CPU-consuming processes.

#### Press Ctrl+C to exit watch when you're done monitoring.



## 31. Use pkill

You can also use the `pkill` command to send signals to processes based on their names rather than their PIDs.

```
pkill firefox
```
- Terminate a process named "firefox":
### Additional Options:
- l or -L: List available signal names and numbers.
- -s: Specify the signal to be sent (e.g., `-s HUP`).

## 32. Use `top` and `htop`

`top` and `htop` are both command-line utilities used to monitor system resources, but they provide different interfaces and functionalities.
```
top
```
```
htop
```

### Which One to Use?

`top`

- Standard and available on most Unix-like systems.
- Provides a lightweight, basic overview of system resources.
- Good for quick checks and basic monitoring.

`htop`

- Offers an enhanced, more visually appealing interface.
- Includes additional features like tree view and mouse support.
- Useful for a more detailed and interactive examination of system resource usage.


## 33. Use `df`

The `df` command in Unix-like operating systems is used to display information about disk space usage on file systems. It provides details about the amount of disk space used, available, and total capacity on mounted file systems. 

```
df
```
- This command displays information about all mounted file systems.

```
df /path
```
- Display with the path to the specific mounted file system you want to check.

```
df -h
```
- Display sizes in a human-readable format (e.g., KB, MB, GB).
```
df -T
```
- Display file system types in the output.
```
df -T ext4
```
- This shows disk space information only for file systems of type ext4.
```
df -i
```
- Display inode information (number of used and available inodes).

### Output Columns:
| Filesystem | 1K-blocks | Used    | Available | Use% | Mounted on |
|------------|-----------|---------|-----------|------|------------|
| /dev/sda1  | 20511356  | 3528688 | 15936864  | 19%  | /          |


### Understanding Output Columns:
- `Filesystem`: The mounted file system.
- `1K-blocks`: Total size of the file system in 1-kilobyte blocks.
- `Used`: Amount of disk space used.
- `Available`: Amount of disk space available.
- `Use%`: Percentage of disk space used.
- `Mounted` on: The mount point of the file system.

## 34. Use `du`

The `du` command in Linux is used to estimate file space usage. It reports the sizes of directories and their subdirectories, helping you understand the disk space consumption of files and directories. 

```
du -h /path/to/directory
```
- The `-h` option makes the output human-readable, showing sizes in KB, MB, GB, etc.


```
du -sh /path/to/directory
```
- Display only the total for each argument.

```
du -c /path/to/dir1 /path/to/dir2
```
- Display a grand total for all the specified files or directories..


```
du -h --max-depth=2 .
```
- Set the maximum depth of the current directory tree to be displayed.

```
du -h -a /path/to/directory
```
- Show sizes for files as well, not just directories.

```
du -h --max-depth=1 /
```
- This command displays the sizes of the top-level directories in the root file system.

```
du -h /dir1 /dir2 /dir3
```
- This shows the disk space usage for multiple directories.

```
du -h --total /dir1 /dir2
```
- This provides a total disk space usage for the specified directories.

### Understanding Output:
The output of `du` displays the sizes of directories and files. The sizes are cumulative, showing the total size of each directory and its contents. The `-h` option makes the output human-readable, while other options like `-s`, `-c`, and `-d` provide additional control over the displayed information.

## 35. Use `ifconfig/ip`

The `ipconfig/ip` command is used in Windows operating systems to display and manage the IP configuration of a computer. It provides information about the computer's network interfaces, IP addresses, subnet masks, default gateways, and more. 
```
ip a
```
```
ip a show 
```
```
ip address show
ip route show
```
- The `ip` command is a versatile tool for network configuration.
```
cat /etc/resolv.conf
```
- Show DNS Configuration
```
netstat -rn
```
-  The `netstat` command provides information about network connections and routing.

## 36. Use `ping`

```
ping shovoua.com
```
- Display domain IP.

## 37. Use `ssh`
 
The `ssh` (Secure Shell) command is used to establish a secure and encrypted connection to a remote server or device. It allows you to log into another machine over a network, execute commands in a remote machine, and transfer files securely between the local and remote machines. Here are some common use cases for the `ssh` command:

```
ssh username@remote_host

ssh ashadozzaman@192.168.0.103
```
- Replace `username` with your `username` on the remote server and `remote_host` with the hostname or IP address of the remote server.

```
ssh -p port_number username@remote_host
```
- Replace port_number with the specific port number if it's not the default port 22.

### Key-Based Authentication:
```
ssh-keygen -t rsa -b 2048
```
- Generate an SSH key pair if you don't have one:
```
ssh-copy-id username@remote_host
```
- Copy your public key to the remote server:
```
ssh username@remote_host
```
- Now you can log in without a password

### Remote Command Execution

```
ssh username@remote_host "command_to_execute"
```
- Execute a Command on the Remote Server
- Replace `command_to_execute` with the specific command you want to run on the remote server.

```
scp local_file username@remote_host:/path/to/destination
```
- Copy Files from Local to Remote:
- Replace `local_file` with the local file you want to copy, and specify the destination path on the remote server. 

```
scp username@remote_host:/path/to/remote_file local_destination
```
- Copy Files from Remote to Local
- Replace `remote_file` with the file on the remote server and specify the local destination.

### SSH Configuration
```
nano ~/.ssh/config
```
- Add custom configurations, such as aliases, options, or proxy settings.

```
eval "$(ssh-agent -s)"
```
- Start the SSH agent

```
ssh-add ~/.ssh/private_key
```
- Add your private key to the agent