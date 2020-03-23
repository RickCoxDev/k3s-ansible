# Kubernetes for Raspberry Pi
This project is a collection of [Ansible](https://www.ansible.com/) playbooks to install kubernetes on a group of Raspberry Pi boards. There is support for installing either [k8](https://kubernetes.io/) or [k3](https://k3s.io/). Along with these playbooks there is also one for installing the [kubernetes dashboard](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/).

## Setup
- Install ansible on your computer. Go [here](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) for instructions.
- Make sure your raspberry pi's are setup and you are able to ssh into them. (Will not be covered here)
- Update inventory file to match the info required to ssh into your raspberry pi's
- Run: 
  ```shell
  ansible-playbook k3s.yml
  ```
  or
  ```shell
  ansible-playbook k8s.yml
  ```
  based on whether you want K3s or K8s

## Ansible Inventory
The inventory file is pretty self explanitory. What ever host names you set in the inventory file will be set for the raspberry pi's in the installation playbooks. Under the master group place the host names of ones you want to serve as master nodes.

## Playbooks

| File Name       | Description                  |
|-----------------|------------------------------|
| k3s.yml         | Install K3                   |
| k3s-cleanup.yml | Uninstall K3                 |
| k8s.yml         | Install K8                   |
| k8s-cleanup.yml | Uninstall K8                 |
| dashboard.yml   | Install Kubernetes Dashboard |

### K3s
As a part of installing K3s [Traefik](https://docs.traefik.io/) and a Loadbalancer is added to the cluster. In the future I will add support to allow you to update the traefik config as a part of installing k3s.

### K8s
When running the K8s installation playbook you are prompted whether to install [Weave](https://www.weave.works/docs/net/latest/overview/) or [Flannel](https://github.com/coreos/flannel) to use are your network between the nodes.