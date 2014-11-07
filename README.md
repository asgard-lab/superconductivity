superconductivity
=================

This repository contains the source code, documentation and related material for the Superconductivity project.

The Superconductivity project explores a number of components involved in computer networking emulations, with the objective to improve scalability in high bandwidth scenarios where possible.


Motivation
==========

Nowadays, there is no shortage of tools and solutions for emulating a network topology. One current trend is to exercise real networking code in a mostly virtualized environment, exploiting the facilities offered in modern kernels. In such scenarios, virtual machines or containers are deployed and interconnected to replicate the desired topology.

A featured example in the Software-Defined Networking area is [Mininet](https://github.com/mininet/mininet), a tool frequently used for rapid prototyping. It currently emulates a complete network on a single machine, using process-based virtualization (Linux namespaces / containers) for hosts, Open vSwitch for OpenFlow switches, and virtual ethernet pairs as links.

There has been efforts to develop a "cluster edition" for Mininet, partitioning the network topology and enabling it to run on more than a single 
machine. However, this does not solve scalability issues for high bandwidth experiments -- distributing a link on multiple machines ins't possible.

Inspiration to solve this problem comes from the notion of *time dilatation* [Diwaker Gupta et al., "To Infinity and Beyond: Time-Warped Network Emulation"; NSDI '06], which lead to naming this project "Superconductivity".

The paper mentioned above applies time dilatation to fully virtualized machines. However, by not counting on the availability of a hypervisor, we found find alternate ways to achieve similar functionality.

Superconductivity starts with a study of the Linux kernel networking stack. Using a set of scripts and tools built on top of **kprobes** and **ftrace**, we can better understand how Mininet interacts with the networking stack. Analyzing the results for Mininet is a starting point that can lead us to a more general approach to this problem.


Authors
=======
 * Cesar Marcondes
 * Ricardo Gesuatto
