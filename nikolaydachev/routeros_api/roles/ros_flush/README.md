ros_flush
=========

This general role will flush/remove **ALL** configuration parameters for the given path except dynamically created items by routeros via RouterOS API.  

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

NOTE: This role require variable [ros_flush_path](https://docs.ansible.com/ansible/latest/collections/community/network/routeros_api_module.html#parameter-path)  

All role variables are combination from role name as prefix and the the actual RouterOS property   
Role var prefix: **ros_flush_**  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros flush config example
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_flush
    ros_flush_path: "ip firewall filter"
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)