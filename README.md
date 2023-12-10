# How-To: VM Home Lab
This is a compilation of fundamental basics on Virtual Machines (VMs) that I learned before starting my home lab journey. This post serves as my personal reference guide for navigating the initial steps in building and managing VMs for my home lab.

## Hypervisors
The first component that is very important in building a home lab is a hypervisor. A hypervisor (or Virtual Machine Monitor - VMM) is software or hardware that creates and runs virtual machines on a physical computer. Its primary function is to abstract and share the underlying hardware resources among multiple virtual machines, allowing them to run independently as if they were on separate physical machines. There are two types of hypervisors:

- Type 1 (Bare-Metal):
<ul>A Type 1 hypervisor, also known as a "bare-metal" hypervisor, operates directly on the physical hardware of a computer or server without the need for an underlying operating system, offering superior performance as it has direct access to hardware resources. It is usually used in enterprise environments, data centres, and cloud infrastructure where optimizing resource efficiency and performance is crucial.</ul>

- Type 2 (Hosted): Installed on top of an existing operating system (e.g., VMware Workstation, Oracle VirtualBox).
<ul>Type 2 hypervisors are installed as software applications on an existing operating system like Windows, macOS, or Linux. It introduces more overhead and typically offers lower performance compared to Type 1 hypervisors. They are commonly used in development, testing, and personal computing scenarios where performance is not the primary concern.</ul>

If the goal is to set up a home lab for learning and testing, a Type 2 hypervisor is often more user-friendly and practical for beginners (like me). It allows users to experiment with virtual machines without needing a dedicated server or complex infrastructure.

Being unemployed and also a recent graduate, naturally, I tend to look for free alternatives to everything (To my fellow unemployed fresh grads, I gotcha 😉). There are a lot of free and open-source hypervisors available. Some of the commonly used ones that I found are **[VirtualBox](https://virtualbox.org/)**, **[Proxmox VE](https://www.proxmox.com/en/downloads)** and **[Windows' Hyper-V](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/)**.

If you are running on Windows 10/11 Pro, chances are you already have Hyper-V installed on your computer.
### To Check:
- Open up "Command Prompt" (run as Admin) or "Windows PowerShell".
- In the PowerShell or Command Prompt window, type:

```
Get-WindowsOptionalFeature -FeatureName Microsoft-Hyper-V-All -Online | Select-Object FeatureName, State
```

You have Hyper-V installed if you get the following output:
```
FeatureName              State
-----------              -----
Microsoft-Hyper-V-All Disabled
```
Follow [these steps](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v) to have it enabled.

## Installation
For this guide, I will be installing [VirtualBox](https://www.virtualbox.org/wiki/Downloads).
> [!TIP]
> While downloading, you can check the SHA256 checksums to make sure that your file has not been altered during the download.

### To Check File Hash:
- `cd` to the directory that VirtualBox is downloaded to. Alternatively, right-click on the folder/ directory VirtualBox is downloaded to and click "Open Terminal".
- Use the `Get-FileHash filename` command.
>[!NOTE]
>Your filename will be different, depending on the version you downloaded.
```
PS C:> Get-FileHash .\VirtualBox-7.0.12-159484-Win.exe

Algorithm       Hash                                                                   Path
---------       ----                                                                   ----
SHA256          9769BAE970244249E043BDE9C74D704D25A80773ACCED5C59A04DF64A10A5DB7       C:
```
- Copy the Hash number and compare it with the Hash provided on the download page.
![image](https://github.com/liyanahazizun/VM-basics/assets/80376369/181d9829-7c2d-4217-bb67-143949f7a454)

### To Install:
- Double-click on the VirtualBox file and click "Next" until you see this pop-up.
- You can customize the features you want to download. Otherwise, all features will be downloaded by default.
- Here, you can also choose where you want your VirtualBox to be installed in.
<img src="https://github.com/liyanahazizun/VM-basics/assets/80376369/4ddb9c79-faf5-4995-b5f3-413e86474d93" width="500" height="400">

- Continue to click "Yes" or "Next" until you see the "Install" button and click that to install.
