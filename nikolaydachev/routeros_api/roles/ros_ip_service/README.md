ros_ip_addr
=========

This role will configure RouterOS IP service via API.  
https://wiki.mikrotik.com/wiki/Manual:IP/Services  

galaxy: https://galaxy.ansible.com/nikolaydachev/routeros_api  
github: https://github.com/NikolayDachev/ansible_collections  

Requirements
------------

module: [community.routeros.api](https://galaxy.ansible.com/community/routeros)  

Role Variables
--------------

https://ansible.fontein.de/collections/community/routeros/api_module.html#ansible-collections-community-routeros-api-module  

ros_hostname: "community.routeros.api hostname"  
ros_username: "community.routeros.api username"  
ros_password: "community.routeros.api password"  
ros_ssl: "community.routeros.api ssl", default for this role is set to "true"  

All role variables are combination from role name as prefix and the the actual RouterOS property  

RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/Services#Properties  
Role var prefix: **ros_ip_service_**

NOTE: Variable **ros_ip_service_set** is type dictionary  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros ip service
  hosts: all
  gather_facts: no
  connection: local
  vars:
    ros_ip_service_set:
      telnet:
        - disabled=yes
      api-ssl:
        - disabled=false
        - address=10.20.30.40

  roles:
  - nikolaydachev.routeros_api.ros_ip_service
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)