ros_int_bridge
=========

This role will configure RouterOS interface bridge via API.  
https://wiki.mikrotik.com/wiki/Manual:Interface/Bridge  

IMPRTATN NOTES!
- Please be extremely careful when you manage bridge filter rules with any sort of automation!   

- _calea, _filter and _nat are list vars. Each list item is a rule, rules will be added one by one from first list item to last one (in routeos the order is from top(first list item) to bottom(last list itme))!  

- **ros_int_bridge_acl_flush** varible will remove all rules selceted in **ros_int_bridge_config** (calea, filter and nat) at once! The main usage is to make more easy bridge filter rules configuration managment. The flush happen before adding new rules, so for example if you set it to "true" with combination of 'filter' and 'nat', this role will first remove all exsiting rules under 'interface brige filter' and then will add the new rules also will do the same and for 'interface brige nat' etc. Can be used as general, so first to remove all exsiting rules before add any type of interface brige calea, filter or nat rules.  
As suggestion, different playbooks for different 'interface brige calea, filter or nat' sub configurations (**ros_int_bridge_config**) can be used!  

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
With general configuration variable this role can configure only selected RouterOS sub configurations.  

Role var prefix: **ros_int_bridge_**  
General configuration variable: **ros_int_bridge_config** type list  
Sub configuations:  
- add  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Interface/Bridge#Properties  

- host  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Interface/Bridge#Hosts_Table  

- mdb  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Interface/Bridge#IGMP_Snooping  

- msti  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Spanning_Tree_Protocol#Multiple_Spanning_Tree_Protocol  

- port-controller  
  RouterOS reference: https://help.mikrotik.com/docs/display/ROS/Controller+Bridge+and+Port+Extender  

- port-controller_device  
  RouterOS reference: https://help.mikrotik.com/docs/display/ROS/Controller+Bridge+and+Port+Extender  

- port-controller_path  
  RouterOS reference: https://help.mikrotik.com/docs/display/ROS/Controller+Bridge+and+Port+Extender  

- port-extender  
  RouterOS reference: https://help.mikrotik.com/docs/display/ROS/Controller+Bridge+and+Port+Extender    

- port  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Interface/Bridge#Port_Settings  

- settings  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Interface/Bridge#Bridge_Settings  

- vlan  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Interface/Bridge#Bridge_VLAN_Filtering

- calea  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Interface/Bridge#Bridge_Firewall  

- filter  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Interface/Bridge#Bridge_Firewall  

- nat  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Interface/Bridge#Bridge_Firewall  

special var:  
- ros_int_bridge_acl_flush  
  Description: When is set to "true" will flush/remove all rules for calea, filter or nat subconfigs before add new rules

NOTE: Any "-" from RouterOS property is replaced with "_" for example, "last-member-interval" is "last_member_interval", so the full var name is "ros_int_bridge_last_member_interval"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros interface bridge example
  hosts: all
  gather_facts: no
  connection: local

  tasks:
    - name: Bridge Config
      include_role: 
        name: nikolaydachev.routeros_api.ros_int_bridge
      vars:
        ros_int_bridge_config: "{{ item.ros_int_bridge_config }}"

        ros_int_bridge_name: "{{ item.ros_int_bridge_name }}"

        ros_int_bridge_port_bridge: "{{ item.ros_int_bridge_port_bridge }}"
        ros_int_bridge_port_interface: "{{ item.ros_int_bridge_port_interface }}"

        ros_int_bridge_vlan_bridge: "{{ item.ros_int_bridge_vlan_bridge }}"
        ros_int_bridge_vlan_untagged: "{{ item.ros_int_bridge_vlan_untagged }}"
        ros_int_bridge_vlan_vlan_ids: "{{ item.ros_int_bridge_vlan_vlan_ids }}"

        ros_int_bridge_acl_flush: "{{ item.ros_int_bridge_acl_flush }}"
        ros_int_bridge_filter: "{{ item.ros_int_bridge_filter }}"

      loop:
        "{{ ros_int_bridge }}"

# Example inventory for host_vars/
# ---
# ros_int_bridge:
#   - ros_int_bridge_config:
#       - add
#     ros_int_bridge_name: "loopback"
# 
#   - ros_int_bridge_config:
#       - add
#       - port
#       - vlan
#     ros_int_bridge_name: "lan_br"
# 
#     ros_int_bridge_port_bridge: "lan_br"
#     ros_int_bridge_port_interface: "ether3"
# 
#     ros_int_bridge_vlan_bridge: "lan_br"
#     ros_int_bridge_vlan_untagged: "ether4"
#     ros_int_bridge_vlan_vlan_ids: "12"
# 
#   - ros_int_bridge_config:
#       - port
#     ros_int_bridge_port_bridge: "lan_br"
#     ros_int_bridge_port_interface: "ether4"
# 
#   - ros_int_bridge_config:
#       - filter
#     ros_int_bridge_acl_flush: "true"
#     ros_int_bridge_filter:
#       - chain=forward action=accept in-interface=ether3
#       - chain=forward action=drop in-interface=ether4
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)