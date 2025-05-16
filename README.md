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

- `k3s_installation_api_endpoint` This defaults to the IP / Hostname of the first server node, but If a LB is used the VIP should be entered here.
- `k3s_installation_api_port` This sets under which port the kubernetes api is available, in case of using a LB on the same node with different port, this one should be entered.
- `k3s_installation_k3s_version` Version of the k3s which should get installed.
- `k3s_installation_user_kubectl` This is by default set to true and gives the option to not create the kubeconfig for the regular user on the control nodes.
- `k3s_installation_token` This defines the secret token for joining to the cluster, this has a default value but should be changed!
- `k3s_installation_extra_server_args` This adds extra arguments during the installation of the cluster. An example is `--disable-traefik`
- `k3s_installation_extra_agent_args` This is the same option as mentioned above, just for the agents / workers.
- `k3s_installation_cidr` Sets the CIDR for the cluster, this defaults already to 192.168.0.0/16.
- `k3s_installation_registry_mirrors` Adds private registry mirrors according to [k3s/rke private registry configuration](https://docs.k3s.io/installation/private-registry). Supports image rewrite using `rewrite_pattern` and `rewrite_string` sub-elements.
- `k3s_installation_registry_configs` Adds authentication config for private registry mirrors according to [k3s/rke private registry configuration](https://docs.k3s.io/installation/private-registry).

## Dependencies

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

## Example Playbook

```YAML
- name: Test of k3s_installation role
  hosts: k3s_cluster
  remote_user: user
  roles:
    - hornjo.k3s_installation
  vars:
    k3s_installation_registry_mirrors:
        - name: docker.io
          endpoints:
            - https://registry.test.local
          rewrite_pattern: "(.*)"
          rewrite_string: "proxy-docker/$1"

    # Vault reference if possible
    # k3s_installation_registry_configs:
    #   registry.test.local:
    #     auth:
    #       username: ""
    #       password: ""
```

## License

Apache 2.0

## Contribution

Follow the ansible-lint guidelines and run ansible-lint in the root of the repo.

```shell
ansible-lint
```

Make sure that the role does succeed, when using the `--check` flag.

```shell
ansible-playbook tests/test.yml --check
```
