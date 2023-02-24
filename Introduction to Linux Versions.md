# Introduction to Linux versiona

Linux is a free and open-source operating system that is based on the Unix operating system. It was created by Linus Torvalds in 1991 and has since become a popular alternative to commercial operating systems such as Windows and macOS.

### Features of LINUX operating system-

- **Open source**: *Linux is an open-source operating system, which means that the source code is available for anyone to view, modify, and distribute. This allows for greater transparency, collaboration, and innovation.*
- **Security**: *Linux is known for its security features, including built-in firewalls and user permissions, which help to protect against malware and other security threats.*
- **Stability**: *Linux is known for its stability and reliability, with many systems running for years without requiring a reboot or experiencing crashes.*
- **Flexibility**: *Linux is highly customizable, allowing users to choose from a wide range of software and tools to create a tailored system that meets their specific needs.*
- **Multitasking**: *Linux supports multitasking, which means that multiple processes can run simultaneously without impacting system performance.*
- **Portability**: *Linux can run on a wide range of hardware platforms, from small embedded devices to large servers and supercomputers.*
- **Compatibility**: *Linux can run many popular software applications, including web browsers, office suites, media players, and development tools.*
- **Command line interface**: *Linux provides a powerful command line interface, which allows users to perform a wide range of tasks quickly and efficiently.*
- **Community support**: *Linux has a large and active community of developers and users, who provide support, documentation, and resources for users.*
- **Cost-effective**: *Linux is free to use and distribute, which makes it a cost-effective option for individuals and organizations.*

### Why it is believed that Linux is better for Development-

Linux provides a powerful command Line Interface that allows developers to perform a wide range of tasks quickly and efficiently. This can be especially useful for tasks such as debugging, file management, and automation. 

- **Package managers**: *Linux provides package managers that allow developers to easily install, update, and manage software packages. This can save time and effort compared to manually installing and managing software.*
- **Compatibility**: *Linux can run many popular software applications and programming languages, including Python, Java, Ruby, and PHP, making it a popular choice for development.*
- **Security** : *Linux is known for its security features, which can help to protect against malware and other security threats. This can be especially important for developers who may be handling sensitive data.*
- **Stability** : *Linux is known for its stability and reliability, which can help to prevent crashes and data loss during the development process.*
- **Flexibility** : *Linux is highly customizable and can be tailored to meet specific development needs. This can include customizing the desktop environment, installing development tools, and configuring network settings.* 

Overall, the combination of these features has made Linux a popular and attractive option for developers looking for a stable, flexible, and efficient operating system for development.

### How does Linux Work?

Linux works differently than proprietary operating systems like Windows or macOS, as it follows a modular design where the kernel, the core component of the operating system, interacts with other components to provide a full computing environment.

Here's a high-level overview of how Linux works:

`Kernel`:  At the heart of Linux is the kernel, which manages the system's hardware and software resources. The kernel interacts directly with the computer's hardware to perform tasks like allocating memory, managing input/output (I/O) operations, and controlling processes.

`Shell` : Linux has a command-line interface, also called a shell, that allows users to interact with the system by entering commands. The shell is responsible for interpreting commands and executing them on behalf of the user.

`Libraries and Utilities` : Linux comes with a wide range of software libraries and utilities that provide essential functionality to the system. These libraries and utilities work together to provide functions like managing files, networking, and user authentication.

`Applications` : Linux supports a wide variety of applications, ranging from text editors and web browsers to productivity suites and multimedia players. Many of these applications are open-source and available for free, while others may require a license or a fee.

In summary, Linux works by providing a modular, open-source environment in which the kernel interacts with other components to manage hardware and software resources while providing a command-line interface and a wide range of libraries, utilities, and applications.

### How to install Linux Kernel Source tree for All Versions -

**Step 1)**
To clone the Linux Kernel Stable Tree. Make a folder named "Linux-stable" in the home location: home/username-clone the repo in the folder "Linux-stable" using
```
git clone git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git. 
```
This will download the current kernel source repository. This will take lots of time, so just hang on!

![image](https://user-images.githubusercontent.com/54492585/221061737-7aef6c9e-74eb-458b-8ecd-a387b955d52a.png)

Hurray! you are done! You will see these files once you are done!

![image](https://user-images.githubusercontent.com/54492585/221061778-2b0a552a-7aa7-4612-9571-90121f132a8e.png)

Various versions of tags are available in Linux-stable which can be seen using git tag -l.

![image](https://user-images.githubusercontent.com/54492585/221061810-43dcfbe3-cf85-4dd6-9575-766eaa623deb.png)

There, are 4711 versions of Linux now, and every Thursday a new version is added. You can git checkout to the version you want. An example is shown below-

![image](https://user-images.githubusercontent.com/54492585/221061847-fb815f96-4161-4cdb-9736-b6958851e10b.png)

**Step 2)** Additionally, you will need to clone files for different versions of the Linux kernel.
```
git clone https://git.kernel.org/pub/scm/linux/kernel/git/xiang/erofs-utils.git
```

![image](https://user-images.githubusercontent.com/54492585/221061874-b105f1f6-0b60-4631-8495-bca2222eac27.png)

![image](https://user-images.githubusercontent.com/54492585/221061899-90706a87-c3d0-4613-bb8d-d55ed063b998.png)

```
git clone https://git.kernel.org/pub/scm/linux/kernel/git/legion/kbd.git
```

![image](https://user-images.githubusercontent.com/54492585/221061920-6764a22f-8a96-4ba0-8772-80a9b7d53607.png)

![image](https://user-images.githubusercontent.com/54492585/221061932-dc49c5b4-f6d2-4f1c-a810-b70bb1144816.png)

The following versions are available in the archives kernel source tree:- `0.99` , `1.01wip` , `1.03wip` , `1.04` , `1.05` , `1.06` , `1.08` , `1.10` ,  `1.12` , `1.14` , `1.14.1` , `1.15` , `1.15.1` , `1.15.1-rc1` , `1.15.2` , `1.15.3` , `1.15.4` , `1.15.5` , `1.15.5-dev` , `2.0.0` , `2.0.1` , `2.0.2` , `2.0.2-rc2` , `2.0.3` , `2.0.3-rc1` , `2.0.4` , `2.0.4-rc1` , `2.5-rc1.1` , `2.5-rc1.2` , `2.5-rc2` , ` v2.0.90` , `v2.1.0` , `v2.2.0` , `v2.2.90` , `v2.3.0` , ..............................to `v2.4.0` ,`v2.5-rc1` , `v2.5.0` , `v2.5.1` 

```
git clone https://git.kernel.org/pub/scm/linux/kernel/git/tglx/history.git
```
![image](https://user-images.githubusercontent.com/54492585/221061953-6ac238d0-2a79-47d4-9bdb-99b2669c66ff.png)
![image](https://user-images.githubusercontent.com/54492585/221061968-9ecfbe6f-89e0-46b2-ade3-feae169f9f18.png)


The following versions are available in the archives kernel source tree:-`lia64-v2.5.8-pre3` , `lia64-v2.5.10` , `lia64-v2.5.18` , `lia64-v2.5.39` , `lia64-v2.5.45` , `lia64-v2.5.52+` , `lia64-v2.5.60` , `lia64-v2.5.64` , `lia64-v2.5.67` , `v2.5.0` , `v2.5.1` , `v2.5.2` , `v2.5.3` , `v2.5.4` , `v2.5.4-pre1` , `v2.5.4-pre2` , `v2.5.4-pre3` , `v2.5.4-pre4` , `v2.5.4-pre5` , `v2.5.4-pre6` , `v2.5.5` , `v2.5.5-pre1` , `v2.5.6` ,..............to   ` `v2.6.12-rc2` 

```
git clone https://kernel.googlesource.com/pub/scm/linux/kernel/git/nico/archive
```

![image](https://user-images.githubusercontent.com/54492585/221061993-c88f38df-84dc-48f1-9d2d-6b3d45c61bb6.png)

![image](https://user-images.githubusercontent.com/54492585/221062007-fa3a02c6-9d4e-4eb8-a403-121332c30e01.png)


The following versions are available in the archives kernel source tree:- `v0.01` , `v0.10` , `v0.11` , `v0.12` , `v0.95` , `v0.95a` , `v0.95c` , `v0.95c+`, `v0.96a` , `v0.96a-pl1` , `v0.96a-pl2` , `v0.96a-pl3` , `v0.96a-pl4` , `v0.96b` , `v0.96b-pl1` , `v0.96b-pl2` , `v0.96c` , `v0.96c-pl1`  ............ to `v0.99.15` , `v1.0` , `v1.0-pre1`
