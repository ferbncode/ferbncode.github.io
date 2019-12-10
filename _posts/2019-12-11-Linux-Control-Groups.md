---
layout: post
title:  "Linux Control Groups"
folder: "Drafts"
categories: linux, cgroups
---

#### Introduction

Linux Control Groups is a kernel feature that limits, accounts for and isolates the CPU, memory, disk I/O and network usage of one or more processes.  The `cgroup` framework is very useful enabling: 

- **Resource Limiting**: Limiting resource usage by a (set of) process. ***Each process can be part of only one `cgroup` at a time***, which may define limits on usage of it's various resources like memory, maximum number of processors running the process, devices which handle peripheral functions, etc.
- **Prioritization**:  A process inside a `cgroup` with higher number of reserved I/O operations, for example,  with work better in comparison to a process inside a `cgroup` with lower number of reserved I/O operations. Hence, a process can be given a higher priority by allocating it to a `cgroup` with higher upper limits on resource usage. A very good example of prioritization using  `cgroups` is explained [here](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/resource_management_guide/control-group-application-examples#proc-IO_throughput_prioritization). 
- **Monitoring**: A groups' resource usage is monitored or measured and this is made available by the kernel. For example, the command `systemd-cgtop` gives a overview of resource usage per `cgroup` (and children `cgroups`).
- **Control**: If a process or set of processes in a `cgroup` possess problems, they (groups of processes) can be frozen, stopped or restarted by the different subsystems or controllers that the Linux Kernel provides.

Control Groups can be hierarchical: Subgroups inherit the limits set on the parent group. A process can also be pinned to a (set of/single) CPU core using `cgroups`. A process is only aware of the resources available to it. 

#### Controllers or Subsystems (explanations would be good addition)

A control group subsystem represents one kind of resources like a processor time or number of `pids` (number of processes in a control group). Linux kernel provides support for following subsystems, as described in this [post](https://0xax.gitbooks.io/linux-insides/content/Cgroups/linux-cgroups-1.html). The controllers or subsystems are responsible for distributing specific type of system resources to a set of one or more processes:

* `cpuset` - assigns individual processor(s) and memory nodes to task(s) in a group.

* `cpu` - uses the (process) scheduler to provide `cgroup` tasks access to the processor resources.

* `cpuacct` - generates reports about processor usage by a group;

* `io` - sets limit to read/write from/to [block devices](https://en.wikipedia.org/wiki/Device_file);

* `memory` - sets limit on memory usage by a task(s) from a group;

* `devices` - allows access to devices by a task(s) from a group;

* `freezer` - allows to suspend/resume for a task(s) from a group;

* `net_cls` - allows to mark network packets from task(s) from a group;

* `net_prio` - provides a way to dynamically set the priority of network traffic per network interface for a group;

* `perf_event` - provides access to [perf events](https://en.wikipedia.org/wiki/Perf_/(Linux/)) to a group;

* `hugetlb` - activates support for [huge pages](https://www.kernel.org/doc/Documentation/vm/hugetlbpage.txt) for a group;

* `pid` - sets limit to number of processes in a group.

#### Let's try them (wip)

* Monitor resource usage: 

```
systemd-cgtop
```



