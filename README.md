# ansible-k8s
### Install a Kubernetes cluster **(using Kubeadm)** on Ubuntu Server using Ansible

This is a work-in-progress, but has been successfully tested on virtual machines running Ubuntu Server (x64) 20.04.2 LTS.

I am new to Ansible, so I am sure there is plenty of code that could be cleaned up or done differently.  I welcome any and all pull requests if you have proposed changes.

WHAT THIS DOES:
* Installs all prerequisite apt packages and does all prerequisite operating system configuration.
* Uses the containerd CRI, which is installed from Docker's official repository.  The containerd configuration is modified to use 'systemd' as the c-group driver.
* Uses the latest version of Kubernetes, which is installed from Google's official repository.
* Initializes a Kubernetes cluster onto a single Master node using kubeadm.
  * The kubelet configuration is modified to use 'systemd' as the c-group driver.
  * The Network CNI being used is [Calico](https://www.tigera.io/project-calico/).
  * Optionally, you can join more Master nodes to the cluster for high availability.  This will use Kube-Vip to provide high availability.
* Join one or more Worker nodes to the cluster.

THE TWO PLAYBOOKS:
* playbook-k8s-master-single.yml
  * This is designed to build a Kubernetes cluster that contains 1 Master Node and N Worker Nodes.
  * This uses the default IP address of the Master Node as the cluster endpoint.
* playbook-k8s-master-cluster.yml
  * This is designed to build a Kubernetes cluster that contains N Master Nodes and N Worker Nodes.
  * This installs [Kube-Vip](https://kube-vip.io/) and therefore uses a Virtual IP (VIP) as the cluster endpoint.

TO DO:
* Test this on Ubuntu Server (ARM) on Raspberry Pi and modify code as needed.
