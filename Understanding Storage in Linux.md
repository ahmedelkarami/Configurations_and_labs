# **Understanding Storage in Linux: A Step-by-Step Tutorial**

This tutorial will guide you through the fundamentals of storage management in Linux, covering **file systems**, **disks**, **logical volumes**, **volume groups**, and **NFS (Network File System)**. By the end, you will have a solid understanding of how to manage storage in Linux.

---

## **Table of Contents**
1. **Understanding Disks and Partitions**
2. **File Systems in Linux**
3. **Logical Volume Management (LVM)**
4. **Network File System (NFS)**
5. **Putting It All Together: A Practical Example**

---

## **1. Understanding Disks and Partitions**

### **Step 1: Identify Disks**
- Use the `lsblk` command to list all block devices (disks and partitions):
  ```bash
  lsblk
  ```
  Example output:
  ```
  NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
  sda      8:0    0   100G  0 disk
  ├─sda1   8:1    0    50G  0 part /
  └─sda2   8:2    0    50G  0 part /home
  ```

### **Step 2: Create Partitions**
- Use `fdisk` or `gdisk` to create partitions:
  ```bash
  sudo fdisk /dev/sdb
  ```
  - Press `n` to create a new partition.
  - Specify the size and type of the partition.
  - Press `w` to write changes to the disk.

### **Step 3: Format Partitions**
- Use `mkfs` to create a file system on the partition:
  ```bash
  sudo mkfs.ext4 /dev/sdb1
  ```

### **Step 4: Mount the Partition**
- Create a mount point and mount the partition:
  ```bash
  sudo mkdir /mnt/data
  sudo mount /dev/sdb1 /mnt/data
  ```
- Verify the mount:
  ```bash
  df -h
  ```

---

## **2. File Systems in Linux**

### **Step 1: Common File Systems**
- **ext4**: Default for most Linux systems.
- **XFS**: High-performance file system for large files.
- **Btrfs**: Modern file system with snapshots and compression.
- **ZFS**: Enterprise-grade file system with built-in RAID.

### **Step 2: Create and Mount a File System**
- Format a partition with a specific file system:
  ```bash
  sudo mkfs.xfs /dev/sdb2
  ```
- Mount the file system:
  ```bash
  sudo mount /dev/sdb2 /mnt/xfs
  ```

### **Step 3: Check File System Health**
- Use `fsck` to check and repair file systems:
  ```bash
  sudo fsck /dev/sdb1
  ```

---

## **3. Logical Volume Management (LVM)**

### **Step 1: Install LVM Tools**
- Install LVM utilities:
  ```bash
  sudo apt install lvm2  # On Debian/Ubuntu
  sudo yum install lvm2  # On CentOS/RHEL
  ```

### **Step 2: Create Physical Volumes**
- Initialize disks or partitions as physical volumes:
  ```bash
  sudo pvcreate /dev/sdb1 /dev/sdc1
  ```

### **Step 3: Create a Volume Group**
- Combine physical volumes into a volume group:
  ```bash
  sudo vgcreate my_volume_group /dev/sdb1 /dev/sdc1
  ```

### **Step 4: Create Logical Volumes**
- Create a logical volume from the volume group:
  ```bash
  sudo lvcreate -L 20G -n my_logical_volume my_volume_group
  ```

### **Step 5: Format and Mount the Logical Volume**
- Format the logical volume:
  ```bash
  sudo mkfs.ext4 /dev/my_volume_group/my_logical_volume
  ```
- Mount the logical volume:
  ```bash
  sudo mount /dev/my_volume_group/my_logical_volume /mnt/lvm
  ```

---

## **4. Network File System (NFS)**

### **Step 1: Install NFS Server**
- Install NFS server tools:
  ```bash
  sudo apt install nfs-kernel-server  # On Debian/Ubuntu
  sudo yum install nfs-utils          # On CentOS/RHEL
  ```

### **Step 2: Configure NFS Exports**
- Edit the `/etc/exports` file to share a directory:
  ```bash
  /mnt/lvm 192.168.1.0/24(rw,sync,no_subtree_check)
  ```
- Export the shared directory:
  ```bash
  sudo exportfs -a
  ```

### **Step 3: Start NFS Service**
- Start and enable the NFS service:
  ```bash
  sudo systemctl start nfs-server
  sudo systemctl enable nfs-server
  ```

### **Step 4: Mount NFS Share on Client**
- Install NFS client tools:
  ```bash
  sudo apt install nfs-common  # On Debian/Ubuntu
  sudo yum install nfs-utils   # On CentOS/RHEL
  ```
- Mount the NFS share:
  ```bash
  sudo mount 192.168.1.100:/mnt/lvm /mnt/nfs
  ```

---

## **5. Putting It All Together: A Practical Example**

### **Scenario**
- You have two disks (`/dev/sdb` and `/dev/sdc`).
- You want to:
  1. Create a volume group.
  2. Create a logical volume.
  3. Format it with XFS.
  4. Share it over NFS.

### **Steps**
1. Create physical volumes:
   ```bash
   sudo pvcreate /dev/sdb /dev/sdc
   ```
2. Create a volume group:
   ```bash
   sudo vgcreate my_vg /dev/sdb /dev/sdc
   ```
3. Create a logical volume:
   ```bash
   sudo lvcreate -L 50G -n my_lv my_vg
   ```
4. Format the logical volume with XFS:
   ```bash
   sudo mkfs.xfs /dev/my_vg/my_lv
   ```
5. Mount the logical volume:
   ```bash
   sudo mount /dev/my_vg/my_lv /mnt/shared
   ```
6. Share the directory over NFS:
   - Edit `/etc/exports`:
     ```bash
     /mnt/shared 192.168.1.0/24(rw,sync,no_subtree_check)
     ```
   - Start the NFS service:
     ```bash
     sudo systemctl start nfs-server
     ```

---

## **Conclusion**
You now have a solid understanding of storage management in Linux, including:
- Disk partitioning and file systems.
- Logical Volume Management (LVM).
- Network File System (NFS).

Practice these steps on a virtual machine or a test system to reinforce your knowledge. Let me know if you have any questions! 😊
