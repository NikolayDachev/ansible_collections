ros_ip_dchp_server
=========

This role will configure RouterOS router user via API.  
https://wiki.mikrotik.com/wiki/Manual:Router_AAA  

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

Role var prefix: **ros_user_**  
General configuration variable: **ros_user_config** type list  
Sub configuations:  
- group
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Router_AAA#User_Groups

- aaa
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Router_AAA#Remote_AAA

- ssh-keys
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Router_AAA#SSH_Keys

- ssh-keys_private
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Router_AAA#SSH_Keys

- user
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Router_AAA#Router_Users

NOTE: Any "-" from RouterOS property is replaced with "_" for example, default-group" is "default_group", so the full var name is "ros_user_aaa_default_group"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros user
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_user
    ros_user_config:
#      - group
#      - aaa
#      - ssh-keys
#      - ssh-keys_private
      - user
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)