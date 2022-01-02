ros_ip_route
=========

This general role will configure ip route via RouterOS API.  
https://wiki.mikrotik.com/wiki/Manual:IP/Route

galaxy: https://galaxy.ansible.com/nikolaydachev/routeros_api  
github: https://github.com/NikolayDachev/ansible_collections  

NOTE: Work only for RouterOS 6 !  

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

All role variables are combination from role name as prefix, general configuration variable and the actual RouterOS property.  
With general configuration variable this role can configure only selected RouterOS sub configurations.  

Role var prefix: **ros_ip_route_**  
General configuration variable: **ros_ip_route_config** type list  
Sub configuations:  
- add  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/Route#General_properties  
- rule  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/Route  
- vrf  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/Route  


NOTE: Any "-" from RouterOS property is replaced with "_" for example, "dst-address" is "dst_address", if rule is use, the full var name is "ros_ip_route_rule_dst_address"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros ip route 
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_ip_route
    ros_ip_dhcp_server_config:
      #- vrf
      - add
      #- rule
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)