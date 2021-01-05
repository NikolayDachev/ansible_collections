ros_int_vrrp
=========

This role will configure RouterOS VRRP interface via API.  
https://wiki.mikrotik.com/wiki/Manual:Interface/VRRP  

galaxy: https://galaxy.ansible.com/nikolaydachev/routeros_api  
github: https://github.com/NikolayDachev/ansible_collections  

Requirements
------------

module: [community.routeros.api](https://galaxy.ansible.com/community/routeros)  
role: [nikolaydachev.routeros_api.ros_ip_addr](https://galaxy.ansible.com/nikolaydachev/routeros_api)  

Role Variables
--------------

https://docs.ansible.com/ansible/latest/collections/community/routeros/api_module.html  

ros_hostname: "community.routeros.api hostname"  
ros_username: "community.routeros.api username"  
ros_password: "community.routeros.api password"  
ros_ssl: "community.routeros.api ssl", default for this role is set to "true"  

All role variables are combination from role name as prefix and the the actual RouterOS property  

RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Interface/VRRP#Property_reference  
Role var prefix: **ros_int_vrrp_**  

NOTE: Any "-" from RouterOS property is replaced with "_" for example "on-backup" is "on_backup", so the full var name is "ros_int_vrrp_on_backup"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros vrrp 
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_int_vrrp
  - role: nikolaydachev.routeros_api.ros_ip_addr
    ip_addr_interface: "{{ ros_int_vrrp_name }}"
    ip_addr_address: "{{ ros_int_vrrp_vip }}"
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)