# Storage Management In Linux

**How the disk is divided into partitions and how the information about these partitions is stored?**\
MBR (Master Boot Record) and GPT (GUID Partition Table) are two different partitioning schemes used to organize and manage data on storage devices, particularly on hard disk drives (HDDs) and solid-state drives (SSDs).

**List, create, delete, and modify physical storage partitions**

*Lists information about block devices?*
```
sudo lsblk
sudo cfdisk /dev/sdb
or
sudo fdisk --list /dev/sdb
```

*How to check whether your disk is using the Master Boot Record (MBR) or the GUID Partition Table (GPT) on Ubuntu*
```
sudo parted /dev/sda print
or
Install gdisk if it's not already installed
sudo apt-get install gdisk
sudo gdisk /dev/sda
```

```
sudo lsblk
sudo pvdisplay 
sudo cfdisk /dev/sdb
sudo lsblk 
sudo pvcreate /dev/sdc1 //create physical volumn
sudo pvdisplay 
sudo vgdisplay 
sudo vgextend vg0 /dev/sdc1  // vg0 means root group, /dev/sdc1 means new added stroage location.
sudo vgdisplay 
sudo lvdisplay 
sudo df -h //total space
sudo lvextend -L +50G /dev/vg0/lv-0
sudo lvextend -l +100%FREE /dev/vg0/lv-0
sudo resize2fs /dev/vg0/lv-0
sudo df -h
```
### Given details for all command

`sudo lsblk`

- `lsblk` stands for "list block devices."
- This command is used to display information about block devices (such as hard drives and partitions) in a tree-like format.

`sudo pvdisplay`

- `pvdisplay` stands for "physical volume display."
This command is used to show attributes of physical volumes (PVs) in the `LVM` (Logical Volume Manager) system.

`sudo cfdisk /dev/sdb`

- `cfdisk` is an interactive disk partitioning tool.
- `/dev/sdb` is the second block device (hard drive) in the system.
This command opens the cfdisk tool for the specified device, allowing you to create, delete, and manage partitions.

`sudo pvcreate /dev/sdc1`

- `pvcreate` initializes a physical volume for later use by LVM.
- `/dev/sdc1` is a partition on the third block device, which is being prepared as a physical volume.

`sudo vgdisplay`

- `vgdisplay` stands for "volume group display."
- Shows information about volume groups (VGs) in the LVM system.

`sudo vgextend vg0 /dev/sdc1`

- `vgextend` extends an existing volume group (vg0 in this case) by adding a physical volume (/dev/sdc1).


`sudo lvdisplay`

- `lvdisplay` stands for "logical volume display."
Displays information about logical volumes within the volume group.

`sudo df -h`

- `df` stands for "disk free."
- Shows information about disk space usage, including the total, used, and available space on file systems.

`sudo lvextend -L +50G /dev/vg0/lv-0`

- `lvextend` is used to extend the size of a logical volume (lv-0 in volume group vg0) by a specified amount (in this case, 50GB).

`sudo lvextend -l +100%FREE /dev/vg0/lv-0`

- An alternative way to extend the logical volume, using all available free space in the volume group.

`sudo resize2fs /dev/vg0/lv-0`

- `resize2fs` is used to resize an `ext2`, `ext3`, or `ext4` file system.
- Resizes the file system on the logical volume to fill the available space.

**Create and configure file systems**

The mkfs command is used to create a new file system on a device (such as a partition or a disk).\
`sudo mkfs.ext4 /dev/sdb1`

The tune2fs command is used to adjust various parameters and settings of an existing ext2, ext3, or ext4 file sst   ystem.\
`sudo tune2fs -L MyVolume /dev/sdb1`

Mount /dev/sdb1 into /mnt directory\
`sudo mount /dev/sdb1 /mnt`

Check block device ID\
`sudo blkid /dev/sdb1`


## Full Setup Step By Step

`lsblk` => `df -h` => `sudo cfdisk /dev/sdc` => `lsblk` => `sudo pvdisplay` => `sudo pvcreate /dev/sdb1` => `sudo pvdisplay` => `sudo vgdisplay` => `sudo vgextend vg0 /dev/sdb1` => `sudo lvextend -L +2G /dev/vg0/lv-1` => `sudo resize2fs /dev/vg0/lv-1`


**Configure systems to mount file systems at or during boot**

```
sudo vim /etc/fstab
#add this end of the line
/dev/sdb1   /mnt/   ext4   noauto   0   0

#If you want to mount via BLKID
UUID=1a11e12f-ca67-4235-89ca-dce3cb67c964   /mnt/  ext4   defaults   0   0

```

**Configure systems to mount file systems on demand**

Mount NFS Filesystems with autofs, This is NFS Server IP and share directory.\
Make sure that the NFS server (172.17.17.210 in this case) is reachable from your Ubuntu machine, and there are no firewall issues preventing the connection. Also, ensure that the NFS service is running on the server.\
This is my NFS Server share directory.\
*/var/k8-nfs/data 172.17.17.0/24(rw,sync,no_subtree_check,no_root_squash,no_all_squash)*

Install autofs on Ubuntu
```
sudo apt-get update
sudo apt-get install autofs
```
Edit auto.master file, open the auto.master file using your preferred text editor.\
`sudo vi /etc/auto.master`

Go to the end of the file and add this line.\
`/shares /etc/auto.shares --timeout=400`

Create and edit the auto.shares file, open the auto.shares file.\
`sudo vi /etc/auto.shares`

Add the following line to the file.\
`mynetworkshare -fstype=nfs,rw,soft 172.17.17.210:/var/k8-nfs/data`

Reload autofs
```
sudo systemctl reload autofs
sudo service autofs status
```
Verify the configuration, Try listing the contents of the NFS share.\
`ls /shares/mynetworkshare`

You should see the contents of the 172.17.17.210:/var/k8-nfs/data directory.

*/shares*: This is the mount point or directory on your local file system where the remote NFS shares will be automatically mounted by autofs.\
*/var/k8-nfs/data*: This is the directory on the NFS server (172.17.17.210) that you want to mount on your local machine.\
*mynetworkshare*: This is a label or name given to the NFS share. It serves as an identifier that you will use when accessing the mounted NFS share.

Putting it all together:\
The line in auto.shares configures autofs to mount the NFS share from the server (172.17.17.210) with the path /var/k8-nfs/data under the label or name mynetworkshare.\
The line in auto.master tells autofs to use the configuration in auto.shares and mount the shares under the local directory /shares.\
When you access /shares/mynetworkshare on your local machine, autofs will automatically mount the NFS share from the specified server and path (172.17.17.210:/var/k8-nfs/data), making the contents of that remote directory accessible on your local system.\
In summary, /shares is the local mount point, /var/k8-nfs/data is the remote directory on the NFS server, and mynetworkshare is the label or name assigned to this particular NFS share configuration.

