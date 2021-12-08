# Machine Setup Automation
This project uses Ansible to automate setting up machines for different purposes. 
Once a Virtual Machine has been setup it's configuration can be automated using Ansible from the control machine with the files here. 
This saves time and provides a consistent approach for creating the infrastructure required to perform tasks like development, malware analysis, and pentesting.

<br>

### Details

This repository consists of the following files:
- local.yml -- This is the Playbook that Ansible expects to find by default in pull-mode, think of it as an "index" of sorts that pulls other Playbooks in.

- ansible.cfg -- Configuration settings for Ansible goes here.

- group_vars/ -- This directory is where I can place variables that will be applied on every system.

- host_vars/ -- Each laptop/desktop/server gets a host_vars file in this folder, named after its hostname. Sets variables specific to that computer.

- inventory -- This is the inventory file and is used by Ansible to known which group to put a machine in.

- role -- This directory contains my base, dev_machine, attack_machine, and malware_machine roles. Every host gets the base role. Then either is assigned another role via the inventory file, depending on it's intended usage.

- roles/base -- This role is for every host, regardles of the type of device it is. This role contains things that are intended to be on every host, such as default configs, users, etc.

- roles/dev_machine -- This role is for development machines and installs a development environment that currently includes; Python, Go, VSCode, and neovim. It also changes GUI-specific things based on the GNOME desktop.

- roles/attack_machine -- This role is for machines used for penetration testing and it installs pentesting tools and can be used to attack targets.

- roles/malware_machine -- This role is for malware analysis machines and installs appropriate tools for this.



<br>

### Usage

1. create default VM of machine and install OpenSSH server (`sudo apt install openssh-server`).
2. SSH into the system with `ssh <user>@<ip>`.
3. run `ansible-playbook --ask-become-pass bootstraml.yml -k <user_pass>` to prime machine for setup.
4. find IP address of machine and add it under the configuration group in `inventory` file.
5. add required variables in `host_vars` directory under IP address of the machine.
5. run `ansible-playbook machines.yml -k` (if you don't want to use SSH key) to configure defined machine.

> Alternatively you can setup an SSH key and run `ansible-playbook machines.yml` (see commented out lines in boostrap.yml)

<br>

To do:
- automate attack_machine
- automate malware_machine
