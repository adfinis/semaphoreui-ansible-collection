# Ansible Collection - adfinis.semaphoreui

![License](https://img.shields.io/github/license/adfinis/semaphoreui-ansible-collection)
![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/adfinis/semaphoreui-ansible-collection/ansible-lint.yml)
[![adfinis.semaphoreui on Ansible Galaxy](https://img.shields.io/badge/collection-adfinis.semaphore-blue)](https://galaxy.ansible.com/ui/repo/published/adfinis/semaphoreui/)

Ansible Collection to manage and deploy Semaphore UI in Docker.

## Install

The Collection can be installed from Ansible Galaxy:
``` bash
ansible-galaxy collection install adfinis.semaphoreui
```

Alternatively put the collection into a `requirements.yml` file:
``` yaml
---
collections:
  - name: adfinis.semaphoreui
```

## Roles

### `adfinis.semaphoreui.semaphore`

Ansible role to deploy and manage Semaphore UI servers and runners using Docker Compose.
* Works with the free version of Semaphore UI and Semaphore UI Pro.
* Optional Caddy reverse proxy for easy HTTPS
* Supports multiple database backends (sqlite (default), postgres, mysql).
* Ability to run different Ansible versions on the Semaphore UI Runner for backwards compatibility with older systems.

#### Usage
##### Inventory

The Ansible role expect two host groups: `servers` (required!), `runners` (optional).
The individual server and runner tasks are only applied to hosts in their relative host group.

A simple example:

**INI:**
```ini
[servers]
vm-semaphore-server-01.example.com

[runners]
vm-semaphore-runner-01.example.com
vm-semaphore-runner-02.example.com
```

**YAML:**
``` yaml
---
servers:
  hosts:
    vm-semaphore-server-01.example.com:

runners:
  hosts:
    vm-semaphore-runner-01.example.com:
    vm-semaphore-runner-02.example.com:
```

##### Role variables

All arguments can be found in `roles/semaphore/meta/arguments_specs.yml`. You can display them with `ansible-doc`:
``` bash
ansible-doc -t role adfinis.semaphoreui.semaphore
```

The following variables are required:
* `semaphore_address`: Public domain or IP address for the Semaphore instance. 
* `semaphore_admin_username`: Username for the Semaphore UI admin account.
* `semaphore_admin_password`: Password for the Semaphore UI admin account.

##### Playbook
The Ansible Collection features a playbook to call the role `adfinis.semaphoreui.semaphore` without having to write one yourself:
``` bash
ansible-playbook adfinis.semaphoreui.semaphore_playbook
```

## License

[GPL-3.0-or-later](https://github.com/adfinis/semaphoreui-ansible-collection/blob/main/LICENSE)

## Author Information

The Ansible collection `adfinis.semaphore` was written by:

* Adfinis AG | [Website](https://www.adfinis.com/) | [GitHub](https://github.com/adfinis)

