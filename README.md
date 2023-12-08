# How-To: VM Home Lab
This is a compilation of fundamental basics on Virtual Machines (VMs) that I learned before starting my home lab journey. This post serves as my personal reference guide for navigating the initial steps in building and managing VMs for my home lab.

<h2>Hypervisors</h2>
A hypervisor (or Virtual Machine Monitor - VMM) is software or hardware that creates and runs virtual machines on a physical computer. Its primary function is to abstract and share the underlying hardware resources among multiple virtual machines, allowing them to run independently as if they were on separate physical machines. There are two types of hypervisors:

<li>Type 1 (Bare-Metal): 
<ul>A Type 1 hypervisor, also known as a "bare-metal" hypervisor, operates directly on the physical hardware of a computer or server without the need for an underlying operating system, offering superior performance as it has direct access to hardware resources. It is usually used in enterprise environments, data centres, and cloud infrastructure where optimizing resource efficiency and performance is crucial.</ul>
</li>

<li>Type 2 (Hosted): Installed on top of an existing operating system (e.g., VMware Workstation, Oracle VirtualBox).</li>
<ul>Type 2 hypervisors are installed as software applications on an existing operating system like Windows, macOS, or Linux. It introduces more overhead and typically offers lower performance compared to Type 1 hypervisors. They are commonly used in development, testing, and personal computing scenarios where performance is not the primary concern.</ul>

If the goal is to set up a home lab for learning and testing, a Type 2 hypervisor is often more user-friendly and practical for beginners (like me). It allows users to experiment with virtual machines without needing a dedicated server or complex infrastructure.
