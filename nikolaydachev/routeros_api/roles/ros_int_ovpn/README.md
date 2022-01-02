ros_int_ovpn
=========

This general role will configure openvpn server/client via RouterOS API.  
https://help.mikrotik.com/docs/display/ROS/OpenVPN

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

All role variables are combination from role name as prefix, general configuration variable and the actual RouterOS property.  
With general configuration variable this role can configure only selected RouterOS sub configurations.  

Role var prefix: **ros_int_ovpn_**  
General configuration variable: **ros_int_ovpn_config** type list  
Sub configuations:  
- server_user_int  
  RouterOS reference: https://help.mikrotik.com/docs/display/ROS/OpenVPN#OpenVPN-OVPNServer  
- server  
  RouterOS reference: https://help.mikrotik.com/docs/display/ROS/OpenVPN#OpenVPN-OVPNServer  
- client  
  RouterOS reference: https://help.mikrotik.com/docs/display/ROS/OpenVPN#OpenVPN-OVPNClient  


NOTE: Any "-" from RouterOS property is replaced with "_" for example, "server-default-profile" is "server_server_default_profile", if server is use, the full var name is "ros_int_ovpn_server_server_default_profile"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros interface ovpn
  hosts: ros
  gather_facts: no
  connection: local
  ignore_errors: yes

  tasks:
    - name: Add interface ovpn-client
      include_role: 
        name: nikolaydachev.routeros_api.ros_int_ovpn
      vars:
        ros_int_ovpn_config:
          - client
        ros_int_ovpn_client_add_default_route: ""
        ros_int_ovpn_client_auth: "sha1"
        ros_int_ovpn_client_certificate: "vpn.user1"
        ros_int_ovpn_client_cipher: "aes256"
        ros_int_ovpn_client_comment: "open vpn user1"
        ros_int_ovpn_client_copy_from: ""
        ros_int_ovpn_client_disabled: "no"
        ros_int_ovpn_client_mac_address: ""
        ros_int_ovpn_client_max_mtu: ""
        ros_int_ovpn_client_mode: "ip"
        ros_int_ovpn_client_name: "ovpn-user1"
        ros_int_ovpn_client_password: "SUPER_PASSWORD"
        ros_int_ovpn_client_port: "1194"
        ros_int_ovpn_client_profile: "default"
        ros_int_ovpn_client_use_peer_dns: ""
        ros_int_ovpn_client_verify_server_certificate: ""
        ros_int_ovpn_client_connect_to: "vpn.server.com"
        ros_int_ovpn_client_user: "user1"

    - name: interface ovpn-server
      include_role: 
        name: nikolaydachev.routeros_api.ros_int_ovpn
      vars:
        ros_int_ovpn_config:
          - server
        ros_int_ovpn_server_server_auth: "sha1"
        ros_int_ovpn_server_server_certificate: "vpn-server"
        ros_int_ovpn_server_server_cipher: "aes256"
        ros_int_ovpn_server_server_default_profile: "vpn-users-encryption"
        ros_int_ovpn_server_server_enabled: "yes"
        ros_int_ovpn_server_server_keepalive_timeout: ""
        ros_int_ovpn_server_server_mac_address: ""
        ros_int_ovpn_server_server_max_mtu: ""
        ros_int_ovpn_server_server_mode: "ip"
        ros_int_ovpn_server_server_netmask: "24"
        ros_int_ovpn_server_server_port: "1194"
        ros_int_ovpn_server_server_require_client_certificate: "yes"
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)