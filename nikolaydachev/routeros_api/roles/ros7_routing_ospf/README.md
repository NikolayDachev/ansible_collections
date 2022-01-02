ros7_routing_ospf
=========

This general role will configure routing ospf via RouterOS API.  
https://help.mikrotik.com/docs/pages/viewpage.action?pageId=328218  

galaxy: https://galaxy.ansible.com/nikolaydachev/routeros_api  
github: https://github.com/NikolayDachev/ansible_collections  

NOTE: Work only for RouterOS 7 !  

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

Role var prefix: **ros7_routing_ospf**  
General configuration variable: **ros7_routing_ospf_config** type list  
Sub configuations:  
  - instance
  - area
  - area_range
  - interface-template
  - static-neighbor

    RouterOS reference: https://help.mikrotik.com/docs/pages/viewpage.action?pageId=328218  


NOTE: Any "-" from RouterOS property is replaced with "_" for example, "area-id" is "area_id", if area is use, the full var name is "ros7_routing_ospf_area_area_id"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros7 routing ospf 
  hosts: ros
  gather_facts: no
  connection: local
  ignore_errors: yes

  tasks:
    - name: (ros7) Add routing ospf instance
      include_role: 
        name: nikolaydachev.routeros_api.ros7_routing_ospf
      vars:
        ros7_routing_ospf_config:
          - instance
        ros7_routing_ospf_instance_comment: ""
        ros7_routing_ospf_instance_disabled: "no"
        ros7_routing_ospf_instance_domain_tag: ""
        ros7_routing_ospf_instance_mpls_te_address: ""
        ros7_routing_ospf_instance_name: "default-v2"
        ros7_routing_ospf_instance_out_filter_chain: "ospf-out"
        ros7_routing_ospf_instance_redistribute: "connected"
        ros7_routing_ospf_instance_routing_table: ""
        ros7_routing_ospf_instance_version: ""
        ros7_routing_ospf_instance_copy_from: ""
        ros7_routing_ospf_instance_domain_id: ""
        ros7_routing_ospf_instance_in_filter_chain: "ospf-in"
        ros7_routing_ospf_instance_mpls_te_area: ""
        ros7_routing_ospf_instance_originate_default: ""
        ros7_routing_ospf_instance_out_filter_select: ""
        ros7_routing_ospf_instance_router_id: ""
        ros7_routing_ospf_instance_use_dn: ""
        ros7_routing_ospf_instance_vrf: ""

    - name: (ros7) Add routing ospf area
      include_role: 
        name: nikolaydachev.routeros_api.ros7_routing_ospf
      vars:
        ros7_routing_ospf_config:
          - area
        ros7_routing_ospf_area_area_id: "0.0.0.0"
        ros7_routing_ospf_area_comment: ""
        ros7_routing_ospf_area_copy_from: ""
        ros7_routing_ospf_area_default_cost: ""
        ros7_routing_ospf_area_disabled: "no"
        ros7_routing_ospf_area_instance: "default-v2"
        ros7_routing_ospf_area_name: "backbone"
        ros7_routing_ospf_area_no_summaries: ""

    # This task will flush all routing ospf interface-templates before next task !
    #- name: ros flush routing ospf interface-template
    #  import_role:
    #    name: nikolaydachev.routeros_api.ros_flush
    #  vars:
    #    ros_flush_path: "routing ospf interface-template"
    #    ros_flush_query: ".id"

    - name: (ros7) Add routing ospf interface-template
      include_role: 
        name: nikolaydachev.routeros_api.ros7_routing_ospf
      vars:
        ros7_routing_ospf_config:
          - interface-template
         ros7_routing_ospf_interface_template_area: "backbone"
         ros7_routing_ospf_interface_template_auth_key: ""
         ros7_routing_ospf_interface_template_cost: ""
         ros7_routing_ospf_interface_template_hello_interval: ""
         ros7_routing_ospf_interface_template_networks: "10.0.0.1/32"
         ros7_routing_ospf_interface_template_prefix_list: ""
         ros7_routing_ospf_interface_template_transmit_delay: ""
         ros7_routing_ospf_interface_template_vlink_transit_area: ""
         ros7_routing_ospf_interface_template_auth: ""
         ros7_routing_ospf_interface_template_comment: "loopback interface"
         ros7_routing_ospf_interface_template_dead_interval: ""
         ros7_routing_ospf_interface_template_instance_id: ""
         ros7_routing_ospf_interface_template_passive: ""
         ros7_routing_ospf_interface_template_priority: ""
         ros7_routing_ospf_interface_template_type: ""
         ros7_routing_ospf_interface_template_auth_id: ""
         ros7_routing_ospf_interface_template_copy_from: ""
         ros7_routing_ospf_interface_template_disabled: "no"
         ros7_routing_ospf_interface_template_interfaces: "loopback"
         ros7_routing_ospf_interface_template_place_before: ""
         ros7_routing_ospf_interface_template_retransmit_interval: ""
         ros7_routing_ospf_interface_template_vlink_neighbor_id: ""
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)