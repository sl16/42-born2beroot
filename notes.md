The following are personal notes of 42Prague student vbartos regarding the project Born2BeRoot.

# Useful cmds

`sudo` (superuser do): Allows authorized users to run specific commands as the superuser (root) or another user with elevated privileges.

`su`: Switch to another user account, typically the root user.

`lsblk`: Displays a hierarchical view of all block devices connected to the system, including hard drives, solid-state drives (SSDs), USB drives, and partitions.

`apt-get`: A package management command used to install, update, or remove software packages on Debian-based distributions.

`hostname`: Displays or sets the hostname of the system. 

`systemctl`: A command for managing system services using systemd, the init system used in many modern Linux distributions. It allows you to start, stop, restart, enable, or disable services.

`chown`: Managesmanage user password expiration and aging settings user password expiration and aging settings.

`chown`: Changes the ownership of files or directories. 

`chmod`: Changes the permissions of files or directories.

`whoami`: Displays the username associated with the current user executing the command.

`groupadd groupname`: Creates a group named groupname.

`getent`: Retrieves entries from databases. `getent group` to list existing groups.

`adduser name group`: Adds user name to group group.

`usermod`: Make changes to various attributes of an existing user account. `sudo usermod -aG group1,group2 username` to assign user to groups. 

`crontab -e`: Opens the crontab file in an editor to add or modify entries.

`hostnamectl set-hostname <new_hostname>`: Changes the hostname.

`uname`: Provides information about the system and the kernel.

# Virtual machine basics
Virtual machine is a software emulation of a physical computer system. It allows users to run multiple operating systems and applications on a single physical machine simultaneously.

The virtualization software (aka hypervisor) creates a virtual layer that sits between the physical hardware and the operating systems or applications running on it.

The hypervisor allocates the physical resources of the host machine, such as CPU, memory, storage, and network, to the virtual machines.

Each virtual machine operates as an independent and isolated environment, capable of running its own operating system and applications.

The guest operating systems and applications running within the virtual machines interact with the virtual hardware provided by the hypervisor, which abstracts the underlying physical hardware.

## Disc partitioning
Physical storage (HDD, SSD) can be divided into multiple logical sections called partitions. Each partition is treated as a separate entity and can be formatted with a file system to store data independently.

**Primary Partition** is a basic partition that can be used to install an operating system or store data. A disk can have up to four primary partitions.

**Extended Partition** is a special type of primary partition that can be further divided into logical partitions. It allows you to overcome the limitation of having only four primary partitions on a disk.

**Logical Partitions** reside within an extended partition and are used to create additional storage sections beyond the four primary partitions.

## Logical Volume Manager
Logical Volume Manager (LVM) is a software-based approach to managing disk storage in Linux-based operating systems. It provides a flexible and dynamic way to manage storage by allowing the creation, resizing, and migration of logical volumes (LVs) that span across multiple physical storage devices.

**Physical Volumes** are the underlying physical storage devices, such as hard disk drives (HDDs) or solid-state drives (SSDs).

**Volume Group** is a virtual container that combines multiple Physical Volumes. You can add or remove PVs from a VG to increase or decrease its capacity. VGs provide a centralized pool of storage that can be divided into smaller logical volumes.

**Logical Volumes** are the logical partitions created within a Volume Group. LVs can be dynamically resized, moved, or extended across multiple PVs. LVs are treated as independent block devices and can be formatted with file systems and mounted like regular partitions.

### File system (Ext4)
A file system is a method or structure used by an operating system to organize, store, and retrieve files on a storage device. It defines how data is stored, accessed, and managed on the storage medium. File systems provide a way to organize files into directories or folders, and they maintain metadata associated with each file, such as permissions, timestamps, and file attributes.

**ext4** is the default file system used in many Linux distributions. It is an enhanced version of its predecessor, ext3, and provides improved performance, scalability, and support for larger file sizes and partitions.

### Swap area
The swap area, also known as swap space or swap partition, is a dedicated portion of a computer's hard disk drive (HDD) or solid-state drive (SSD) that serves as virtual memory extension. It acts as an overflow area when the system's physical memory (RAM) becomes fully utilized.

### GRUB Boot Loader
GRUB (GRand Unified Bootloader) is a widely used boot loader in many Linux-based operating systems. It is responsible for loading the operating system kernel into memory and initializing the system during the boot process. GRUB provides a user-friendly interface that allows users to select the operating system they want to boot into when multiple operating systems are installed on a computer.

## Virtual machine snapshots
Virtual machine snapshots are a feature provided by virtualization platforms that allow you to capture the current state of a virtual machine at a specific point in time. Essentially, a snapshot is a saved copy of the virtual machine's disk and memory state.

# Server config basics

## Apt vs Aptitude
APT and Aptitude are both package management tools for Debian-based systems. APT provides a straightforward command-line interface, while Aptitude offers a more advanced text-based interactive interface with additional features.

The package database, also known as the package repository or package index, is a collection of metadata and information about available software packages for a specific Linux distribution. It is maintained by the distribution's package management system and contains details about package names, versions, dependencies, and other package-related information.

## AppArmor
A Linux kernel security module that provides an additional layer of security by enforcing access control policies on individual programs or processes. It acts as a Mandatory Access Control (MAC) system and limits the capabilities and permissions of applications to prevent them from accessing unauthorized resources or performing unintended actions.

AppArmor works by defining security profiles, known as "profiles," for specific applications. These profiles specify the resources that an application is allowed to access, such as files, directories, network sockets, and system capabilities. The profiles also define the actions that an application can perform, helping to mitigate potential security vulnerabilities.

## User & root
The root user, also known as the superuser or administrator, is a special user account with the highest level of privileges and permissions on a Unix-like system, including Linux. The root account has unrestricted access to all system files, directories, and commands. It can perform administrative tasks, install software, modify system configurations, and manage other user accounts. The root user has the power to make critical changes to the system, so it should be used with caution to prevent accidental damage or security risks.

### Sudoers
The `sudoers` file is a configuration file that determines which users or groups are allowed to run specific commands with superuser (root) privileges using the sudo command. The sudoers file controls access to the sudo command, which allows regular users to perform administrative tasks temporarily by providing their own password.

It is also possible to create a custom config file (inside sudoers.d).

### TTY
A TTY provides an interface for users to interact with the system through text-based input and output. It allows users to execute commands, run programs, and view the system's response in a text format. TTYs are typically accessed through a console, terminal emulator, or remote shell session.

In context of SSH setup, TTY mode only gives connection to the terminal that a user has SSH'd in from.

## Remote connection
### SSH
SSH (Secure Shell) is a network protocol that allows secure remote access and communication between two computers. It provides a secure channel over an unsecured network, such as the internet, allowing users to log in to remote systems and execute commands remotely.

### UFW
UFW stands for Uncomplicated Firewall. It is a user-friendly command-line utility used for managing firewall rules on Linux systems, particularly in Ubuntu and Debian-based distributions. UFW provides a simplified interface for configuring and managing the underlying iptables firewall, which is a powerful tool for filtering network traffic.

### Ports
In computer networking, a port is a logical construct used to identify specific processes or services running on a computer. It allows multiple applications to share a single network interface and IP address. Ports are [numbered and categorized into different types](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers):

**Well-known Ports**: Ports numbered from 0 to 1023 are known as well-known ports and are assigned to specific services or protocols. For example, port 80 is typically used for HTTP (web) traffic, port 22 is used for SSH, and port 443 is used for HTTPS (secure web) traffic.

**Registered Ports**: Ports numbered from 1024 to 49151 are registered ports. They are typically used by applications or services that are not officially assigned to a well-known port but have registered with the Internet Assigned Numbers Authority (IANA).

**Dynamic or Private Ports**: Ports numbered from 49152 to 65535 are dynamic or private ports. These ports can be used by applications dynamically as needed and are not officially assigned to any specific service.

--

UFW allows you to configure firewall rules to control network traffic to and from your system. It uses port-based rules to define which incoming or outgoing connections are allowed or denied. For example, you can create UFW rules to allow SSH traffic on port 22 or deny incoming HTTP traffic on port 80.

SSH (Secure Shell) uses port 22 by default for secure remote access to a server. When you connect to a remote server using SSH, the SSH client on your local machine sends data to the SSH server on the remote machine via port 22. The SSH server then authenticates the connection and provides you with a secure shell session to execute commands or transfer files.

### NAT
NAT stands for Network Address Translation. It is a technique used in computer networking to allow multiple devices on a local network to share a single public IP address when accessing the internet.

When a device within a local network sends a request to access a resource on the internet, the NAT device (typically a router or firewall) modifies the source IP address and port number of the request packet to the public IP address and a unique port number. This process is called "masquerading" or "IP masquerading."

# VM Signature
In the context of virtualization, a VM signature refers to a unique identifier or fingerprint associated with a virtual machine (VM). It is used to distinguish one VM from another and is typically generated during the creation or provisioning of the virtual machine.

The sha1sum command is used to calculate and display the SHA-1 hash value of a file. The SHA-1 (Secure Hash Algorithm 1) is a cryptographic hash function that generates a unique 160-bit hash value for a given input.

A hash is a fixed-size numerical value that is generated from an input data of arbitrary size. The process of generating a hash is performed by a hash function, which takes the input data and applies a mathematical algorithm to produce the fixed-size hash value.

## Common Gateway Interface (CGI)
The Common Gateway Interface (CGI) is a standard protocol that defines how web servers communicate with external programs or scripts. It enables the execution of scripts or programs on a web server in response to specific HTTP requests, such as form submissions or URL queries.

# Evaluation notes
- show partitioning `lsblk`
- show SSH status `systemctl status ssh`
- show UFW status `ufw status`
- change hostname with `hostnamectl set-hostname <newname>`. `hostnamectl status` to check.
- create new user `useradd`
- create new group `groupadd`
- add user to group `usermod -aG groupname username`
- check group uders `getent group`
- show password policies `chage -l username`
- show sudo rules `sudo -l`

