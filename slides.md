---
marp: true
---

<!-- _class: invert -->

## Flatcar - Kubernetes Readiness

* With Flatcar instances up and running in a few seconds, we certainly have to
  know what is already installed and configured in Flatcar Container Linux when
  it comes to bringing up multiple instances/nodes integrated into a kubernetes
  cluster.

---

## Kubernetes Installers

* Kubernetes allows for a professional installation and configuration with open
  source components only.

* One of the most well known installers is developed and releases (published) by
  the community and it is called *kubeadm*.

* It is hosted under the same organization in GitHub, where the *kubernetes*
  (Production-Grade Container Scheduling and Management) is hosted as well as
  *minikube* (Run Kubernetes Locally) and *kops* (Kubernetes Operations (kops) -
  Production Grade K8s Installation, Upgrades, and Management) among others.

* In the nearby organization *kubernetes-sigs* another kubernetes installer
  *kubespray* (Deploy a Production Ready Kubernetes Cluster) can be found.

---

## Kubernetes Installers (II)

* kops and kubespray include functionality to provide and prepare the underlying
  infrastructure mostly on public clouds and then run the core installer.

* So, their design may be called opinionated, and are not easily adopted to
  different assumptions.

  * *kops* brings its own binary.

  * *kubespray* builds upon *ansible*

  * *kubeadm* brings its own binary.

* kubeadm requires the underlying infrastructure to be already provided, runs on
  every node of the kubernetes cluster and integrates it, fed with according
  parameters for finding other nodes - controllers and executors.

---

## Kubernetes GitHub Stars

| Repository | GitHub Stars |
|:-----------|-------------:|
| kubernetes |        83.3K |
| kubeadm    |         2.9K | 
| minikube   |        22.6K |
| kops       |        13.6K |
| kubespray  |        22.5K |

---

<!-- _class: invert -->

## Kubernetes Ingredients

* A Kubernetes cluster has usually two or three types of nodes.

  * [etcd nodes]

  * controller nodes

  * executor nodes

* All control nodes make the so called control plane.

* Instead of isolated etcd nodes, etcd functionality can live on controller
  nodes as well and this configuration is called *stacked control plane*.

---

<!-- _class: invert -->

## Kubernetes Ingredients (II)

* etcd serves as the brain of the cluster, realized by an eventually consistent
  datastore.

* controller nodes serve as the heart of the cluster and its components are:

  * [etcd — in a stacked configuration.]

  * kube-apiserver — API and core of our cluster

  * kube-controller-manager — performs operations on Kubernetes resources

  * kube-scheduler — main scheduler

  * [kubelets — start and control containers/pods on executor nodes]

  * [container runtime]

  * [kube-proxy] and or network fabric 

---

<!-- _class: invert -->

## Kubernetes Ingredients (III)

* controller nodes can set up etcd, kube-apiserver, kube-controller-manager, and
  kube-scheduler either as systemd units with according binaries or as static
  pods with container images.

  * kubeadm sets up the control plane with static pods ...

  * NB: Rancher Kubernetes Engine (RKE2) brings a third option.

* executor nodes serve as the limbs of the cluster and its components are:

  * kubelets — start and control containers/pods on executor nodes

  * container runtime

  * [kube-proxy] and or network fabric

* Of course, kubelet and container runtime may be optional on controller nodes,
  but they are mandatory on executor nodes.

---

## Kubeadm System Requirements

* Further steps towards a full kubernetes cluster will build upon containerd and kubeadm.

* Installation of containerd

  * Is containerd installed? PATH? Version?

* Installation of kubeadm, kubelet and kubectl

  * Is kubeadm installed? PATH? Version?

  * Is kubelet installed? PATH? Version?

  * Is kubectl installed? PATH? Version?

---

## Kubeadm System Requirements (II)

* Verify what that release tarball of containerd is installed?

  * The small tarball *containerd-1.5.8-linux-amd64.tar.gz* contains

    * containerd, three shims, and ctr

  * The large tarball *cri-containerd-cni-1.5.8-linux-amd64.tar.gz* contains

    * plus cni-plugins, runc, the unit file containerd.service ...

  * We need essentially the large tarball ...

* With respect to kubelet and containerd we have to make sure, that they are

  * enabled and

  * started.

---

<!-- _class: invert -->

## AWS Flatcar Exploration

* This is what we will see. Encouraging.

  * [x] /opt/bin/containerd / v1.5.7
  * [x] /opt/bin/crictl / v1.20.0
  * [x] /opt/bin/runc / 1.0.2
  * [x] /opt/bin/kubeadm / v1.22.4
  * [x] /opt/bin/kubelet / v1.22.4
  * [x] /opt/bin/kubectl / v1.22.4
  
  * [x] containerd.service enabled / active
  * [x] kubelet.service enabled / activing
