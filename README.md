Ansible NGINX Role
===================

This role installs NGINX Open Sourcen on RedHat/Amazon Linux, Debian/Ubuntu.

**Note:** This role is still in active development. There may be unidentified issues and the role variables may change as development continues.

Requirements
------------

**Ansible**

Instructions on how to install Ansible can be found in the [Ansible website](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).


Installation
------------

**Ansible Galaxy**

Use `ansible-galaxy install mehdi_wsc.nginx` to install the latest stable release of the role on your system.

**Git**

Use `git clone https://github.com/mehdi-wsc/nginx.git` to pull the latest edge commit of the role from GitHub.

Platforms
---------

The NGINX Ansible role supports Redhat , Amazon Linux Image, Debian and Ubuntu:

```yaml
Debian:
  versions:
    - Buster
    - Stretch
    - Jessie
    - Wheezy

Ubuntu:
  versions:
    - Eoan Ermine
    - Bionic Beaver
    - Xenial Xerus
    - Trusty Tahr
AMazon:
  versions:
    - 2018.03
RedHat:
  versions:
    - 6
    - 7
```

Role Variables
--------------

I split variables in two directories , the default  and vars :

defaults :
- Variables declared here are commons for Nginx configuration , I set default values,However you can modify to your own.
```
---
    #major vars
    nginx_error_log: /var/log/nginx/error.log
    pid_path: /run/nginx.pid
    access_log_path: /var/log/nginx/access.log
    #events
    worker_connections: 1024
    #http
    listening_port: 80
    root_path: /usr/share/nginx/html
    keepalive: 65
    hash_size: 2048
    send_file: on
    tcp_nopush: on
    tcp_nodelay: on
```
You can modify variables to your own values.

vars :
- Variables included here are for OS plateform and put it in files,and also you can customize it :
```
vars
├── Debian.yml
├── main.yml
├── RedHat.yml
└── Ubuntu.yml
```
Note: Amazon Linx have same vars like Redhat.

Overriding configuration templates
----------------------------------
If you can't customize via variables because an option isn't exposed, you can override the template used to generate the nginx.conf file:
```
templates/
└── nginx-config.j2
```

Dependencies
------------

None

Example Playbook
----------------
This is a sample playbook file for deploying the Ansible Galaxy NGINX role in a localhost and installing the open source version of NGINX.
```
---
- hosts: localhost
  become: true
  roles:
    - role: nginxinc.nginx
```
This is a sample playbook file for deploying the Ansible Galaxy NGINX role in a localhost and installing the open source version of NGINX with including vars.
```
---
- hosts: localhost
  become: true
  roles:
    - role: nginxinc.nginx
  vars:
    worker_connections: 2048
    listening_port: 8080
    keepalive: 130
```
License
-------
[GNU GENERAL PUBLIC LICENSE](https://github.com/mehdi-wsc/nginx/blob/master/LICENSE)