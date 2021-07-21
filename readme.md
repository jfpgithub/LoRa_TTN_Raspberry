# LoRa and The Things Stack

Configure the [Dragino LoRa/GPS Hat](http://wiki.dragino.com/index.php?title=Lora/GPS_HAT) for the Raspberry Pi 3 to use the Raspberry as LoRa Gateway (with connection to *The Things Stack (V3)*).

## Software
The following software was used:
- **LoRa Gateway:** https://github.com/tftelkamp/single_chan_pkt_fwd and sourceclimber's fork (https://github.com/sourceclimber/LoRa_TTN_Raspberry) of the original.

## Configure the Raspberry as LoRa TTN Gateway
### Preparation
- Use the raspi-config tool (with `sudo raspi-config`) to enable SPI on the Raspberry Pi
- Install wiringpi (`sudo apt-get install wiringpi`)

### Download
- Download and unzip the software for a *Single Channel Gateway*:<br>
`wget https://github.com/tftelkamp/single_chan_pkt_fwd/archive/master.zip`<br>
`unzip master.zip`

### Configuration for The Things Network Stack ( TTN V3 )
- The server address which is used by the gateway software must be changed to one of the TheThingsNetwork Stack V3 servers.
- Use the nearest TTN V3 server (e.g. 'eu1.cloud.thethings.network'). The IP address can be resolved using the `nslookup` command.<br>
- Because the original main.cpp file can only handle IP addresses for the server address, an IP address must be obtained.<br> In using `nslookup`, 52.212.223.226 surfaced as a functioning address (July 20th 2021).
- Edit the *main.cpp* file and insert the IP address of the server 'eu1.cloud.thethings.network' (in line 88, into the define **SERVER1**):<br>
`#define SERVER1 "52.212.223.226"`

### Build and Run
- Build the program by calling `make`
- Execute the compiled program: `./single_chan_pkt_fwd`
- The output of the program contains a *Gateway ID*. This ID is needed to register the gateway on the The Things Network website.


### Autostart LoRa TTN Gateway
The LoRa TTN gateway program can be set up to automatically start on boot.

- Edit the file */etc/rc.local*: `sudo vi /etc/rc.local`
- Add the following line (before `exit 0`):<br>
`/path/to/lora_ttn_gw/start_lora_ttn_gw.sh &`<br>
notice the **&** at the end!





