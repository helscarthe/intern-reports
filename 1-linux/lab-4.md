# Ansible - Installing web service on a remote server

The remote server(s) of choice will be provided using EC2 instances on a personal AWS account. We will have one control node and two managed nodes, each serving a sample website also provided from the control node.

### Preparing the instances

- Create 3 EC2 instances, one for each node\
<img src=images/lab-4/image-1.png width=500>
- Configure the shared Security Group of the managed nodes to allow SSH and HTTP inbound connections\
<img src=images/lab-4/image-2.png width=500>

### Ansible configuration

- Final working Ansible directory:\
<img src=images/lab-4/image-3.png width=400>
- First, add managed nodes hostnames/IP addresses to `inventory`

```
; these are only sample IPs
[server1]
13.229.133.54 ansible_ssh_private_key_file=ansibleKeyPair.pem

[server2]
18.139.163.120 ansible_ssh_private_key_file=ansibleKeyPair.pem
```
- Perform a ping test to ensure that the managed nodes are reachable from the control node\
<img src=images/lab-4/image-4.png width=600>
- Configure the roles. In this configuration, 3 roles will be used - one for common configuration of httpd on all managed nodes, and one for specific tasks on each node.\
<img src=images/lab-4/image-5.png width=400>
- Configure the common tasks in `httpd/tasks/main.yml`
```yaml
---
# These tasks install the httpd package.

- name: Install httpd
  yum: name=httpd state=present

- name: httpd service state
  service: name=httpd state=started enabled=yes
```
- Configure the node-specific tasks in `[node-name]/tasks/main.yml`, in this case, copying the sample website from the control node
```yaml
---
# This task copies the prepare html code into
# the destination server.

- name: Copy code from control node
  copy:
    src: roles/server1/files/index.html
    dest: /var/www/html/index.html
```
- Configuring `playbook.yml`
```yaml
---
# This playbook executes all configured tasks.

- name: install httpd
  hosts: all
  become: true
  roles:
    - httpd

- name: configure server 1
  hosts: server1
  become: true
  roles:
    - server1

- name: configure server 2
  hosts: server2
  become: true
  roles:
    - server2
```
- First run\
<img src=images/lab-4/image-6.png width=600>
- Testing the webpages\
<img src=images/lab-4/image-7.png width=600>
<img src=images/lab-4/image-8.png width=600>
- Subsequent runs\
<img src=images/lab-4/image-9.png width=600>