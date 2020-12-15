ros_ip_ipsec
=========

This role will configure RouterOS Firewall via API.  
https://wiki.mikrotik.com/wiki/Manual:IP/Firewall  

IMPRTATN NOTES!
- Please be extremely careful when you manage firewall rules with any sort of automation!   

- _address_list, _calea, _filter _layer7_protocol, _mangle, _nat and _raw are list vars. Each list item is a rule, rules will be added one by one from first list item to last one (in routeos the order is from top(first list item) to bottom(last list itme))!  

- **ros_ip_firewall_flush** varible will remove all rules selceted in **ros_ip_firewall_config** at once! The main usage is to make more easy firewall rules configuration managment. The flush happen before adding new rules, so for example if you set it to "true" with combination of 'filter' and 'nat', this role will first remove all exsiting rules under 'ip firewall filter' and then will add the new rules also will do the same and for 'ip firewall nat' etc. Can be used as general, so first to remove all exsiting rules before add any type of ip firewall rules.  
As suggestion, different playbooks for different 'ip firewall' sub configurations (**ros_ip_firewall_config**) can be used!  

galaxy: https://galaxy.ansible.com/nikolaydachev/routeros_api  
github: https://github.com/NikolayDachev/ansible_collections  

Requirements
------------

module: [community.routeros.api](https://galaxy.ansible.com/community/routeros)  
role:  
- [nikolaydachev.routeros_api.ros_flush](https://galaxy.ansible.com/nikolaydachev/routeros_api)  
- [nikolaydachev.routeros_api.ros_add](https://galaxy.ansible.com/nikolaydachev/routeros_api)  

Role Variables
--------------

https://docs.ansible.com/ansible/latest/collections/community/routeros/api_module.html  

ros_hostname: "community.routeros.api hostname"  
ros_username: "community.routeros.api username"  
ros_password: "community.routeros.api password"  
ros_ssl: "community.routeros.api ssl", default for this role is set to "true"  

All role variables are combination from role name as prefix, general configuration variable and the the actual RouterOS property.  
With general configuration variable this role can configure only selected RouterOS sub configurations.  

Role var prefix: **ros_ip_firewall_**  
General configuration variable: **ros_ip_firewall_config** type list  
Sub configuations:  
- address-list:  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/Firewall/Address_list  

- service-port  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/Services#Service_Ports  

- nat  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/Firewall/NAT  

- raw  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/Firewall/Raw  

- filter  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/Firewall/Filter  

- calea  
  RouterOS reference: https://wiki.mikrotik.com/wiki/CALEA  

- layer7-protocol  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/Firewall/L7  

- mangle  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/Firewall/Mangle  

- connection-tracking  
  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:IP/Firewall/Connection_tracking  

special var:  
- ros_ip_firewall_flush  
  Description: When is set to "true" will flush/remove all rules for the current subconfig before add new rules

NOTE: Any "-" from RouterOS property is replaced with "_" for example, "tcp-max-retrans-timeout" is "tcp_max_retrans_timeout", so the full var name is "ros_ip_firewall_connection_tracking_tcp_max_retrans_timeout"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros ip firewall example
  hosts: all
  gather_facts: no
  connection: local

  tasks:
    - name: Firewall General Config
      include_role: 
        name: nikolaydachev.routeros_api.ros_ip_firewall
      vars:
        ros_ip_firewall_config:
          - settings
          - connection-tracking
        ros_ip_firewall_service_port_name: "sctp"
        ros_ip_firewall_service_port_disabled: "yes"
        ros_ip_firewall_service_port_ports: ""

        ros_ip_firewall_connection_tracking_tcp_time_wait_timeout: "20s"

    - name: Firewall Config rules
      include_role: 
        name: nikolaydachev.routeros_api.ros_ip_firewall
      vars:
        ros_ip_firewall_config: "{{ item.ros_ip_firewall_config }}"
        ros_ip_firewall_flush: "{{ item.ros_ip_firewall_flush }}"

        ros_ip_firewall_filter: "{{ item.ros_ip_firewall_filter }}"
        ros_ip_firewall_nat: "{{ item.ros_ip_firewall_nat }}"
        ros_ip_firewall_raw: "{{ item.ros_ip_firewall_raw }}"

      loop:
        "{{ ros_ip_firewall_rules }}"


# Example inventory for host_vars/
# ---
# ros_ip_firewall_rules:
#   - ros_ip_firewall_config:
#       - filter
#     ros_ip_firewall_flush: "true"
#     ros_ip_firewall_filter:
#       - action=accept chain=forward connection-state=established,related,untracked
#       - action=accept chain=forward protocol=icmpv6
#       - action=accept chain=forward protocol=139
#       - action=accept chain=forward protocol=udp dst-port=500,4500
#       - action=accept chain=forward protocol=ipsec-ah
#       - action=accept chain=forward protocol=ipsec-esp
# 
#   - ros_ip_firewall_config:
#       - nat
#     ros_ip_firewall_flush: "true"
#     ros_ip_firewall_nat:
#       - chain=srcnat action=masquerade out-interface=ether1 ipsec-policy=out,none
# 
#   - ros_ip_firewall_config:
#       - raw
#     ros_ip_firewall_flush: "true"
#     ros_ip_firewall_raw:
#       - action=accept chain=input
#       - action=drop chain=input
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)