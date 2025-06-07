# Introduction

The Ansible roles create root priviladge user.

The play creates a static one time password for the user, which will be output at the end of the play. This password has to change on the very first login.

## How to use

```sh
ansible-playbook main.yml -i inventory.yml -u ansibleuser --private-key ~/.ssh/id_rsa --become -e 'systemuser=rootuser comments="This is a root user"'

ansible-playbook main.yml -i inventory.yml -u ansibleuser --private-key ~/.ssh/id_rsa --become -e 'systemuser=rootuser comments="This is a root user with specifi group" group_name=mygroup'
```
