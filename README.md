## Tips and Hints

### Check Ansible localhost connection
Execute 'ansible all -i "localhost," -c local -m shell -a 'echo hello world'' to confirm Ansible can function on your local box.

You can modify `/etc/ansible/hosts` to include `localhost ansible_connection=local ansible_python_interpreter=python`, add groupings and childs if desired then test again with:
'ansible all -m shell -a 'echo hello world’'

### Basic playbook helloworld.yml
`---
 - hosts: all
   tasks:
     - shell: echo "hello world"`
####
Test the helloworld.yml by executing: `ansible-playbook -i "localhost," -c local helloworld.yml`

***

## How to run this playbook



#### Remote Execution
To run against a remote host via ssh, simply supply inventory via a file, Tower Inventory, `-i '123.456.789.0,'` etc:

`ansible-playbook display-vars.yml -i '<hostmachine>,' -u someuser --private-key=/path/to/privatekey.pem`

#### Local Execution
To run locally, supply loopback in inventory and set `ansible_connection=local`:

`ansible-playbook display-vars.yml -i 'localhost,' -e "ansible_connection=local"`

Possible syntax:
-e "owner= " -e "sg_group_id= " -e "vpc_subnet_id= " -e "iamrole_name= " -e "provision_machine= " -e "cloud_type= " -e "nat= " -e "region= " -e "namespace= " -e "build_node= "

***

## Packer
Packer is an open source tool for building images on many platforms, but these templates are specific to AWS as they utilize the [Amazon EBS Builder](https://www.packer.io/docs/builders/amazon-ebs.html). These templates were tested with version 1.1.1.

This directory contains .json files prefixed with `packer-`. Packer accomplishes this by starting an instance using a temporary keypair, security group etc and running the specified Ansible Playbook against it remotely. Once complete, Packer creates an AMI from the resulting machine and then cleans up any temporary resources created in the process.

Packer generally relies on the Default VPC existing and prefers to launch into the default subnet of said VPC. In the absence of said VPC or for whatever other reason one may wish, you can easily specify a subnet/security group ID in which Packer can launch its builder instances. Packer also accepts a list of regions to which it copies your AMI for disaster recovery or other purposes.


***

## Update permitted SSH group for access (to be scripted):
Check for permissible groups: 'cat /etc/ssh/sshd_config |grep -i allowgroups'
`AllowGroups ssh_users`

Add required groups I.e. 'AllowGroups ssh_users yvrdevops'

### SSH Time-out modification
`cat /etc/ssh/sshd_config |grep -i client
 ClientAliveInterval 600 #10 minutes
 ClientAliveCountMax 0`
Reference `Google "ssh clientaliveinterval clientalivecountmax"`


***

## PIP hints
Force upgrade syntax:
`pip install --upgrade --force-reinstall <package>`

Force ignore to overwrite:
`pip install -I <package>
pip install --ignore-installed <package>`