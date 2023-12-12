# How-To: VM Home Lab
This is a compilation of fundamental basics on Virtual Machines (VMs) that I learned before starting my home lab journey. This post serves as my personal reference guide for navigating the initial steps in building and managing VMs for my home lab.

## Hypervisors
The first component that is very important in building a home lab is a hypervisor. A hypervisor (or Virtual Machine Monitor - VMM) is software or hardware that creates and runs virtual machines on a physical computer. Its primary function is to abstract and share the underlying hardware resources among multiple virtual machines, allowing them to run independently as if they were on separate physical machines. There are two types of hypervisors:

- Type 1 (Bare-Metal):
<ul>A Type 1 hypervisor, also known as a "bare-metal" hypervisor, operates directly on the physical hardware of a computer or server without the need for an underlying operating system, offering superior performance as it has direct access to hardware resources. It is usually used in enterprise environments, data centres, and cloud infrastructure where optimizing resource efficiency and performance is crucial.</ul>

- Type 2 (Hosted): Installed on top of an existing operating system (e.g., VMware Workstation, Oracle VirtualBox).
<ul>Type 2 hypervisors are installed as software applications on an existing operating system like Windows, macOS, or Linux. It introduces more overhead and typically offers lower performance compared to Type 1 hypervisors. They are commonly used in development, testing, and personal computing scenarios where performance is not the primary concern.</ul>

If the goal is to set up a home lab for learning and testing, a Type 2 hypervisor is often more user-friendly and practical for beginners (like me). It allows users to experiment with virtual machines without needing a dedicated server or complex infrastructure.

Being unemployed and also a recent graduate, naturally, I tend to look for free alternatives to everything 😉. There are a lot of free and open-source hypervisors available. Some of the commonly used ones that I found are **[VirtualBox](https://virtualbox.org/)**, **[Proxmox VE](https://www.proxmox.com/en/downloads)** and **[Windows' Hyper-V](https://learn.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/)**.

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
>Your filename might be different, depending on the version you downloaded.
```
PS C:> Get-FileHash .\VirtualBox-7.0.12-159484-Win.exe

Algorithm       Hash                                                                   Path
---------       ----                                                                   ----
SHA256          9769BAE970244249E043BDE9C74D704D25A80773ACCED5C59A04DF64A10A5DB7       C:
```
- Copy the Hash number and compare it with the Hash provided on the download page.
![image](https://github.com/liyanahazizun/VM-basics/assets/80376369/181d9829-7c2d-4217-bb67-143949f7a454)

### To Install:
- Double-click on the VirtualBox file and click **"Next"** until you see this pop-up.
- You can customize the features you want to download. Otherwise, all features will be downloaded by default.
- Here, you can also choose where you want your VirtualBox to be installed.
<img src="https://github.com/liyanahazizun/VM-basics/assets/80376369/4ddb9c79-faf5-4995-b5f3-413e86474d93" width="500" height="400">

- Continue to click **"Yes"** or **"Next"** until you see the **"Install"** button and click that to install.

Now that we have VirtualBox installed, the next step is to create a virtual machine using the desired OS.

## Guest OS

The great thing about virtualization is that you can install and experiment with multiple OSs. In virtualization, generally, one operating system (OS) corresponds to one virtual machine (VM). Each VM runs its own instance of an operating system, and the resources allocated to that VM are dedicated to running that specific OS.

For this documentation, I will be installing Windows 10.

### Windows 10 Installation

- Download [Windows 10 media creation tool](https://www.microsoft.com/en-ca/software-download/windows10). This will allow you to generate an image (ISO file).
- Select **"Accept"** on the license terms.
- Select **"Create installation media for another PC"**, and then select **"Next"**.
- You have the option to choose the language, edition, and architecture (64-bit or 32-bit). I left mine to use the recommended options. Select **"Next"**.
- Now, we have to select which media to use. Select the **"ISO file"** and click **"Next"**.
- To create a Windows 10 VM, open VirtualBox and click **"New"**.
- Enter the name of the VM and select the directory where you want to store the VM. Here, you can choose to store it on an external disk.
- At the **"ISO Image"** section, select **"Other..."** and navigate through your directory to select the Windows ISO file that was installed.
- To configure the OS manually, click on the checkbox that says **"Skip unintended installation."**
> [!NOTE]
> Unintended installation enables automatic installation of the OS. If you have the box unchecked, you will need to set up the required parameters for unattended guest OS installation in the next step. The parameters are **Username and Password, Guest Additions and Additional Options, which include Product Key, Hostname and Domain Name.** 

- Next, modify the VM's hardware (RAM and CPU) specifications. 
- Click on **"Finish"** when you're done.
#### Setting up the OS
- Click on the **"Start"** button.
- Once it's running, you should be able to see the Windows 10 setup. On the setup page, select your language, time, and keyboard preferences, and then select **"Next"**.
- Select **"Install Now"**.
- On the Activate Windows page, choose **"I don't have a product key"** and click on **"Next"** and then choose the Windows 10 variation you want to install. I installed the Windows 10 Pro.
- Click on **"Next"** and click **"Accept the license terms"**.
- Click on **"Next"**, and you will see a page in which you can choose the type of installation. I chose the **"Custom: Install Windows only"** and DONE!

### Kali Linux Installation
- I would recommend downloading the [pre-built Kali images](https://www.kali.org/get-kali/#kali-virtual-machines) for VM. However, you can manually download Kali Linux using the [ISO file](https://www.kali.org/get-kali/#kali-installer-images).
- Depending on your machine, download the 64-bit or 32-bit version for VirtualBox. To check machine specification, run the following in **Command Prompt**:
```
echo %PROCESSOR_ARCHITECTURE%
```
> [!CAUTION]
> The Kali Linux image file is approximately 3 GB in size. Before starting the download, ensure that your device has sufficient available storage space. I recommend having a strong and stable internet connection to prevent interruptions during the download process. If your device has limited storage, consider downloading the file to an external storage device for convenience.

#### Setting up the OS
- To set up the OS in VirtualBox, we first need to extract the file.
- Once the file has been extracted, navigate into the folder and double-click on the file with the `.vbox` extension. It will automatically be imported into VirtualBox.
>[!NOTE]
> The default login credentials for Kali are as follows: the username is "kali," and the password is also set to "kali." 


## Questions
A list of questions I had throughout my learning about VMs

**1.  Q: Can VM be installed on an external hard disk?**
    
Yes, a VM can be installed on an external hard disk. Most virtualization platforms allow choosing the location where VM files, including the virtual hard disk file and configuration files, are stored.

Here are the general steps to install a VM on an external hard disk:
- Connect the external hard disk to your computer.
- Install the hypervisor on your computer.
- Configure VM Settings:
  - When creating a new virtual machine, or if you're modifying the settings of an existing one, choose the external hard disk as the location for storing VM files.
- Continue with the VM creation process or start the existing VM. The hypervisor will use the external hard disk as the storage location for the VM.
- Once the VM is created or started, it will operate using the resources on your computer, but the VM files (disk image, configuration) are stored on the external hard disk.

Keep in mind the following considerations:
- Performance: Running a VM from an external hard disk may result in slightly lower performance compared to running it from an internal drive.
- Storage Space: Make sure that the external hard disk has enough space for the VM files and any additional data you plan to store within the VM.
- Connectivity: Make sure the external hard disk remains connected while the VM is running, as the VM relies on access to its files.

**2. Can the ISO file be installed on an external hard disk?**

Yes, it can. After following the installation steps above, you will be presented with a screen asking where to have it installed. You can connect your external hard disk to the computer and save it there.

**3. Can the ISO file be deleted after mounting it to the VM?**

Yes, once you have successfully installed the operating system on your virtual machine using the ISO file, you can delete the ISO file from your laptop. The ISO file is only needed during the installation process. However, so that you know, you will need to use the ISO file every time you create a new VM. If you plan to create multiple VMs with the same OS, save the ISO file externally so you have it whenever you need it instead of installing it every single time.




