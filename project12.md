## jenkins job enhancement

creating new directory in jenkins-ansible server to store artifacts

`$ sudo mkdir /home/ubuntu/ansible-config-artifact`

change dir permission so jenkins can save files there

`$ chmod -R 777 /home/ubuntu/ansible-config-artifact`

![](images/jenkins-ansiblemkdirchmod1.png)

installing copy artifact plugin on jenkins

![](images/jenkins-ansiblecopyartifact2.png)

creating freestyle project, save_artifacts, and configuring it to be triggered upon completion of the ansible project

![](images/jenkins-ansiblesaveartigener3.png)

![](images/jenkins-ansiblesaveartigener33.png)

![](images/jenkins-ansiblesaveartigener333.png)

the artifacts will be saved into /home/ubuntu/ansible-confi-artifact dir

![](images/jenkins-ansiblesaveartigener333ansiblejob.png)

![](images/jenkins-ansiblesaveartigener333ansiblejobaggregate.png)

configuring /home/ubuntu/ansible-config-artifact to allow jenkins have access 

`$ sudo apt install acl -y`

this command should be used on each dir: /home, /ubuntu...

`$ sudo setfacl -m u:jenkins:rwx /home/ubuntu/ansible-config-artifact/`

![](images/jenkins-ansiblesetfaclonall4.png)

![](images/jenkins-ansiblesetfaclonallbuild44.png)

![](images/jenkins-ansiblesetfaclonallbuild444.png)

![](images/jenkins-ansiblesetfaclonallbuild44444.png)

`$ ls /home/ubuntu/ansible-config-artifact`

![](images/jenkins-ansiblesetfaclonallbuild4444.png)

## refactoring ansible code by importing other playbooks into site.yml

creating new file, site.yml, inside playbooks dir

creating new dir, static-assignments, inside the repo

moving common.yml inside static-assignments dir

importing common.yml playbook inside site.yml file

![](images/jenkins-ansiblesiteyml6.png)

creating another playbook, common-del.yml, to run against dev servers

![](images/jenkins-ansiblecommondel7.png)

updating site.yml file with common-del.yml playbook 

![](images/jenkins-ansiblesiteyml77.png)

editing /etc/ansible file to include inventory path containing all the servers ip address in the config file

`$ sudo vi /etc/ansible/ansible.cfg`

` inventory = /home/ubuntu/ansible-config-artifact/inventory`

pinging the servers via ansible to be sure they are accessible

`$ ansible all -m ping`

![](images/jenkins-ansibleinventoryping88.png)

![](images/jenkins-ansiblepinginventory9.png)

running site.yml against dev.yml 

`$ ansible-playbook -i inventory/dev.yml playbooks/site.yml`

![](images/jenkins-ansibleplaybooktest10.png)

confirming the code worked by ssh-ing into each webserver to confirm wireshark has been deleted

`$ ssh@public-ip-address`

`$ which wireshark`

`$ wireshark --version`

![](images/jenkins-ansibleplaybooktest1010.png)

## configuring uat webservers with a role webserver

launched two new ec2 instances for the uat webservers

created webserver dir

inside webserver dir, created readme.md file, defaults dir, main.yml inside defaults...

screenshot:

![](images/webservers.png)

updating uat.yml file with uat webservers ip addresses

![](images/jenkins-ansibleuatservers11.png)

edited /etc/ansible to add full path to roles dir

`$ sudo vi /etc/ansible/ansible.cfg`

`$ roles_path = /home/ubuntu/ansible_config_artifact_roles`

![](images/jenkins-ansibleroles12.png)

![](images/jenkins-ansibleroles1212.png)

populating main.yml file with tasks to:

install & configure apache

clone tooling website from github

ensure tooling website code is deployed to /var/www/html on each of the 2 uat webservers

make surre httpd service is started

![](images/jenkins-ansiblemainyml13.png)

creating uat-webservers.yml assignment within static-assignments dir to reference roles

![](images/jenkins-ansibleuatwebserver14.png)

importing uat-webservers.yml in site.yml file

![](images/jenkins-ansiblesiteyml1414.png)

