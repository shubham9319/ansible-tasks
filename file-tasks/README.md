# Detailed Explanation of Ansible Code for Managing files and directories tasks.

### Directory structure
```
file-tasks
├── copy-file-remote-servers.yml
├── file-directory-tasks.yml
├── files
│   └── index.html
├── file-tasks.yml
└── templates
    └── nginx.conf.j2
```

## Explanation of Each File
### 1. `file-tasks/file-tasks.yml` Main playbook to copy files and directories.
#### Modules Used:
- `copy:` Copies files and directories to the remote host.
- `fetch:` Fetches files from remote nodes to the local machine.
- `delegate_to:` Executes tasks on a different host than the current one.

#### Detailed Explanation
1. Copy file to html directory from ansible machine to worker1 host:
- Uses the copy module to copy index.html from the Ansible machine to /var/www/html on worker1.

2. Copy file from ansible machine to worker1 host in a tmp directory:
- Uses the copy module to copy test.txt from /tmp on the Ansible machine to /tmp on worker1.

3. Copy the file from the tmp directory on a remote server to the DevOps tmp directory on the same server:
- Uses the copy module with remote_src: yes to copy test.txt from /tmp to /tmp on worker1.

4. Copy directory from ansible machine to worker1 host:
- Uses the copy module to copy the files directory from the Ansible machine to /var/www/html on worker1.

5. Copy directory from the html directory on a remote server to the tmp directory on the same server:
- Uses the copy module with remote_src: yes to copy files from /var/www/html to /tmp on worker1.

6. Fetch file from worker1 to ansible machine:
- Uses the fetch module to fetch test.txt from /tmp on worker1 to /tmp on the Ansible machine.

7. Copy file /tmp/test.txt to worker2 host:
- Uses the copy module to copy test.txt from /tmp on the Ansible machine to /tmp on worker2 using delegate_to.



### 2. `file-tasks/file-directory-tasks.yml` Playbook to handle file and directory tasks.
#### Modules Used:
- `file:` Manages files and directories.
- `stat:` Retrieves facts about files and directories.
- `debug:` Prints statements during playbook execution.
- `template:` Processes templates to remote nodes.
- `shell:` Executes shell commands on remote nodes.

#### Detailed Explanation
1. Create directory testuser:
- Uses the file module to create /tmp/testuser with specific permissions and ownership.

2. Check if directory exists:
- Uses the stat module to check if /tmp/testuser exists and registers the result.

3. Print message if directory is present:
- Uses the debug module to print a message if /tmp/testuser exists.

4. Print message if directory is not present:
- Uses the debug module to print a message if /tmp/testuser does not exist.

5. Create file test.txt with owner and group devops:
- Uses the file module to create /tmp/testuser/test.txt with specific permissions and ownership.

6. Copy file index.html from ansible host to worker1 host:
- Uses the copy module to copy index.html from the Ansible machine to /tmp/testuser on worker1 with specific permissions and ownership.

7. Check if file exists:
- Uses the stat module to check if /tmp/testuser/index.html exists and registers the result.

8. Print message if file is present:
- Uses the debug module to print a message if /tmp/testuser/index.html exists.

9. Print message if file is not present:
- Uses the debug module to print a message if /tmp/testuser/index.html does not exist.

10. Check if file is copied with correct permissions:
- Uses the stat module to check the permissions of /tmp/testuser/index.html and registers the result.

11. Debug copied file information:
- Uses the debug module to print the permissions of /tmp/testuser/index.html.

12. Copy Configurations:
- Uses the template module to process nginx.conf.j2 and copy it to /tmp/testuser/nginx.conf with specific permissions and ownership.

13. Verify template file content:
- Uses the shell module to execute a command to verify the content of /tmp/testuser/nginx.conf and registers the result.

14. Debug template file content:
- Uses the debug module to print the content of /tmp/testuser/nginx.conf.

15. Copy file from remote to local machine:
- Uses the fetch module to fetch shubham.txt from /tmp/testuser on worker1 to /tmp-dev/shubham.txt on the Ansible machine.

16. Remove directory testuser:
- Uses the file module to remove /tmp/testuser.

### 3. `file-tasks/copy-file-remote-servers.yml` Playbook to copy files between remote servers.
#### Modules Used:
- `fetch:` Fetches files from remote nodes to the local machine.
- `copy:` Copies files and directories to the remote host.

#### Detailed Explanation
1. Copy file from worker1 to Ansible Host:
- Uses the fetch module to fetch index.html from /tmp on worker1 to /tmp on the Ansible machine.

2. Copy file from Ansible Host to worker2:
- Uses the copy module to copy index.html from /tmp on the Ansible machine to /tmp on worker2 with specific permissions.

### 4. `file-tasks/files/index.html` HTML file to be copied.

### 5. `file-tasks/templates/nginx.conf.j2` Nginx configuration template.

## Summary
This set of playbooks demonstrates various file and directory operations in Ansible, including copying files and directories, creating and deleting directories, checking file and directory existence, and managing file permissions and ownership. The tasks also cover more advanced operations such as using templates and transferring files between remote hosts.
