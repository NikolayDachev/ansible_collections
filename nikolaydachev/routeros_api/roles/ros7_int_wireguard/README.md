ros7_int_wireguard
=========

This general role will configure wireguard via RouterOS API.  
https://help.mikrotik.com/docs/display/ROS/WireGuard

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

Role var prefix: **ros7_int_wireguard**  
General configuration variable: **ros7_int_wireguard_config** type list  
Sub configuations:  
  - add
  - peers

    RouterOS reference: https://help.mikrotik.com/docs/display/ROS/WireGuard  


NOTE: Any "-" from RouterOS property is replaced with "_" for example, "endpoint-address" is "endpoint_address", if peers is use, the full var name is "ros7_int_wireguard_peers_endpoint_address"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros7 interface wireguard
  hosts: ros
  gather_facts: no
  connection: local
  ignore_errors: yes

  tasks:
    - name: (ros7) Add interface wireguard
      include_role: 
        name: nikolaydachev.routeros_api.ros7_int_wireguard
      vars:
        ros7_int_wireguard_config:
          - add
        ros7_int_wireguard_copy_from: ""
        ros7_int_wireguard_disabled: "no"
        ros7_int_wireguard_listen_port: "51820"
        ros7_int_wireguard_mtu: "1420"
        ros7_int_wireguard_name: "wireguard-rw"
        ros7_int_wireguard_private_key: "{{ vault_ros_wg_prvkey }}"

    - name: (ros7) Add interface wireguard peers
      include_role: 
        name: nikolaydachev.routeros_api.ros7_int_wireguard
      vars:
        ros7_int_wireguard_config:
          - peers
        ros7_int_wireguard_peers_allowed_address: "0.0.0.0/0"
        ros7_int_wireguard_peers_comment: "wg_peer1"
        ros7_int_wireguard_peers_copy_from: ""
        ros7_int_wireguard_peers_disabled: "no"
        ros7_int_wireguard_peers_endpoint_address: ""
        ros7_int_wireguard_peers_endpoint_port: ""
        ros7_int_wireguard_peers_interface: "wireguard-rw"
        ros7_int_wireguard_peers_persistent_keepalive: ""
        ros7_int_wireguard_peers_place_before: ""
        ros7_int_wireguard_peers_preshared_key: ""
        ros7_int_wireguard_peers_public_key: "BLABLABLALBALABLABLAJSnNJgAI+imVh4="
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)