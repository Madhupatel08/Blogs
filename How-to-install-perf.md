
**Step 1)** Install Required Packages like `libelf-dev` `libdw-dev` `binutils-dev` `libaudit-dev`Using Command- 
  
   ```
   sudo apt-get install build-essential libelf-dev libdw-dev binutils-dev libaudit-dev
   ```
    
**Step 2)** Download the Source code for perf-tools v6.3
 - ```
   git clone git://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git
   ```
 - To check files of specific version use eg.for v6.3
    ```    
     cd linux
     git tags
     git checkout v<VERSION_NUMBER>
   ```

**Step 3)** Install perf command- Perf command is available in package  linux-tools-common , linux-intel-iotg-tools-common`, etc. Hence, install any of these. 

**Step 4)** Run `make` command to build the project
 
    4.1) It may show an error since the config file is not set and has to be changed. 
    Run `make xconfig`  for this. 
    4.2) We will also need to install qt5 for this.  Install it using `sudo apt-get install qtbase5-dev` OR `sudo apt install qt5*` and set the path using
                `export PKG_CONFIG_PATH=/usr/lib/x86_64-linux-gnu/pkgconfig:/usr/share/pkgconfig`
    4.3) Check if qt5 has been installed properly using `qmake --version` 
    4.4) Now, Finally run `make xconfig` ad it will run fine.  Sample output:-
    ![](https://paper-attachments.dropboxusercontent.com/s_F00D9D1D5A370E3877A85946245F899B0A44760A51A9A15D2883704479DBE673_1678271988827_image.png)

     And an output screen will be visible that will have the kernel configuration. 
     ![](https://paper-attachments.dropboxusercontent.com/s_F00D9D1D5A370E3877A85946245F899B0A44760A51A9A15D2883704479DBE673_1678272083113_image.png)

**Step 5)** Go to the root directory of the kernel and run the `perf test`


### Extra Guide
-  On running `perf test` this error may come- 
![](https://paper-attachments.dropboxusercontent.com/s_F00D9D1D5A370E3877A85946245F899B0A44760A51A9A15D2883704479DBE673_1678216153393_image.png)

-  If Perf does not exist - Install perf using any of the following -
        - sudo apt install linux-intel-iotg-tools-common    # version 5.15.0-1025.30, or
        - sudo apt install linux-nvidia-tools-common        # version 5.15.0-1017.17
        - sudo apt install linux-tools-common               # version 5.15.0-67.74
        - sudo apt install linux-nvidia-tegra-tools-common 
    
- Note - Do not install two packages, it may cause conflict. 

Run these commands to resolve the issue of conflict

-   `sudo apt-get remove -f linux-intel-iotg-tools-common`
-   `sudo dpkg -i --force-overwrite /var/cache/apt/archives/linux-tools-common_5.15.0-67.74_all.deb`
![](https://paper-attachments.dropboxusercontent.com/s_F00D9D1D5A370E3877A85946245F899B0A44760A51A9A15D2883704479DBE673_1678250832490_image.png)



    
