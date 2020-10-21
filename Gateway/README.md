# Gateway

Instructions to Build a Single Channel LoRa Gateway

> All linked Repositorys could be deprecated in the future. So maybe i need to change it later.  

## What do you need?
### Hardware

> Raspberry Pi 4 Modell B

<img src="https://github.com/darthkali/LoRa_Node_Gateway/blob/main/Assets/Images/raspberryPi_4.jpg" alt="alt text" width="100" >

> Seeed Studio Raspberry Pi LoRa/GPS HAT (868MHz)

<img src="https://github.com/darthkali/LoRa_Node_Gateway/blob/main/Assets/Images/LoRaHAT_RaspberryPi.jpg" alt="alt text" width="100" >

> 16 GB SD-Card

<img src="https://github.com/darthkali/LoRa_Node_Gateway/blob/main/Assets/Images/SD-Card-16.jpg" alt="alt text" width="50" >

### Software

- Raspberry Pi Operation System [link and instruction below]
- Single Channel LoRaWAN Gateway [link and instruction below] [deprecated]



## Installation
> First we need to Install the RaspberryPi OS

https://www.raspberrypi.org/documentation/installation/installing-images/

> Linux
```bash
sudo apt install rpi-imager
```

> Windows
Download it from this Page:
https://www.raspberrypi.org/downloads/

or use Chocolatey [[Whats this?](https://chocolatey.org/why-chocolatey)]
```bash

choco install rpi-imager
```
Setup Raspberry
Use raspi-config to enable SPI:


```bash
sudo raspi-config
```

- Select 5 Interfacing Options:
- Select P2 [SSH] and P4 [SPI]:
- Select *Yes*

- reboot

```bash
sudo shutdown -r now
```

### Setup the Raspberry Pi Software



1) Login to Raspberry Pi as the Pi user
2) Clone the repo [in root folder]
```bash
git clone https://github.com/tftelkamp/single_chan_pkt_fwd
```
3) Install wiringPi:

```bash
sudo apt-get install wiringpi
```


## Config
1) go to the single channel gateway code:

```bash
cd ~/single_chan_pkt_fwd
```

2) open main.cpp to configurate the LoRa Gateway
```bash
nano main.cpp
```

3) Change some stuff
- Find the line:
```bash
#define SERVER1 "54.72.145.119" // The Things Network: croft.thethings.girovito.nl
```

- Replace the IP with your chosen Server-IP:
> the following list is from the 21.10.2020 so maybe this is changed in the meantime. if you Gateway dosn´t work, please check the following site and search for the correct IP: https://www.thethingsnetwork.org/docs/gateways/packet-forwarder/semtech-udp.html

| Region                              | Router address                                                          | Server-IP      |
|-------------------------------------|-------------------------------------------------------------------------|----------------|
| router.eu.thethings.network         | EU 433 and EU 863-870                                                   | 52.169.76.203  |
| router.us.thethings.network         | US 902-928                                                              | 13.66.213.36   |
| router.cn.thethings.network         | China 470-510 and 779-787                                               | 52.187.168.248 |
| router.as.thethings.network         | Southeast Asia 923 MHz                                                  | 52.163.90.53   |
| router.as1.thethings.network        | Southeast Asia 920-923 MHz                                              | 52.187.76.166  |
| router.as2.thethings.network        | Southeast Asia 923-925 MHz                                              | 52.187.78.172  |
| router.jp.thethings.network         | Korea 920-923 MHz                                                       | 104.215.150.17 |
| router.cn.thethings.network         | Japan 923-925 MHz (with EIRP cap according to Japanese regulations)     | 52.187.168.248 |
| au915.thethings.meshed.com.au       | Australia 915-928 MHz                                                   | 52.62.83.250   |
| as923.thethings.meshed.com.au       | Australia (Southeast Asia 923MHz frequency plan)                        | 52.65.94.162   |
| ttn.opennetworkinfrastructure.org   | Switzerland (EU 433 and EU 863-870)                                     | 86.119.29.227  |




## Example
