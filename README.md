# RHCSA (EX200) — Printable Exam Workbook (RHEL 10)
**RHEL 10 | Exam Practice + On-the-Job Reference**

> This workbook reflects **RHEL 10 defaults and behavior** while remaining aligned
> with Red Hat’s RHCSA (EX200) skills expectations.

---

## HOW TO USE THIS WORKBOOK
- Practice tasks until they **survive reboot**
- Validate every change
- Assume **no partial credit**
- Favor **supported tools and defaults**

---

# DAY-OF-EXAM CRAM

## Mental Model
Login → Verify → Configure → Persist → Validate  
If it doesn’t persist after reboot, it doesn’t exist.

---

## Essential Commands (Memorize)

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

# IDENTITY & ACCESS (RHEL 10)

## Users and Groups
useradd user1  
groupadd dev  
usermod -aG dev user1  
passwd user1  

## Sudo Configuration
visudo  

> RHEL 10 still prefers **sudo via wheel group**.

---

# PERMISSIONS & OWNERSHIP

chmod 640 file  
chown user:group file  

Special permission bits:
- 4 → SUID
- 2 → SGID
- 1 → Sticky

---

# STORAGE (LVM — STILL HIGH VALUE)

> XFS remains the default filesystem in RHEL 10.

pvcreate /dev/sdb  
vgcreate vgdata /dev/sdb  
lvcreate -n lvdata -L 5G vgdata  
mkfs.xfs /dev/vgdata/lvdata  

Persistent mount:
echo "/dev/vgdata/lvdata /data xfs defaults 0 0" >> /etc/fstab  
mount -a  

Validate:
df -h  
lsblk  

---

# NETWORKING (NMCLI — REQUIRED)

nmcli con show  
nmcli con mod eth0 ipv4.method manual ipv4.addresses 192.168.1.10/24  
nmcli con up eth0  
ip a  

> Legacy network scripts remain **unsupported**.

---

# SERVICES & BOOT

systemctl enable --now httpd  
systemctl status httpd  

Change default target (if asked):
systemctl set-default multi-user.target  

---

# FIREWALL (FIREWALLD DEFAULT)

firewall-cmd --add-service=http --permanent  
firewall-cmd --reload  

Verify:
firewall-cmd --list-all  

---

# SELINUX (ENFORCING BY DEFAULT)

getenforce  
setenforce 0   (temporary troubleshooting only)

Persistent mode:
vi /etc/selinux/config  

Fix contexts:
ls -Z  
restorecon -Rv /var/www/html  

> **Do not disable SELinux permanently** — this is still a common exam failure.

---

# CONTAINERS (RHEL 10 — PODMAN)

> Scope reminder:
> - **Podman only**
> - **No Kubernetes**
> - **No advanced image builds**

---

## Container Basics

List images and containers:
podman images  
podman ps  
podman ps -a  

Pull image:
podman pull registry.redhat.io/ubi10/ubi  

---

## Run a Container

podman run -d --name web -p 8080:80 nginx  

Validate:
podman ps  
ss -tulnp  

---

## Stop / Remove Containers

podman stop web  
podman rm web  

Remove image if needed:
podman rmi nginx  

---

## Inspect & Logs (Exam Favorite)

podman inspect web  
podman logs web  

Check:
- Status
- Port mapping
- Errors

---

## Rootless Containers (Strongly Preferred)

Enable lingering:
loginctl enable-linger user1  

Run as user:
podman run -d --name web -p 8080:80 nginx  

---

## Environment Variables

podman run -d \
  --name demo \
  -e APP_ENV=prod \
  ubi10/ubi env  

Verify:
podman inspect demo  

---

## Volume Mounts + SELinux (VERY COMMON)

podman run -d \
  --name webdata \
  -v /data:/usr/share/nginx/html:Z \
  -p 8080:80 \
  nginx  

Notes:
- `:Z` fixes SELinux labeling
- Missing this often causes failures

---

## Persistent Containers (SYSTEMD)

Generate unit:
podman generate systemd --name web --files --new  

Install:
mv container-web.service /etc/systemd/system/  
systemctl daemon-reload  
systemctl enable --now container-web  

Verify:
systemctl status container-web  

---

# PRACTICE LABS

## LAB 1 — Users & Groups
Create users, groups, and sudo access  
Skills: useradd, groupadd, visudo  

---

## LAB 2 — Storage (LVM)
Create logical volumes and mount persistently  
Skills: pvcreate, vgcreate, lvcreate, /etc/fstab  

---

## LAB 3 — Networking
Configure static IP and hostname  
Skills: nmcli, hostnamectl  

---

## LAB 4 — Services & Firewall
Install service, enable at boot, open firewall  
Skills: dnf, systemctl, firewall-cmd  

---

## LAB 5 — SELinux
Fix access issues using correct contexts  
Skills: restorecon, SELinux modes  

---

## LAB 6 — Archiving

tar -czvf backup.tar.gz /data  
tar -xzvf backup.tar.gz -C /restore  

---

# LAB 7 — BASH SCRIPTING (STILL REQUIRED)

## Script Rules
- Shebang required
- Executable bit set
- Handles missing arguments
- Safe to re-run

---

## FOR Loop — Create Users

#!/bin/bash
USERS="dev1 dev2 dev3"

for user in $USERS; do
  id "$user" &>/dev/null || useradd "$user"
done

---

## WHILE Loop — Read File

#!/bin/bash
while read user; do
  id "$user" &>/dev/null || useradd "$user"
done < users.txt

---

## WHILE Loop — Wait for Service

#!/bin/bash
SERVICE=httpd

while ! systemctl is-active --quiet "$SERVICE"; do
  sleep 2
done

echo "$SERVICE is running"

---

## CASE Statement — Service Control

#!/bin/bash

case "$1" in
  start) systemctl start httpd ;;
  stop) systemctl stop httpd ;;
  status) systemctl status httpd ;;
  *)
    echo "Usage: $0 {start|stop|status}"
    exit 1
    ;;
esac

---

# LAB 8 — CONTAINERS (RHEL 10)

Objective:
- Run a container
- Expose a port
- Apply SELinux-safe volume
- Persist across reboot

---

# COMMON FAILURE PATTERNS

- Forgot /etc/fstab
- Service not enabled
- Firewall rule not permanent
- Disabled SELinux instead of fixing it
- Script not executable
- Container not persistent
- Missing :Z on volume mounts

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
Red Hat grades **outcomes**, not effort.  
Make it work. Make it persistent. Validate everything.
