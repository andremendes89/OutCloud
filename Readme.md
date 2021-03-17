# OutCloud Project

This project is for creating two machines via Ansible for automation and configuration:
 - Machine A with Wordpress 
 - Machine B with MySQL 

### Pre-Requisites

- Having Linux (no GUI) installed on Machine A and Machine B.
    - Having openssh-server net-tools installed on both machines.

- Having ansible openssh-server net-tools git installed on main machine (Machine M)

### How to 
__Storage__: I have choosed using a ubuntu/bionic64 minimal version (no GUI) for this exercise and confiured the iso file in the Virtual Box storage.


__Networking:__ Fot Machine A and Machine B be able to talk to each other and for security reasons I have choosed NAT network since it acts like our home network with a wireless router. I have created NAT Network "Rede" and changed IP of Machine M to 192.168.100.6 Machine B to 192.168.100.7 and Machine A to 192.168.100.8.<br>
I need to set a port fowarding for accessing the VM from another bash console <br>
I have followed [VirtualBox PortForwarding](https://www.virtualbox.org/manual/ch06.html "VirtualBox Port Forwarding") to find out how to do it<br>


Installing the tools required:
```
sudo apt update
sudo apt install ansible net-tools git openssh-server 
```

Create an ssh key pair for accessing the VM withouth the need for using password
```
ssh-keygen -t rsa -b 2048 -C "Generating SSH keys for accessing VM"
ssh-copy-id -i <home_dir>/.ssh/id_rsa.pub user@ip_host
```



Create project directory
```
mkdir OutCloud
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

At the end test the connection to your database and wordpress site:

```
telnet -e$ <mysql_machine_ip> 33306
```
Check access to wordpress:
```
curl -v http://<ip_wordpress_machine> 
```

