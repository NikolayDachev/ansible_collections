ros_sys_script
=========
This role will add/run script via RouterOS API.  
https://wiki.mikrotik.com/wiki/Manual:Scripting  

galaxy: https://galaxy.ansible.com/nikolaydachev/routeros_api  
github: https://github.com/NikolayDachev/ansible_collections  

Requirements
------------

module: [community.routeros.api](https://galaxy.ansible.com/community/routeros)  

Role Variables
--------------

https://docs.ansible.com/ansible/latest/collections/community/routeros/api_module.html  

ros_hostname: "community.routeros.api hostname"  
ros_username: "community.routeros.api username"  
ros_password: "community.routeros.api password"  
ros_ssl: "community.routeros.api ssl", default for this role is set to "true"  

All role variables are combination from role name as prefix and the actual RouterOS property.  
Role var prefix: **ros_sys_script_**  

NOTE: Any "-" from RouterOS property is replaced with "_" for example, "dont-require-permissions" is "dont_require_permissions", so the full var name is "ros_sys_script_dont_require_permissions"  

- ros_sys_script_run_script: If is set to "true", role will run {{ ros_sys_script_name }}
```
ros_sys_script_run_script: "false"
```

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros system script 
  hosts: ros
  gather_facts: no
  connection: local
  ignore_errors: yes
  
  tasks:
  - name: add system script
    include_role: 
      name: nikolaydachev.routeros_api.ros_sys_script
    vars:
      # script vars
      ros_backup_ftp: "192.168.1.20"
      # role vars
      ros_sys_script_run_script: ""
      ros_sys_script_comment: "Create ros backup and send it via ftp"
      ros_sys_script_copy_from: ""
      ros_sys_script_dont_require_permissions: ""
      ros_sys_script_name: "BackupFTP"
      ros_sys_script_owner: ""
      ros_sys_script_policy: ""
      ros_sys_script_source: |
        :local host value=[/system identity get name];
        :local date value=[/system clock get date];
        :local day [ :pick $date 4 6 ];
        :local month [ :pick $date 0 3 ];
        :local year [ :pick $date 7 11 ];
        :local name value=($host."-".$day."-".$month."-".$year);
        /system backup save name=$name;
        /export file=$name;
        /tool fetch address={{ ros_backup_ftp }} user=ros password="{{ vault_ros_bck_pwd }}" mode=ftp dst-path=("/mikrotik/rsc/".$name.".rsc") src-path=($name.".rsc") upload=yes;
        /tool fetch address={{ ros_backup_ftp }} user=ros password="{{ vault_ros_bck_pwd }}" mode=ftp dst-path=("/mikrotik/backup/".$name.".backup") src-path=($name.".backup") upload=yes;

```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)