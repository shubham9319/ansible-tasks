# Streamlined Automation Tasks Using Ansible: A Comprehensive Guide

### Introduction
Ansible is a powerful IT automation tool that enables you to automate and manage your infrastructure efficiently. It simplifies tasks such as configuration management, application deployment, and task automation, making it a popular choice for DevOps engineers.

### Why Use Ansible?
Ansible stands out due to its simplicity, agentless architecture, and powerful automation capabilities. Key features include:

- `Agentless:` No need to install any software on your managed nodes.
- `Simple YAML Syntax:` Playbooks are written in human-readable YAML format.
- `Idempotent:` Ensures that a task only executes when necessary, maintaining the desired state.
- `Extensible:` Supports a wide range of modules to manage various systems and applications.

### Prerequisites
Before getting started, ensure you have the following:

- Ansible installed on your control node.
- SSH access to your managed nodes.
- Python installed on your managed nodes.

### Project Structure

```
ansible-tasks
├── apache2.yml
├── database
│   ├── main.yml
│   ├── mysql
│   │   ├── defaults
│   │   │   └── main.yml
│   │   ├── files
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── meta
│   │   │   └── main.yml
│   │   ├── README.md
│   │   ├── tasks
│   │   │   ├── database.yml
│   │   │   ├── main.yml
│   │   │   ├── package.yml
│   │   │   └── user.yml
│   │   ├── templates
│   │   ├── tests
│   │   │   ├── inventory
│   │   │   └── test.yml
│   │   └── vars
│   │       └── main.yml
│   ├── mysql.yml
│   └── remove-mysql.yml
├── files
│   └── index.html
├── file-tasks
│   ├── copy-file-remote-servers.yml
│   ├── file-directory-tasks.yml
│   ├── files
│   │   └── index.html
│   ├── file-tasks.yml
│   └── templates
│       └── nginx.conf.j2
├── inventory.ini
├── network
│   └── ufw-conf.yml
├── nginx-setup
│   ├── main.yml
│   ├── nginx
│   │   ├── defaults
│   │   │   └── main.yml
│   │   ├── files
│   │   ├── handlers
│   │   │   └── main.yml
│   │   ├── meta
│   │   │   └── main.yml
│   │   ├── README.md
│   │   ├── tasks
│   │   │   ├── configure.yml
│   │   │   ├── install.yml
│   │   │   └── main.yml
│   │   ├── templates
│   │   │   ├── index.html.j2
│   │   │   └── nginx.config.j2
│   │   ├── tests
│   │   │   ├── inventory
│   │   │   └── test.yml
│   │   └── vars
│   │       └── main.yml
│   └── remove-nginx.yml
├── README.md
├── remove-apache2.yml
├── user-group-tasks
│   ├── add-user-group.yml
│   ├── check-user-group.yml
│   └── remove-user-group.yml
└── vars
    └── sudo_password.yml
```

### Inventory File
The inventory.ini file defines the hosts and their groupings. Here is an example:
```
localhost ansible_host=localhost ansible_connection=local ansible_python_interpreter=/usr/bin/python3

[worker]
worker1 ansible_host=10.10.10.10 ansible_user=worker1
worker2 ansible_host=10.10.10.20 ansible_user=worker2

[worker:vars]
ansible_connection=ssh
ansible_python_interpreter=/usr/bin/python3
ansible_ssh_private_key_file=/home/ansible/.ssh/id_rsa
```

### Variables File
Store sensitive information securely using Ansible Vault. Encrypt the vars/sudo_password.yml file:
```
ansible_become_password: "devops"
user_password: adminpass
```

To encrypt the file, use the command:
```
ansible-vault encrypt vars/sudo_password.yml
```

### Apache Installation Playbook
- The `apache2.yml` playbook installs Apache on the managed nodes.

#### Remove Apache Playbook
- The `remove-apache2.yml` playbook removes Apache from the managed nodes.

#### Explanation of Ansible Modules Used
* `debug:` Prints statements for debugging.
* `yum:` Manages packages with the yum package manager (used for RedHat-based systems).
* `apt:` Manages packages with the apt package manager (used for Debian-based systems).
* `service:` Manages services (starting, stopping, enabling).
* `copy:` Copies files from the control node to the managed node.
* `file:` Manages file properties (such as removing files).

### `NOTE:` For more details, please check the README.md file located in the respective directory's.
