ros_sys_clock
=========

This role will configure RouterOS system clock via API.  
https://wiki.mikrotik.com/wiki/Manual:System/Time#Clock_and_Time_zone_configuration  

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

All role variables are combination from role name as prefix and the the actual RouterOS property  

RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:System/Time#Clock_and_Time_zone_configuration  
Role var prefix: **ros_sys_clock_**  

NOTE: Any "-" from RouterOS property is replaced with "_" for example "time-zone-name" is "time_zone_name", so the full var name is "ros_sys_clock_time_zone_name"  

ros_sys_clock_manual_ will apply only if ros_sys_clock_time_zone_name var is set to "manual"

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros system clock
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_sys_clock
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)