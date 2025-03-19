# Role Name

This role was initially a fork of the k3s-ansible role. This was more or less taken and merged to one role instead of following the multi-role approach.

## Requirements

The control node must have Ansible 8.0+ (ansible-core 2.15+)

Packages:

- ansible.posix

All managed nodes in inventory must have:

Password-less SSH access
Root access (or a user with equivalent permissions)
It is also recommended that all managed nodes disable firewalls and swap. See K3s Requirements for more information.

## Role Variables

In this role only default variables are set. Here is a brief description which variables can be set:

```YAML

```

## Dependencies

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

## License

BSD

## Author Information

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
