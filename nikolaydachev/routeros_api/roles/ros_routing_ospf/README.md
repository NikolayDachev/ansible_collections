ros_routing_ospf
=========
NOTE: This role will not work witn RouterOS v7 !  

This role will configure RouterOS routing ospf via API.  
https://wiki.mikrotik.com/wiki/Manual:Routing/OSPF  

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

Role var prefix: **ros_routing_ospf_**  
General configuration variable: **ros_routing_ospf_config** type list  
Sub configuations:  
- instance:  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Routing/OSPF#Properties  
- area:  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Routing/OSPF#Area  
- area_range:  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Routing/OSPF#Description_2  
- interface:  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Routing/OSPF#Interface  
- network:  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Routing/OSPF#Network  
- nbma_neighbor:  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Routing/OSPF#NBMA_Neighbor  
- sham_link:  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Routing/OSPF#Sham_link  
- virtual_link:  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Routing/OSPF#Virtual_Link

NOTE: Any "-" from RouterOS property is replaced with "_" for example, "area-id" is "area_id", so the full var name is "ros_routing_ospf_area_area_id"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros routing ospf 
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_routing_ospf
    ros_routing_ospf_config:
      - area
#      - area_range
      - instance
#      - interface
#      - nbma_neighbor
      - network
#      - sham_link
#      - virtual_link

    ros_routing_ospf_instance_name: "ros_test"
    ros_routing_ospf_instance_redistribute_connected: "as-type-1"
  
    ros_routing_ospf_area_area_id: "0.0.0.22"
    ros_routing_ospf_area_name: "ros_test"
    ros_routing_ospf_area_instance: "ros_test"
  
    ros_routing_ospf_network_network: "10.20.30.0/30"
    ros_routing_ospf_network_area: "ros_test"
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)