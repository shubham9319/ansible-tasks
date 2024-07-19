# Efficient Firewall Management with Ansible: A Comprehensive Guide
This guide explains the configuration and management of firewalls using Ansible. The focus is on a playbook designed to manage UFW (Uncomplicated Firewall) on a remote host.

### Explanation of File
- Playbook: `network/ufw-conf.yml`

This playbook ensures that UFW is enabled on the target host, configures it to allow HTTP and HTTPS traffic, verifies the firewall rules, and adds a DNS entry to the /etc/hosts file.

### Modules Used:
### 1. Module: `ufw`
- `state: enabled` ensures UFW is turned on.
- `policy: allow` sets the default policy to allow all incoming connections.
- `rule: allow` specifies that traffic should be allowed.
- `port:`
  - `80` indicates the HTTP port.
  - `443` indicates the HTTPS port.
- `proto: tcp` specifies the protocol to be TCP.

### 2. Module: `command`
Executes the ufw status command to get the status of the firewall rules.
- `register: ufw_status` saves the output of the command.
- `changed_when: false` ensures the task is marked as unchanged in Ansible.

### 3. Module: `debug`
- `msg:`
  - Prints a message if port 80 is open.
  - Prints a message if port 443 is open.
- `when:`
  - Condition to check if '80/tcp' is present in ufw_status.stdout.
  - Condition to check if '443/tcp' is present in ufw_status.stdout.

### 4. Module: `lineinfile`
- `path: /etc/hosts` specifies the file to modify.
- `regexp: '^127\.0\.0\.1'` regular expression to find the matching line.
- `line: 127.0.0.1 localhost` specifies the line to be added or replaced.
- `owner: root` sets the owner of the file.
- `group: root` sets the group of the file.
- `mode: '0644'` sets the permissions of the file.
- `backup: yes` creates a backup of the file before modifying it.

## Summary
This playbook provides a comprehensive approach to managing UFW on a remote host, ensuring that HTTP and HTTPS traffic is allowed and verifying the rules. Additionally, it manages the /etc/hosts file to ensure proper DNS resolution. This guide demonstrates the power and flexibility of Ansible in automating firewall configurations and system settings.
