ansible-role-oracle-common
=========

Ansible role to setup common Oracle stuff.

- Setup Oracle groups (oinstall, oper, dba, asmdba, asmoper, ...)
- Setup Oracle users (oracle, grid)

Requirements
------------

No requirements yet.

Role Variables
--------------

Variable | Default | Meaning | Hints
:--- | --- | --- | :---
oracle_app_directory | /u01/app | Base directory under which Oracle products will be installed |
oracle_inventory_group_name |  oinstall | Name of Oracle Inventory owner group |
oracle_inventory_group_id | 54321 | GID of Oracle Inventory owner group |
oracle_inventory_directory | '{{ oracle_app_directory }}/oraInventory' | Directory where the Oracle Inventory will be stored |
oracle_inventory_file | '{{ oracle_inventory_directory }}/ContentsXML/inventory.xml' | Path to file containing the Oracle inventory |
oracle_role_separation | True | Set to True to create separate roles (dba, oper, backupdba, ...) else False |
oracle_db_osdba_group_name | dba | Name of DB group OSDBA | Only used if oracle_role_separation is set to True
oracle_db_osdba_group_id | 54322 | GID of DB group OSDBA | Only used if oracle_role_separation is set to True
oracle_db_osoper_group_name | oper | Name of DB group OSOPER | Only used if oracle_role_separation is set to True
oracle_db_osoper_group_id | 54323 | GID of DB group OSOPER | Only used if oracle_role_separation is set to True
oracle_db_osbackupdba_group_name |  backupdba | Name of DB group OSBACKUPDBA (new in 12c) | Only used if oracle_role_separation is set to True and an Oracle 12c DB is installed
oracle_db_osbackupdba_group_id | 54324 | GID of DB group OSBACKUPDBA (new in 12c) | Only used if oracle_role_separation is set to True and an Oracle 12c DB is installed
oracle_db_osdgdba_group_name | dgdba | Name of DB group OSDGDBA (new in 12c) | Only used if oracle_role_separation is set to True and an Oracle 12c DB is installed
oracle_db_osdgdba_group_id | 54325 | GID of DB group OSDGDBA (new in 12c) | Only used if oracle_role_separation is set to True and an Oracle 12c DB is installed
oracle_db_oskmdba_group_name | kmdba | Name of DB group OSKMDBA (new in 12c) | Only used if oracle_role_separation is set to True and an Oracle 12c DB is installed
oracle_db_oskmdba_group_id | 54326 | GID of DB group OSKMDBA (new in 12c) | Only used if oracle_role_separation is set to True and an Oracle 12c DB is installed
oracle_db_owner_user_name | oracle | Name of Oracle Database Software owner |
oracle_db_owner_user_id | 54321 | UID of Oracle Database Software owner |
oracle_db_owner_user_home | /home/oracle | Home directory of the Oracle Database Software owner |
oracle_db_owner_user_shell | /bin/bash | Shell used by the Oracle Database Software owner |
oracle_db_oracle_base | '{{oracle_app_directory}}/{{ oracle_db_owner_user_name }}' | ORACLE_BASE of Oracle Database
oracle_gi_osdba_group_name | asmdba | Name of GI group OSDBA | Only used is Grid Infrastructure is installed and oracle_role_separation is set to True
oracle_gi_osdba_group_id | 54327 | GID of GI group OSDBA | Only used is Grid Infrastructure is installed and oracle_role_separation is set to True
oracle_gi_osoper_group_name | asmoper | Name of GI group OSOPER | Only used is Grid Infrastructure is installed and oracle_role_separation is set to True
oracle_gi_osoper_group_id | 54328 | GID of GI group OSOPER | Only used is Grid Infrastructure is installed and oracle_role_separation is set to True
oracle_gi_osasm_group_name | asmadmin | Name of GI group OSASM | Only used is Grid Infrastructure is installed and oracle_role_separation is set to True
oracle_gi_osasm_group_id | 54329 | GID of GI group OSASM | Only used is Grid Infrastructure is installed and oracle_role_separation is set to True
oracle_gi_owner_user_name | grid | Name of Oracle Grid Infrastructure Software owner | Only used is Grid Infrastructure is installed
oracle_gi_owner_user_id | 54322 | UID of Oracle Grid Infrastructure Software owner | Only used is Grid Infrastructure is installed
oracle_gi_owner_user_home | /home/grid | Home directory of Oracle Grid Infrastructure owner | Only used is Grid Infrastructure is installed
oracle_gi_owner_user_shell| /bin/bash | Shell used by Oracle Grid Infrastructure owner | Only used is Grid Infrastructure is installed
oracle_gi_oracle_base | '{{ oracle_app_directory }}/{{ oracle_gi_owner_user_name }}' | ORACLE_BASE of Grid Infrastructure  | Only used is Grid Infrastructure is installed
oracle_shells | - | Variable containing typical shells and associated profile files | DON'T CHANGE IT

Dependencies
------------

No dependencies.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: Nosmoht.ansible-role-oracle-common }

License
-------

BSD

Author Information
------------------

Name: Thomas Krahn
mail: ntbc@gmx.net

