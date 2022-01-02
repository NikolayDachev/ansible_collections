ros_caps_man
=========

This general role will configure CAPsMAN via RouterOS API.  
https://help.mikrotik.com/docs/display/ROS/CAPsMAN

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

All role variables are combination from role name as prefix, general configuration variable and the actual RouterOS property.  
With general configuration variable this role can configure only selected RouterOS sub configurations.  

Role var prefix: **ros_caps_man_**  
General configuration variable: **ros_caps_man_config** type list  
Sub configuations:  
  - aaa
  - security
  - access-list
  - rates
  - actual-interface-configuration
  - channel
  - interface
  - datapath
  - configuration
  - provisioning
  - manager

  RouterOS reference: https://help.mikrotik.com/docs/display/ROS/CAPsMAN  

NOTE: Any "-" from RouterOS property is replaced with "_" for example, "client-tx-limit" is "client_tx_limit", if access-list is use, the full var name is "ros_caps_man_access_list_client_tx_limit"  

Full variable list can be found under role defaults.  

Dependencies
------------

n/a

Example Playbook
----------------
```
- name: ros caps-man
  hosts: ros
  gather_facts: no
  connection: local
  ignore_errors: no

  tasks:
    - name: ros caps-man manager
      include_role: 
        name: nikolaydachev.routeros_api.ros_caps_man
      vars:
        ros_caps_man_config:
          - manager
        ros_caps_man_manager_ca_certificate: "ca"
        ros_caps_man_manager_certificate: "auto"
        ros_caps_man_manager_enabled: "yes"
        ros_caps_man_manager_package_path: ""
        ros_caps_man_manager_require_peer_certificate: ""
        ros_caps_man_manager_upgrade_policy: ""

    - name: ros caps-man security
      include_role:
        name: nikolaydachev.routeros_api.ros_caps_man
      vars:
        ros_caps_man_config:
          - security
        ros_caps_man_security_authentication_types: "wpa2-psk"
        ros_caps_man_security_comment: ""
        ros_caps_man_security_copy_from: ""
        ros_caps_man_security_disable_pmkid: "yes"
        ros_caps_man_security_eap_methods: ""
        ros_caps_man_security_eap_radius_accounting: ""
        ros_caps_man_security_encryption: "aes-ccm"
        ros_caps_man_security_group_encryption: "aes-ccm"
        ros_caps_man_security_group_key_update: "1h"
        ros_caps_man_security_passphrase: "{{ vault_ros_caps_man_security_pass_common }}"
        ros_caps_man_security_tls_certificate: ""
        ros_caps_man_security_tls_mode: ""
        ros_caps_man_security_name: "sec1"

    - name: ros caps-man channel
      include_role: 
        name: nikolaydachev.routeros_api.ros_caps_man
      vars:
        ros_caps_man_config:
          - channel
        ros_caps_man_channel_band: "5ghz-onlyac"
        ros_caps_man_channel_comment: ""
        ros_caps_man_channel_control_channel_width: ""
        ros_caps_man_channel_copy_from: ""
        ros_caps_man_channel_extension_channel: "disabled"
        ros_caps_man_channel_frequency: ""
        ros_caps_man_channel_reselect_interval: ""
        ros_caps_man_channel_save_selected: ""
        ros_caps_man_channel_secondary_frequency: ""
        ros_caps_man_channel_skip_dfs_channels: "yes"
        ros_caps_man_channel_tx_power: ""
        ros_caps_man_channel_name: "ac"

    - name: ros caps-man datapath
      include_role: 
        name: nikolaydachev.routeros_api.ros_caps_man
      vars:
        ros_caps_man_config:
          - datapath
        ros_caps_man_datapath_arp: ""
        ros_caps_man_datapath_bridge: ""
        ros_caps_man_datapath_bridge_cost: ""
        ros_caps_man_datapath_bridge_horizon: ""
        ros_caps_man_datapath_client_to_client_forwarding: "yes"
        ros_caps_man_datapath_comment: ""
        ros_caps_man_datapath_copy_from: ""
        ros_caps_man_datapath_interface_list: ""
        ros_caps_man_datapath_l2mtu: ""
        ros_caps_man_datapath_local_forwarding: "yes"
        ros_caps_man_datapath_mtu: ""
        ros_caps_man_datapath_openflow_switch: ""
        ros_caps_man_datapath_vlan_id: "2"
        ros_caps_man_datapath_vlan_mode: "use-tag"
        ros_caps_man_datapath_name: "vlan2-wifi"

    - name: ros caps-man configuration
      include_role: 
        name: nikolaydachev.routeros_api.ros_caps_man
      vars:
        ros_caps_man_config:
          - configuration
        ros_caps_man_configuration_channel: "ac"
        ros_caps_man_configuration_copy_from: ""
        ros_caps_man_configuration_frame_lifetime: ""
        ros_caps_man_configuration_hw_protection_mode: ""
        ros_caps_man_configuration_keepalive_frames: ""
        ros_caps_man_configuration_mode: "ap"
        ros_caps_man_configuration_rx_chains: ""
        ros_caps_man_configuration_ssid: "wifi_ac"
        ros_caps_man_configuration_country: "bulgaria"
        ros_caps_man_configuration_disconnect_timeout: ""
        ros_caps_man_configuration_guard_interval: ""
        ros_caps_man_configuration_hw_retries: ""
        ros_caps_man_configuration_load_balancing_group: ""
        ros_caps_man_configuration_multicast_helper: ""
        ros_caps_man_configuration_security: "sec1"
        ros_caps_man_configuration_tx_chains: ""
        ros_caps_man_configuration_comment: ""
        ros_caps_man_configuration_datapath: "vlan2-wifi"
        ros_caps_man_configuration_distance: "indoor"
        ros_caps_man_configuration_hide_ssid: ""
        ros_caps_man_configuration_installation: "indoor"
        ros_caps_man_configuration_max_sta_count: ""
        ros_caps_man_configuration_rates: ""
        ros_caps_man_configuration_name: "ac"

    - name: ros caps-man interface
      include_role: 
        name: nikolaydachev.routeros_api.ros_caps_man
      vars:
        ros_caps_man_config:
          - interface
        ros_caps_man_interface_arp: ""
        ros_caps_man_interface_channel: ""
        ros_caps_man_interface_comment: ""
        ros_caps_man_interface_datapath: ""
        ros_caps_man_interface_disable_running_check: ""
        ros_caps_man_interface_l2mtu: "1600"
        ros_caps_man_interface_master_interface: "none"
        ros_caps_man_interface_name: "ap01.lan-ac"
        ros_caps_man_interface_radio_name: "ap01.lan-ac"
        ros_caps_man_interface_security: ""
        ros_caps_man_interface_arp_timeout: ""
        ros_caps_man_interface_configuration: "ac"
        ros_caps_man_interface_copy_from: ""
        ros_caps_man_interface_disabled: "no"
        ros_caps_man_interface_mac_address: "2C:C8:1C:8B:A6:A6"
        ros_caps_man_interface_mtu: ""
        ros_caps_man_interface_radio_mac: "2C:C8:1C:8B:A6:A6"
        ros_caps_man_interface_rates: ""

    # This task will flush all acl before next task !
    #- name: ros flush caps-man access-list
    #  import_role:
    #    name: nikolaydachev.routeros_api.ros_flush
    #  vars:
    #    ros_flush_path: "caps-man access-list"
    #    ros_flush_query: ".id"

    - name: ros caps-man access-list
      include_role: 
        name: nikolaydachev.routeros_api.ros_caps_man
      vars:
        ros_caps_man_config:
          - access-list
        ros_caps_man_access_list_action: "reject"
        ros_caps_man_access_list_ap_tx_limit: ""
        ros_caps_man_access_list_client_tx_limit: ""
        ros_caps_man_access_list_copy_from: ""
        ros_caps_man_access_list_interface: ""
        ros_caps_man_access_list_mac_address_mask: ""
        ros_caps_man_access_list_private_passphrase: ""
        ros_caps_man_access_list_signal_range: "-120..-70"
        ros_caps_man_access_list_time: ""
        ros_caps_man_access_list_vlan_mode: ""
        ros_caps_man_access_list_allow_signal_out_of_range: "10s"
        ros_caps_man_access_list_client_to_client_forwarding: "no"
        ros_caps_man_access_list_comment: "signal limit"
        ros_caps_man_access_list_disabled: "no"
        ros_caps_man_access_list_mac_address: ""
        ros_caps_man_access_list_place_before: ""
        ros_caps_man_access_list_radius_accounting: ""
        ros_caps_man_access_list_ssid_regexp: "wifi_ac*"
        ros_caps_man_access_list_vlan_id: ""

    # This task will flush all provisioning before next task !
    #- name: ros flush caps-man provisioning
    #  import_role:
    #    name: nikolaydachev.routeros_api.ros_flush
    #  vars:
    #    ros_flush_path: "caps-man provisioning"
    #    ros_flush_query: ".id"

    - name: ros caps-man provisioning
      include_role: 
        name: nikolaydachev.routeros_api.ros_caps_man
      vars:
        ros_caps_man_config:
          - provisioning
        ros_caps_man_provisioning_action: "create-enabled"
        ros_caps_man_provisioning_comment: ""
        ros_caps_man_provisioning_common_name_regexp: ""
        ros_caps_man_provisioning_copy_from: ""
        ros_caps_man_provisioning_disabled: "no"
        ros_caps_man_provisioning_hw_supported_modes: "ac"
        ros_caps_man_provisioning_identity_regexp: ""
        ros_caps_man_provisioning_ip_address_ranges: ""
        ros_caps_man_provisioning_master_configuration: "ac"
        ros_caps_man_provisioning_name_format: "identity"
        ros_caps_man_provisioning_name_prefix: "ap"
        ros_caps_man_provisioning_place_before: ""
        ros_caps_man_provisioning_radio_mac: ""
        ros_caps_man_provisioning_slave_configurations: ""
```
License
-------

GNU General Public License v3.0 or later.

Author Information
------------------

Nikolay Dachev (@NikolayDachev)