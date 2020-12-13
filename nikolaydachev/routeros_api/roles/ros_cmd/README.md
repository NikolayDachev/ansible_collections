ros_cmd
=========

This general role can execute set of RouterOS commands in key/value format via RouterOS API.  

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

ros_cmd_cfg: "community.routeros.api cmd"  

NOTE: **ros_cmd_cfg** is a list of commands in a dictionary format, key is used for path and value is used for command  
      - "path": "action key=value key=value .."  
      - "path": "action key=value key=value .."  

All role variables are combination from role name as prefix and the the actual RouterOS property   
Role var prefix: **ros_cmd_**

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros cmd example
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_cmd
    ros_cmd_cfg:
      - "ip address": "add address=2.2.2.2 interface=ether1"
      - "ip address": "add address=3.3.3.3 interface=ether1"
      - "ip dhcp-client": "add interface=ether3 disabled=no"
      - "ip dhcp-client": "add interface=ether4 disabled=no"
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)