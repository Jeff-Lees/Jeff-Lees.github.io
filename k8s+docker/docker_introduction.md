# Docker architecture
+ The Docker daemon
+ The Docker client
+ Docker registries

#  Docker objects
+ IMAGES
+ CONTAINERS
+ SERVICES

# The underlying technology
+ Namespaces
  - The pid namespace: Process isolation (PID: Process ID).
  - The net namespace: Managing network interfaces (NET: Networking).
  - The ipc namespace: Managing access to IPC resources (IPC:   _ InterProcess Communication).
  - The mnt namespace: Managing filesystem mount points (MNT: Mount).
  - The uts namespace: Isolating kernel and version identifiers. (UTS: Unix Timesharing System).


+ Control groups:  
Docker Engine on Linux also relies on another technology called control groups (cgroups). A cgroup limits an application to a specific set of resources. Control groups allow Docker Engine to share available hardware resources to containers and optionally enforce limits and constraints.

+ Union file systems:  
Union file systems, or UnionFS, are file systems that operate by creating layers, making them very lightweight and fast. Docker Engine uses UnionFS to provide the building blocks for containers.

+ Container format:  
Docker Engine combines the namespaces, control groups, and UnionFS into a wrapper called a container format
