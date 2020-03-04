app-tier
=========

This role sets up the apache and tomcat server.

Requirements
------------

* openstacksdk
* openstacksdk >= 0.12.0
Direct network connectivity or jumphost into OpenStack environment.

Role Variables
--------------

This is a play variable for the second play.
```yaml
# next line won't run the base-config at all
run_base_config: "norun"
# next line will run the base-config on all three tiers
run_base_config: "run"
```

Dependencies
------------

None.

Example Playbook
----------------

Ensure base-config runs once before a different tier-related play.

Change *run_base_config* variable in the 2nd play.

    - name: Gather OSP facts
      hosts: workstation
      gather_facts: true
      roles:
        - osp-facts
    
    # Break out base-config to make it skippable / easy to comment out
    - name: Three-Tier-App - base-config (repos)
      become: yes
      hosts: appdbs:apps:frontends
      gather_facts: false
      vars:
        run_base_config: "norun"
      roles:
        - role: base-config
          tags: base-config
          when: run_base_config == "run"
    
    - name: Three-Tier-App - setup app tier
      hosts: apps
      become: yes
      gather_facts: false
      roles:
        - {name: app-tier, tags: [apps, tomcat]}

License
-------

BSD

Author Information
------------------

Marek Anderson
