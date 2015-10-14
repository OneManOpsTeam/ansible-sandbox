Ansible Sandbox
===============

A Vagrant-based Ansible development environment to test Ansible roles on multiple operating systems.

List of Linux distribution (used [bento](https://github.com/chef/bento) boxes):

  - CentOS 6
  - CentOS 7
  - Ubuntu 12.04
  - Ubuntu 14.04

Requirements
------------

You must have [Vagrant](https://www.vagrantup.com/), [VirtualBox](https://www.virtualbox.org/) and [Ansible](http://docs.ansible.com/intro_installation.html) installed on your host machine:

Tips
----

To disable host key checking add to `~/.ssh/config`:

```
Host 127.0.0.1
  StrictHostKeyChecking no
  UserKnownHostsFile=/dev/null
```

To use auto-generated inventory create shell aliases:

```
alias vansible="ansible -i .vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory -u vagrant"
alias vansible-playbook="ansible-playbook -i .vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory -u vagrant"
```
