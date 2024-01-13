# CIS Hardened ISO Images
CIS provides thorough benchmarks for hardening devices depending on their operating system. Although the configuration of any given endpoint is dependent on its use case, the hardening guidelines provide a great foundation.

I'll be delving into the process of following along with CIS's benchmark for a Windows 10 system. Throughout the hardening process I'll document my procedures as well as any pertinent details regarding the actual security decisions I make!
## Purpose:
I believe in order to properly secure a device, one must know all the ways in which it can break. That's the very foundation on which red teaming in cybersecurity is built upon. Windows has many different intricacies that you might not make note of unless you seek them out, so, naturally, I'm going to seek them out.

The point of going through this process is to familiarize myself with the ins and outs of the most common workstation in businesses across the world. It will assist me in creating images for pen-testing practices by taking a known secure build and tweaking very specific aspects of it.

## Structure:
This project will be broken up between two different, primary directories for the two levels of system hardening covered by CIS in their Windows 10 benchmark. 

| Level | Intended Environment | Use Case | Effects on System |
| ---- | ---- | ---- | ---- |
| L1 | Commercial/Corporate/Enterprise | Provides a strong baseline for the security of an employee/end user | Minimal impact on performance and availability of services |
| L2 | High Security/Highly Sensitive Data | Builds upon L1, expanding its implementation in a way that considers security first before UX | Sacrificed performance, compatibility, and remote access capabilities |

I'll cover L1 in depth first before jumping to L2 <sub>Note: Everything mentioned in L1 applies to systems in L2 as well</sub>

It's additionally worth noting that there are three subcategories for both L1 and L2:
1. L1/L2 + BitLocker (BL): this incorporates the usage of BitLocker, Microsoft's proprietary, software-based disk encryption utility
2. L1/L2 + Next Generation Windows Security (NG): this incorporates an expansion onto the existing Windows Defender utility, enabling next gen capabilities including:
	1. Behavior-based, real-time antivirus protection (constant surveilling of files and apps for behavior deemed unsafe, leading to the subject being quarantined and blocked)
	2. Cloud-delivered protection: a cloud-based security service to rapidly distribute relevant information to Windows Security such as signatures and IoCs; additionally, cloud-based resources are used for constant surveillance as well to enable rapid response
	3. Dedicated protection and product updates
3. L1/L2 + BL + NG: an implementation of L1 or L2 incorporating both BitLocker and Next Generation Windows Security
I'll make note of procedures/policies that pertain to any particular subcategory.

All the information that I'm going to list can be found within CIS's benchmark itself, but what I aim to do is make it a bit more concise and digestible for the average reader that isn't a fan of a >1200 page document.

## Endpoint Details:
The endpoint will be a Windows 10 Pro virtual machine running on VirtualBox. Once Windows 10 has finished installation, the system will be added to a preconfigured Active Directory domain so new policies may be configured through the Group Policy Management Console.

For the Active Directory Domain Controller, I'll be using a Windows Server 2019 virtual machine also running on VirtualBox.

If you'd like to setup the VM for yourself and follow along, you can download the necessary files here:
- [Windows 10 ISO](https://www.microsoft.com/en-us/software-download/windows10)
- [Windows Server 2019 ISO](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)
- [CIS Windows 10 Benchmark](https://www.cisecurity.org/benchmark/microsoft_windows_desktop)
<hr />

# FAQ
## "Wait, why Windows 10?"
In a corporate environment, you can't throw a stick without hitting someone's computer running some version of Windows. Nowadays, Windows 7 has long been phased out for many employee's personal workstations, though it, Windows XP, and Windows 8 still find their fair share of usage for reason ranging from compatibility to straight up being forgotten and never updated. 

Regardless, with Windows 10 going on its ninth year of life and Windows 11 only in year three of its release, along with its adoption still not quite being widespread (source: I still run Windows 10), Windows 10 is undoubtedly the most likely end user operating system. Thus, the best candidate for this project is ol' reliable Windows 10.

## "Isn't this...a lot?"
Yes. Yes it is.

I'm not gonna sugarcoat it, this is going to be very involved and will \[likely] not appeal to most people. It is going to get boring at times, but hey I suppose that's why I'm doing this and you're reading it after it's done, right? We'll keep the suffering to the minimum one required person.

## "Why not just automate it?"
There does exist the tools CIS-CAT Pro and CIS-CAT Lite that automatically scan a system to determine compliance with a given benchmark as well as CIS Build Kits that help automate the process of actually implementing hardened configurations via preconfigured Windows Group Policy Objects and the \*nix shell. And yes, these tools would undoubtedly speed up this process and save me countless hours. However, I have a couple problems with utilizing them:
1. CIS-CAT doesn't actually help me much. Yes, it can check if the configurations that should be enabled by default are properly set, but this is a fresh Windows install. I already know that everything I need to manually setup isn't currently compliant
2. CIS Build Kits are not free, and I'm not a CIS SecureSuite member, so I'll need to perform the manual configurations anyways
3.  Using automated tools kinda defeats the whole purpose of this project
The point of doing this isn't to say that I've done it, it's to experience the process firsthand and to document it so that others can learn from it. Automating things is great and all, but if I want to actually learn all that I'm about to do, I've gotta be the one to do it.
</hr>

# Conclusion
I think that just about covers it! This project is going to take...awhile probably? I'm gonna try to do each section in reasonably sized chunks (I include the word "reasonable" specifically for you, section 18). Building on L2 will begin once L1 finishes, but expect L2 to be far less content overall as the vast majority will be covered in L1.

But yeah, that's it! I hope you enjoy reading through all my documentation! Maybe, just maybe, you'll find that some of my effort will help you in your own security endeavors ✨
