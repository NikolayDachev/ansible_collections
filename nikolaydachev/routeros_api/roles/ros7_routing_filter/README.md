ros7_routing_filter
=========

This general role will configure routing filter via RouterOS API.  
https://help.mikrotik.com/docs/pages/viewpage.action?pageId=74678285  

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

Role var prefix: **ros7_routing_filter**  
General configuration variable: **ros7_routing_filter_config** type list  
Sub configuations:  
  - rule  
  - select-rule  
  - num-set  
  - community-set  
  - community-ext-set  
  - community-large-set  

    RouterOS reference: https://help.mikrotik.com/docs/pages/viewpage.action?pageId=74678285  


NOTE: Any "-" from RouterOS property is replaced with "_" for example, "do-group-num" is "do_group_num", if select-rule is use, the full var name is "ros7_routing_filter_select_rule_do_group_num"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros7 routing filter
  hosts: ros
  gather_facts: no
  connection: local
  ignore_errors: no

  tasks:
    # This task will flush all routing filters before next task !
    #- name: ros routing filter rule
    #  import_role:
    #    name: nikolaydachev.routeros_api.ros_flush
    #  vars:
    #    ros_flush_path: "routing filter rule"
    #    ros_flush_query: ".id"

    - name: (ros7) Add routing filter rule
      include_role: 
        name: nikolaydachev.routeros_api.ros7_routing_filter
      vars:
        ros7_routing_filter_config:
          - rule
        ros7_routing_filter_rule_chain: "ospf-out"
        ros7_routing_filter_rule_comment: "Default accept ospf-out"
        ros7_routing_filter_rule_copy_from: ""
        ros7_routing_filter_rule_disabled: "no"
        ros7_routing_filter_rule_place_before: ""
        ros7_routing_filter_rule_rule: "if (dst in 0.0.0.0/0) {accept}"
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)