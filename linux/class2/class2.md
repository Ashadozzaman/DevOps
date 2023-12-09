## Ubuntu Linux Installation
##### Bellow shows some Linux commands with a description.
1 Displays detailed system information, including the kernel version. 
```
$uname -a
```
`Output:- Linux user-B760M-DS3H-AX 6.2.0-36-generic #37~22.04.1-Ubuntu SMP PREEMPT_DYNAMIC Mon Oct  9 15:34:04 UTC 2 x86_64 x86_64 x86_64 GNU/Linux`

2. Displays the hardware platform or instruction set architecture.
```
$uname -a
```
`Output:- x86_64`

3. Displays the machine or system type.
```
$uname -m
```
`Output:- x86_64`

4. Shows the bit-width of the system.
```
$getconf LONG_BIT
```
`Output:- 64`

5. Get IP details connecting the server
```
$ ip -a
$ curl ifconfig.me
```
`Output:- 192.168.0.102`

6. List files and directories
```
$ ll
```
`Output:- show all files and directorate with the hidden file`

7. show files and directories horizontally
```
$ ls
```
`Output:- show all files and directorate`

8. Change the current directory
```
$ cd ../
$ cd Downloads
```
Output:- 
`1. Back one step; 
2. Enter download Dir (user@user-B760M-DS3H-AX:~/Downloads$)`

9. Show current directory.
```
$ pwd
```
`Output:- /home/user/Downloads`

10. Create a new directory.
```
$ mkdir class3
$ mkdir dir1 dir2 //create multiple directories
$ ls
```
`Output:- Enter ls, show new dir`

11. Remove an empty directory.
```
$ rmdir class3
$ ls
```
`Output:- Enter ls, show remove dir`


12. Create a new file.
```
$ touch new-file.txt
$ ls
```
`Output:- Enter ls, show newly created file`

13. Remove files or directories.
```
$ rm new-file.txt
rm -rf /path/to/directory //delete force
$ ls
```
`Output:- Enter ls, remove new-file.txt file`
- you can use the `rm` command with the `-r` (recursive) and `-f` (force) options

14. Copy the file and directorate.
```
$ cp source_file destination  // copy normal
$ cp file.txt backup/newfile.txt //copy file with rename
$ cp /path/to/source/file.txt /path/to/destination/  //copy file to different destination
$ cp file1.txt file2.txt /path/to/destination/  //copy multiple files
$ cp -r source_directory destination/  //copy directory with content like recursive, but must need permission.

```
`Output:- Write comment for each command`

##### Move or Rename files and directories 

15. To move a file or directory from one location to another.

```
$ mv source_file_or_directory destination
```

16. To move a directory and its contents to another location, use the -r (or -R) option for recursive move.

```
$ mv -r old_directory/ new_location/
```
17. Renaming.

```
$ mv old_file.txt new_file.txt
```

18. Moveing with renaming.

```
$ mv old_directory/ new_location/new_directory/

```
19. Display the content of a file

```
$ cat readfile.txt
```
`cat command use for read any file in terminal`

