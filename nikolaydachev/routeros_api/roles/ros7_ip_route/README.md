ros7_ip_route
=========

This general role will configure ip route via RouterOS API.  
https://wiki.mikrotik.com/wiki/Manual:IP/Route

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

All role variables are combination from role name as prefix and the actual RouterOS property.  
Role var prefix: **ros_ip_route_**  

NOTE: Any "-" from RouterOS property is replaced with "_" for example, "dst-address" is "dst_address", so the full var name is "ros_ip_route_dst_address"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros7 ip route
  hosts: ros
  gather_facts: no
  connection: local
  ignore_errors: no

  tasks:
    - name: (ros7) Add ip route
      include_role: 
        name: nikolaydachev.routeros_api.ros7_ip_route
      vars:
        ros_ip_route_blackhole: ""
        ros_ip_route_comment: "FO - 4G"
        ros_ip_route_disabled: "no"
        ros_ip_route_dst_address: "8.8.4.4/32"
        ros_ip_route_pref_src: ""
        ros_ip_route_scope: "11"
        ros_ip_route_target_scope: "10"
        ros_ip_route_check_gateway: ""
        ros_ip_route_copy_from: ""
        ros_ip_route_distance: "1"
        ros_ip_route_gateway: "192.168.8.1"
        ros_ip_route_routing_table: ""
        ros_ip_route_suppress_hw_offload: ""
        ros_ip_route_vrf_interface: ""
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)