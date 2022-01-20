o0_o.vagrant
=========

Installs Vagrant, installs specified Vagrant boxes and initializes `Vagrantfile` in the current working directory. This role does not configure VMs. Use `blockinfile` to add VMs to `Vagrantfile` in playbooks or other roles.

Requirements
------------

Currently, the only Vagrant provider supported is VirtualBox. However, unless provider-specific configuration is needed in `Vagrantfile`, any provider should work.

Role Variables
--------------

Available variables are listed below, along with default values (see `defaults/main.yml`):

The current working directory variable determines where `Vagrantfile` is generated. By default it's set to the `VAGRANT_CWD` environmental variable, and if that isn't set, `PWD` is used.

```
vagrant_cwd: "{{ lookup('env', 'VAGRAND_CWD') | default(lookup('env', 'PWD')) }}"
```

As mentioned, currently, the only supported Vagrant provider is VirtualBox, but that will likely change in the future.

```
vagrant_provider: virtualbox
```

Vagrant boxes (example: `generic/debian11`) are provided as a list. These are installed, but not updated.

```
vagrant_boxes: []
```

Example Playbook
----------------

```
- hosts: localhost
  connection: local
  roles:
  - o0_o.vagrant
```

```
- hosts: vagrant_vms
  tasks:
    include_role:
      name: o0_o.vagrant
      apply:
        delegate_to: 127.0.0.1
```

License
-------

MIT
