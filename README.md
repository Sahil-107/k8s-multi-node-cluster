# Kubernetes Multi-node Cluster 
This is an Ansible playbook for launching Kubernetes multi-node cluster in the AWS with one node as the master node and two as the worker node.

### The repo contains 3 Ansible Roles:-
#### provisioning_instances:-
This role will launch the 3 instances in the AWS and update the IP addresses of those instances in **ip.txt** which is the ansible inventry.

#### config-k8s-master:-
This role will first setup the **Kubernetes repo** in the machine and then download and configure **kubeadm** , this will also initialize the **kubeadm** with the specific IP range. You can change the IP range in **main.yml** in **vars** directory.

#### config-k8s-slave:-
This role will configure two slave nodes same as the master node but the difference is that it will not initialize the kubeadm.

### cluster.yml:-
This is the main file it will first launch the instances in the AWS, configure those nodes and at last it will generate the token from the **master node** and paste in the **slave nodes**. But before running this file make sure to enter you IP address in **ip.txt**.

Just create one file by the name **pass.yml** with the help of **ansible vault** (How to use ansible vault you can check [here](https://docs.ansible.com/ansible/latest/user_guide/vault.html)) and you are good to go.

Now just run the `ansible-playbook cluster.yml --ask-vault-pass` it will ask for the vault password in which your AWS credentials is stored and that's all!!
