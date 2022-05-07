# Course: https://www.udemy.com/course/complete-ansible-devops-automation-training/

# Note: all ansible, ansible-doc, ansible-playbook commands are performed on control vm

# check the directory structure
tree

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
ansible all -m shell -a "uptime"
ansible [target] -m [module] -a "[module options]"
ansible localhost -m ping
ansible all -m file -a "path=/home/asaxena/adhoc1 state=touch mode='700'"
ansible all -m file -a "path=/home/asaxena/adhoc1 state=absent"
ansible all -m copy -a "src=/tmp/adhoc2 dest=/home/asaxena/adhoc2"
ansible all -m yum -a "name=telnet state=present"
ansible all -m yum -a "name=httpd-manual state=present"
ansible all -m service -a "name=httpd state=started enabled=yes"
ansible all -m shell -a "systemctl status httpd"
ansible all -m yum -a "name=httpd state=absent"
ansible all -m user -a "name=jsmith home=/home/jsmith shell=/bin/bash"
ansible all -m shell -a "echo 'password123' | passwd jsmith --stdin"
ansible all -m user -a "name=jsmith group=asaxena"
ansible all -m user -a "name=jsmith state=absent remove=yes"
ansible all -m group -a "name=jsmith state=absent"
ansible all -m setup
ansible 192.168.84.130 -m shell -a "systemctl reboot"

# disable the deprecation warnings
cat /etc/ansible/ansible.cfg | grep deprecation_warning
	deprecation_warnings = False

# Install additional Ansible collection for firewalld
Note: This is not needed on rhel8
ansible-galaxy collection install ansible.posix

# Start a playbook at a specific task
ansible-playbook yamlfile.yaml --start-at-task 'Task name'

# Start a playbook that executes roles (a role is just one play). You can execute multiple roles on different hosts through one playbook
ansible-playbook httpd-install-through-roles.yaml

# Roles can be created based on:
environments like dev, test, pre-prod, prod
types of servers like webservers, database servers
applications like apache, bind, chrony

# pre-written Roles can be downloaded from Ansible Galaxy at galaxy.ansible.com
<just search for the role in search box>
ansible-galaxy install <role>
ansible-galaxy install singleplatform-eng.users
cat ~/.ansible/roles/singleplatform-eng.users/tasks/main.yml | less

# run specific tag(s) in an ansible playbook
ansible-playbook -h | grep -i tags
ansible-playbook httpbytags.yaml --list-tags
ansible-playbook httpbytags.yaml -t i-httpd
ansible-playbook httpbytags.yaml --skip-tags=i-httpd

# handlers are tasks that only run when notified to start, reload, restart, and stop services but not if the configuration is unchanged

# when condition is used with facts gathered by the setup module
