# Machine Setup Automation
This project uses Ansible to automate setting up machines for different purposes. 
Once a Virtual Machine has been setup it's configuration can be automated using Ansible from the control machine with the files here. 
This saves time and provides a consistent approach for creating the infrastructure required to perform tasks like development, malware analysis, and pentesting.

---

### Details

This repository consists of the following files:
- **machines.yml** -- This is the default Playbook that Ansible runs and is used to configure all machines using roles.

- **bootstrap.yml** -- This is a bootstrap Playbook that is used to prime all machines to be configured using machines.yml file.

- **ansible.cfg** -- Configuration settings for Ansible.

- **host_vars/** -- Each machine gets a host_vars file in this folder, named after its hostname (or IP address), which sets variables specific to that machine.

- **inventory** -- This is the inventory file and is used by Ansible to known which group to put a machine in.

- **roles** -- This directory contains my base, dev_machine, attack_machine, and malware_machine roles. Every host gets the base role. Then either is assigned another role via the inventory file, depending on it's intended usage.

- **roles/base** -- This role is for every host, regardles of the type of device it is. This role contains things that are intended to be on every host, such as default configs, users, etc.

- **roles/dev_machine** -- This role is for development machines and installs a development environment that currently includes; Python, Go, VSCode, and neovim. It also changes GUI-specific things based on the GNOME desktop.

- **roles/docker_machine** -- This role is for machines that run/host docker images and installs docker, Portainer (for GUI management), and configures Heimdall image for dashboard management of internal services.

- **roles/attack_machine** -- This role is for machines used for penetration testing and it installs pentesting tools and can be used to attack targets.

- **roles/malware_machine** -- This role is for malware analysis machines and installs appropriate tools for this.

---

### Usage

Walkthrough:
1. create default Virtual Machine and install OpenSSH server (`sudo apt install openssh-server`).
2. SSH into the system with `ssh <user>@<ip>`.
3. find IP address of machine and add it under the configuration group in **inventory** file.
4. run `ansible-playbook --ask-become-pass bootstraml.yml -k <user_pass>` to prime machine for setup.
5. add required variables in **host_vars** directory under IP address of the machine.
6. run `ansible-playbook machines.yml -k` (if you don't want to use SSH key) to configure defined machine.

> Alternatively you can setup an SSH key and run `ansible-playbook machines.yml` (see commented out lines in boostrap.yml)

<br>

---

To do:
- add config files and tasks to copy across for common tools in roles/base
- automate docker_machine
- automate attack_machine
- automate malware_machine
