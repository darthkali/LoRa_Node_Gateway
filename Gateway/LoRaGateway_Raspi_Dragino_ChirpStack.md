# Gateway - ChirpStack
Instructions to Build a Dual Channel LoRa Gateway with ChirpStack

## What do you need?
### Hardware

- Raspberry Pi 4 Modell B
- Dragino LoRa/GPS HAT
- 16 GB SD-Card

### Software
- Raspberry Pi Operation System [link and instruction below]
- Dual Channel Package Forwarder [link and instruction below]

## Installation RaspberryPi OS
>You can find all Informations here:
> https://www.raspberrypi.org/software/

#### Linux
```bash
sudo apt install rpi-imager
```

#### Windows
> Download it from this Page:
https://www.raspberrypi.org/downloads/

or use Chocolatey [[Whats this?](https://chocolatey.org/why-chocolatey)]

```bash
choco install rpi-imager
```
## Setup Raspberry

#### Remote access:

```bash
sudo raspi-config
```

- Select 5 Interfacing Options:
- Select P2 [SSH] and P4 [SPI]:
- Select *Yes*

```bash
sudo apt-get install xrdp
```
Find your IP-Address:
```bash
ifconfig
```
write down the IP-Address from your device (eth0 -> inet)

```bash
sudo shutdown -r now
```
> - after this step you have access to your device from your PC oder Laptop or other devices
> - in Windows you can use Putty or the "Remote Desktop Connection"
> - you need the IP-Address to connect

### Setup - Dual Channel Package Forwarder

1) Login to Raspberry Pi as the Pi user
2) Clone the repo [in root folder]

```bash
git clone https://github.com/dragino/dual_chan_pkt_fwd.git
```
3) Install wiringPi:

```bash
sudo apt-get install wiringpi
```
### Config - Dual Channel Package Forwarder
1) go to the dual channel forwarder folder:

```bash
cd ~/dual_chan_pkt_fwd
```

2) open global_conf.json to configurate the Package Forwarder
```bash
nano global_conf.json
```

3) Change the Server to the ChirpStack Address

```json
{
  "SX127x_conf":
  {
    "freq": 868100000,
    "freq_2": 868100000,
    "spread_factor": 7,
    "pin_nss": 6,
    "pin_dio0": 7,
    "pin_nss_2": 6,
    "pin_dio0_2": 7,
    "pin_rst": 3,
    "pin_led1":4,
    "pin_NetworkLED": 22,
    "pin_InternetLED": 23,
    "pin_ActivityLED_0": 21,
    "pin_ActivityLED_1": 29
  },
  "gateway_conf":
  {
    "ref_latitude": 0.0,
    "ref_longitude": 0.0,
    "ref_altitude": 10,

    "name": "your name",
    "email": "a@b.c",
    "desc": "Dual channel pkt forwarder",

    "interface": "eth0",

    "servers":
    [
      {
        "address": "TYPE_IN_YOUR_CHIRPSTACK_SERVER_ADDRESS",
        "port": 1700,
        "enabled": true
      },
      {
        "address": "router.eu.thethings.network",
        "port": 1700,
        "enabled": false
      }
    ]
  }
}
```


```json
"address": "TYPE_IN_YOUR_CHIRPSTACK_SERVER_ADDRESS",
```
> the adress should be something like: 
> router.eu.thethings.network
> or
> myserver.com

4) Compile the dual channel forwarder code:
> get shure, that you are in the main directory [dual_chan_pkt_fwd]

```bash
make
```
5) run the Gateway
```bash
sudo ./ dual_chan_pkt_fwd
```
> - in some cases the "sudo" option generates a failure. If you get an “Unrecognized transreciver”, try the command without “sudo”
> - you can Stop the Gateway with Crtl + C

6) Copy the **Gateway ID** from the Console in your clipboard

```bash
pi@raspberrypi:~/dual_chan_pkt_fwd $ ./dual_chan_pkt_fwd 
server: .address = TYPE_IN_YOUR_CHIRPSTACK_SERVER_ADDRESS; .port = 1700; .enable = 1
server: .address = router.eu.thethings.network; .port = 1700; .enable = 0
Gateway Configuration
  your name (a@b.c)
  Dual channel pkt forwarder
  Latitude=0.00000000
  Longitude=0.00000000
  Altitude=10
  Interface: eth0
Trying to detect module CE0 with NSS=6 DIO0=7 Reset=3 Led1=unused
SX1276 detected on CE0, starting.
Trying to detect module CE1 with NSS=6 DIO0=7 Reset=3 Led1=unused
SX1276 detected on CE1, starting.
Gateway ID: 00:00:00:00:00:00:00:00
Listening at SF7 on 868.100000 Mhz.
Listening at SF7 on 868.100000 Mhz
```


## Gateway on Chirp Stack 

 1. Login to your ChirpStack Server
 2. go to Gateways (left sidebar)
> if there is no sidebar, click on the 3 Rows in the top-left of the page to open the menu
 3. click on **+ CREATE**
 4. enter a Gateway name and description
 5. paste in the Gateway ID from your clipboard
 6. select a network server
> maybe you need to Create a Service profile first
 7. set the altitude and the location of the gateway
 8. click on **CREATE GATEWAY**

***Now your gateway should work.***

You can look at the page from the gateway and click on the "LIVE LORAWAN FRAMES" tab to see yout Up- and Downlinks. 
> A node must send data before. Without a node, you don't receive frames in the Gateway
