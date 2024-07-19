# Comprehensive Guide to Nginx Setup and Removal with Ansible
This guide provides detailed instructions for installing, configuring, and removing Nginx using Ansible playbooks. The playbooks leverage roles and handlers to streamline the management of Nginx on a remote host.

### Directory structure
```
nginx-setup
├── main.yml
├── nginx
│   ├── defaults
│   │   └── main.yml
│   ├── files
│   ├── handlers
│   │   └── main.yml
│   ├── meta
│   │   └── main.yml
│   ├── README.md
│   ├── tasks
│   │   ├── configure.yml
│   │   ├── install.yml
│   │   └── main.yml
│   ├── templates
│   │   ├── index.html.j2
│   │   └── nginx.config.j2
│   ├── tests
│   │   ├── inventory
│   │   └── test.yml
│   └── vars
│       └── main.yml
└── remove-nginx.yml
```

### Explanation of File
1. Playbook: `nginx-setup/main.yml`

   This playbook installs and configures Nginx using an Ansible role.
  * `vars_files:` Specifies the file containing the sudo password required for privilege escalation.
  * `ansible_python_interpreter:` Specifies the Python interpreter to be used on the remote host.

2. Playbook: `nginx-setup/remove-nginx.yml`

   This playbook removes Nginx and its configuration files from the remote host.

    2.1 Remove Nginx Package
    - Module: `apt`
      - `name:` Specifies the package name to be removed.
      - `state: absent` ensures that the package is removed.

    2.2 Remove Nginx Configuration Files
    - Module: `file`
      - `path:` Specifies the path of the files or directories to be removed.
      - `state: absent` ensures that the files or directories are deleted.
   
3. Playbook: `nginx/tasks/main.yml`

   The Nginx role contains tasks for installing and configuring Nginx.

    3.1 Playbook: `nginx/tasks/install.yml`
    - Module: `apt`
      - `name:` Specifies the package name to be installed.
      - `state: present` ensures that the package is installed.
      - `update_cache: yes` updates the package cache before installing.
     
    - Module: `service`
      - `name:` Specifies the service name to be managed.
      - `state: started` ensures that the service is running.
      - `enabled: yes` ensures that the service starts on boot. 

    3.2 Playbook: `nginx/tasks/configure.yml`
    - Module: `template`
      - `src:` Specifies the source template file.
      - `dest:` Specifies the destination path on the remote host.
      - `mode:` Sets the file permissions.
    
    - `Module: `file`
      - `path:` Specifies the file or directory path.
      - `state: absent` ensures that the file or directory is deleted.
      - `src:` Specifies the source path for creating a symbolic link.
      - `dest:` Specifies the destination path for the symbolic link.
      - `state: link` ensures that a symbolic link is created.
     
4. Playbook: `nginx/handlers/main.yml`

    - Module: `service`
      - `name:` Specifies the service name to be managed.
      - `state: restarted` ensures that the service is restarted.
     
5. Templates: `nginx/templates/index.html.j2`

```
<!DOCTYPE html>
<html>
<head>
    <title>Welcome to Nginx</title>
</head>
<body>
    <h1>Welcome to Nginx</h1>
    <p>This is a sample index.html page served by Nginx.</p>
</body>
</html>

```

  6. Templates: `nginx/templates/nginx.config.j2`
```
server {
    listen 80;
    server_name localhost;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    # Additional configuration settings
    # You can include more server blocks or settings here
}
```

## Summary
This comprehensive guide demonstrates the installation, configuration, and removal of Nginx using Ansible playbooks. The use of roles, tasks, templates, and handlers in the playbooks showcases the power and flexibility of Ansible in automating server configurations and management.
