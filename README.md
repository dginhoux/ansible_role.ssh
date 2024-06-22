# ROLE dginhoux.ssh



## DESCRIPTION

This ansible role configure ssh server and ssh client.

## ROADMAP

- support for centralisation of pubkeys and pukeys command script
- support for include files and deploy them... maybe in "raw" format



## REQUIREMENTS

#### SUPPORTED PLATFORMS

| Platform | Versions |
|----------|----------|
| Debian | all |
| EL | all |
| Fedora | all |
| Ubuntu | all |

#### ANSIBLE VERSION

Ansible >= 2.13

#### DEPENDENCIES

None.



## INSTALLATION

#### ANSIBLE GALAXY

```shell
ansible-galaxy install dginhoux.ssh
```
#### GIT

```shell
git clone https://github.com/dginhoux/ansible_role.ssh dginhoux.ssh
```


## USAGE

#### EXAMPLE PLAYBOOK

```yaml
- name: Playbook
  hosts: all
  tasks:
    - name: Start role dginhoux.ssh
      ansible.builtin.include_role:
        name: dginhoux.ssh
      vars:

        ssh_client_opt_spec:
          - "Username"
        ssh_client_cfg_spec:
          Username: rundeck
          Hosts:
            - rule: server1
              options:
                - "Port 28022"

        ssh_server_opt_spec:
          - "Port"
        ssh_server_cfg_spec:
          Port: 28022
          Matchs:
            - rule: "Host server1 User rundeck"
              options:
                - "PubKeyAuthentication yes"

```


## VARIABLES

This role configure `server` and `client` separatly and use their own vars like that : <br />
For `client` : <br />
- `ssh_client_opt_spec`, `ssh_client_opt_spec_group`, `ssh_client_opt_spec_host` list defined wich options must be configured.
- `ssh_client_cfg_spec`, `ssh_client_cfg_spec_group`, `ssh_client_cfg_spec_host` dict defined values for options.

For `server` : <br />
- `ssh_server_opt_spec`, `ssh_server_opt_spec_group`, `ssh_server_opt_spec_host` list defined wich options must be configured.
- `ssh_server_cfg_spec`, `ssh_server_cfg_spec_group`, `ssh_server_cfg_spec_host` dict defined values for options.

**NOTE**: Each _group/_host vars are merged with the main



#### DEFAULT VARIABLES

Defaults variables defined in `defaults/main.yml`.<br />
<br />
Their main switchs for toggle function : 

```yaml
ssh_install_pkgs: true
ssh_server_service_start_or_restart_and_enable: true
ssh_server_regenerate_host_keys: false
ssh_server_generate_host_config: true
ssh_client_generate_host_config: true
```

<br />
It contain the defaults configuration : <br />

```yaml
ssh_client_opt_default
ssh_client_cfg_default
ssh_server_opt_default
ssh_server_opt_default
```

<br /><br />
**NOTE**: Theses default variables contains common and generic configuration.<br />




#### EXAMPLES VARIABLES

This will configure `server` and set only Port option.<br />
For all, it will be set at 22222.

```yaml
ssh_server_opt_spec:
  - "Port"
ssh_server_cfg_spec:
  Port: 22222
```

To change this value for spcific group/host simply use : <br />

```yaml
ssh_server_cfg_spec_group:
  Port: 4444
ssh_server_cfg_spec_host:
  Port: 7777
```

To set PubkeyAuthentication in addition to Port at 22222 for specific host: <br />

```yaml
ssh_server_opt_spec_host:
  - PubkeyAuthentication
ssh_server_cfg_spec_host:
  PubkeyAuthentication: "yes"
```





#### DEFAULT OS SPECIFIC VARIABLES

Those variables files are located in `vars/*.yml` are used to handle OS differences.<br />
One of theses is loaded dynamically during role runtime using the `include_vars` module and set OS specifics variable's.




## AUTHOR

Dany GINHOUX - https://github.com/dginhoux



## LICENSE

MIT
