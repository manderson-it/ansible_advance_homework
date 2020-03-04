osp-instance-delete
=========

This role deletes OSP instances and floating IPs.

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

None.

Example Playbook
----------------

    - name: Delete deployed instances from OSP
      hosts: workstation
      become: yes
      roles:
        - osp-instance-delete

License
-------

BSD

Author Information
------------------

Marek Anderson
