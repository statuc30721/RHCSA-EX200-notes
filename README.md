# RHCSA (EX200) Practice Repository - RHEL 10

Hands-on RHCSA exam preparation, VM labs, and on-the-job Linux administration reference.

This repository provides a practical, exam-aligned study framework for the
Red Hat Certified System Administrator (RHCSA - EX200) exam, updated for RHEL 10.

---

## Repository Purpose

This project is intended to:

- Provide hands-on practice aligned to official EX200 objectives
- Support VM-based, exam-style lab work
- Reinforce persistence, validation, and correctness
- Serve as a practical Linux administration reference

---

## Official Exam Reference

- Exam: RHCSA (EX200)
- Operating System: Red Hat Enterprise Linux 10
- Exam format: Performance-based, hands-on
- Official objectives:
  https://www.redhat.com/en/services/training/ex200-red-hat-certified-system-administrator-exam

IMPORTANT:
Red Hat exams award credit only for correct and persistent results.
Non-persistent or partially correct configurations do not score.

---

## Scope of This Repository

Covered topics include:

- Essential Linux commands
- User and group management
- Permissions and ownership
- Storage management (LVM, XFS)
- Networking using nmcli
- System services and boot targets
- Firewall configuration using firewalld
- SELinux (enforcing mode, contexts)
- Bash scripting fundamentals
- Containers using Podman (EX200 scope)

Intentionally out of scope:

- Kubernetes
- Advanced container image builds
- CI/CD pipelines

---

## Repository Layout

```
.
├── README.md
├── workbook/
│   └── rhcsa_workbook.md
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
│   └── examples/
├── checklists/
│   └── auto-grading.md
└── vm-lab/
    ├── build.md
    └── reset.md
```

---

## VM Lab Environment

Recommended setup:

- Hypervisor: KVM, VMware, VirtualBox, or Proxmox
- OS: RHEL 10 or compatible rebuild
- VM count: 1 (exam-style) or 2 (client/server practice)
- Resources:
  - 2 vCPU
  - 4 GB RAM
  - 30 to 40 GB disk

Root or sudo access is required.

---

## Exam-Style Lab Workflow

1. Snapshot or reset the VM
2. Read the lab objective only
3. Perform tasks without notes
4. Reboot the system
5. Validate all results
6. Self-grade using the checklist

Rule:
If it does not survive reboot, it does not count.

---

## Containers (EX200 Reminder)

RHCSA tests basic Podman usage only:

- Running containers
- Inspecting containers
- Port mapping
- Volume mounts with SELinux
- Persisting containers using systemd

Kubernetes and orchestration platforms are not tested.

---

## DISCLAIMER AND EXAM INTEGRITY NOTICE

THIS REPOSITORY IS PROVIDED FOR EDUCATIONAL AND PROFESSIONAL DEVELOPMENT PURPOSES ONLY.

- This project DOES NOT contain real Red Hat exam questions, answers, screenshots,
  or any material obtained from live certification exams.
- All labs, scenarios, scripts, and examples are ORIGINAL and based solely on
  publicly available RHCSA (EX200) exam objectives.
- This repository DOES NOT violate Red Hat Non-Disclosure Agreements (NDA),
  exam policies, or certification agreements.
- Users are solely responsible for complying with all Red Hat certification
  terms, conditions, and ethical guidelines.

Red Hat, RHCSA, and RHEL are trademarks of Red Hat, Inc.
This repository is NOT affiliated with, sponsored by, or endorsed by Red Hat.

DO NOT contribute exam-confidential, NDA-protected, or proprietary material
to this repository.

---

## Study Guidance

Recommended study order:

1. Review the workbook
2. Practice core administration labs
3. Practice services, SELinux, and firewall tasks
4. Practice bash scripting
5. Practice containers
6. Perform a timed mock exam

Exam strategy reminders:

- Validate after every task
- Do not disable SELinux
- Use supported tools only
- Assume systems reboot during grading

---

## Contributions

Contributions are welcome if they:

- Stay within EX200 scope
- Use supported RHEL tools
- Improve clarity or accuracy
- Do not include exam-confidential material

Open a pull request with a clear description of changes.

---

## Final Advice

Red Hat exams grade outcomes, not effort.

Make it work.
Make it persistent.
Validate everything.
