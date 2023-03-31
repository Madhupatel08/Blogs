# Build AGL Image

### 1. QEMU (Emulation)

1. Download the [compressed prebuilt image](https://download.automotivelinux.org/AGL/snapshots/master/latest/qemux86-64/deploy/images/qemux86-64/agl-demo-platform-crosssdk-qemux86-64.ext4.xz).

2. Download the [compressed kernel image](https://download.automotivelinux.org/AGL/snapshots/master/latest/qemux86-64/deploy/images/qemux86-64/bzImage).

3. Install [QEMU](https://www.qemu.org/download/) :

    ```sh
    $ apt-get install qemu
    ```
    ![image](https://user-images.githubusercontent.com/54492585/229208288-f8f06d44-1e82-4a9e-a7b1-cbdcfe6197a6.png)
4. Install [vinagre](https://wiki.gnome.org/Apps/Vinagre) :

    ```sh
    $ sudo apt install vinagre
    ```
    ![image](https://user-images.githubusercontent.com/54492585/229208411-533e0edc-da36-4538-9394-7c73b4928d6a.png)
5. Create boot directory and copy compressed images (prebuilt & kernel) into them :

    ```sh
    $ mkdir ~/agl-demo/
    $ cp ~/Downloads/agl-demo-platform-crosssdk-qemux86-64.ext4.xz ~/agl-demo/
    $ cp ~/Downloads/bzImage ~/agl-demo/
    $ cd ~/agl-demo
    $ sync
    ```
![image](https://user-images.githubusercontent.com/54492585/229211716-1a8fe323-9db8-425e-8704-1cba3c6ce755.png)
6. Extract prebuilt compressed image :

    ```sh
    $ xz -v -d agl-demo-platform-crosssdk-qemux86-64.ext4.xz
    ```

7. Launch QEMU with vinagre (for scaling), remove `- snapshot \` if you want to save changes to the image files :

  ```sh
    $ ( sleep 5 && vinagre --vnc-scale localhost ) > /tmp/vinagre.log 2>&1 &
    $ qemu-system-x86_64 -device virtio-net-pci,netdev=net0,mac=52:54:00:12:35:02 -netdev user,id=net0,hostfwd=tcp::2222-:22 \
      -drive file=agl-demo-platform-crosssdk-qemux86-64.ext4,if=virtio,format=raw -show-cursor -usb -usbdevice tablet -device virtio-rng-pci \
      -snapshot -vga virtio \
      -vnc :0 -soundhw hda -machine q35 -cpu kvm64 -cpu qemu64,+ssse3,+sse4.1,+sse4.2,+popcnt -enable-kvm \
      -m 2048 -serial mon:vc -serial mon:stdio -serial null -kernel bzImage \
      -append 'root=/dev/vda rw console=tty0 mem=2048M ip=dhcp oprofile.timer=1 console=ttyS0,115200n8 verbose fstab=no'
  ```
[-show-cursor: invalid option], hence remove it 
- to install `qemu-system-x86`
   - ```sudo apt install qemu-system-x86```      # version 1:6.2+dfsg-2ubuntu6.6, or
   - ```sudo apt install qemu-system-x86-xen```  # version 1:6.2+dfsg-2ubuntu6.6
output screen:-
![image](https://user-images.githubusercontent.com/54492585/229212294-3a946ddc-bcb7-4561-ab4e-5bee66edd874.png)
  - Login into AGL :

    ```sh
    Automotive Grade Linux 11.0.0+snapshot qemux86-64 ttyS1

    qemux86-64 login: root
    ```
![image](https://user-images.githubusercontent.com/54492585/229212808-781b8379-1f55-4396-b405-5c8268803cd6.png)
After logging in, users can explore and navigate the AGL system using standard Linux commands. The apt-get command can be used to install or update packages, while network settings can be configured using the ifconfig command. The AGL system can be customized by installing new software, modifying the user interface, or configuring services. Developers can use AGL's SDK to develop applications in multiple languages, and can test and debug their applications using tools such as gdb, valgrind, and strace.

### 3. x86 physical system

  **NOTE :** UEFI enabled system is required.

  1. Download the [compressed prebuilt image](https://download.automotivelinux.org/AGL/snapshots/master/latest/qemux86-64/deploy/images/qemux86-64/agl-demo-platform-crosssdk-qemux86-64.wic.xz).

  2. Extract the image into USB drive :

     ```sh
     $ lsblk
     $ sudo umount <usb_device_name>
     $ xzcat agl-demo-platform-crosssdk-qemux86-64.wic.xz | sudo dd of=<usb_device_name> bs=4M
     $ sync
     ```


  3. Boot from USB drive on the x86 system.
