rnp-tools-ansible-roles-installpackages
=========

Ansible Role - Install packages

![Overwiew](https://gitlab.com/rachuna-net.pl/tools/ansibleroles/rnp-tools-ansibleroles-configuressh/-/raw/master/docs/configurationSSH.png)

Role Variables
--------------

Defaults role values:
```yaml
input_role_os_distribution:       "{{ ansible_distribution }}"
input_role_packages_upggrade:     no
input_role_enable_restart_server: no
input_role_repository_keys:       []
input_role_repositories:          []
input_role_packages_to_install:   []
input_role_packages_to_remove:    []
```

Example Playbook
----------------

```yaml
- hosts: Ubuntu
  become: yes
  remote_user: vagrant
  gather_facts: yes
  
  tasks:
    - include_role:
        name: ../../
      vars:
        input_role_os_distribution: "{{ ansible_distribution }}"
        input_role_repository_keys:
          - url: https://apt.releases.hashicorp.com/gpg
            state: present
        input_role_repositories:
          - repo: deb [arch=amd64] https://apt.releases.hashicorp.com focal main
            filename: hashicorp
            state: present
        input_role_packages_to_install:
          - virtualbox
          - vagrant

- hosts: CentOS, RedHat
  become: yes
  remote_user: vagrant
  gather_facts: yes
  
  tasks:
    - include_role:
        name: ../../
      vars:
        input_role_os_distribution: "{{ ansible_distribution }}"
        input_role_repository_keys:
        input_role_repositories:
          - name: google-chrome
            file: google-chrome
            description: google-chrome
            baseurl: http://dl.google.com/linux/chrome/rpm/stable/x86_64
            gpgcheck: yes
            enabled: yes
            gpgkey: https://dl.google.com/linux/linux_signing_key.pub
            state: present
        input_role_packages_to_install:
          - gcc
          - google-chrome-stable
```

License
-------

BSD 3-Clause

Author Information
------------------

### Maciej Rachuna
SysOps/DevOps