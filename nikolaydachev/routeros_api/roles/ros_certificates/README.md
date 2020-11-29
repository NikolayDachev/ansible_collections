ros_certificates
=========

This role will configure RouterOS certificates via API.  
https://wiki.mikrotik.com/wiki/Manual:System/Certificates  

note: SCEP not supported yet!  

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

Role var prefix: **ros_certificates_**  
General configuration variable: **ros_certificates_config** type list  
Sub configuations:  
- add
- sign
- create-certificate-request
- sign-certificate-request
- crl
- export-certificate
- import
- issued-revoke
- settings

  RouterOS reference: https://wiki.mikrotik.com/wiki/Manual:Create_Certificates  

NOTE: Any "-" from RouterOS property is replaced with "_" for example, "add-days-valid" is "add_days_valid", so the full var name is "ros_certificates_add_days_valid"  

Full variable list can be found under role defaults.  

**Example Vars**  
```
---
ros_certs:
# ca
    - ros_certificates_add_common_name: "CA"
      ros_certificates_add_country: "BG"
      ros_certificates_add_days_valid: "365"
      ros_certificates_add_key_size: "2048"
      ros_certificates_add_key_usage: "key-cert-sign,crl-sign"
      ros_certificates_add_name: "CA"
      ros_certificates_add_organization: "DACHEV"
      ros_certificates_add_state: "SOFIA"
      ros_certificates_add_subject_alt_name: ""
      ros_certificates_add_trusted: "yes"

      ros_certificates_sign_ca: ""
      ros_certificates_sign_number: "CA"

# clients
    - ros_certificates_add_common_name: "ros1"
      ros_certificates_add_country: "BG"
      ros_certificates_add_days_valid: "365"
      ros_certificates_add_key_size: "2048"
      ros_certificates_add_key_usage: "tls-client"
      ros_certificates_add_name: "ros1"
      ros_certificates_add_organization: "DACHEV"
      ros_certificates_add_state: "SOFIA"
      ros_certificates_add_subject_alt_name: "IP:192.168.1.1"
      ros_certificates_add_trusted: "yes"

      ros_certificates_sign_ca: "CA"
      ros_certificates_sign_number: "ros1"

    - ros_certificates_add_common_name: "ros2"
      ros_certificates_add_country: "BG"
      ros_certificates_add_days_valid: "365"
      ros_certificates_add_key_size: "2048"
      ros_certificates_add_key_usage: "tls-client"
      ros_certificates_add_name: "ros2"
      ros_certificates_add_organization: "DACHEV"
      ros_certificates_add_state: "SOFIA"
      ros_certificates_add_subject_alt_name: "IP:192.168.1.2"
      ros_certificates_add_trusted: "yes"

      ros_certificates_sign_ca: "CA"
      ros_certificates_sign_number: "ros2"

```

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros certificates 
  hosts: all
  gather_facts: no
  connection: local

  tasks:
    - name: Generate Certs
      include_role: 
        name: nikolaydachev.routeros_api.ros_certificates
      vars:
        ros_certificates_config:
          - add
          - sign
#           - create-certificate-request
#           - sign-certificate-request
#           - crl
#           - export-certificate
#           - import
#           - issued-revoke
#           - settings
    
        ros_certificates_add_common_name: "{{ item.ros_certificates_add_common_name }}"
        ros_certificates_add_country: "{{ item.ros_certificates_add_country }}"
        ros_certificates_add_days_valid: "{{ item.ros_certificates_add_days_valid }}"
        ros_certificates_add_key_size: "{{ item.ros_certificates_add_key_size }}"
        ros_certificates_add_key_usage: "{{ item.ros_certificates_add_key_usage }}"
        ros_certificates_add_name: "{{ item.ros_certificates_add_name }}"
        ros_certificates_add_organization: "{{ item.ros_certificates_add_organization }}"
        ros_certificates_add_state: "{{ item.ros_certificates_add_state }}"
        ros_certificates_add_subject_alt_name: "{{ item.ros_certificates_add_subject_alt_name }}"
        ros_certificates_add_trusted: "{{ item.ros_certificates_add_trusted }}"
    
        ros_certificates_sign_ca: "{{ item.ros_certificates_sign_ca }}"
        ros_certificates_sign_number: "{{ item.ros_certificates_sign_number }}"
    
      loop:
        "{{ ros_certs }}"
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)