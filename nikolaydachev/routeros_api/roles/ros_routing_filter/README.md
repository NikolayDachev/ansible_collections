ros_routing_filter
=========

This role will configure RouterOS routing filter via API.  
https://wiki.mikrotik.com/wiki/Manual:Routing/Routing_filters  

IMPRTATN NOTES!
- Please be extremely careful when you manage routing filter rules with any sort of automation!   

- ros_routing_filter is a list vars. Each list item is a rule, rules will be added one by one from first list item to last one (in routeos the order is from top(first list item) to bottom(last list itme))!  

- **ros_routing_filter_flush** varible will remove all routing filter rules at once! The main usage is to make more easy routing filter rules configuration managment. The flush happen before adding new rules, so for example if you set it to "true", this role will first remove all exsiting rules under 'routing filter' and then will add the new rules.  

galaxy: https://galaxy.ansible.com/nikolaydachev/routeros_api  
github: https://github.com/NikolayDachev/ansible_collections  

Requirements
------------

module: [community.routeros.api](https://galaxy.ansible.com/community/routeros)  
role:  
- [nikolaydachev.routeros_api.ros_flush](https://galaxy.ansible.com/nikolaydachev/routeros_api)  
- [nikolaydachev.routeros_api.ros_add](https://galaxy.ansible.com/nikolaydachev/routeros_api)  

Role Variables
--------------

https://docs.ansible.com/ansible/latest/collections/community/routeros/api_module.html  

ros_hostname: "community.routeros.api hostname"  
ros_username: "community.routeros.api username"  
ros_password: "community.routeros.api password"  
ros_ssl: "community.routeros.api ssl", default for this role is set to "true"  

All role variables are combination from role name as prefix, general configuration variable and the the actual RouterOS property.  

Role var prefix: **ros_routing_filter_**  

special var:  
- ros_routing_filter_flush  
  Description: When is set to "true" will flush/remove all rules for routing filter before add new rules

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros routing filter example
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role:  nikolaydachev.routeros_api.ros_routing_filter

# Example inventory for host_vars/
# ---
#   ros_routing_filter_flush: "true"
#   ros_routing_filter:
#     - chain=ospf-out prefix=1.2.3.0/20 action=discard 
#     - chain=ospf-in prefix=3.2.1.0/24 action=discard
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)