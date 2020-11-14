ros_ip_dchp_server
=========

This role will configure RouterOS DHCP Server via API.
https://wiki.mikrotik.com/wiki/Manual:IP/DHCP_Server

galaxy: https://galaxy.ansible.com/nikolaydachev/routeros_api
github: https://github.com/NikolayDachev/ansible_collections

Requirements
------------

module: community.routeros.api
        https://galaxy.ansible.com/community/routeros
role: role: nikolaydachev.routeros_api.ros_ip_pool
      https://galaxy.ansible.com/nikolaydachev/routeros_api

Role Variables
--------------

https://ansible.fontein.de/collections/community/routeros/api_module.html#ansible-collections-community-routeros-api-module

ros_hostname: "community.routeros.api hostname"
ros_username: "community.routeros.api username"
ros_password: "community.routeros.api password"
ros_ssl: "community.routeros.api ssl", default for this role is set to "true"

All role variables are combination from role name as prefix, general configuration variable and the the actual RouterOS property. With general configuration variable this role can configure only selected RouterOS sub configurations.

Role var prefix: "ros_ip_dchp_server_"
General configuration variable: "ros_ip_dhcp_server_config"
Sub configuations:
- network
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/DHCP_Server#Networks

- server
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/DHCP_Server#General

- lease
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/DHCP_Server#Properties

- options
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/DHCP_Server#Properties_3
  
- vci
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/DHCP_Server#Vendor_Classes


NOTE: Any "-" from RouterOS property is replaced with "_" for example in lease, "address-lists" is "address_lists", so the full var name is "ros_ip_dhcp_server_lease_address_lists"

Full variable list can be found under role defaults.

Dependencies
------------

n/a

Example Playbook
----------------

- name: ros dhcp server 
  hosts: all
  gather_facts: no
  connection: local

  roles:
#  - role: nikolaydachev.routeros_api.ros_ip_pool
  - role: nikolaydachev.routeros_api.ros_ip_dhcp_server
    ros_ip_dhcp_server_config:
      - network
      - server
#      - lease
#      - options
#      - vci

License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)