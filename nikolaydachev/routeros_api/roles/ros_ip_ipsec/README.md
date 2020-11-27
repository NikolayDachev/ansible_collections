ros_ip_ipsec
=========

This role will configure RouterOS IPSEC via API.  
https://wiki.mikrotik.com/wiki/Manual:IP/IPsec  

galaxy: https://galaxy.ansible.com/nikolaydachev/routeros_api  
github: https://github.com/NikolayDachev/ansible_collections  

Requirements
------------

module: [community.routeros.api](https://galaxy.ansible.com/community/routeros)  

Role Variables
--------------

https://ansible.fontein.de/collections/community/routeros/api_module.html#ansible-collections-community-routeros-api-module  

ros_hostname: "community.routeros.api hostname"  
ros_username: "community.routeros.api username"  
ros_password: "community.routeros.api password"  
ros_ssl: "community.routeros.api ssl", default for this role is set to "true"  

All role variables are combination from role name as prefix, general configuration variable and the the actual RouterOS property.  
With general configuration variable this role can configure only selected RouterOS sub configurations.  

Role var prefix: **ros_ip_ipsec_**  
General configuration variable: **ros_ip_ipsec_config** type list  
Sub configuations:  
- settings
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/IPsec#Settings

- profile
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/IPsec#Profiles

- peer
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/IPsec#Peers

- key
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/IPsec#Keys

- identity
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/IPsec#Identities

- proposal
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/IPsec#Proposals

- policy_group
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/IPsec#Groups

- mode-config
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/IPsec#Mode_configs

- policy
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/IPsec#Policies

special var:
- ros_ip_ipsec_installed_sa_flush
  Description: When is set to "True" will remove all installed SA
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/IPsec#Installed_SAs

NOTE: Any "-" from RouterOS property is replaced with "_" for example in lease, "sa-dst-address" is "sa_dst_address", so the full var name is "ros_ip_ipsec_policy_sa_dst_address"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros ip ipsec 
  hosts: all
  gather_facts: no
  connection: local

  roles:
#  - role: nikolaydachev.routeros_api.ros_int_ipip
  - role: nikolaydachev.routeros_api.ros_ip_ipsec
    ros_ip_ipsec_config:
#      - settings
      - profile
      - peer
#      - key
      - identity
      - proposal
#      - policy_group
#      - mode-config
      - policy
      # note pilicy will be added on every run!
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)