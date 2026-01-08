*This project has been created as part of the 42 curriculum by mvelasqu.*

# Born2beroot

## Description

**Born2beroot** is a system administration project aimed at introducing the fundamentals of setting up and securing a Linux server.  
The objective is to configure a virtual machine from scratch while applying strict security rules, user management, and system hardening practices.

This project focuses on understanding how an operating system works at a low level, how services are managed, how permissions and authentication are enforced, and how to apply basic security policies in a real-world server environment.

## Process of Learning

1. Familiarizaion on set-up of VM
2. Installation of Sudo
3. Configure User and Groups
4. Install and configure of ssh
5. Install and configure ufw
6. Implement Sudo Policies
7. Implement Password Policies
8. Create Script
9. Install and configure Crontab
10. Create signature.txt

## Terminologies & Simple Definitions

> This section contains simple explanations of key terms encountered during the Born2beroot project.  
> Definitions are intentionally kept short and practical, based on hands-on experience during the setup.

1. **Virtual Machine (VM)**  
   A virtual computer that runs inside another computer, behaving like a real machine with its own OS and resources.

2. **Virtualization**  
   The technology that allows multiple virtual machines to run on a single physical computer.

3. **Hypervisor**  
   Software that creates and manages virtual machines by allocating hardware resources to them.

4. **RAM (Random Access Memory)**  
   Temporary memory used by the system to run programs quickly while the computer is powered on.

5. **CPU (Central Processing Unit)**  
   The brain of the computer — it executes instructions and performs calculations.

6. **Motherboard**  
   The main circuit board that connects and allows communication between all hardware components (often thought of as the spine of the system).

7. **Operating System (OS)**  
   The system software that manages hardware and allows users and applications to interact with the computer (similar to a nervous system).

8. **Kernel**  
   The core part of the operating system that directly communicates with the hardware and manages system resources.

9. **Network Card (NIC)**  
   Hardware that allows the computer to connect to a network or the internet.

10. **Hard Disk (Storage)**  
    Permanent storage used to keep the operating system, programs, and files even when the system is powered off.

11. **GRUB (Grand Unified Bootloader)**  
    A bootloader that loads the operating system when the computer starts.

12. **AppArmor**  
    A security module that restricts what programs can access, improving system security.

13. **apt (Advanced Package Tool)**  
    A package management tool used in Debian to install, update, and manage software.

14. **LVM (Logical Volume Manager)**  
    A system that allows flexible management of disk partitions and storage volumes.

15. **SSH (Secure Shell)**  
    A protocol used to securely connect to and manage a remote system via the command line.

16. **UFW (Uncomplicated Firewall)**  
    A simple firewall tool used to control incoming and outgoing network traffic.

17. **cron**  
    A scheduler that runs commands or scripts automatically at specified times.

18. **sudo**  
    A command that allows permitted users to execute commands with administrative (root) privileges.

19. **root**  
    The superuser account with full control over the system.

---

## Personal Note

This project helped me understand that system administration is not just about following commands, but about knowing **why** each component exists and how they work together.  
Focusing on Debian allowed me to build a stable and secure system while learning core Linux concepts step by step, rather than being overwhelmed by unnecessary complexity.

The operating system chosen for this project is **Debian**, prioritizing stability, documentation, and simplicity for learning core Linux administration concepts.

---

## Project Description & Design Choices

### Operating System Choice

I chose **Debian** as the operating system for this project.

**Reasons for choosing Debian:**
- Stable and well-documented
- Widely used in server environments
- Large community support
- Simpler learning curve compared to enterprise-focused distributions

While the subject also mentions **Rocky Linux**, I decided to focus entirely on Debian to ensure a solid and complete implementation rather than a partial or overly complex setup.

---

### Comparison (Conceptual Only)

> ⚠️ **Honest Note**  
> The following comparisons are based on research and documentation.  
> I did not fully implement or test Rocky Linux, SELinux, or firewalld in this project due to their added complexity and time constraints.  
> The practical implementation was focused on **Debian + AppArmor + UFW**.

#### Debian vs Rocky Linux
- **Debian**
  - Community-driven
  - Excellent documentation
  - Ideal for learning and stability
- **Rocky Linux**
  - Enterprise-oriented (RHEL-compatible)
  - Strong for production servers
  - More complex security stack for beginners

#### AppArmor vs SELinux
- **AppArmor**
  - Easier to understand and configure
  - Profile-based path restrictions
  - Enabled by default on Debian
- **SELinux**
  - More powerful and granular
  - Steeper learning curve
  - Common in enterprise systems (RHEL/Rocky)

#### UFW vs firewalld
- **UFW**
  - Simple and readable rule syntax
  - Ideal for small servers and learning
  - Used in this project
- **firewalld**
  - Zone-based and dynamic
  - More flexible but more complex

#### VirtualBox vs UTM
- **VirtualBox**
  - Cross-platform
  - Well-documented
  - Used for this project
- **UTM**
  - macOS-focused (Apple Silicon)
  - Simple UI but less flexible for advanced setups

---

## Instructions

### Requirements
- VirtualBox
- Debian ISO
- Internet connection

### Installation & Setup
1. Create a new VirtualBox virtual machine
2. Install Debian (minimal installation)
3. Configure:
   - Encrypted partitions (if required)
   - Hostname
   - User and password policies
4. Install and configure:
   - `sudo`
   - `ufw`
   - `openssh-server`
   - `cron`
5. Apply security rules:
   - Password expiration and complexity
   - SSH restrictions
   - Firewall rules
6. Configure monitoring script (`monitoring.sh`) to display system information periodically

---

## Features

- Secure user and group management
- Enforced password policies
- SSH access control
- Firewall configuration with UFW
- Automated system monitoring
- Minimal and hardened Linux server environment

---

## Commands

<details>
<summary><h3 style="display: inline;">1. To check system status</h3></summary>

Check System Hostname and related machine properties
```bash
hostnamectl
```
Check OS version
```bash
cat /etc/os-release
```
Check Status of ssh
```bash
sudo systemctl status ssh
```
check Status of Uncomplicated fire wall (UFW)
```bash
sudo systemctl status ufw
```
check Status of Apparmor
```bash
sudo systemctl status apparmor
```
</details>

<h3>2. Hostname, User and group</h3>
<details>
<summary><strong>2.1. Change Hostname</strong></summary>
		
Step 1: Change hostname using hostnamectl
```bash
sudo hostnamectl set-hostname newname
```
Step 2: Proceed to hosts and edit, **change only the <olduser> name with your <newusername>**
got hosts using this command
```bash
sudo nano /etc/hosts/
```
Step 3: at root, reboot
```bash
sudo reboot
```
</details>
<details>
<summary><strong>2.2. Add user name</strong></summary>
		
Step 1: Add user using adduser command, input password. (Optional: add user info)
```bash
sudo adduser <newusername>
```
Step 2: check if user was created using getent
```bash
getent group users
```
</details>

<details>
<summary><strong>2.3. Add group</strong></summary>
		
Step 1: add a group in your list using groupadd
```bash
sudo groupadd <newgroupname>
```
Step 2: check if group was created using getent
```bash
getent group <newgroupname>
```
</details>

<details>
<summary><strong>2.4. Add user to group</strong></summary>

Step 1: add a user in a exisiting group using adduser
```bash
sudo adduser <username> <groupname>
```
Step 2: verify if added in the group using getent
```bash
getent group <groupname>
```
</details>

<details>
<summary><strong>2.5 Change username</strong></summary>

Step 1: make sure you are in root, use usermod command. 
```bash
sudo usermod -l <new_username> -m -d /home/<new_username> <old_username>
```
- -l: sets the new login name
- -d: specifies the new home diretory
- -m: move the contents from the old to new directory

Step 2: Verify the change after logging in as the new user
```bash
id <new_username> or whoami
```
</details>
<details>
<summary><strong>2.6 Change group name</strong></summary>

Step 1: change existing group name, use groupmod command. 
```bash
sudo groupmod -n <new_groupname> <old_groupname>
```
- -groupdmode: command for modifying group name
- -n: specifying the new name of the group

Step 2: Verify the change in group list
```bash
getent group <new_groupname>
```
</details>
<details>
<summary><strong>2.7 Delete Username and Group</strong></summary>

Step 1: delete using userdel -r command. 
```bash
sudo userdel -r <username>
```

Step 2: delete username in groups using groupdel
```bash
sudo groupdel <username>
```
</details>
<details>
<summary><strong>2.7 Delete Username in a Group</strong></summary>

Step 1: delete using userdel -r command. 
```bash
sudo userdel -r <username>  <groupname>
```

Step 2: check using getent
```bash
getent group <groupname>
```
</details>

</br>

<details>
<summary><h3 style="display:inline">3. Singature.txt Commands</h3></summary>

Display cpu information
```bash
cat /proc/cpuinfo/
```

Display Ram information
```bash
free
```

Display the amount of available and used disk space on all currently mounted file systems
```bash
df -h
```
- df: disk free
- -h: human-readable 

Displays block storage devices in a tree structure using lsblk (list block devices) command
```bash
lsblk
```
Display tcp sockets
```bash
ss -ta
```

Display names of all logged-in users
```bash
users
```

Display IP
```bash
hostname -I
```


</details>

---

## Personal Note

This project helped me understand that system administration is not just about following commands, but about knowing **why** each component exists and how they work together.  
Focusing on Debian allowed me to build a stable and secure system while learning core Linux concepts step by step, rather than being overwhelmed by unnecessary complexity.


## Resources

- Debian Documentation: https://www.debian.org/doc/
- Linux man pages (`man sudo`, `man sshd`, `man ufw`, `man pam_pwquality`, `man crontab`)
- 42 Born2beroot Subject PDF
- AppArmor Documentation: https://gitlab.com/apparmor/apparmor/-/wikis/home

### AI Usage Disclosure
AI tools were used for:
- Clarifying Linux concepts
- Understanding configuration options
- Reviewing documentation explanations

All configurations, commands, and implementations were manually executed and verified
