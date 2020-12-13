ros_query
=========

This general role will do a query in the given path via RouterOS API.  

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

ros_query_for: "community.routeros.api query"

NOTE: This role require variable [ros_query_path](https://docs.ansible.com/ansible/latest/collections/community/network/routeros_api_module.html#parameter-path)

NOTE: This role register var **rosquery**

All role variables are combination from role name as prefix and the the actual RouterOS property   
Role var prefix: **ros_query_**

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros query example
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_query
    ros_query_path: "ip firewall filter"
    ros_query_for: ".id chain WHERE chain == forward"
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)