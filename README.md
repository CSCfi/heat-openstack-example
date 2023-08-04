# Ansible heat OpenStack deployment
Ansible heat OpenStack deployment

## Overview

This repository contains Ansible playbooks and Heat OpenStack template for provisioning a Virtual Machine and deploying an Nginx appliocation as an example on cPouta Openstack enviroonmnet.

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

Then edit the file and fill in the parameters according to your needs.

### Deploying the application

```
cd heat-openstack-example
ansible-playbook site.yml
```

## Destroying the application
```
cd heat-openstack-example
export STACK_NAME=nginx-vm-stack
ansible-playbook destroy-nginx-vm.yml
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
