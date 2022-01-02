ros_int_sstp
=========

This general role will configure SSTP server/client via RouterOS API.  
https://help.mikrotik.com/docs/display/ROS/SSTP  

galaxy: https://galaxy.ansible.com/nikolaydachev/routeros_api  
github: https://github.com/NikolayDachev/ansible_collections  

NOTE: "force-aes" is missing in ros7, if is needed for ros6 please uncomment it in ./tasks/server.yml  
```
    #force-aes="{{ ros_int_sstp_server_server_force_aes }}"  
```

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

Role var prefix: **ros_int_sstp**  
General configuration variable: **ros_int_sstp_config** type list  
Sub configuations:  
- server_user_int  
  RouterOS reference: https://help.mikrotik.com/docs/display/ROS/SSTP  
- server  
  RouterOS reference: https://help.mikrotik.com/docs/display/ROS/SSTP  
- client  
  RouterOS reference: https://help.mikrotik.com/docs/display/ROS/SSTP  


NOTE: Any "-" from RouterOS property is replaced with "_" for example, "server-tls-version" is "server_tls_version", if server is use, the full var name is "ros_int_sstp_server_server_tls_version"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros interface sstp
  hosts: ros
  gather_facts: no
  connection: local
  ignore_errors: yes

  tasks:
    - name: interface sstp-server
      include_role: 
        name: nikolaydachev.routeros_api.ros_int_sstp
      vars:
        ros_int_sstp_config:
          - server
        ros_int_sstp_server_server_authentication: "mschap2"
        ros_int_sstp_server_server_certificate: "vpn-server"
        ros_int_sstp_server_server_default_profile: "vpn-users-encryption"
        ros_int_sstp_server_server_enabled: "yes"
        ros_int_sstp_server_server_force_aes: "yes"
        ros_int_sstp_server_server_keepalive_timeout: ""
        ros_int_sstp_server_server_max_mru: ""
        ros_int_sstp_server_server_max_mtu: ""
        ros_int_sstp_server_server_mrru: ""
        ros_int_sstp_server_server_pfs: "yes"
        ros_int_sstp_server_server_port: "443"
        ros_int_sstp_server_server_tls_version: ""
        ros_int_sstp_server_server_verify_client_certificate: ""
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)