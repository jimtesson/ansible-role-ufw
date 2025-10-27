Setup requirements
=========

```
  pyenv install 3.12.0
  pyenv virtualenv 3.12.0 ansible-env
  pyenv activate ansible-env
  pip install --upgrade pip
  pip install -r requirements.txt
```

Role Name
=========

UFW basic setup. Default behavior is restrictive: deny all connections !

Role Variables
--------------

You can specify ufw is enabled or not, and the rules (port, proto, rule).

```
  ufw_enabled: true
  ufw_rules:
    - port: '22'
      proto: 'tcp'
      rule: 'allow'
```

Example
----------------

```
  - hosts: webservers
    tasks:
      - name: "Include ufw role"
        ansible.builtin.include_role:
          name: "jimtesson.ufw_setup"
          vars:
            ufw_enabled: true
            ufw_rules:
              - { port: '22', proto: 'tcp', rule: 'allow' }
              - { port: '80', proto: 'tcp', rule: 'allow' }
              - { port: '443', proto: 'tcp', rule: 'allow' }

```

Tests
----------------

```
  # create the instance
  molecule create

  # apply the playbook
  molecule converge

  # test the playbook
  molecule verify

  # destroy the instance
  molecule destroy  
```

License
-------

BSD
