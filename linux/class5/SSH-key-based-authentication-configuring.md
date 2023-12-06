# SSH keys based authentication configuration with Custom Host
<br>
Configuring SSH key-based authentication involves generating a key pair, copying the public key to the remote host, and configuring the local SSH client to use the private key when connecting to the remote host. Here's a step-by-step guide.
 
The `ssh` (Secure Shell) command is used to establish a secure and encrypted connection to a remote server or device. It allows you to log into another machine over a network, execute commands in a remote machine, and transfer files securely between the local and remote machines. Here are some common use cases for the `ssh` command:


## Step-1: Key-Based Authentication

Open a terminal on your local machine and run the following command:
```
ssh-keygen -t rsa -b 2048
```
- Generate an SSH key pair if you don't have one:

## Step 2: Copy Public Key to Remote Host

```
ssh-copy-id username@remote_host
```
- This command adds your public key to the `~/.ssh/authorized_keys` file on the remote host.

## Step 3: Test SSH Connection

```
ssh username@remote_host

ssh ashadozzaman@192.168.0.100
```
- Replace `username` with your `username` on the remote server and `remote_host` with the hostname or IP address of the remote server.

It's nececary for security, when we configure server we should be change post.
```
ssh -p port_number username@remote_host
```
- Replace port_number with the specific port number if it's not the default port 22.
- It's use when we changed default port

### Change Port

If we want to change post, we need to change here:-
```
sudo vim /etc/ssh/sshd_config
```

## Step 4: SSH Configuration

To simplify connections, you can create an SSH config file (~/.ssh/config) on your local machine. Edit the file with a text editor.

```
vim ~/.ssh/config
```
- Add custom configurations, such as aliases, options, or proxy settings.


Add the following lines, replacing "hostname" with your remote host's address and "key" with the path to your private key.\

```
Host myhost
  HostName hostname/ip
  User username
  Port 5454
  IdentityFile ~/.ssh/key

```
## Step 5: Connect Using SSH Config
Now you can connect to your remote host using the configured alias:\
`ssh myhost`

### More Info
#### SSH start

```
sudo systemctl start ssh
```

#### SSH stop
```
sudo systemctl stop ssh
```
#### SSH restart
```
sudo systemctl restart ssh
```

#### Check SSH status
```
sudo systemctl status ssh
```

#### Start the SSH agent
```
eval "$(ssh-agent -s)"
```

```
ssh-add ~/.ssh/private_key
```
- Add your private key to the agent

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



