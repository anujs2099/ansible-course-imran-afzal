# Course: https://www.udemy.com/course/complete-ansible-devops-automation-training/

# Note: all ansible, ansible-doc, ansible-playbook commands are performed on control vm

# ansible-playbook syntax check
ansible-playbook --syntax-check helloworld.yaml

# ansible-playbook dry run
ansible-playbook --check helloworld.yaml

# ansible-playbook execution
ansible-playbook helloworld.yaml

# ansible-modules help
ansible-doc -l | grep -i <search word>
ansible-doc -l | grep -i yum
ansible-doc yum
/EXAMPLE

# hosts file
cat /etc/ansible/hosts | less

# list hosts
ansible-inventory --list
ansible all --list-hosts

# list all hosts on which a particular playbook will be executed
ansible-playbook httpd-telnet.yaml --list-hosts
ansible-playbook helloworld.yaml --list-hosts

# setup the hosts file
on remote vms
ip addr | grep -i inet

on control vm
vi /etc/ansible/hosts
	<add the ip address either separately or as a group>
ansible-inventory --list

# setup passwordless ssh
on control vm
id
ssh-keygen
ssh-copy-id 10.253.1.18
<provide the remote vms password>
ssh-copy-id 10.253.1.20
<provide the remote vms password>
ssh 10.253.1.18
	exit
ssh 10.253.1.20
	exit

# test inventory file
ansible all -m ping

# run ad-hoc commands on remote vms
ansible all -a "uptime"

# disable the deprecation warnings
cat /etc/ansible/ansible.cfg | grep deprecation_warning
	deprecation_warnings = False

# Install additional Ansible collection for firewalld
Note: This is not needed on rhel8
ansible-galaxy collection install ansible.posix

# Start a playbook at a specific task
ansible-playbook yamlfile.yaml --start-at-task 'Task name'
