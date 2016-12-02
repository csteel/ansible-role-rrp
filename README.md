rrp
===

Description
-----------

**rrp** or run, retrieve and process, is used to run commands, retrieve and / or process the results as desired.

Role Variables
--------------

### group_vars

```shell

# ensure for group_vars/rrp/rrp_defaults
mkdir -p group_vars/rrp
cp roles/rrp/files/group_vars/rrp_defaults.yml group_vars/rrp/rrp_defaults.yml

```

#### group_vars/rrp/rrp_defaults.yml example content.

Edit `group_vars/rrp/rrp_defaults.yml` updating deploy user and active interface variables.

```yaml

---
# group_vars/rrp/rrp_defaults.yml

rrp_user: '<deployment_user>'
rrp_active_interface : 'eth0'

```

### rrp/defaults/main.yml

```yaml

---
# file: roles/rrp/defaults/main.yml

rrp_slash: "/"

rrp_ensure_dirs_on_remote:

  dir_home_command_output_dmidecode:

    state          : "directory"
    path           : "command_output"
    owner          : '{{ rrp_user }}'
    group          : '{{ rrp_user }}'
    mode           : '0770'
    package        : "dmidecode"
    command        : "dmidecode"
    command_options: ""

  dir_home_command_output_ethtool:

    state          : "directory"
    path           : "command_output"
    owner          : '{{ rrp_user }}'
    group          : '{{ rrp_user }}'
    mode           : '0770'
    package        : "ethtool"
    command        : "ethtool"
    command_options: '{{ rrp_active_interface }}'


rrp_ensure_dirs_on_local:

  project_home_ace_fetched_files:

    state       : "directory"
    path        : "../ace_fetched_files"
    owner       : "{{ rrp_user }}"
    group       : "{{ rrp_user }}"
    mode        : "0770"
    recursive   : True

```

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

Depends on the Galaxy role **ensure_dirs**. The dependency is defined **roles/rrp/meta/main.yml** as follows:

    ---
    # file: roles/rrp/meta/main.yml
    dependencies:
      - { role: ensure_dirs, 
            ensure_dirs_on_remote: "{{ rrp_ensure_dirs_on_remote }}",
            ensure_dirs_on_local : "{{ rrp_ensure_dirs_on_local }}"
        }

The values for **rrp_ensure_dirs_on_remote** and **rrp_ensure_dirs_on_local** are defined in **roles/rrp/defaults/main.yml**. See the example above in the **roles/rrp/defaults/main.yml** example.
        path        : "../ace_fetched_files"

IMPORTANT: if you do not use one of the definitions, for example, if you do not want to use **rrp_ensure_dirs_on_local** then you should define it as empty like this:

    rrp_ensure_dirs_on_local []

Example Playbook
----------------

```yaml

---
# file: rrp.yml

- hosts: rrp
  gather_facts: true
  roles:
    - rrp

```

To create the above playbook quickly 

```shell

cp roles/rrp/files/rrp.yml rrp.yml

```

Ansible Command
---------------

Example of an Ansible command:

```shell

ansible-playbook systems.yml -i inventory/dev

```

License
-------

MIT

Author Information
------------------

Christopher Steel
