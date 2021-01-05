ros_add
=========

This general role will add multiple configuration parameters for the given path via RouterOS API.  
https://wiki.mikrotik.com/wiki/Manual:Console#General_Commands  
RouterOS "add".  

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

ros_add_list: "List of parametes to be added"

NOTE: This role require variable [ros_add_path](https://docs.ansible.com/ansible/latest/collections/community/network/routeros_api_module.html#parameter-path)

All role variables are combination from role name as prefix and the the actual RouterOS property   
Role var prefix: **ros_add_**

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros add config example
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_add
    ros_add_path: "ip firewall filter"
    ros_add_list:
      - action=accept chain=input
      - action=drop chain=input
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)