## Permisssion File folder in Linux
Example bellow.
```
chmod -R 777 /home/user/Development/DevOps
```
This command sets the permissions to read, write, and execute for the owner, group, and others. In octal notation, it's represented as rwxrwxrwx.

- Owner: Read, Write, and Execute.
- Group: Read, Write, and Execute.
- Others: Read, Write, and Execute.

This gives full read, write, and execute access to all users, making it even more permissive than chmod -R 666. It is extremely open and generally not recommended for regular use, especially for files and directories containing sensitive information.

```
chmod -R 666 /home/user/Development/DevOps
```
It almost same 777, but it not permited to edit by editor like vs code. 

