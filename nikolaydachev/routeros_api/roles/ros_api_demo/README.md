ros_api_demo
=========

This role is used only for ansible routeros api module testing and **direct usage is not suggested**, however contains examples for diffrent tasks which can be done with routeros api module  

galaxy: https://galaxy.ansible.com/nikolaydachev/routeros_api  
github: https://github.com/NikolayDachev/ansible_collections  

Requirements
------------

module: [community.routeros.api](https://galaxy.ansible.com/community/routeros)  

Role Variables
--------------

n/a - testing 

Dependencies
------------

n/a

Example Playbook
----------------

```
- name: test role for routeros api 
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_api_demo
```

License
-------

BSD

Author Information
------------------

Nikolay Dachev (@NikolayDachev)  