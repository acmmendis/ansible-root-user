# Introduction

This Ansible role creates a user with root privileges on a target system.

The playbook generates a static, one-time password for the user, which is displayed at the end of the play. The user must change this password upon first login. The role also sets up group membership and sudo privileges as required.

## Features

- Creates a user with specified username and comment
- Optionally creates and assigns a custom group
- Sets a secure, random password (displayed only once)
- Configures password expiry policy
- Sets up sudoers file for passwordless sudo (configurable)

## Usage

```sh
ansible-playbook main.yml -i inventory.yml -u ansibleuser --private-key ~/.ssh/id_rsa --become -e 'systemuser=rootuser comments="This is a root user"'

ansible-playbook main.yml -i inventory.yml -u ansibleuser --private-key ~/.ssh/id_rsa --become -e 'systemuser=rootuser comments="This is a root user with specific group" group_name=mygroup'
```

### Extra Variables

- `systemuser` (required): The username to create
- `comments` (optional): Comment/description for the user
- `group_name` (optional): Custom group name. If not set, defaults to the username
- `sudoers` (optional): Sudoers rule (default: `ALL=(ALL) NOPASSWD:ALL`)

## Notes

- The generated password is a OTP (one time password) that shown only once for security reasons.
- The user is forced to change the password at first login.
- Ensure you have SSH access and privilege escalation rights on the target host.
