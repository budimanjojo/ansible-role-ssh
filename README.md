Ansible SSH Role
=====================

Role to manage SSH configs.

Supported OS Families
---------------------

- Ubuntu (tested)
- Arch Linux (tested)
- Redhat (tested)

Role Variables
--------------

Available variables are listed below, the default values are in [defaults/main.yml](./defaults/main.yml):
```
ssh_service_name: service name of ssh, default to 'sshd' (string)
ssh_directory_path: path where the ssh directory is located, default to '/etc/ssh' (string)

## List of ssh packages to install
ssh_packages: []

## Dict of sshd_config options
ssh_sshd_config_options:
  key: value(string|int|list)

## List of ssh_config.config options for each hostnames:
ssh_ssh_config_options:
- hostnames: []
  options:
    key: value(string|int|list)
```

Dependencies
------------

None

Example Playbook
----------------

Here is an example playbook:
```
- hosts: all

  vars:
    ssh_packages:
    - openssh-server
    - openssh-client
    ssh_sshd_config_options:
      ChallengeResponseAuthentication: "no"
      UsePAM: "yes"
      X11Forwarding: "yes"
      Port: 22
    ssh_ssh_config_options:
    - hostnames: ["*"]
      options:
        Port: 22
        ForwardX11: "yes"
        IdentityFile:
        - ~/.ssh/id_rsa
        - ~/.ssh/id_ecdsa
        - ~/.ssh/id_ed25519

  roles:
  - budimanjojo.ssh
```

License
-------

MIT License
