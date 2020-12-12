ros_reset_config
=========

This role will **reset** RouterOS configuration via API.  
https://wiki.mikrotik.com/wiki/Manual:Reset  

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
Role var prefix: **ros_reset_config_**  

NOTE: Variable **ros_reset_config_confirm** is type boolean  
+ This role will be executed only when **ros_reset_config_confirm** is set to **True**  

Full variable list can be found under role defaults. 

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros reset configuration
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_reset_config
    ros_reset_config_confirm: True
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)