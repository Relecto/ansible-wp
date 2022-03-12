# LEMP stack Ansible playbook

Playbook to deploy LEMP stack onto Ubuntu machine, and install Wordpress on it.

## How to use

### 1. Create a Vagrant VM (optional)

If you have Vagrant installed, you can use the included Vagrantfile to create a VM for this project.

In the project directory run:

```bash
vagrant up
```

**NOTE: Vagrant is configured to provision the machine with your ssh public rsa key, found in ~/.ssh/id_rsa.pub**

### 2. Inventory file

Playbook will deploy to the host aliased `worker`. You can update hosts.yml with your details.

No changes are necessary if you are using Vagrant VM from the previos step.

```yaml
all:
  hosts:
    worker:
      ansible_host: 192.168.56.10
      ansible_user: vagrant
      ansible_become_pass: vagrant
```

### 3. Run playbook

Run the playbook 

```bash
ansible-playbook -i hosts.yml master.yml
```

It is going to:
- Install mysql and configure it with default user and wordpress database
- Install and configure nginx and php-fpm
- Download Wordpress and create wp-config.php

It is possible to skip different stages with tags, for example, to only download wordpress:

```bash
ansible-playbook -i hosts.yml --tags install_wp master.yml 
```

### 4. Proceed to wordpress installation

Wordpress will be accessible on port 80 on the worker machine.

If provisioned with Vagrant, site will be accessible at localhost:8080. Proceed to installation on http://localhost:8080/wp-admin/install.php.

