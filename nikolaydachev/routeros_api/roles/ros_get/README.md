ros_get
=========

This general role will return information that's accessible from particular RouterOS command level via API.  
https://wiki.mikrotik.com/wiki/Manual:Console  
RouterOS "print".

Result will be registerd to "print_path" and added to output as debug msg.

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

NOTE: This role require variable [ros_get_path](https://docs.ansible.com/ansible/latest/collections/community/network/routeros_api_module.html#parameter-path)  

All role variables are combination from role name as prefix and the the actual RouterOS property   
Role var prefix: **ros_get_**  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros check current config
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_get
    ros_get_path: "ip address"
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)