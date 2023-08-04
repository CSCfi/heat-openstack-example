# heat-openstack-example
Ansible heat OpenStack deployment

Project structure:-

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

## OpenStach cheat sheets
```sh
 openstack stack list
 openstack image list
 openstack flavor list
 openstack stack event list <Server>
 openstack stack show nginx-vm-stack
 openstack stack delete nginx-vm-stack
```

## Deploying the application

```
ansible-playbook site.yml
```

## Destroying the application
```
export STACK_NAME=nginx-vm-stack
ansible-playbook destroy-nginx-vm.yml
```
