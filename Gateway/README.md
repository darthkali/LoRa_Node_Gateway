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

4) Configure the single channel gateway code:

```bash
cd ~/single_chan_pkt_fwd
```

5) open main.cpp to configurate the LoRa Gateway
```bash
nano main.cpp
```
## Usage


## Example
