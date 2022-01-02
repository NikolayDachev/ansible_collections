ros_ip_dns
=========

This general role will configure DNS via RouterOS API.  
https://help.mikrotik.com/docs/display/ROS/DNS

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
note: _server_ is excluded for server vars(check defaults)!  

Role var prefix: **ros_ip_dns**  
General configuration variable: **ros_ip_dns_config** type list  
Sub configuations:  
- server  
  RouterOS reference: https://help.mikrotik.com/docs/display/ROS/DNS  
- static  
  RouterOS reference: https://help.mikrotik.com/docs/display/ROS/DNS#DNS-DNSStatic  


NOTE: Any "-" from RouterOS property is replaced with "_" for example, "max-udp-packet-size" is "max_udp_packet_size", if server is use, the full var name is "ros_ip_dns_max_udp_packet_size"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros ip dns
  hosts: ros
  gather_facts: no
  connection: local
  ignore_errors: yes

  tasks:
  - name: Configure DNS
    include_role: 
      name: nikolaydachev.routeros_api.ros_ip_dns
    vars:
      ros_ip_dns_config:
        - server
      ros_ip_dns_allow_remote_requests: "yes"
      ros_ip_dns_max_concurrent_queries: ""
      ros_ip_dns_query_server_timeout: ""
      ros_ip_dns_use_doh_server: "https://1.1.1.1/dns-query"
      ros_ip_dns_cache_max_ttl: ""
      ros_ip_dns_max_concurrent_tcp_sessions: ""
      ros_ip_dns_query_total_timeout: ""
      ros_ip_dns_verify_doh_cert: "yes"
      ros_ip_dns_cache_size: ""
      ros_ip_dns_max_udp_packet_size: ""
      ros_ip_dns_servers: ""
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)