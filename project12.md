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


