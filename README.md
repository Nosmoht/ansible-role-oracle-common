oracle-common
=========
- [Introduction](#introduction)
- [Usage](#usage)

# Introduction
Ansible role to setup common stuff used or required by Oracle Grid Infrastructure, Oracle Database and Oracle Client installations.

The role will ensure that:
- all groups required to install Oracle Grid Infrastructure, Oracle Database or Oracle Client exist
- all users required to install Oracle Grid Infrastructure, Oracle Database or Oracle Client installations exist vars.
- Oracle inventory directory exist and has the right permissions
- oraInst.log exists and has right permissions

The role was tested on RHEL 6+7, CentOS 6+7 and Oracle Linux 6+7 installing Oracle 11gR2 and Oracle 12cR1.

# Requirements
- Ansible

# Dependencies
- [ansible-role-oracle-config]

# Variables
All variables are inherited from [ansible-role-oracle-config]

# Usage
Without defining any variable the following playbook would just create the group oinstall as well as user oracle.
```yaml
- hosts: oracle-server
  roles:
   - role: oracle-common
```

# Author
[Thomas Krahn](mailto:ntbc@gmx.net)

[ansible-role-oracle-config]: (http://srv-git-01-hh1.alinghi.tipp24.net/dba/ansible-role-oracle-config)
