ros_ppp
=========

This general role will configure ppp atributes via RouterOS API.  
  - aaa  
  - l2tp-secret  
  - profile  
  - secret  

https://help.mikrotik.com/docs/display/ROS

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

Role var prefix: **ros_ppp**  
General configuration variable: **ros_ppp_config** type list  
Sub configuations:  
  - aaa  
  - l2tp-secret  
  - profile  
  - secret  

NOTE: Any "-" from RouterOS property is replaced with "_" for example, "change-tcp-mss" is "change_tcp_mss", if profile is use the full var name is "ros_ppp_profile_change_tcp_mss"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros ppp
  hosts: all
  gather_facts: no
  connection: local
  ignore_errors: yes

  tasks:
    - name: Add PPP profile
      include_role: 
        name: nikolaydachev.routeros_api.ros_ppp
      vars:
        ros_ppp_config:
          - profile
        ros_ppp_profile_comment: "added by ansible"
        ros_ppp_profile_name: "test_profile"
        ros_ppp_profile_local_address: "192.168.1.1"
        ros_ppp_profile_remote_address: "192.168.1.2"
        ros_ppp_profile_dns_server: "8.8.8.8"
        ros_ppp_profile_use_encryption: "yes"

    - name: Add PPP secrets
      include_role: 
        name: nikolaydachev.routeros_api.ros_ppp
      vars:
       ros_ppp_config:
         - secret
       ros_ppp_secret_name: "test_secret"
       ros_ppp_secret_password: "SUPER_PASS"
       ros_ppp_secret_profile: "test_profile"
       ros_ppp_secret_service: "any"
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)