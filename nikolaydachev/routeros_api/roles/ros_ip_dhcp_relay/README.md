ros_ip_dhcp_relay
=========

This role will configure RouterOS IP address via API.  
https://wiki.mikrotik.com/wiki/Manual:IP/DHCP_Relay  

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

RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/DHCP_Relay#Properties  
Role var prefix: **ros_ip_dhcp_relay_**

NOTE: Any "-" from RouterOS property is replaced with "_" for example "local-address" is "local_address", so the full var name is "ros_ip_dhcp_relay_local_address"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros ip dhcp-relay
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_ip_dhcp_relay
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)