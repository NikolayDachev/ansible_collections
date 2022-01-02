ros_ip_neighbor_discovery
=========

This general role will configure ip neighbor discovery via RouterOS API.  
https://help.mikrotik.com/docs/display/ROS/Neighbor+discovery  

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

All role variables are combination from role name as prefix and the actual RouterOS property.  
Role var prefix: **ros_ip_neighbor_discovery_**  

NOTE: Any "-" from RouterOS property is replaced with "_" for example, "lldp-med-net-policy-vlan" is "lldp_med_net_policy_vlan", so the full var name is "ros_ip_neighbor_discovery_lldp_med_net_policy_vlan"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros ip neighbor discovery
  hosts: ros
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_ip_neighbor_discovery
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)