oracle-common
=========
- [Introduction](#introduction)
- [Variables](#variables)
  - [Common](#common)
  - [Groups](#groups)
    - [Database groups](#database_groups)
    - [Grid Infrastructure groups](#gird_infrastructure_groups)
  - [Users](#users)
    - [Database user](#datanase_user)
    - [Grid Infrastructure user](#grid_infrastructure_user)
- [Usage](#usage)

# Introduction
Ansible role to setup common stuff used or required by Oracle Database and Oracle Client installations.

The role will ensure:
- all groups required to install an Oracle Database or Oracle Client.
Each group is defined by several variables that can be changed via group or host vars. Role seperation is enabled by default but can be changed.
- all operating system accounts required by Oracle Grid Infrastructure, Oracle Database or Oracle Client installations. Each user is defined by several variables that can be changed by group or host vars.
- permissions and content of Oracle Inventory
- TNS_ADMIN directory and conent of tnsnames.ora if __oracle_tns_names__ is defined

# Requirements
- Ansible 1.9

# Variables
## Common
| Name | Default | Description | Hints |
|:---------|:--------|:------------|:------|
| oracle_app_directory | /u01/app | Base directory under which Oracle products will be installed |
| oracle_inventory_group_name |  oinstall | Name of Oracle Inventory owner group |
| oracle_inventory_group_id | 54321 | GID of Oracle Inventory owner group |
| oracle_inventory_directory | '{{ oracle_app_directory }}/oraInventory' | Directory where the Oracle Inventory will be stored |
| oracle_inventory_file | '{{ oracle_inventory_directory }}/ContentsXML/inventory.xml' | Path to file containing the Oracle inventory |
| oracle_role_separation | True | Enable or disable role separation |
| oracle_shells | - | Variable containing typical shells and associated profile files | DON'T CHANGE IT |

## Groups
### Database groups
| Name | Default | Description | Hints |
|:---------|:--------|:------------|:------|
| oracle_db_osdba_group_name | dba | Name of DB group OSDBA | Only used if oracle_role_separation is set to True
| oracle_db_osdba_group_id | 54322 | GID of DB group OSDBA | Only used if oracle_role_separation is set to True
| oracle_db_osoper_group_name | oper | Name of DB group OSOPER | Only used if oracle_role_separation is set to True
| oracle_db_osoper_group_id | 54323 | GID of DB group OSOPER | Only used if oracle_role_separation is set to True
| oracle_db_osbackupdba_group_name |  backupdba | Name of DB group OSBACKUPDBA (new in 12c) | Only used if oracle_role_separation is set to True and an Oracle 12c DB is installed
| oracle_db_osbackupdba_group_id | 54324 | GID of DB group OSBACKUPDBA (new in 12c) | Only used if oracle_role_separation is set to True and an Oracle 12c DB is installed
| oracle_db_osdgdba_group_name | dgdba | Name of DB group OSDGDBA (new in 12c) | Only used if oracle_role_separation is set to True and an Oracle 12c DB is installed
| oracle_db_osdgdba_group_id | 54325 | GID of DB group OSDGDBA (new in 12c) | Only used if oracle_role_separation is set to True and an Oracle 12c DB is installed
| oracle_db_oskmdba_group_name | kmdba | Name of DB group OSKMDBA (new in 12c) | Only used if oracle_role_separation is set to True and an Oracle 12c DB is installed
| oracle_db_oskmdba_group_id | 54326 | GID of DB group OSKMDBA (new in 12c) | Only used if oracle_role_separation is set to True and an Oracle 12c DB is installed

### Grid Infrastructure groups
| Variable | Default | Description | Hints |
|:---------|:--------|:------------|:------|
| oracle_gi_osdba_group_name | asmdba | Name of GI group OSDBA | Only used is Grid Infrastructure is installed and oracle_role_separation is set to True |
| oracle_gi_osdba_group_id | 54327 | GID of GI group OSDBA | Only used is Grid Infrastructure is installed and oracle_role_separation is set to True
| oracle_gi_osoper_group_name | asmoper | Name of GI group OSOPER | Only used is Grid Infrastructure is installed and oracle_role_separation is set to True
| oracle_gi_osoper_group_id | 54328 | GID of GI group OSOPER | Only used is Grid Infrastructure is installed and oracle_role_separation is set to True
| oracle_gi_osasm_group_name | asmadmin | Name of GI group OSASM | Only used is Grid Infrastructure is installed and oracle_role_separation is set to True
| oracle_gi_osasm_group_id | 54329 | GID of GI group OSASM | Only used is Grid Infrastructure is installed and oracle_role_separation is set to True

## Users
### Database user
| Variable | Default | Description |
|:---------|:--------|:------------|
| oracle_db_owner_user_name | oracle | Name of Oracle Database Software owner |
| oracle_db_owner_user_id | 54321 | UID of Oracle Database Software owner |
| oracle_db_owner_user_home | /home/oracle | Home directory of the Oracle Database Software owner |
| oracle_db_owner_user_shell | /bin/bash | Shell used by the Oracle Database Software owner |
| oracle_db_oracle_base | '{{oracle_app_directory}}/{{ oracle_db_owner_user_name }}' | ORACLE_BASE of Oracle Database

### Grid Infrastructure user
Following variables are only used if Oracle Grid Infrastructure is installed.

| Variable | Default | Description |
|:---------|:--------|:------------|
| oracle_gi_owner_user_name | grid | Name of Oracle Grid Infrastructure Software owner |
| oracle_gi_owner_user_id | 54322 | UID of Oracle Grid Infrastructure Software owner |
| oracle_gi_owner_user_home | /home/grid | Home directory of Oracle Grid Infrastructure owner |
| oracle_gi_owner_user_shell| /bin/bash | Shell used by Oracle Grid Infrastructure owner |
| oracle_gi_oracle_base | '{{ oracle_app_directory }}/{{ oracle_gi_owner_user_name }}' | ORACLE_BASE of Grid Infrastructure  |

# Usage

Without defining any variable the following playbook would just create the group oinstall as well as user oracle.
```yaml
- hosts: oracle-server
  roles:
   - role: oracle-common
```

To define TNS entries use variable __oralce_tns_names__ like bellow.
```yaml
oracle_tns_names:
- name: ORCL
  hosts:
  - dbserver.example.com
  port: 1521
  sid: ORCL
```

A more complex example with failover to connect to Oracle RAC.
```yaml
oracle_tns_names:
- name: RAC
  load_balance: true
  failover: true
  hosts:
  - rac-01.example.com
  - rac-02.example.com
  port: 1521
  service_name: ORCL
```

# Author
[Thomas Krahn](mailto:ntbc@gmx.net)
