ros_too_romon
=========

This role will configure RouterOS romon service via API.  
https://wiki.mikrotik.com/wiki/Manual:Tools/RoMON    

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

All role variables are combination from role name as prefix, general configuration variable and the the actual RouterOS property.  
With general configuration variable this role can configure only selected RouterOS sub configurations.  

Role var prefix: **ros_tool_romon_**  
General configuration variable: **ros_tool_romon_config** type list  
Sub configuations:  
- enabled  
  Will enable romon and other related configuations  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Tools/RoMON#Configuration  

- port  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Tools/RoMON#Configuration  

NOTE: Any "-" from RouterOS property is replaced with "_" for example, "copy-from" is "copy_from", so the full var name is "ros_tool_romon_port_copy_from"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros tool romon
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_tool_romon
    ros_tool_romon_config:
      - enabled
      - port

```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)