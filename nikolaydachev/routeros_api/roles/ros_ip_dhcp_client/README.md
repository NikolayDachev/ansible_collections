ros_ip_dhcp_client
=========

This role will configure RouterOS DHCP Server via API.  
https://wiki.mikrotik.com/wiki/Manual:IP/DHCP_Client  

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

Role var prefix: **ros_ip_dhcp_client_**  
General configuration variable: **ros_ip_dhcp_client_config** type list  
Sub configuations:  
- add  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/DHCP_Client#Properties  

- option  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/DHCP_Client#Option  

NOTE: Any "-" from RouterOS property is replaced with "_" for example, "default-route-distance" is "default_route_distance", so the full var name is "ros_ip_dhcp_client_default_route_distance"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros ip dhcp-client 
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_ip_dhcp_client
    ros_ip_dhcp_client_config:
      - add
#      - option
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)