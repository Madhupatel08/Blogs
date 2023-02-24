# How to Enable SSH in UBUNTU 22.04

Open your terminal and type-

**Step 1)** Upadate the system repositories by using 
```
sudo apt update
```
![image](https://user-images.githubusercontent.com/54492585/221065323-4cb69ddd-88e6-454f-bc27-43a4b49933ec.png)


**Step 2)** Install the OpenSSH-server package on Ubuntu by using the following command
```
sudo apt install openssh-server
```

![image](https://user-images.githubusercontent.com/54492585/221065336-3206bc9c-bb7d-49b2-a1c0-dcb93e693cdf.png)


**Step 3)** ```sudo systemctl status ssh```

![image](https://user-images.githubusercontent.com/54492585/221065536-b92a9ed6-e02b-46f7-967d-28b0741cdea1.png)


Press cntr + c to exit

**Step 4)** ```sudo ufw allow ssh```
![image](https://user-images.githubusercontent.com/54492585/221065543-eb452618-43d3-497b-ae55-3dd8cd666602.png)


**Step 5)** Check the IP address of your device by using —

``ip a```

![image](https://user-images.githubusercontent.com/54492585/221065560-6939182b-da15-4486-8c3e-ea13bf041812.png)


**Step 6)** And the final step. Open the terminal where you want to ssh and type

```ssh `username`_of_old_server@`ip_address`_of_old_server```
