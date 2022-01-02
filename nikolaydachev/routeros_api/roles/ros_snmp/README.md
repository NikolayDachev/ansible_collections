ros_snmp
=========

This general role will configure snmp via RouterOS API.  
https://help.mikrotik.com/docs/display/ROS/SNMP  

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

Role var prefix: **ros_snmp_**  
General configuration variable: **ros_snmp_config** type list  
Sub configuations:  
- community  
  RouterOS reference: https://help.mikrotik.com/docs/display/ROS/SNMP  
- snmp  
  RouterOS reference: https://help.mikrotik.com/docs/display/ROS/SNMP  

NOTE: Any "-" from RouterOS property is replaced with "_" for example, "engine-id" is "engine_id", so the full var name is "ros_snmp_engine_id"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros snmp
  hosts: ros
  gather_facts: no
  connection: local
  ignore_errors: yes

  tasks:
    - name: add snmp community
      include_role: 
        name: nikolaydachev.routeros_api.ros_snmp
      vars:
        ros_snmp_config:
          - community
        ros_snmp_community_addresses: "192.168.1.1"
        ros_snmp_community_authentication_protocol: "SHA1"
        ros_snmp_community_copy_from: ""
        ros_snmp_community_encryption_password: "{{ vault_ros_snmp_pwd }}"
        ros_snmp_community_name: "mycommunity"
        ros_snmp_community_security: "private"
        ros_snmp_community_authentication_password: "{{ vault_ros_snmp_pwd }}"
        ros_snmp_community_comment: ""
        ros_snmp_community_disabled: "no"
        ros_snmp_community_encryption_protocol: "AES"
        ros_snmp_community_read_access: "yes"
        ros_snmp_community_write_access: "no"

    - name: configure snmp
      include_role: 
        name: nikolaydachev.routeros_api.ros_snmp
      vars:
        ros_snmp_config:
          - snmp
        ros_snmp_contact: "snmp@domain.com"
        ros_snmp_engine_id: ""
        ros_snmp_src_address: ""
        ros_snmp_trap_generators: ""
        ros_snmp_trap_target: ""
        ros_snmp_enabled: "yes"
        ros_snmp_location: "Office1"
        ros_snmp_trap_community: "mycommunity"
        ros_snmp_trap_interfaces: ""
        ros_snmp_trap_version: "3"
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)