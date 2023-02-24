# How to Enable SSH in UBUNTU 22.04

## Usage
Enabling SSH (Secure Shell) in Linux allows remote access to the system over a secure, encrypted connection. SSH is a network protocol used to establish a secure, encrypted communication channel between two computers, enabling remote access and management of the Linux system from a remote location. It provides a more secure connection between the client and the server.


## Steps to Follow
**Step 1)** Download the updated package lists and metadata to your local system  
```
sudo apt update
```
![image](https://user-images.githubusercontent.com/54492585/221065323-4cb69ddd-88e6-454f-bc27-43a4b49933ec.png)


**Step 2)** Install the OpenSSH-server package on Ubuntu by using the following command
```
sudo apt install openssh-server
```

![image](https://user-images.githubusercontent.com/54492585/221065336-3206bc9c-bb7d-49b2-a1c0-dcb93e693cdf.png)


**Step 3)** Check the current status of the SSH (Secure Shell) service on your Linux system
```sudo systemctl status ssh```

![image](https://user-images.githubusercontent.com/54492585/221065536-b92a9ed6-e02b-46f7-967d-28b0741cdea1.png)

Press cntr + c to exit

**Step 4)** ```sudo ufw allow ssh```
![image](https://user-images.githubusercontent.com/54492585/221065543-eb452618-43d3-497b-ae55-3dd8cd666602.png)


**Step 5)** Check the IP address of your device by using —

``ip a```

![image](https://user-images.githubusercontent.com/54492585/221065560-6939182b-da15-4486-8c3e-ea13bf041812.png)


**Step 6)** And the final step. Establish a secure shell (SSH) connection to a remote Linux server using followinf command

```ssh `username`_of_old_server@`ip_address`_of_old_server```
