# RHCSA (EX200) Practice Repository — RHEL 10

**Hands-on RHCSA exam preparation, VM labs, and on-the-job Linux administration reference**

This repository provides a **practical, exam-aligned study framework** for the  
**Red Hat Certified System Administrator (RHCSA – EX200)** exam, updated for **RHEL 10**.

It is designed to:
- Mirror **Red Hat’s hands-on grading style**
- Provide **repeatable VM-based labs**
- Serve as a **production-ready Linux admin reference**

---

## Repository Goals

- ✅ 100% coverage of **official EX200 objectives**
- ✅ Focus on **persistence, correctness, and validation**
- ✅ Use **supported RHEL 10 tools only**
- ✅ Avoid exam-unsafe shortcuts
- ✅ Double as a real-world sysadmin reference

---

## Official Exam Reference

- **Exam**: RHCSA (EX200)
- **OS**: Red Hat Enterprise Linux 10
- **Exam Format**: Performance-based (hands-on)
- **Official Objectives**:  
  https://www.redhat.com/en/services/training/ex200-red-hat-certified-system-administrator-exam

> ⚠️ Red Hat exams award credit **only for correct outcomes**.  
> Partial or non-persistent configurations do not score.

---

## What This Repo Covers

| Domain | Coverage |
|-----|---------|
| Essential Linux commands | ✅ |
| Users & groups | ✅ |
| Permissions & ACL basics | ✅ |
| Storage (LVM, XFS) | ✅ |
| Networking (nmcli) | ✅ |
| Services & boot targets | ✅ |
| Firewall (firewalld) | ✅ |
| SELinux (enforcing, contexts) | ✅ |
| Bash scripting | ✅ |
| Containers (Podman – EX200 scope) | ✅ |

**Out of scope (by design):**
- Kubernetes
- Advanced container image builds
- CI/CD pipelines

---

## Repository Structure

```text
.
├── README.md                  # This file
├── workbook/
│   └── rhcsa_workbook.md      # Printable exam workbook
├── labs/
│   ├── lab01-users/
│   ├── lab02-storage/
│   ├── lab03-networking/
│   ├── lab04-services/
│   ├── lab05-selinux/
│   ├── lab06-archiving/
│   ├── lab07-scripting/
│   └── lab08-containers/
├── scripts/
│   └── examples/              # Bash script drills
├── checklists/
│   └── auto-grading.md
└── vm-lab/
    ├── build.md               # VM setup guide
    └── reset.md               # Lab reset instructions
