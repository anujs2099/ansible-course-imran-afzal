# Course: https://www.udemy.com/course/complete-ansible-devops-automation-training/

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
ansible-inventory --list

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

# 
