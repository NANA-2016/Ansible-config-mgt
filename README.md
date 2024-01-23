# Ansible-config-mgt
##Ansible  project configuration
#   A n s i b l e - c o n f i g - m g t 
# Ansible installation

![image](https://github.com/NANA-2016/Ansible-config-mgt/assets/141503408/5fbe35c2-06c9-46a9-9962-4608d90503fe)

commands used for ansible installation

sudo apt update
sudo apt install ansible

##confuguring jenkins . Ataached screen shots show it is up and running with playbooks and inventory folder with there content in Ansible .

![image](https://github.com/NANA-2016/Ansible-config-mgt/assets/141503408/8f958eae-bb6e-4449-979c-212d4ad83751)

![image](https://github.com/NANA-2016/Ansible-config-mgt/assets/141503408/d3736862-1a86-4a5b-847c-39d4117f6006)


##Ansible development on vs code opening folder
 invertory
 Files:dev,staging,uat,prod all .yml

 Playbooks
 File:Common.yml
 
![image](https://github.com/NANA-2016/Ansible-config-mgt/assets/141503408/29dcfe09-f055-48be-aaff-eb3c98f7c24c)

 Install jenkins and ensure it active and running with the commands attached below.

 sudo apt update
sudo apt install fontconfig openjdk-17-jre

sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo dnf upgrade
# Add required dependencies for the jenkins package
sudo dnf install fontconfig java-17-openjdk
sudo dnf install jenkins
sudo systemctl daemon-reload
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins

![image](https://github.com/NANA-2016/Ansible-config-mgt/assets/141503408/b0e37d83-2b64-4f1a-972b-45c72aef68c4)


use the command shown to clone jerkins ansible  to the git hub repository as the jump server  clone <ansible-config-mgt repo link>



 ##Creating an ssh agent where we will import our key.
 COMMAND 
eval `ssh-agent -s`
ssh-add <path-to-private-key>
ssh-add -l command that confirm ssh key has been added into the jenkins Ansible )

##SSH TO MAIN SERVER COMMAND NOW 
ssh -A ubuntu@public-ip

![image](https://github.com/NANA-2016/Ansible-config-mgt/assets/141503408/a1b7d1fd-a2f5-4c50-bcf3-7c0df633dced)


 UPDATING THE Inventory/dev.yml
[nfs]
<NFS-Server-Private-IP-Address> ansible_ssh_user=ec2-user

[webservers]
<Web-Server1-Private-IP-Address> ansible_ssh_user=ec2-user
<Web-Server2-Private-IP-Address> ansible_ssh_user=ec2-user

[db]
<Database-Private-IP-Address> ansible_ssh_user=ec2-user 

[lb]
<Load-Balancer-Private-IP-Address> ansible_ssh_user=ubuntu

---
- name: update web, nfs and db servers
  hosts: webservers, nfs, db
  become: yes
  tasks:
    - name: ensure wireshark is at the latest version
      yum:
        name: wireshark
        state: latest
   
Creating a common play beook on common.yml
- name: update LB server
  hosts: lb
  become: yes
  tasks:
    - name: Update apt repo
      apt: 
        update_cache: yes

    - name: ensure wireshark is at the latest version
      apt:
        name: wireshark
        state: latest

Using the vs code , the command git add ., git commit -m"" and git push will be used again and again to update the git hub repository for any changes done on the vs code .

cd into Ansible-config-mgt and run the ansible test .

Chweck id wire shark has ben installed . Wire shark installation was impossible for me.





 


 
