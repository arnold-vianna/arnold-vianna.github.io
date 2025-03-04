---
title: increase swap memory
date: 2025/2/24 12:00:00 -500
categories: [windows]
tags: [memory, raspberry]    # tags should allways be lowercase
---
# increase swap memory of raspberry pi & Debian-based distros
-----------------------------------------------------------------------------------
* all steps 

```bash
free -h # check the amount of swap memory

sudo nano /etc/dphys-swapfile   # edit this file

CONF_SWAPSIZE=200   #  find this line 

CONF_SWAPSIZE=1024  #  change from 200 into 1024

CTRL + X, then Y and Enter  # to Save and exit 

sudo dphys-swapfile swapoff  # Disable current swap

sudo dphys-swapfile setup    # Apply new swap size

sudo dphys-swapfile swapon   # Enable new swap

free -h # check if the swap size has increased
```

----------------------------------------------------------------------------------- 
# step by step


* check the amount of swap memory
```bash
free -h
```
----------------------------------------------------------------------------------- 

* edit this file
```bash
sudo nano /etc/dphys-swapfile
```
----------------------------------------------------------------------------------- 

* find this line 
```bash
CONF_SWAPSIZE=200
```   
----------------------------------------------------------------------------------- 

* change from 200 into 1024
```bash
 CONF_SWAPSIZE=1024 
``` 
* Save and exit with 
* (CTRL + X, then Y and Enter)

----------------------------------------------------------------------------------- 

*  Disable current swap
```bash
 sudo dphys-swapfile swapoff 
``` 
----------------------------------------------------------------------------------- 

 * Apply new swap size
```bash
 sudo dphys-swapfile setup
``` 
----------------------------------------------------------------------------------- 

* Enable new swap
```bash
 sudo dphys-swapfile swapon
```

----------------------------------------------------------------------------------- 

* check if the swap size has increased
```bash
free -h
```

----------------------------------------------------------------------------------- 
# Increase Swappiness (Use Swap More Frequently)


* Swappiness controls how aggressively Linux swaps memory to disk. A higher value makes the system use swap more often, which can help when RAM is limited


*Check Current Swappiness (Default is usually 60.)

```bash
cat /proc/sys/vm/swappiness
```

------------------------------------------------------------------------------------


* Set Swappiness to 80

```bash
sudo nano /etc/sysctl.conf
```

------------------------------------------------------------------------------------


* Add this line at the bottom

```bash
vm.swappiness=80
```

------------------------------------------------------------------------------------

* Save and exit,  apply changes

```bash
CTRL + X, then Y and Enter 
```

------------------------------------------------------------------------------------


* apply changes

```bash
sudo sysctl -p
```

------------------------------------------------------------------------------------
## This should help your Raspberry Pi run smoother with more available virtual memory

------------------------------------------------------------------------------------
