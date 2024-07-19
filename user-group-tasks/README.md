# Comprehensive Guide to Managing Users and Groups with Ansible
This guide covers playbooks for creating, managing, and removing users and groups on an Ubuntu system using Ansible. These playbooks illustrate how to use Ansible modules for user and group management tasks.

1. Playbook: `user-group-tasks/add-user-group.yml`
   Title: Create and Configure User and Group on Ubuntu

   - Modules Used
    - Module: `group`
      - `name:` Specifies the name of the group to be created.
      - `state: present` ensures the group is created.

    - Module: `user`
      - `name:` Specifies the username to be created.
      - `create_home: yes` creates a home directory for the user.
      - `groups:` Specifies the groups to which the user should be added.
      - `append: yes` appends the user to existing groups.
      - `password:` Specifies the hashed password for the user.
     
  2. Playbook: `user-group-tasks/check-user-group.yml`
     Title: Verify and Manage Users and Groups

     - Modules Used
      - Module: `command`
        - `command:` Executes shell commands to check for user and group existence.
      - Module: `user`
        - `name:` Specifies the username to be managed.
        - `state: present` ensures the user is created.
      - Module: `group`
        - `name:` Specifies the group name to be managed.
        - `state: present` ensures the group is created.
       
   3. Playbook: `user-group-tasks/remove-user-group.yml`
      Title: Remove User and Group from Ubuntu System

      - Modules Used
       - Module: `user`
         - `name:` Specifies the username to be removed.
         - `state: absent` ensures the user is removed.
         - `remove: yes` deletes the user's home directory.
         - `force: yes` forces the removal of the user.
      - Module: `group`
        - `name:` Specifies the group name to be removed.
        - `state: absent` ensures the group is deleted.
      - Module: `file`
        - `path:` Specifies the path to be removed.
        - `state: absent` ensures the directory is deleted

## Summary
These playbooks provide a comprehensive approach to user and group management on Ubuntu systems using Ansible.
