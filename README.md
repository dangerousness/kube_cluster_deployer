# This is an Ansible driven Kubernetes (K8s) cluster deployer

This currently only supports a single master however you may have as many workers as you want


## Prerequisites for the Cluster

* At least 3 Ubuntu servers virtual or physical

* All must have IPs that you can be reached from a deploy machine running the ansible scripts 

* All servers need to be able to reach eachother as well as connect out to the internet

* All need to have a preexisting sudo user by the name of 'user'

* All servers need to have a minimun of 2 CPUs


## Prerequisites for the deploy machine

* Any Mac or Linux machine with ansible installed

* It should be able to reach the IPs of the aforementioned servers 

* You should already have generated ssh keys on the deploy machine (~/.ssh/id_rsa.pub exists) 


## Config on deploy machine

Clone this repo to the deploy machine:
```bash
git clone https://github.com/dangerousness/kube_cluster_deployer.git
```
cd into that directory (kube_cluster_deployer) and edit the file 'hosts' located in this repo

Change the IPs to match those of your Ubuntu servers:
```
[masters]
master0 ansible_host=10.10.10.53 ansible_user=user

[workers]
worker1 ansible_host=10.10.10.54 ansible_user=user
worker2 ansible_host=10.10.10.55 ansible_user=user
worker3 ansible_host=10.10.10.56 ansible_user=user

[all:vars]
ansible_python_interpreter=/usr/bin/python3
```

## Usage

```bash

ansible-playbook --ask-sudo-pass -i hosts 0_user_setup.yml

ansible-playbook --ask-sudo-pass -i hosts 1_dependencies.yml 

ansible-playbook --ask-sudo-pass -i hosts 2_master.yml 

ansible-playbook --ask-sudo-pass -i hosts 3_workers.yml
```
