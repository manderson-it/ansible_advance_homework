osp-setup
=========

This role creates objects in OSP. The objects created are:
- flavor
- image
- keypair
- network
- security groups

Requirements
------------

* openstacksdk
* openstacksdk >= 0.12.0
Direct network connectivity or jumphost into OpenStack environment.

Role Variables
--------------

- osp_networks (defines internal and external network for OSP)
- osp_router (defined the router for the external network for OSP)

Examples `vars/main.yml`:
```yaml
osp_networks:
  # Public Facing Network   
  external:
    cloud_name: ospcloud
    network_name: ext_network
    subnet_name: ext_subnet
    cidr_network: "10.10.10.0/24"
    state: present
    external: true


  # Private Facing Network   
  internal:
    cloud_name: ospcloud
    network_name: int_network
    subnet_name: int_subnet
    cidr_network: "20.20.20.0/24"
    state: present
    external: false

  # Public Facing Router connecting the two networks
osp_router:
  router:
    cloud_name: ospcloud
    state: present
    name: router
    network: ext_network
```

Dependencies
------------

None.

Example Playbook
----------------

    - name: Create flavor, image, keypair, network, and security groups in OSP 
      hosts: workstation
      become: yes
      roles:
        - osp-setup

License
-------

BSD

Author Information
------------------

Marek Anderson
