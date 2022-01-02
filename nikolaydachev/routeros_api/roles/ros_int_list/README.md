ros_int_list
=========

This general role will create interface list via RouterOS API.  
https://help.mikrotik.com/docs/display/ROS/List  

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

Role var prefix: **ros_int_list_**  
General configuration variable: **ros_int_list_config** type list  
Sub configuations:  
- add  
  RouterOS reference:https://help.mikrotik.com/docs/display/ROS/List  

- member  
  RouterOS reference:https://help.mikrotik.com/docs/display/ROS/List  

NOTE: Any "-" from RouterOS property is replaced with "_" for example, "copy-from" is "copy_from", so the full var name is "ros_int_list_copy_from"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros interface list
  hosts: ros
  gather_facts: no
  connection: local
  ignore_errors: yes

  tasks:
  - name: add interface list
    include_role: 
      name: nikolaydachev.routeros_api.ros_int_list
    vars:
      ros_int_list_config: "add"
      ros_int_list_name: list1"

  - name: add interface member to list
    include_role: 
      name: nikolaydachev.routeros_api.ros_int_list
    vars:
      ros_int_list_config: "member"
      ros_int_list_member_interface: "ether1"
      ros_int_list_member_list: "list1"
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)