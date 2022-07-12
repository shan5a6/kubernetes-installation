### If you are working on Aws 
###### Make sure that you are picking the AMI ID's as specified below.
```
Make sure that you are selecting any ubuntu image with version >= Ubuntu Server 20.04 LTS (HVM)
```
### Installing K8S using ansible 

##### Prerequisite 
Luanch one server and install the ansible & git as below
###### Ubuntu
```
apt-get update -y
apt-get upgrade -y
apt-add-repository ppa:ansible/ansible
apt-get update
apt-get  install ansible -y
root@ip-172-31-16-231:~# ansible --version
ansible 2.9.27
Note: Make sure that your ansible version is latest
```

###### Centos
```
yum install epel-release ansible -y
```
###### Amazon Linux
```
sudo amazon-linux-extras install epel -y
sudo yum install ansible -y
```

### Clone the repository 
```
git clone https://github.com/shan5a6/kubernetes-installation.git
cd kubernetes-installation
Update the pem key to file "mykey.pem"
chmod 600 mykey.pem
```
### Run the playbooks for k8s installation
```
update the hosts file with neccessary hosts information
Note: Take only private dns  
```
### hosts file content 
```
[kubernetes-master-nodes]
ip-172-31-29-161.ec2.internal ansible_user=ubuntu os_type="Ubuntu"

[kubernetes-worker-nodes]
ip-172-31-20-9.ec2.internal ansible_user=ubuntu  os_type="Ubuntu"
```

### Configuring  master node & installing neccessary pre configurations 
```
ansible-playbook settingup_kubernetes_cluster.yml
```
### Joining worker nodes to the cluster 
```
ansible-playbook join_kubernetes_workers_nodes.yml
```
### Delete the cluster 
```
ansible-playbook clear_k8s_setup.yml
```
