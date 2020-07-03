# Container runtimes
## Cgroup drivers （systemd、cgroupfs）
+ When systemd is chosen as the init system for a Linux distribution, the init process generates and consumes a root control group (cgroup) and acts as a cgroup manager. Systemd has a tight integration with cgroups and will allocate cgroups per process. It's possible to configure your container runtime and the kubelet to use cgroupfs. Using cgroupfs alongside systemd means that there will be two different cgroup managers.
+ Control groups are used to constrain resources that are allocated to processes. A single cgroup manager will simplify the view of what resources are being allocated and will by default have a more consistent view of the available and in-use resources. When we have two managers we end up with two views of those resources. We have seen cases in the field where nodes that are configured to use cgroupfs for the kubelet and Docker, and systemd for the rest of the processes running on the node becomes unstable under resource pressure.
+ Changing the settings such that your container runtime and kubelet use systemd as the cgroup driver stabilized the system. Please note the native.cgroupdriver=systemd option in the Docker setup below.

# Types of container runtimes

+ Docker
+ CRI-O
+ Containerd
