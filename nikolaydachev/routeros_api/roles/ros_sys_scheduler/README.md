ros_sys_scheduler
=========
This role will add scheduler task via RouterOS API.  
https://help.mikrotik.com/docs/display/ROS/Scheduler  

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
Role var prefix: **ros_sys_scheduler_**  

NOTE: Any "-" from RouterOS property is replaced with "_" for example, "on-event" is "on_event", so the full var name is "ros_sys_scheduler_on_event"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros system scheduler 
  hosts: ros
  gather_facts: no
  connection: local
  ignore_errors: yes
  
  tasks:
  - name: add system scheduler
    include_role: 
      name: nikolaydachev.routeros_api.ros_sys_scheduler
    vars:
        ros_sys_scheduler_comment: "Run script BackupFTP"
        ros_sys_scheduler_copy_from: ""
        ros_sys_scheduler_disabled: "no"
        ros_sys_scheduler_interval: "1w"
        ros_sys_scheduler_on_event: "BackupFTP"
        ros_sys_scheduler_policy: ""
        ros_sys_scheduler_start_date: "jul/19/2020"
        ros_sys_scheduler_start_time: "13:43:22"
        ros_sys_scheduler_name: "BackupFTP"
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)