ros_update
=========

This general role will do configuration parameter update by **RouterOS API .id** for the given path via RouterOS API.  

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

ros_update_cfg: "This is a Dictunary {".id numebr":"parameter=new_valur"}"

NOTE: This role require variable [ros_update_path](https://docs.ansible.com/ansible/latest/collections/community/network/routeros_api_module.html#parameter-path)

All role variables are combination from role name as prefix and the the actual RouterOS property   
Role var prefix: **ros_update_**

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros update example
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_update
    ros_update_path: "ip firewall filter"
    ros_update_cfg:
      "*67":
        "comment=test_ros_update_67"
      "*68":
        "comment=test_ros_update_68"
      "*69":
        "comment=test_ros_update_69"
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)