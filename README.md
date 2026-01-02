# RHCSA (EX200) — Printable Exam Workbook
**RHEL 9 | Exam Practice + On-the-Job Reference**

---

## HOW TO USE THIS WORKBOOK
- Practice until tasks **survive reboot**
- Validate after every change
- Assume **no partial credit**
- Written to match **Red Hat grading behavior**

---

# DAY-OF-EXAM CRAM (MEMORIZE)

## Mental Model
Login → Verify → Configure → Persist → Validate  
If it doesn’t persist after reboot, it doesn’t exist.

---

## Essential Commands (Muscle Memory)

hostnamectl  
ip a  
nmcli  
lsblk  
df -h  
mount  
systemctl  
firewall-cmd  
getenforce  
setenforce  
podman  

---

## IDENTITY & ACCESS

### Users and Groups
useradd user1  
groupadd dev  
usermod -aG dev user1  
passwd user1  

### Sudo
visudo  

---

## PERMISSIONS & OWNERSHIP

chmod 640 file  
chown user:group file  

Special bits:
- 4 → SUID
- 2 → SGID
- 1 → Sticky

---

## STORAGE (LVM — EXAM FAVORITE)

pvcreate /dev/sdb  
vgcreate vgdata /dev/sdb  
lvcreate -n lvdata -L 5G vgdata  
mkfs.xfs /dev/vgdata/lvdata  

Persist mount:
echo "/dev/vgdata/lvdata /data xfs defaults 0 0" >> /etc/fstab  
mount -a  

---

## NETWORKING

nmcli con show  
nmcli con mod eth0 ipv4.method manual ipv4.addresses 192.168.1.10/24  
nmcli con up eth0  
ip a  

---

## SERVICES & BOOT

systemctl enable --now httpd  
systemctl status httpd  

---

## FIREWALL

firewall-cmd --add-service=http --permanent  
firewall-cmd --reload  

---

## SELINUX (DO NOT PANIC)

getenforce  
setenforce 0   # temporary only  

Persistent:
vi /etc/selinux/config  

Fix contexts:
ls -Z  
restorecon -Rv /var/www/html  

---

## CONTAINERS (EX200 — PODMAN ONLY)

### Run Container
podman pull registry.redhat.io/ubi9/ubi  
podman run -d --name web -p 8080:80 nginx  

### Persistent Container (EXAM FAVORITE)
podman generate systemd --name web --files --new  
mv container-web.service /etc/systemd/system/  
systemctl daemon-reload  
systemctl enable --now container-web  

---

# PRACTICE LABS (EXAM STYLE)

## LAB 1 — USERS & GROUPS
Objective: Create user, assign groups, configure sudo  
Skills: useradd, groupadd, visudo  

---

## LAB 2 — STORAGE (LVM)
Objective: Create LVM and mount persistently  
Skills: pvcreate, vgcreate, lvcreate, /etc/fstab  

---

## LAB 3 — NETWORKING
Objective: Configure static IP and hostname  
Skills: nmcli, hostnamectl  

---

## LAB 4 — SERVICES & FIREWALL
Objective: Install service, enable at boot, open firewall  
Skills: dnf, systemctl, firewall-cmd  

---

## LAB 5 — SELINUX
Objective: Diagnose access issue and fix context  
Skills: restorecon, SELinux modes  

---

## LAB 6 — ARCHIVING

tar -czvf backup.tar.gz /data  
tar -xzvf backup.tar.gz -C /restore  

---

## LAB 7 — BASH SCRIPTING (REQUIRED)

### Task
Create a script that:
- Accepts a username
- Creates user if missing
- Logs result to /var/log/user_create.log

### Script Skeleton
#!/bin/bash

if [ $# -ne 1 ]; then
  echo "Usage: $0 <user>"
  exit 1
fi

id "$1" &>/dev/null || useradd "$1"
echo "$(date): $1 ensured" >> /var/log/user_create.log

# ADDITIONAL BASH SCRIPT EXAMPLES (RHCSA / EX200)

These examples demonstrate the **exact level of scripting expected** on the RHCSA exam:
- No advanced Bash features
- Clear logic
- Idempotent behavior
- Safe to run multiple times

---

## 1. FOR LOOP — Bulk User Creation

### Scenario
Create multiple users from a predefined list.

### Script
```bash
#!/bin/bash

USERS="dev1 dev2 dev3"

for user in $USERS; do
  if id "$user" &>/dev/null; then
    echo "User $user already exists"
  else
    useradd "$user"
    echo "Created user $user"
  fi
done

---

## LAB 8 — CONTAINERS (PODMAN)
Objective:
- Run container
- Expose port
- Persist across reboot

---

# COMMON FAILURE PATTERNS (READ TWICE)

- Forgot /etc/fstab
- Service not enabled
- Firewall rule not permanent
- Disabled SELinux instead of fixing it
- Script not executable
- Container not persistent

---

# AUTO-GRADING CHECKLIST

Every task must:
- Survive reboot
- Produce no errors
- Have correct ownership
- Keep SELinux enforcing
- Use permanent firewall rules
- Enable service/container at boot

---

# ON-THE-JOB QUICK REFERENCE

Disk usage: df -h  
Logs: journalctl -u service  
Ports: ss -tulnp  
Processes: ps aux  
SELinux contexts: ls -Z  

---

## FINAL EXAM ADVICE
Red Hat grades outcomes, not intent.  
Make it work. Make it persistent. Validate everything.
