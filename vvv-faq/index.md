# Very, very, very frequently asked questions

## 1. **Firmware.** *What firmware is best? Should I upgrade to a specific firmware? Where should I get to, where should I stay?*

### **A**: Rule of thumb: **lower is better**.

There are two main "levels" on which exploit releases will target currently (this is a lie; there are four, but the other two simply don't matter yet).

**Full system-level** access allows code running in the TrustZone, which implies code running in all lower levels of execution (kernel, userland). This is what you want for "CFW".  
**Homebrew** support allows you to develop and run native applications on the Switch.

Current, there is confirmation of **full system-level access**, through TrustZone exploits, for all firmwares **up to 4.1.0**.  
Likewise, **homebrew** support is *publically* available on **3.0.0**.

#### **System-level access timeline**

Release of full system-level access tools and exploits are expected as development progresses. Priority is on 1.0.0 first.  
The tiers for system-level access are as follows, from soonest to latest: **1.0.0; 2.0.0-3.0.0; 3.0.1-4.1.0**.

#### **Homebrew support timeline**

Release of homebrew access tools, development tools, and exploits are targeting 3.0.0.  
If you are on 2.0.0-2.3.0, you may upgrade to 3.0.0 at your discretion. 2.0.0-3.0.0 will have further system-level access at the same time, after 1.0.0.  
If you are on 1.0.0 we ***do not recommend*** upgrading for this as you will be able to get system-level access first.

**Q: What about more recent/current firmware?**
**A:** There really is nothing left to do but **wait**. Don't update if you can avoid it, or buy an older Switch with older firmware.  
3.0.1 and up has **NOTHING public** so far. 3.x and 4.x are in the running for future TrustZone exploitation, so stay tuned, and do not update from **or to** 3.0.1 and up, including 4.x.

Remember the mantra! **Wait! Don't Update!!**

## 2. **Privileges**. *Kernel? TrustZone? Userland? Horizon? ACE? ROP? EL0? EL3? OMG, WTF?*

### **A:** Chill out, it's not as hard as it looks. Here's a little glossary:

**ROP** is a non-functional form of code execution used to bootstrap further exploitation. PegaSwitch uses ROP to pop into ACE.  
**ACE** is **A**rbitrary **C**ode **E**xecution. This is the "holy grail" of homebrew, and allows one to write programs which run in the Switch.

**Horizon/NX**, aka HOS, is the Switch OS, a modern, service-based modular microkernel OS. It is derived from the OS on the Nintendo 3DS, Horizon/CTR, which extensive changes and modernization throughout. *It is not FreeBSD-based, or based on any known OS/RTOS kernel. It is entirely custom.*

**Userland** is where regular applications on the Switch live.  
They are stripped of all but the most essential privileges, and may be limited in temrs of hardware access and capabilities.

When we say **Kernel** access we're talking about getting ACE from a fully-privileged context.  
This allows for a greatly expanded set of capabilities for homebrew development, system modification, and development capabilities, such as **CFW**, and **patching** of system binaries and applications to change their behaviors.

**TrustZone** is a new concept in the ARM architecture, and Nintendo is using it for the first time on the Switch.  
Its job, through "Secure Monitor calls", or SMCs, is to perform crypto and a small number of system tasks like power management and sleep.  
It is necessary to get TrustZone access to dump one's own keys for off-system crypto, and to bootstrap a custom hypervisor in "EL2".

#### **About TrustZone and ARM hypervistors.**

`/* You are not expected to understand this */` (it isn't going to be on the test), but it's still nice to know and will be included here for reference.

The TrustZone runs within a "Secure World", which is considered, for all intents and purposes, a separate machine from the main OS.  
Secure World can have its own operating system, kernel, and userland running within it, but the Switch does not do that; it runs a very simple "Secure Monitor" on top of EL3.

The **Hypervisor** level is entirely unused on the stock Switch, currently. It sits below TrustZone, but still above the kernel and system. It allows one to virtualize the OS underneath it, which may be useful for close-to-metal development, emulation of the Switch and other systems on the Switch, and booting other OSes such as Linux or Android without interfering with the Horizon system.

Going a bit deeper, **Exception levels**, or privilege levels, in order from least to most privileged, refer to different "planes" of system access, underneath which restrictions can be managed.  
These levels are **Userland** (EL0), **Kernel/Supervisor** (EL1), **Hypervisor** (EL2, unused), and **TrustZone**, or "Secure Monitor" (EL3).

If you want to learn more about ARM hypervisors and the trust platform ARMv8 provides, feel free to ask. More reference manuals will be linked to here in due time.