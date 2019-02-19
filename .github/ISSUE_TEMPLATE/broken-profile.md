---
name: Broken profile
about: Program doesn't have access to something critical for it work
title: Broken profile for Foo
labels: bug
assignees: foxcpp

---

### Troubleshooting steps
- [ ] Boot with `audit=1`, install auditd and do `systemctl start auditd`, run program, attach `/var/audit/audit.log`
- [ ] Launch program from console, include output
