*This project has been created as part of the 42 curriculum by <login1>.*

# Born2beroot

## Description

**Born2beroot** is a system administration project aimed at introducing the fundamentals of setting up and securing a Linux server.  
The objective is to configure a virtual machine from scratch while applying strict security rules, user management, and system hardening practices.

This project focuses on understanding how an operating system works at a low level, how services are managed, how permissions and authentication are enforced, and how to apply basic security policies in a real-world server environment.

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

## Resources

- Debian Documentation: https://www.debian.org/doc/
- Linux man pages (`man sudo`, `man sshd`, `man ufw`)
- 42 Born2beroot Subject PDF
- AppArmor Documentation: https://gitlab.com/apparmor/apparmor/-/wikis/home

### AI Usage Disclosure
AI tools were used for:
- Clarifying Linux concepts
- Understanding configuration options
- Reviewing documentation explanations

All configurations, commands, and implementations were manually executed and verified
