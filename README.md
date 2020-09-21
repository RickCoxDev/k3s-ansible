# Kubernetes for Raspberry Pi
This project is a collection of [Ansible](https://www.ansible.com/) playbooks to install kubernetes on a group of Raspberry Pi boards. There is support <s>for installing either [k8](https://kubernetes.io/) or</s> [k3](https://k3s.io/). Along with these playbooks there is also one for installing the [kubernetes dashboard](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/).

## K8s Playbook is **Depricated**
I'm finding more of a use case with using K3s with Raspberry Pi rather than K8 with it being smaller and easier to use. The K8s playbooks you can still find on the [K8s branch](https://github.com/RickCoxDev/raspi-k8s/tree/k8s)

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
  ansible-playbook k8s.yml //Deprecated
  ```
  based on whether you want K3s <s>or K8s</s>

## Ansible Inventory
The inventory file is pretty self explanitory. What ever host names you set in the inventory file will be set for the raspberry pi's in the installation playbooks. Under the master group place the host names of ones you want to serve as master nodes.

## Kubeconfig File
After running the ansible installation playbook the kubeconfig for the resulting cluster will be placed in the kubeconfig folder.

## Playbooks

| File Name              | Description                  |
|------------------------|------------------------------|
| k3s.yml                | Install K3                   |
| k3s-cleanup.yml        | Uninstall K3                 |
| <s>k8s.yml</s>         | <s>Install K8</s>            |
| <s>k8s-cleanup.yml</s> | <s>Uninstall K8</s>          |
| dashboard.yml          | Install Kubernetes Dashboard |

### K3s
#### Components
As a part of installing K3s there are a number of component that are [installed](https://rancher.com/docs/k3s/latest/en/installation/install-options/server-config/#kubernetes-components).
- coredns
- servicelb
- traefik
- local-storage
- metrics-server

The K3s playbook will prompt you on what components you don't want installed. By default they are all installed. In the future I will add support to allow you to update the traefik config as a part of installing k3s.

#### External Database
A standard K3s installation will use Sqlite embedded database. If you wish to use an external database fill out the connection settings in `database.yml`. When prompted during the ansible playbook whether to use an external database enter "yes" and the external database will be used.

### K8s **DEPRECATED**
When running the K8s installation playbook you are prompted whether to install [Weave](https://www.weave.works/docs/net/latest/overview/) or [Flannel](https://github.com/coreos/flannel) to use as your network between the nodes.