# OutCloud Project

This project is for creating two machines via Ansible for automation and configuration:
 - Machine A with Wordpress 
 - Machine B with MySQL 

### Pre-Requisites

- Having Linux (no GUI) installed on Machine A and Machine B.
    - Having openssh-server net-tools installed on both machines.

- Having ansible openssh-server net-tools git installed on main machine (Machine M)

### How to 
Storage: I have choosed using a ubuntu/bionic64 minimal version (no GUI) for this exercise and confiured the iso file in the Virtual Box storageI am using a ubuntu/bionic64 minimal version (no GUI) for this exercise
<br>
In case you are using NAT network on the host you need to set a port forwarding for accessing the VM from another bash console <br>
Go to [VirtualBox PortForwarding](https://www.virtualbox.org/manual/ch06.html "VirtualBox Port Forwarding") to find out how to do it<br>

Using a bash console or windows WSL create an ssh key pair for accessing the VM
```
ssh-keygen -t rsa -b 2048 -C "Generating SSH keys for accessing VM"
ssh-copyid -i <home_dir>/.ssh/id_rsa.pub user@ip_host
```

Installing the tools required:
```
sudo apt update
sudo apt install ansible vagrant virtualbox net-tools git openssh-server telnet curl -y
```
Create your project directory
```
mkdir vagrant_project && cd vagrant_project
touch Vagrantfile
touch playbook.yml
touch inventory
```
Encrypt your variables using ansible-vault command:
```
ansible-vault encrypt vars.yml
```
Run ansible command:
```
ansible-playbook playbook.yml -i inventory.ini --user=andre --extra-vars "ansible_sudo_pass=" --ask-vault-password
```
Get the Machines up with
```
sudo vagrant up --provision
```

At the end test the connection to your database and wordpress site:

```
telnet -e$ <mysql_machine_ip> 33306
```
Check access to wordpress:
```
curl -v http://<ip_wordpress_machine> 
```

