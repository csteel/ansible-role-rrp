rrp
===

Description
-----------

**rrp** or run, retrieve and process, is used to run commands, retrieve and / or process the results as desired.

Role Variables
--------------

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

and the values for **rrp_ensure_dirs_on_remote** and **rrp_ensure_dirs_on_local** are defined in **roles/rrp/defaults/main.yml** as in the following example using the **dmidecode** command:

    ---
    # file: roles/rrp/defaults/main.yml
    
    rrp_slash: "/"
    
    rrp_ensure_dirs_on_remote:
    
      dir_home_command_ouput:
    
        state       : "directory"
        path        : "command_output"
        owner       : '{{ ansible_ssh_user }}'
        group       : '{{ ansible_ssh_user }}'
        mode        : '0770'
        command     : "dmidecode"
    
    rrp_ensure_dirs_on_local:
    
      project_home_ace_fetched_files:
    
        state       : "directory"
        path        : "../ace_fetched_files"

IMPORTANT: if you do not use one of the definitions, for example, if you do not use **rrp_ensure_dirs_on_local** then you should define it as empty like this:

    rrp_ensure_dirs_on_local []

Example Playbook
----------------

    ---
    # file: rrp.yml
    - hosts: rrp
    # become: true
      gather_facts: true
      roles:
        - ansible-role-rrp

License
-------

MIT

Author Information
------------------

Christopher Steel
