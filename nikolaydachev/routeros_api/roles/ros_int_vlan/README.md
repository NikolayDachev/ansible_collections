ros_int_vlan
=========

This general role will create vlan interface via RouterOS API.  
https://help.mikrotik.com/docs/display/ROS/VLAN  

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
Role var prefix: **ros_int_vlan_**  

NOTE: Any "-" from RouterOS property is replaced with "_" for example, "arp-timeout" is "arp_timeout", so the full var name is "ros_int_vlan_arp_timeout"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros interface vlan
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_int_vlan
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)