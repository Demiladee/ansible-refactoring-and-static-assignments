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

updating site.yml file with common-del.yml playbook and running it against dev.yml

![](images/jenkins-ansiblesiteyml77.png)

the code in the playbook deletes the wireshark we installed in the previous project

## configuring uat webservers with a role webserver

launched two new ec2 instances for the uat webservers

created webserver dir

inside webserver dir, created readme.md file, defaults dir, main.yml inside defaults...

screenshot:

![](images/webservers.png)

