### **1. System Information & Basics**
- **Uptime**: Shows how long the system has been running.
- **Free memory**: Use `free -h` to display available memory.
- **Filesystem Hierarchy**:
  - Linux has a single unified filesystem tree, regardless of storage devices.
  - No inherent concept of file extensions (metadata defines file type).
- **File Details**:
  - `file [filename]`: Displays file type/details.
  - `ls -s`: Sorts files by size.
  - `less`: Scroll through text files interactively.

---

### **2. Linux Filesystem Hierarchy**
| **Directory**       | **Purpose**                                                                 |
|----------------------|----------------------------------------------------------------------------|
| `/bin` → `/usr/bin`  | User binaries (deprecated, now symlinked to `/usr/bin`).                   |
| `/boot`              | Kernel, initramfs, bootloader files.                                       |
| `/dev`               | Device nodes (e.g., `/dev/sda`).                                           |
| `/etc`               | System-wide config files (e.g., `/etc/passwd`, `/etc/fstab`).              |
| `/lib`               | Shared libraries for core system binaries.                                 |
| `/lost+found`        | Recovered files after filesystem corruption.                               |
| `/media`             | Mount points for removable media (USB, CD).                                |
| `/mnt`               | Manual mount points for temporary devices.                                 |
| `/opt`               | Optional/third-party software.                                             |
| `/proc`              | Virtual filesystem for kernel/process info (e.g., `/proc/cpuinfo`).        |
| `/run`               | Ephemeral runtime data (cleared on reboot).                                |
| `/sbin`              | System admin binaries.                                                     |
| `/sys`               | Kernel-detected device info.                                               |
| `/tmp`               | Temporary files (cleared periodically). Use `mktemp -d` for secure temp dirs. |
| `/usr`               | User programs and support files.                                           |
| `/var`               | Variable data (logs, databases).                                           |
| `/libexec`           | Helper executables for other programs.                                     |

- **`.d` Directories** (e.g., `/etc/cron.d`): Modular config/script directories.
- **`/etc/init.d`**: SysV init scripts (legacy, replaced by `systemd`).

---

### **3. Files & Permissions**
- **File Structure**:
  - Data (content) + Name (metadata).
- **Links**:
  - **Hardlinks**: Reference files only (no directories).
  - **Symlinks**: Can reference directories. Use relative paths for portability.
- **Permissions**:
  - `rwx` for user (u), group (g), others (o).
  - `chmod [ugoa][+-=][rwx]` or octal notation (e.g., `755`).
  - **Special Bits**:
    - `setuid` (4000): Run as owner.
    - `setgid` (2000): Inherit directory’s group.
  - `umask`: Sets default permissions (e.g., `022`).
- **Ownership**:
  - `chown user:group [file]` (requires `sudo`).

---

### **4. Process Management**
- **Commands**:
  - `ps aux`: Snapshot of processes.
  - `top`/`htop`: Real-time process monitor.
  - `kill [PID]`/`killall [name]`: Terminate processes.
  - `nice`/`renice`: Adjust process priority.
- **Signals**:
  - `SIGKILL` (9), `SIGTERM` (15), `SIGSEGV` (11).
- **Background Jobs**:
  - `&`: Run in background.
  - `jobs`/`fg`/`bg`: Manage background jobs.
- **Systemd vs. Init**:
  - `systemd` uses unit files (faster, parallel startup).
  - `init` uses sequential scripts (`/etc/init.d`).

---

### **5. Redirection & Pipes**
- **Standard Streams**:
  - `0` (stdin), `1` (stdout), `2` (stderr).
- **Redirection**:
  - `>` (overwrite), `>>` (append), `2>` (stderr), `&>` (stdout + stderr).
  - `/dev/null`: Discard output.
- **Pipes**:
  - `|`: Send stdout to another command’s stdin (e.g., `ls | sort | uniq`).
  - `tee`: Split output to file and stdout (e.g., `ls | tee files.txt`).

---

### **6. Networking**
- **Commands**:
  - `ping`: Check host reachability.
  - `traceroute`: Trace network path.
  - `ssh`: Secure remote login.
  - `scp`: Secure file copy.
  - `netstat`/`ss`: Network stats.
- **Protocols**:
  - Avoid `ftp` (unencrypted); use `sftp`/`scp`.

---

### **8. System Administration**
- **Storage**:
  - `mount`/`umount`: Manage filesystems.
  - `/etc/fstab`: Auto-mount at boot.
  - `dd`: Low-level data copy (e.g., `dd if=/dev/sda of=backup.img`).
- **Logs**:
  - `/var/log`: System logs.
  - `tail -f`: Monitor logs in real-time.
- **Cron**:
  - User crontabs: `/var/spool/cron`.
  - System cron: `/etc/crontab`, `/etc/cron.d`.

---

### **9. Troubleshooting**
- **Processes**:
  - `strace`: Trace system calls.
  - `vmstat`/`iostat`: Resource monitoring.
- **Disk**:
  - `df -h`: Filesystem usage.
  - `du -h`: Directory space usage.
- **Libraries**:
  - `LD_LIBRARY_PATH`: For shared libraries (not `PATH`).

---

### **10. Quick Reference**
- **grep**:
  ```bash
  grep -i "pattern" file.txt  # Case-insensitive
  grep -r "pattern" /dir      # Recursive
  grep -v "exclude" file.txt  # Invert match
  ```
- **Permissions**:
  - `r` (read), `w` (write), `x` (execute).
  - `chmod 755 script.sh`: `rwxr-xr-x`.

---


### **11. File Operations & Text Processing**
#### **Searching & Filtering**
- **`grep`**:
  ```bash
  grep "error" /var/log/syslog    # Basic search
  grep -i "warning" file.txt      # Case-insensitive
  grep -r "pattern" /dir         # Recursive search
  grep -v "exclude" file.txt     # Invert match
  grep -l "text" *.txt           # List matching files
  grep -w "word" file.txt        # Whole-word match
  grep -A 3 -B 2 "context" file  # Show surrounding lines
  ```
- **`find`**:
  ```bash
  find /path -name "*.log"       # Search by name
  find /var -size +10M           # Files >10MB
  find /home -user alice         # Files owned by user
  ```

#### **Text Manipulation**
- **`head`/`tail`**:
  ```bash
  head -n 5 file.txt             # First 5 lines
  tail -n 5 file.txt             # Last 5 lines
  tail -f /var/log/syslog        # Real-time monitoring
  ```
- **`sort`/`uniq`**:
  ```bash
  sort file.txt | uniq           # Sort and deduplicate
  sort -r file.txt               # Reverse sort
  uniq -d file.txt               # Show duplicates
  ```
- **`awk`/`sed`**:
  ```bash
  awk '{print $1}' file.txt      # Print first column
  sed 's/old/new/g' file.txt     # Replace text
  ```

---

### **12. System Monitoring & Performance**
#### **Resource Usage**
- **CPU/Memory**:
  ```bash
  top                            # Interactive process viewer
  htop                           # Enhanced top (install with `sudo apt install htop`)
  vmstat 5                       # System stats every 5 seconds
  free -h                        # Memory usage (human-readable)
  ```
- **Disk I/O**:
  ```bash
  iostat                         # Disk I/O statistics
  df -h                          # Filesystem disk usage
  du -sh /path                   # Directory size summary
  ```

#### **Process Analysis**
- **Process Hierarchy**:
  ```bash
  pstree                         # Tree view of processes
  ps auxf                        # Process list with hierarchy
  ```
- **Strace** (Debugging):
  ```bash
  strace -f -e trace=file ls     # Trace file operations
  strace -p <PID>                # Attach to running process
  ```

---

### **13. User & Group Management**
#### **User Accounts**
- **Files**:
  - `/etc/passwd`: User accounts.
  - `/etc/shadow`: Encrypted passwords.
  - `/etc/group`: Group definitions.
- **Commands**:
  ```bash
  sudo useradd alice             # Create user
  sudo passwd alice              # Set password
  sudo usermod -aG sudo alice    # Add to sudo group
  sudo userdel alice             # Delete user
  ```

#### **Permissions**
- **Special Modes**:
  ```bash
  chmod u+s /path/to/bin         # setuid (run as owner)
  chmod g+s /dir                 # setgid (inherit group)
  chmod +t /tmp                  # Sticky bit (restrict deletion)
  ```
- **ACLs** (Advanced Permissions):
  ```bash
  setfacl -m u:alice:rwx file.txt  # Grant user-specific access
  getfacl file.txt               # View ACLs
  ```

---

### **14. Networking & Remote Access**
#### **Diagnostics**
- **Connectivity**:
  ```bash
  ping google.com                # Check reachability
  traceroute google.com          # Trace network path
  mtr google.com                 # Continuous traceroute
  ```
- **Ports & Connections**:
  ```bash
  netstat -tuln                  # List listening ports
  ss -tuln                       # Modern alternative
  lsof -i :80                    # Processes using port 80
  ```

#### **Secure Remote Access**
- **SSH**:
  ```bash
  ssh user@remote-host           # Basic login
  scp file.txt user@remote:/path # Secure copy
  ssh-keygen -t ed25519          # Generate key pair
  ```
- **Firewall** (UFW):
  ```bash
  sudo ufw allow 22              # Allow SSH
  sudo ufw enable                # Enable firewall
  ```

---

### **15. Package Management (Debian/Ubuntu)**
#### **APT Commands**
```bash
sudo apt update                 # Update package list
sudo apt upgrade                # Upgrade installed packages
sudo apt install package        # Install package
sudo apt remove package         # Remove package
sudo apt autoremove             # Remove unused dependencies
```

#### **Debian Packages**
```bash
dpkg -i package.deb            # Install .deb file
dpkg -l                        # List installed packages
```

---

### **16. Shell Scripting Essentials**
- **Variables**:
  - `PATH`: Directories for executable search.
  - `export`: Make variables available to child processes.
- **Expansion**:
  - `$(command)`: Command substitution.
  - Quotes: Single (`'`) suppresses expansion.

#### **Variables & Expansion**
```bash
name="Alice"                   # Assign variable
echo "Hello, $name"            # Variable expansion
echo "Today is $(date)"        # Command substitution
```

#### **Conditionals**
```bash
if [ -f "file.txt" ]; then
  echo "File exists"
elif [ -d "dir" ]; then
  echo "Directory exists"
else
  echo "Nothing found"
fi
```

#### **Loops**
```bash
for i in {1..5}; do            # Range loop
  echo "Iteration $i"
done

while [ $count -lt 10 ]; do    # While loop
  echo $count
  ((count++))
done
```

---

### **17. Kernel & Hardware**
#### **Kernel Modules**
```bash
lsmod                          # List loaded modules
modinfo module_name            # Module details
sudo modprobe module_name      # Load module
```

#### **Hardware Info**
```bash
lscpu                          # CPU details
lsblk                          # Block devices (disks)
lspci                          # PCI devices
lsusb                          # USB devices
```

---

### **18. Security Best Practices**
#### **Auditing**
```bash
sudo last                      # Login history
sudo fail2ban-client status    # Brute-force protection
sudo chkrootkit               # Rootkit scanner
```

#### **Sudoers File**
- Edit with `visudo` to configure sudo access:
  ```bash
  alice ALL=(ALL) NOPASSWD:ALL  # Allow passwordless sudo
  %developers ALL=(ALL) ALL     # Group-based access
  ```

---

### **19. Common Pitfalls & Fixes**
#### **Library Errors**
```bash
# Error: "libxyz.so not found"
sudo ldconfig                  # Update library cache
export LD_LIBRARY_PATH=/path/to/libs  # Temporary fix
```

#### **Permission Denied**
```bash
chmod +x script.sh             # Make executable
chown user:group file          # Fix ownership
```

#### **Disk Full**
```bash
du -h --max-depth=1 /          # Find large directories
journalctl --vacuum-size=100M  # Clean system logs
```

---

### **20. Quick Command Reference**
| **Task**               | **Command**                     |
|-------------------------|---------------------------------|
| Search files           | `find / -name "*.log"`         |
| Check ports            | `netstat -tuln \| grep 80`     |
| Kill process           | `kill -9 <PID>`                |
| Archive files          | `tar -czvf archive.tar.gz /dir`|
| Check disk health      | `smartctl -a /dev/sda`         |
| Schedule task          | `crontab -e`                   |

---


#### **1. Process Execution Priorities**
- **Niceness Values**:
  ```bash
  nice -n 19 command      # Start with lowest priority (19)
  renice 5 -p 1234       # Change priority of running process
  ```
- **Real-time Priorities**:
  ```bash
  chrt -f 99 command     # Set FIFO real-time priority (1-99)
  ```

#### **2. Filesystem Links (Hard vs. Symlinks)**
- **Key Differences**:
  | Feature          | Hardlink | Symlink |
  |------------------|----------|---------|
  | Inode reference  | Same     | Different |
  | Cross-filesystem | No       | Yes     |
  | Directory links  | No       | Yes     |
  | Original deleted | Survives | Broken  |

#### **3. Advanced Signal Handling**
- **Custom Signal Handlers**:
  ```bash
  trap "echo 'Signal caught!'" SIGINT SIGTERM
  ```
- **Signal Numbers**:
  ```bash
  kill -l          # List all signals
  kill -SIGKILL %1 # Kill job 1 with SIGKILL (9)
  ```

#### **4. Filesystem Check (fsck) Details**
- **Boot-time Behavior**:
  - Last digit in `/etc/fstab` determines fsck order:
    - `0`: Never check
    - `1`: Check first (root FS)
    - `2+`: Check sequentially

#### **5. setuid/setgid Deep Dive**
- **Security Implications**:
  ```bash
  chmod u+s /usr/bin/passwd   # Example: passwd needs setuid
  find / -perm -4000 -ls      # Find all setuid binaries
  ```

#### **6. /proc Filesystem Details**
- **Critical Files**:
  ```bash
  cat /proc/cpuinfo       # CPU details
  cat /proc/meminfo       # Memory stats
  echo 1 > /proc/sys/net/ipv4/ip_forward  # Temporary enable IP forwarding
  ```

#### **7. Environment Variables Management**
- **Persistence**:
  ```bash
  # System-wide (all users):
  /etc/environment
  /etc/profile.d/*.sh

  # User-specific:
  ~/.bashrc        # Interactive shells
  ~/.bash_profile  # Login shells
  ```

#### **8. Advanced grep Patterns**
- **Regex Examples**:
  ```bash
  grep -E '^[A-Z]{3}' file    # Lines starting with 3 uppercase letters
  grep -P '\d{3}-\d{4}' file  # Perl regex for phone numbers
  ```

#### **9. Shell Expansion Tricks**
- **Brace Expansion**:
  ```bash
  touch file{1..10}.txt      # Creates file1.txt to file10.txt
  cp /path/{old,new}_name    # Quick rename during copy
  ```

#### **10. Filesystem Events with inotify**
- **Real-time Monitoring**:
  ```bash
  inotifywait -m -r /path    # Monitor directory recursively
  ```

---

### **Previously Covered But Worth Highlighting**
1. **`dd` Command Safety**:
   ```bash
   dd if=/dev/zero of=/dev/sdX bs=4M status=progress  # WIPE DISK (DANGEROUS)
   ```
   - Always double-check `if=` (input) and `of=` (output) targets!

2. **SSH Security**:
   ```bash
   ssh-keygen -t ed25519 -a 100              # Strong key generation
   ssh-copy-id -i ~/.ssh/id_ed25519 user@host # Copy key securely
   ```

3. **`strace` Advanced Usage**:
   ```bash
   strace -e trace=open,read ls       # Only trace file operations
   strace -p PID -o debug.log         # Log output to file
   ```

---

### **Visual Cheat Sheet: Permission Octal Codes**
| Octal | Permission | Binary |
|-------|------------|--------|
| 0     | `---`      | 000    |
| 1     | `--x`      | 001    |
| 2     | `-w-`      | 010    |
| 3     | `-wx`      | 011    |
| 4     | `r--`      | 100    |
| 5     | `r-x`      | 101    |
| 6     | `rw-`      | 110    |
| 7     | `rwx`      | 111    |

---
