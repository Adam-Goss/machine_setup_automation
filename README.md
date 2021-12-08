# machine_setup_automation
This project uses Ansible to automate setting up machines for different purposes. 
Once a VM has been setup it's configuration can be automated using Ansible from the control machine with the files here. 
This saves time and provides a consistent approach for creating the infrastructure required to perform tasks like development, malware analysis, and pentesting.

<br>

Three types of machines are defined for configuration:
- dev_machine = development machine installed with: Python, Go, VSCode, neovim -- Ubuntu
- attack_machine = pentest machine with necessary tools installed -- Ubuntu
- malware_machine = malware analysis machine with analysis tools installed -- TBD

<br>

Setup:
1. create default VM of machine and install OpenSSH server (`sudo apt install openssh-server`)
2. SSH into the system with `ssh <user>@<ip>` 
3. run `ansible-playbook --ask-become-pass bootstraml.yml -k <user_pass>`
4. find IP address of machine and add it under the configuration group in `inventory` 
5. add required variables in `host_vars` directory under IP address of the machine
5. run `ansible-playbook machines.yml -k` (if you don't want to use SSH key)

> Alternatively you can setup an SSH key and run `ansible-playbook machines.yml` (see commented out lines in boostrap.yml)

<br>

To do:
- automate attack_machine 
- automate malware_machine
