# Linux User and Group Management With Permissions
## Note:
- Default use have `/etc/passwd` dir
- Default group  have store `/etc/group` dir
- 0-999 no have system users
- user will start 1000 serial number
- All user have create default dir in home directory with user name.
- If you create new user, at a time create a group. Group and user create as a same name.
- `usermod` means user modification
### All Command use flow:-

#### User Management
```
sudo adduser username
```
- Create user
```
sudo usermod -l 'new_login_name' old_login_name
```
- Change user login name
```
sudo usermod -d /new/home/directory username
```
- Change the user's home directory

```
sudo usermod -L username
```
- Lock username

```
sudo usermod -L username
```
- Lock username

```
sudo passwd username
```
- Change user password


```
sudo userdel username
```
- Delete only user, but home dir available

```
sudo userdel -r username
```
- Remove user together with his/her home directory

```
sudo chage -d 0 username
```
- Force a user to change password on next login

```
sudo usermod --expiredate 2023-12-31 username
```
- Set an expiration date for a user account

```
last username
```
- Check a user's login history

```
sudo su username
```
- Switch normal user
```
sudo su - username
```
- Switch user with working dirctorate
```
sudo usermod -aG groupname username
```
- Assign user at group
```
finger username
id username
```
- Both commands show different user information, like:- id,group,login

#### Group Management
```
sudo addgroup groupname
```
- Create a group
```
sudo usermod -aG groupname username
```
- Assign user at group
```
sudo groupmod -n new_name old_gp_name
```
- Change group name
```
sudo deluser username groupname
```
- Remove a user from a group
```
sudo gpasswd -d username groupname
```
- It also use for remove user
```
getent group devops
```
- Display groups members
```
sudo delgroup group_name
```
- Delete group_name
```
sudo usermod -aG group1,group2 username
```
- Changing a user's supplementary groups allows you to manage the
additional groups
```
sudo addgroup --gid 1020 new_group_name
```
- Assign group id when creating group
```
sudo groupmod -gid new_gid group_name
```
- Change GID of an existing group

### Understanding Linux File Permissions
#### Each file and directory has three user based permission groups:
- Owner – The Owner permissions apply only to the owner of the file or directory,
they will not impact the actions of other users.
- Group – The Group permissions apply only to the group that has been
assigned to the file or directory, they will not affect the actions of other users.
- All users – The All Users permissions apply to all other users on the system,
this is the permission group that you want to watch the most.

#### The Permission Groups used are:
- u – Owner
- g – Group
- o – Others
- a – All users
#### Permission Types
- read – The Read permission refers to a user’s capability to read the contents
of the file.
- write – The Write permissions refer to a user’s capability to write or modify a
file or directory.
- execute – The Execute permission affects a user’s capability to execute a file
or view the contents of a directory.
#### Using Binary References to Set permissions
- r=4
- w=2
- x=1

Note: We can give permission to user or group using these binary number or words.
## Directory Structure
### #drwxr-xr-x  2 root root 4096 Nov 13 18:32 devops/
#### When we create directory to sudo user, it's default permission. Bellow explain all think:-
- `d` -Directory indicator
- `rwx` -User have read,write,execute permission
- `r-x` -Group have read,-,execute permission
- `r-x` -Others have read,-,execute permission
###### Full Binary Permission is:- (rwx = 4+2+1) = 7, (r-x = 4+0+1) = 5,(r-x = 4+0+1) = 5 => `755`
- `2` Hard link
- `root` - 1st root is user
- `root` - 2nd root is group
- `4096` - Dir size
- `Nov 13 18:32` - Last Modify Date
- `devops` - Directory
## File Structure
### -rw-r--r--  1 root root    0 Nov 13 18:32 text.txt
- `-` -File indicator
- `rw-` -User have read,write,- permission
- `r--` -Group have read,-,- permission
- `r--` -Others have read,-,- permission
###### Full Binary Permission is:- (rw- = 4+2+0) = 6, (r-- = 4+0+0) = 4,(r-- = 4+0+0) = 4 => `644`
- `1` Hard link
- `root` - 1st root is user
- `root` - 2nd root is group
- `0` - File size
- `Nov 13 18:32` - Last Modify Date
- `text.txt` - file

### Change dir/file owner
```
sudo chown -R ashadozzaman:root test.txt
```
- Change test.txt file owner root to ashadozzaman
```
 sudo chmod -R 444 text.txt
```
- Change file permission, given only read permission all 3 types user.
```
sudo chmod u+w text.txt 
```
- Change permission to symble
- User have write permission in text.txt file
- Output: `-rw-r--r--  1 ashadozzaman root   49 Nov 14 05:10 text.txt`
```
sudo chmod g+w+x text/txt
```
- Group user permited write and execute.
#### Creating a Soft Link/Symbolic Link
In Linux, a symbolic link, often referred to as a `soft link`or "`symlink`," is a file that contains a reference to another file or directory. Symbolic links are similar to shortcuts in Windows or aliases in macOS. 
```
ln -s /path/to/target /path/to/link
```
```
sudo ln -s /etc/nginx/sites-available/shovoua.com /etc/nginx/sites-enabled/
```
- Create soft link
```
rm /etc/nginx/sites-enabled/shovoua.com
```
- Remove soft link

```
readlink ../sites-enabled/shovoua.com
```
- If you want to know what a `soft link` point.
### Important Points:
- Symbolic links can point to files or directories.
- They can span file systems and partitions.
- If you move or delete the target file, the symbolic link becomes broken.
- Symbolic links can be used for various purposes, such as providing a generic name for a specific version of a program, creating shortcuts, or organizing files.


# Linux User and Group Management With Permissions
## Note:
- Default use have `/etc/passwd` dir
- Default group  have store `/etc/group` dir
- 0-999 no have system users
- user will start 1000 serial number
- All user have create default dir in home directory with user name.
- If you create new user, at a time create a group. Group and user create as a same name.
- `usermod` means user modification
### All Command use flow:-

#### User Management
```
sudo adduser username
```
- Create user
```
sudo usermod -l 'new_login_name' old_login_name
```
- Change user login name
```
sudo usermod -d /new/home/directory username
```
- Change the user's home directory

```
sudo usermod -L username
```
- Lock username

```
sudo usermod -L username
```
- Lock username

```
sudo passwd username
```
- Change user password


```
sudo userdel username
```
- Delete only user, but home dir available

```
sudo userdel -r username
```
- Remove user together with his/her home directory

```
sudo chage -d 0 username
```
- Force a user to change password on next login

```
sudo usermod --expiredate 2023-12-31 username
```
- Set an expiration date for a user account

```
last username
```
- Check a user's login history

```
sudo su username
```
- Switch normal user
```
sudo su - username
```
- Switch user with working dirctorate
```
sudo usermod -aG groupname username
```
- Assign user at group
```
finger username
id username
```
- Both commands show different user information, like:- id,group,login

#### Group Management
```
sudo addgroup groupname
```
- Create a group
```
sudo usermod -aG groupname username
```
- Assign user at group
```
sudo groupmod -n new_name old_gp_name
```
- Change group name
```
sudo deluser username groupname
```
- Remove a user from a group
```
sudo gpasswd -d username groupname
```
- It also use for remove user
```
getent group devops
```
- Display groups members
```
sudo delgroup group_name
```
- Delete group_name
```
sudo usermod -aG group1,group2 username
```
- Changing a user's supplementary groups allows you to manage the
additional groups
```
sudo addgroup --gid 1020 new_group_name
```
- Assign group id when creating group
```
sudo groupmod -gid new_gid group_name
```
- Change GID of an existing group

### Understanding Linux File Permissions
#### Each file and directory has three user based permission groups:
- Owner – The Owner permissions apply only to the owner of the file or directory,
they will not impact the actions of other users.
- Group – The Group permissions apply only to the group that has been
assigned to the file or directory, they will not affect the actions of other users.
- All users – The All Users permissions apply to all other users on the system,
this is the permission group that you want to watch the most.

#### The Permission Groups used are:
- u – Owner
- g – Group
- o – Others
- a – All users
#### Permission Types
- read – The Read permission refers to a user’s capability to read the contents
of the file.
- write – The Write permissions refer to a user’s capability to write or modify a
file or directory.
- execute – The Execute permission affects a user’s capability to execute a file
or view the contents of a directory.
#### Using Binary References to Set permissions
- r=4
- w=2
- x=1

Note: We can give permission to user or group using these binary number or words.
## Directory Structure
### #drwxr-xr-x  2 root root 4096 Nov 13 18:32 devops/
#### When we create directory to sudo user, it's default permission. Bellow explain all think:-
- `d` -Directory indicator
- `rwx` -User have read,write,execute permission
- `r-x` -Group have read,-,execute permission
- `r-x` -Others have read,-,execute permission
###### Full Binary Permission is:- (rwx = 4+2+1) = 7, (r-x = 4+0+1) = 5,(r-x = 4+0+1) = 5 => `755`
- `2` Hard link
- `root` - 1st root is user
- `root` - 2nd root is group
- `4096` - Dir size
- `Nov 13 18:32` - Last Modify Date
- `devops` - Directory
## File Structure
### -rw-r--r--  1 root root    0 Nov 13 18:32 text.txt
- `-` -File indicator
- `rw-` -User have read,write,- permission
- `r--` -Group have read,-,- permission
- `r--` -Others have read,-,- permission
###### Full Binary Permission is:- (rw- = 4+2+0) = 6, (r-- = 4+0+0) = 4,(r-- = 4+0+0) = 4 => `644`
- `1` Hard link
- `root` - 1st root is user
- `root` - 2nd root is group
- `0` - File size
- `Nov 13 18:32` - Last Modify Date
- `text.txt` - file

### Change dir/file owner
```
sudo chown -R ashadozzaman:root test.txt
```
- Change test.txt file owner root to ashadozzaman
```
 sudo chmod -R 444 text.txt
```
- Change file permission, given only read permission all 3 types user.
```
sudo chmod u+w text.txt 
```
- Change permission to symble
- User have write permission in text.txt file
- Output: `-rw-r--r--  1 ashadozzaman root   49 Nov 14 05:10 text.txt`
```
sudo chmod g+w+x text/txt
```
- Group user permited write and execute.
#### Creating a Soft Link/Symbolic Link
In Linux, a symbolic link, often referred to as a `soft link`or "`symlink`," is a file that contains a reference to another file or directory. Symbolic links are similar to shortcuts in Windows or aliases in macOS. 
```
ln -s /path/to/target /path/to/link
```
```
sudo ln -s /etc/nginx/sites-available/shovoua.com /etc/nginx/sites-enabled/
```
- Create soft link
```
rm /etc/nginx/sites-enabled/shovoua.com
```
- Remove soft link

```
readlink ../sites-enabled/shovoua.com
```
- If you want to know what a `soft link` point.
### Important Points:
- Symbolic links can point to files or directories.
- They can span file systems and partitions.
- If you move or delete the target file, the symbolic link becomes broken.
- Symbolic links can be used for various purposes, such as providing a generic name for a specific version of a program, creating shortcuts, or organizing files.

