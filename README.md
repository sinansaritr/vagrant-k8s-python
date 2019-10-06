# Vagrant-k8s-python_flask

This repo helps to create k8s cluster via vagrant/ansible and install flask app with mysql DB.


## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.


### Prerequisites

Vagrant
Virtual Box
kubectl
docker

### Installing

### Download repo

mkdir demo

cd demo 

git clone https://github.com/sinansaritr/vagrant-k8s-python.git


### Install k8s cluster via vagrant

cd demo/vagrant-k8s-python

vagrant up


### Copy the Kubernetes config to your local home .kube dir

scp -P 2222 vagrant@127.0.0.1:/home/vagrant/.kube/config ~/.kube/config
vagrant@127.0.0.1's password: vagrant

kubectl cluster-info


### Dockerize flask app

cd demo/vagrant-k8s-python/app

docker build -f Dockerfile -t myflask:latest .

docker tag myflask:latest $container_registry/myflask:latest

docker push $container_registry/myflask:latest

### PS: Replace "$container_registry" with your container registry in command above and in app-deployment.yaml file below.


### Run app and db onto k8s cluster

cd demo/vagrant-k8s-python/k8s

kubectl create -f db-deployment.yml

kubectl create -f app-deployment.yml


### How to Connect App

kubectl get nodes -o wide  ## Get IP of k8s node since we use NodePort to expose service


### Connect Flask app via browser

http://node_ip:30000
