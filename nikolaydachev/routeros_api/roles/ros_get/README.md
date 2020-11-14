ros_get
=========

This role will return information that's accessible from particular RouterOS command level via API.
https://wiki.mikrotik.com/wiki/Manual:Console
RouterOS "print" 

Result will be registerd to "print_path" and added to output as debug msg.

galaxy: https://galaxy.ansible.com/nikolaydachev/routeros_api
github: https://github.com/NikolayDachev/ansible_collections


Requirements
------------

module: community.routeros.api
        https://galaxy.ansible.com/community/routeros

Role Variables
--------------

https://ansible.fontein.de/collections/community/routeros/api_module.html#ansible-collections-community-routeros-api-module

ros_hostname: "community.routeros.api hostname"
ros_username: "community.routeros.api username"
ros_password: "community.routeros.api password"
ros_ssl: "community.routeros.api ssl", default for this role is set to "true"

ros_get_path: "community.routeros.api path"

Dependencies
------------

n/a

Example Playbook
----------------

- name: ros check current config
  hosts: all
  gather_facts: no
  connection: local

  roles:
  - role: nikolaydachev.routeros_api.ros_get

License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)