VXLAN role
========

This role facilitates the configuration of  virtual extensible LAN (VXLAN)   attributes. It supports the configuration of Virtual Networks, Ethernet Virtual Private Network (evpn) and Network Virtualization Edge (nve). This role is abstracted for dellos10 device.

The VXLAN role requires an SSH connection for connectivity to a Dell EMC Networking device. You can use any of the built-in OS connection variables.

Installation
------------

    ansible-galaxy install Dell-Networking.dellos_vxlan

Role variables
--------------
 
- Role is abstracted using the *ansible_network_os* variable that can take dellos10 values
- If variable *dellos_cfg_generate* is set to true, it generates the role configuration commands in a file
- Any role variable with a corresponding state variable setting to absent negates the configuration of that variable
- Setting an empty value for any variable negates the corresponding configuration
- Variables and values are case-sensitive

**dellos_vxlan keys**

| Key        | Type                      | Description                                             | Support               |
|------------|---------------------------|---------------------------------------------------------|-----------------------|
| ``anycast_gateway_mac`` | string | Configures an anycast gateway IP address for a VXLAN virtual network | dellos10 |
| ``loopback`` | dictionary | Configures the loopback interface (see ``loopback.*``) | dellos10 |
| ``loopback.loopback_id`` | integer | Configures the loopback interface number  0 to 16383 | dellos10 |
| ``loopback.description`` | string | Configures the interface description | dellos10 |
| ``loopback.ip_address`` | string | Configure the ip address | dellos10 |
| ``loopback.state`` | string: absent,present\* | Removes loopback interface if set to absent | dellos10 |
| ``nve`` | dictionary | Configures Network Virtualization Edge (see ``nve.*``) | dellos10 |
| ``nve.source_interface`` | integer | Configures source loopback interface | dellos10 |
| ``nve.controller`` | dictionary | Configures controller (OS10 supports only one controller connection at a time)(see ``controller.*``)  | dellos10 |
| ``controller.name`` | string: NSX, ovsdb | Configures the nve controller | dellos10 |
| ``controller.max_backoff`` | integer | Configures max_backoff value (Setting an empty value negates the corresponding configuration) | dellos10 |
| ``controller.control_cfg`` | list | Configures the controller ip and port (see ``control_cfg.*``) | dellos10 |
| ``control_cfg.ip_addr`` | string | Configures the controller ip | dellos10 |
| ``control_cfg.port`` | integer | Configures the controller port | dellos10 |
| ``control_cfg.state`` | string: absent,present\* | Removes the controller ip and port configuration if set to absent   | dellos10 |
| ``controller.state`` | string: absent,present\* | Removes the controller if set to absent | dellos10 |
| ``nve.state`` | string: absent,present\* | Removes the Network Virtualization Edge if set to absent | dellos10 |
| ``evpn`` | dictionary | Enable the evpn in control plane (see ``evpn.*``)  | dellos10 |
| ``evpn.autoevi`` | boolean: True, False | Configures auto-evi (No further manual configuration is allowed in auto-EVI mode) | dellos10 |
| ``evpn.evi`` | list | Configures EVPN instance (see ``evi.*``)| dellos10 |
| ``evi.id`` | integer | Configures the EVPN instance id (The range is from 1 to 65535) | dellos10 |
| ``evi.rd`` | string |  Configure the Route  Distinguisher | dellos10 |
| ``evi.vni`` | dictionary | Configures vni value (see ``vni.*``) | dellos10 |
| ``vni.id`` | integer | Configures vni value (You must configure the same VNI value that you configure for the VXLAN virtual network) | dellos10 |
| ``vni.state`` | string: absent,present\* | Removes the vni if set to absent | dellos10 |
| ``evi.route_target`` | list | Configures route target (see ``route_target.*``) | dellos10 |
| ``route_target.type`` | string: manual,auto  | Configures the route target (auto mode auto-configures an import and export value for EVPN routes) | dellos10 |
| ``route_target.asn_value`` | string | Configures the route target asn value | dellos10 |
| ``route_target.route_target_type`` | string: import,export,both  | Configures the route target type | dellos10 |
| ``route_target.state`` | string: absent,present\* | Removes the route target if set to absent  | dellos10 |
| ``evi.state`` | string: absent,present\*     | Removes EVPN instance id if set to absent  | dellos10 |
| ``evpn.state`` | string: absent,present\* | Removes the EVPN configuration if set to absent | dellos10 |
| ``virtual_network`` | dictionary | Configures the virtual network attributes (see ``virtual_network.*``) | dellos10 |
| ``virtual_network.untagged_vlan`` | integer  | Configures the  reserved untagged VLAN ID, from 1 to 4093  | dellos10 |
| ``virtual_network.virtual_net`` | list  | Configures the virtual network attributes for VXLAN tunneling (see ``virtual_net.*``) | dellos10 |
| ``virtual_net.id`` | integer | Configures a virtual network ( virtual-network ID, from 1 to 65535) | dellos10 |
| ``virtual_net.description`` | string | Configures the Description for Virtual Network | dellos10 |
| ``virtual_net.vlt_vlan_id`` | integer | Configures  VLTi VLAN ID | dellos10 |
| ``virtual_net.member_interface`` | list | Configures the trunk member interface attributes to the virtual network (see ``member_interface.*``) | dellos10 |
| ``member_interface.ifname`` | string | Configures interface name to provision the virtual network member interface |  dellos10 |
| ``member_interface.type`` | string: tagged,untagged | Configures the type to provision the virtual network member interface |  dellos10 |
| ``member_interface.vlanid`` | integer | Configures the VLAN ID to provision the virtual network member interface |  dellos10 |
| ``member_interface.state`` | string: absent,present\* | Removes the virtual network member interface if set to absent  |  dellos10 |
| ``virtual_net.vxlan_vni`` | dictionary | Configures the  VXLAN attributes to  virtual network (see ``vxlan_vni.*``) | dellos10 |
| ``vxlan_vni.id`` | integer | Configures the VXLAN ID to a virtual network   | dellos10 |
| ``vxlan_vni.remote_endpoint`` | list | Configures the IP address of a remote tunnel endpoint in a VXLAN network (see ``remote_endpoint.*``) | dellos10 |
| ``remote_endpoint.ip`` | string | Configures the IP address of a remote tunnel endpoint (1.1.1.1)  | dellos10 |
| ``remote_endpoint.state`` | string: absent,present\* | Removes the remote tunnel endpoint in a VXLAN network if set to absent | dellos10 |
| ``vxlan_vni.state`` | string: absent,present\* | Removes the VXLAN ID if set to absent   | dellos10 |
| ``virtual_net.state`` | string: absent,present\* | Removes a virtual network if set to absent | dellos10 |
| ``vlan_association`` | list | Configures the  vlan association with virtual network  (see ``vlan_association.*``) | dellos10 |
| ``vlan_association.vlan_id`` | integer | Specifies the VLAN ID    | dellos10 |
| ``vlan_association.virtual_net`` | integer | Specifies the virtual netwrok id which is to be associated with vlan  | dellos10 |


> **NOTE**: Asterisk (\*) denotes the default value if none is specified.

Connection variables
--------------------

Ansible Dell EMC Networking roles require connection information to establish communication with the nodes in your inventory. This information can exist in the Ansible *group_vars* or *host_vars* directories or inventory, or in the playbook itself.

| Key         | Required | Choices    | Description                                         |
|-------------|----------|------------|-----------------------------------------------------|
| ``ansible_host`` | yes      |            | Specifies the hostname or address for connecting to the remote device over the specified transport |
| ``ansible_port`` | no       |            | Specifies the port used to build the connection to the remote device; if value is unspecified, the ANSIBLE_REMOTE_PORT option is used; it defaults to 22 |
| ``ansible_ssh_user`` | no       |            | Specifies the username that authenticates the CLI login for the connection to the remote device; if value is unspecified, the ANSIBLE_REMOTE_USER environment variable value is used  |
| ``ansible_ssh_pass`` | no       |            | Specifies the password that authenticates the connection to the remote device |
| ``ansible_become`` | no       | yes, no\*   | Instructs the module to enter privileged mode on the remote device before sending any commands; if value is unspecified, the ANSIBLE_BECOME environment variable value is used, and the device attempts to execute all commands in non-privileged mode |
| ``ansible_become_method`` | no       | enable, sudo\*   | Instructs the module to allow the become method to be specified for handling privilege escalation; if value is unspecified, the ANSIBLE_BECOME_METHOD environment variable value is used |
| ``ansible_become_pass`` | no       |            | Specifies the password to use if required to enter privileged mode on the remote device; if ``ansible_become`` is set to no this key is not applicable |
| ``ansible_network_os`` | yes      | dellos6/dellos9/dellos10, null\*  | Loads the correct terminal and cliconf plugins to communicate with the remote device |
 
> **NOTE**: Asterisk (\*) denotes the default value if none is specified.

Dependencies
------------

The *dellos_vxlan* role is built on modules included in the core Ansible code. These modules were added in Ansible version 2.2.0.

Example playbook
----------------

This example uses the *dellos_vxlan* role to configure the VXLAN network, source ip address on VXLAN tunnel endpoint and virtual networks. It creates a *hosts* file with the switch details, a *host_vars* file with connection variables and the corresponding role variables.

When *dellos_cfg_generate* is set to true, the variable generates the configuration commands as a .part file in *build_dir* path. By default, the variable is set to false. This example writes a simple playbook that only references the *dellos_vxlan* role. The sample host_vars given below is for dellos10. 

**Sample hosts file**
    
    leaf1 ansible_host= <ip_address> 

**Sample host_vars/leaf1**

    hostname: leaf1
    ansible_become: yes
    ansible_become_method: xxxxx
    ansible_become_pass: xxxxx
    ansible_ssh_user: xxxxx
    ansible_ssh_pass: xxxxx
    ansible_network_os: dellos10
    build_dir: ../temp/dellos10
	  
    dellos_vxlan:
        anycast_gateway_mac: "00:22:33:44:55:66"
        loopback:
          loopback_id: 10
          description: "HARDWARE_VXLAN"
          ip_address: "10.8.0.1/32"
          state: "present"
        nve:
          source_interface: 10
          controller:
            name: "ovsdb"
            max_backoff: 2000
            control_cfg:
              - ip_addr: "1.2.3.4"
                port: 30
                state: "present"
            state: "present"
          state: "present"
        evpn:
          autoevi: False
          evi:
            - id: 111
              rd: "auto"
              vni:
                id: 111
                state: "present"
              route_target:
                - type: "manual"
                  asn_value: "111:111"
                  route_target_type: "both"
                  state: "present"
                - type: "manual"
                  asn_value: "11:11"
                  route_target_type: "export"
                  state: "present"
              state: "present"
          state: "present"      
        virtual_network:
          untagged_vlan: 1001
          virtual_net:
            - id: 111
              description: "NSX_Cluster_VNI_111"
              vlt_vlan_id: 11
              member_interface:
                - ifname: "ethernet 1/1/15"
                  type: "tagged"
                  vlanid: 15
                  state: "present"
                - ifname: "port-channel 12"
                  type: "tagged"
                  vlanid: 11
                  state: "present"
              vxlan_vni:
                id: 111
                remote_endpoint:
                  - ip: "1.1.1.1"
                    state: "present"
                  - ip: "11.11.11.11"
                    state: "present"
                state: "present"
              state: "present" 
          vlan_association:
            - vlan_id: 111
              virtual_net: 111

              
**Simple playbook to configure VXLAN - leaf.yaml**

    - hosts: leaf1
      roles:
         - Dell-Networking.dellos_vxlan

**Run**

    ansible-playbook -i hosts leaf.yaml

(c) 2019 Dell Inc. or its subsidiaries. All Rights Reserved.
