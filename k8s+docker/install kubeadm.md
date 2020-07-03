# [Installing kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)
## Before you begin
+ One or more machines running one of:
+ Ubuntu 16.04+
+ Debian 9+
+ CentOS 7
+ Red Hat Enterprise Linux (RHEL) 7
+ Fedora 25+
+ HypriotOS v1.0.1+
+ Container Linux (tested with 1800.6.0)
+ 2 GB or more of RAM per machine (any less will leave little room for your apps)
+ 2 CPUs or more
+ Full network connectivity between all machines in the cluster (public or private network is fine)
+ Unique hostname, MAC address, and product_uuid for every node. See here for more details.
+ Certain ports are open on your machines. See here for more details.
+ Swap disabled. You MUST disable swap in order for the kubelet to work properly

## Installing runtime
Linux node | other operating systems
  --- | ---
By default, Kubernetes uses the Container Runtime Interface (CRI) to interface with your chosen container runtime.|  By default, kubeadm uses Docker as the container runtime. The kubelet integrates with Docker through the built-in dockershim CRI implementation.
If you don't specify a runtime, kubeadm automatically tries to detect an installed container runtime by scanning through a list of well known Unix domain sockets. The following table lists container runtimes and their associated socket paths:
Runtime	Path to Unix domain socket	Docker	/var/run/docker.sock	containerd	/run/containerd/containerd.sock	CRI-O	/var/run/crio/crio.sock
If both Docker and containerd are detected, Docker takes precedence. This is needed because Docker 18.09 ships with containerd and both are detectable even if you only installed Docker. If any other two or more runtimes are detected, kubeadm exits with an error.
The kubelet integrates with Docker through the built-in dockershim CRI implementation.
See [container runtimes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/) for more information.|See [container runtimes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/) for more information.


## Configure cgroup driver used by kubelet on control-plane node

+ When using Docker, kubeadm will automatically detect the cgroup driver for the kubelet and set it in the /var/lib/kubelet/config.yaml file during runtime.

+ If you are using a different CRI, you have to modify the file with your cgroupDriver value, like so:
```shell
apiVersion: kubelet.config.k8s.io/v1beta1
kind: KubeletConfiguration
cgroupDriver: <value>
```
+ Please mind, that you only have to do that if the cgroup driver of your CRI is not cgroupfs, because that is the default value in the kubelet already.
>Note: Since --cgroup-driver flag has been deprecated by kubelet, if you have that in /var/lib/kubelet/kubeadm-flags.env or /etc/default/kubelet(/etc/sysconfig/kubelet for RPMs), please remove it and use the KubeletConfiguration instead (stored in /var/lib/kubelet/config.yaml by default).

+ Restarting the kubelet is required:
```
systemctl daemon-reload
systemctl restart kubelet
```
+ The automatic detection of cgroup driver for other container runtimes like CRI-O and containerd is work in progress.

# Troubleshooting
+ If you are running into difficulties with kubeadm, please consult our [troubleshooting docs.](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/troubleshooting-kubeadm/)
