# SOVOL_KLIPAD50_SYSTEM
This is information about the KLIPAD50 image

# Features and advantages of klipad50  
1. Onboard powerful 4-core 64-bit core SOC, with 1GBytes of DDR3 memory;
2. DC12/24V power supply, more stable power supply;
3. With HDMI 800*480 IPS LCD and capacitive touch screen;
4. Provide 3-way USB interface (can be connected to 3D printer main control board, USB wireless network card, USB camera, U disk, USB keyboard and mouse, etc.);
5. 2.4G wifi on board.

# Download
From Google drive: [KLIPAD50 IMAGE](https://drive.google.com/file/d/1w1y3ECIEyXUpIBp9oqJDD-8qShJKGTBf/view?usp=sharing)

# FLASH TO EMMC
Notice: the system has been burnned the each KLIPAD50 before leaving the factory, and you do not need to burn it again unless you want to update a new image.   

## Hardware Preparation  
- Emmc adaptor card reader, just like [this one](https://www.aliexpress.us/item/3256805428404625.html?spm=a2g0o.store_pc_allProduct.8148356.1.7bca1ad70ZKzwN&pdp_npi=4%40dis%21USD%21US%20%246.99%21US%20%241.99%21%21%216.99%211.99%21%40212aa2ac17038484556595237e184f%2112000033755356288%21sh%21US%21240163459%21&gatewayAdapt=glo2usa)
- PC with windows operating system installed
- Wireless network card or network cable
- Type_C cable
  
## Software preparation  
- Install balenaEtcher v1.5 and above, download link:  
  [https://www.balena.io/etcher/](https://www.balena.io/etcher/) 
- Install putty, download link: [https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)

### Flash system files  
1. Format TF card  
   Format TF card to FAT32 format before flash system files  
2. Insert the EMMC module into the card reader, and insert the card reader into the PC  
3. Unzip the downloaded image file  
4. Run balenaEtcher, import the decompressed image file->Select TF card->Click to start flash  
   ![ddd](https://user-images.githubusercontent.com/12979070/175958595-3052068e-e06e-415a-b01d-b50fd21de4a4.png)  
5. After the flashing is finish, insert the EMMC module into the KLIPAD50 and power on with DC12/24V  

## KLIPAD50 wifi connection

- KLIPAD50 runs with KlipperScreen. You can enter the wifi page throught: "Config"->"WiFi"
- You can scan and find the heatpot, enter the correct password and wait for connect.


## Enter WEB interface  
After connect the KLIPAD50 to the network, you can directly enter the IP address of KLIPAD50 with your PC's browser, and you can either enter mainsail interface with the default port of 80, or fluidd with the port of 81

## Using Serial software on PC(we using Putty to describe below)

Putty is a famous tool, you can use either SSH or Serial to connect to the KLIPAD50.  

- Connect the KLIPAD50 with the TYPE-C cable to the PC, supply power to the PI, check the COM port in the device manager of the PC, and then open Putty
- Select the COM port, set the baud rate to 1500000, and click “Open” to connect

![COM](https://user-images.githubusercontent.com/12979070/175967056-dd6aec07-084d-4b05-8199-88709755ea64.png)  

- If you open a black empty window, click the Enter key, and it will ask you to enter the login user and password
- There are two users in the system provided:
  
  > root user: root  
  > user2: mks  
  > their origin passwords are the same: makerbase  
- After enter the user and password, you can enter the system now.

## Connection KLIPAD50 with motherboard

You can use 3 USB ports to connect KLIPAD50 and your motherboard.  


Most 3D printing motherboards have a USB port converted from the serial port. Use a usb cable to connect it to one of the three B-type USB ports of the KLIPAD50.  
Find the device name of the USB port, login KLIPAD50 from Putty or other serial software and type:   


```shell
ls /dev/serial/by-id/*
```


It will display the name like below(confirm your USB connection is ok):  
```shell
/dev/serial/by-id/usb-Klipper_stm32f407xx_4D0045001850314335393520-if00
```
Copy the device name to the "[mcu]" segment on `printer.cfg` file of Klipper :   

```python
[mcu]  
serial: /dev/serial/by-id/usb-Klipper_stm32f407xx_4D0045001850314335393520-if00
```

