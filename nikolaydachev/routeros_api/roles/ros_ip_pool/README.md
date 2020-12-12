ros_ip_addr
=========

This role will configure RouterOS IP pool via API.  
https://wiki.mikrotik.com/wiki/Manual:IP/Pools  

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

RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/Pools#Property_Description  
Role var prefix: **ros_ip_pool_**  

NOTE: Any "-" from RouterOS property is replaced with "_" for example "next-pool" is "next_pool", so the full var name is "ros_ip_pool_next_pool"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros ip pool 
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_ip_pool
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)