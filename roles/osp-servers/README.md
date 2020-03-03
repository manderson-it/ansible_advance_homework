osp-servers
=========

Provision OSP instances.

Requirements
------------

* openstacksdk
* openstacksdk >= 0.12.0
Direct network connectivity or jumphost into OpenStack environment.

Role Variables
--------------

* osp_servers (One or more definitions of an instance)
Example `vars/main.yml`:
```yaml
osp_servers:
  frontend:
    name: frontend
    state: present
    image: rhel-guest
    key_name: ansible_ssh
    flavor: m2.small
    security_group: frontend
    meta:
      - { group: frontends, deployment_name: QA}
  app1:
    name: app1
    state: present
    image: rhel-guest
    key_name: ansible_ssh
    flavor: m2.small
    security_group: apps
    meta:
      - { group: apps, deployment_name: QA}
  app2:
    name: app2
    state: present
    image: rhel-guest
    key_name: ansible_ssh
    flavor: m2.small
    security_group: apps
    meta:
      - { group: apps, deployment_name: QA}
  db:
    name: db
    state: present
    image: rhel-guest
    key_name: ansible_ssh
    flavor: m2.small
    security_group: db
    meta:
      - { group: appdbs, deployment_name: QA}
```

Dependencies
------------

Role `osp-setup` has to run first to create required OSP objects like flavor, image, keypair, network, and security group.

Example Playbook
----------------

First play is mandatory to create required OSP objects 
    - name: Create flavor, image, keypair, network, and security groups in OSP 
      hosts: workstation
      become: yes
      roles:
        - osp-setup
    
    - name: Create instances for three-tier-app
      hosts: workstation
      become: yes
      roles:
        - osp-servers


License
-------

BSD

Author Information
------------------

Marek Anderson
