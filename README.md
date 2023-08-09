# Ansible heat OpenStack deployment
Ansible heat OpenStack deployment

## Overview

This repository contains Ansible playbooks and Heat OpenStack template for provisioning a Virtual Machine and deploying an Nginx application as an example on cPouta Openstack environment.

## Project structure:-

```
.
├── ansible.cfg
├── destroy-vm.yml
├── files
│   ├── example-heat-params.yml
│   └── html
│       └── index.html
├── playbooks
│   ├── build-heat-stack.yml
│   ├── deploy_nginx_vm.yml
│   ├── group_vars
│   │   └── all.yml
│   ├── heat_params.yml
│   └── heat_stack_vm.yml
├── README.md
└── site.yml

```

## Requirements

### Software
* Ansible >= 2.2
* shade >= 1.8.0
* python-heatclient >= 3.0.0
* openstacksdk >= 1.1.0

For instructions on how to install Ansible, see [the official
documentation](https://docs.ansible.com/).

The easiest way to install it is using pip:

```bash
$ pip install <package>
```

## Usage

First you'll need to clone this repository to a directory on your machine.

You will need to get an openrc file from OpenStack so that Ansible can interact
with it. The easiest way to get it is to login to the web interface and go to
Compute -> Access & Security -> API Access -> Download OpenStack RC File. Once
you have the file, you will need to source it (the name of the file may be
different):

```bash
$ source openrc.sh
```

After that you can fill in the parameters for the Heat stack. First copy the
example Heat parameter file to your current working directory:

```bash
$ cd heat-openstack-example
$ cp files/example-heat-params.yml playbooks/heat_params.yml
```

Then edit the file and fill in the parameters according to your needs. Here is the explanation of each fields:
- ssh_key_name: The name of your SSH key pair used to connect to the instance.
- vm_flavor: The name of the flavor of the instance. Use the command `openstack flavor list` for a complete list.
- vm_image: The name of the image of the instance. Use the command `openstack image list` for a complete list.
- vm_network: The name of the network of the instance. Usually it's the name of the project. Use `openstack network list` for a complete list.
- allow_ssh_cidr: If you want to access from anywhere, use `0.0.0.0/0` (not recommended). Specify a restrict network.
- floating_ip_pool: The name of the floating IP pool list. Usually `public`.
- count: The number of instances to deploy

### Deploying the application
A variable "stack_name" must be set. You can do it so:
```
cd heat-openstack-example
ansible-playbook site.yml -e stack_name="nginx-vm-stack"
```

## Destroying the application
Same as deploying the application, don't forget to set the variable "stack_name"
```
cd heat-openstack-example
ansible-playbook destroy-nginx-vm.yml -e stack_name="nginx-vm-stack"
```


### OpenStach cheat sheets for debugging
```sh
 openstack stack list
 openstack image list
 openstack flavor list
 openstack stack event list <Server>
 openstack stack show nginx-vm-stack
 openstack stack delete nginx-vm-stack
```
