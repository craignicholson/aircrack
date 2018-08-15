# Aircrack-ng

# Install on Ubuntu
 
 Quick Easy Way

> sudo apt-get install aircrack-ng

 Determine the chipset in your wireless card
Determine which of the three options you will use to run the aircrack-ng suite
Get started using the aircrack-ng suite

# Wireless Cards
Setup care in monitor mode.



#  Wifi Chipset
First we need to if our chip supports MON (monitior) mode.

## USB Antenna 
Using the Alfa Realtek RTL8187 which supports all modes

## Six Modes of Wireless
* RFMON (radio freguency mon)
* Master
* Managed
* Ad-hoc
* repeater
* monitor

# Options to see your antenna

### review pci interfaces

> lspcic
00:00.0 Host bridge: Intel Corporation Sky Lake Host Bridge/DRAM Registers (rev 08)
00:02.0 VGA compatible controller: Intel Corporation Sky Lake Integrated Graphics (rev 07)
00:04.0 Signal processing controller: Intel Corporation Skylake Processor Thermal Subsystem (rev 08)
00:13.0 Non-VGA unclassified device: Intel Corporation Device 9d35 (rev 21)
00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
00:15.0 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller (rev 21)
00:15.1 Signal processing controller: Intel Corporation Sunrise Point-LP Serial IO I2C Controller (rev 21)
00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI (rev 21)
00:17.0 SATA controller: Intel Corporation Sunrise Point-LP SATA Controller [AHCI mode] (rev 21)
00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port (rev f1)
00:1f.0 ISA bridge: Intel Corporation Sunrise Point-LP LPC Controller (rev 21)
00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
01:00.0 Network controller: Intel Corporation Wireless 3165 (rev 79)

### Review usb interfaces

> lsusb
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 04f3:2494 Elan Microelectronics Corp. 
Bus 001 Device 003: ID 8087:0a2a Intel Corp. 
Bus 001 Device 002: ID 0bda:58c2 Realtek Semiconductor Corp. 
Bus 001 Device 007: ID 0bda:8187 Realtek Semiconductor Corp. RTL8187 Wireless Adapter
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub


### Additional Command to review... 

> dmseg

### Get the name of the all interfaces

> ifconfig

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:2602 errors:0 dropped:0 overruns:0 frame:0
          TX packets:2602 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:215588 (215.5 KB)  TX bytes:215588 (215.5 KB)

wlp1s0    Link encap:Ethernet  HWaddr ac:2b:6e:5f:b8:2e  
          inet addr:192.168.1.111  Bcast:192.168.1.255  Mask:255.255.255.0
          inet6 addr: fe80::1314:6751:4209:ad7d/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:133332 errors:0 dropped:0 overruns:0 frame:0
          TX packets:45662 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:170334664 (170.3 MB)  TX bytes:6909605 (6.9 MB)

wlx00c0ca8290a3 Link encap:Ethernet  HWaddr 00:c0:ca:82:90:a3  
          UP BROADCAST MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)


### Get the name of the wireless network interfaces

>  iwconfig
wlx00c0ca8290a3  IEEE 802.11  ESSID:off/any  
          Mode:Managed  Access Point: Not-Associated   Tx-Power=20 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:off
          
wlp1s0    IEEE 802.11  ESSID:"Eagleton Parks Dept "  
          Mode:Managed  Frequency:5.22 GHz  Access Point: AC:22:0B:2F:91:6C   
          Bit Rate=390 Mb/s   Tx-Power=22 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=36/70  Signal level=-74 dBm  
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:0  Invalid misc:1073   Missed beacon:0

lo        no wireless extensions.

mon0      IEEE 802.11  Mode:Monitor  Tx-Power=20 dBm   
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on


YOU CAN SEE mon0, this is us in Mode: monitor....
So we can start airodump-ng and start listening to whatver is in the air...

> sudo airodump-ng mon0
The app will cycle through each of the 7 channels and list the devices it sniffs

CH  3 ][ Elapsed: 44 s ][ 2017-09-17 23:03                                         
BSSID              PWR  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSIDCC:65:AD:28:A7:70  -36      342     1121    0   1  54e  WPA2 CCMP   PSK  ATT2sxAZ3A                                                
 
 64:0F:29:06:C5:A1  -60      272       44    1   3  54 . WPA2 CCMP   PSK  2WIRE413                                                  
 3C:DF:A9:81:74:20  -62      175        0    0   1  54e  WPA2 CCMP   PSK  ATT918                                                    
 F0:99:BF:0C:9D:0E  -61      149       31    0   1  54e  WPA2 CCMP   PSK  taco                                                      
 B4:2A:0E:1E:DB:A2  -69       72        8    0   1  54e  WPA2 CCMP   PSK  Goodwin                                                   
 D0:B2:C4:4C:E9:F4  -71        1        0    0   1  54e  WPA2 CCMP   PSK  Jayne                                                     
 E0:22:02:39:22:22  -71       66       41    0   1  54e  WPA2 CCMP   PSK  ATT2JF7SqV                                                
 F8:18:97:B9:27:B2  -72       54       25    0   1  54e  WPA2 CCMP   PSK  ATT2pIz5TJ                                                
 B0:DA:F9:75:D1:D0  -72       11        7    0   1  54e  WPA2 CCMP   PSK  ATTmh23HWa                                                
                                                                                                                                     
 BSSID              STATION            PWR   Rate    Lost    Frames  Probe                                                           
                                                                                                                                     
 (not associated)   44:61:32:E0:01:E9  -38    0 - 1     73       40  2WIRE733                                                        
 (not associated)   44:61:32:E8:00:78  -43    0 - 1     75       52  2WIRE733                                                        
 (not associated)   B4:AE:2B:B8:3A:19  -46    0 - 1      0        2                                                                  
 (not associated)   F4:F5:D8:20:0F:B6  -62    0 - 1      0        2  ATT5pwfivS                                                      
 (not associated)   C8:FF:77:D9:40:98  -53    0 - 1     34       20  Traphouse 2.4                                                   
 (not associated)   A8:54:B2:A6:11:68  -73    0 - 1      0        1  ATT2pIz5TJ                                                      
 CC:65:AD:28:A7:70  BC:9F:EF:D8:3C:DD   -1    1e- 0      0        1                                                                  
 CC:65:AD:28:A7:70  A4:D1:8C:CC:37:EC  -51    0 - 6      0        1                                                                  
 CC:65:AD:28:A7:70  A0:99:9B:39:58:B0  -56    1e-24      0        3                                                                  
 F0:99:BF:0C:9D:0E  F4:31:C3:7E:42:37  -73    0 - 1      0        4                                                                  
 B4:2A:0E:1E:DB:A2  34:C0:59:18:93:AB   -1    1e- 0      0        1                                                                  
 B4:2A:0E:1E:DB:A2  D8:BB:2C:76:57:BE   -1    1e- 0      0        1                                                                  
 D0:B2:C4:4C:E9:F4  90:8D:6C:99:C6:73   -1    1e- 0      0        1                                                                  
 B0:DA:F9:75:D1:D0  C0:D0:12:84:71:95   -1    1e- 0      0        1 

## Change MAC ID
ifconfig wlan0 down
ifconfig wlan0 hw ether de:ad:be:ef:c0:fe
ifconfig wlan0 up
ifconfig wlan0


> airdriver-ng loaded

### Use airmon-ng to find the interfaces

> sudo airmon-ng
Interface	Chipset		Driver
wlx00c0ca8290a3		Realtek RTL8187L	rtl8187 - [phy3]
wlp1s0		Intel AC	iwlwifi - [phy0]
mon0		Realtek RTL8187L	rtl8187 - [phy3]


> sudo airmon-ng start wlx00c0ca8290a3
[sudo] password for craig: 


Found 5 processes that could cause trouble.
If airodump-ng, aireplay-ng or airtun-ng stops working after
a short period of time, you may want to kill (some of) them!

PID	Name
999	avahi-daemon
1005	NetworkManager
1060	avahi-daemon
1157	wpa_supplicant
7302	dhclient
Process with PID 7302 (dhclient) is running on interface wlp1s0


Interface	Chipset		Driver

wlx00c0ca8290a3		Realtek RTL8187L	rtl8187 - [phy3]
				(monitor mode enabled on mon0)
wlp1s0		Intel AC	iwlwifi - [phy0]



craig@cn:~/.local/share/applications$ sudo airmon-ng


Interface	Chipset		Driver

wlx00c0ca8290a3		Realtek RTL8187L	rtl8187 - **[phy5]**
wlp1s0		Intel AC	iwlwifi - **[phy0]**
mon0		Realtek RTL8187L	rtl8187 - [phy5]


craig@cn:~/.local/share/applications$ iw phy phy0 info | grep -A8 modes
	Supported interface modes:
		 * IBSS
		 * managed
		 * AP
		 * AP/VLAN
		 * monitor
		 * P2P-client
		 * P2P-GO
		 * P2P-device
--
	software interface modes (can always be added):
		 * AP/VLAN
		 * monitor
	valid interface combinations:
		 * #{ managed } <= 1, #{ AP, P2P-client, P2P-GO } <= 1, #{ P2P-device } <= 1,
		   total <= 3, #channels <= 2
	HT Capability overrides:
		 * MCS: ff ff ff ff ff ff ff ff ff ff
		 * maximum A-MSDU length

We can see the internal NIC has monitor mode... yeehaw


craig@cn:~/.local/share/applications$ iw phy phy5 info | grep -A8 modes
	Supported interface modes:
		 * IBSS
		 * managed
		 * monitor
	Band 1:
		Bitrates (non-HT):
			* 1.0 Mbps
			* 2.0 Mbps
			* 5.5 Mbps
--
	software interface modes (can always be added):
		 * monitor
	interface combinations are not supported
	HT Capability overrides:
		 * MCS: ff ff ff ff ff ff ff ff ff ff
		 * maximum A-MSDU length
		 * supported channel width
		 * short GI for 40 MHz
		 * max A-MPDU length exponent


craig@cn:~/.local/share/applications$ 





## Environment
Begin Using Kali Linux vmware
running Mac OS El Captian
VMWare Fusion Version 6.0.6 (2684343)


## Compatibility List for Chipsets
http://www.aircrack-ng.org/doku.php?id=compatibility_drivers
http://www.aircrack-ng.org/doku.php?id=compatible_cards&DokuWiki=f4rbj7krnob6tm5t98jlgnb750


Download Kali Linux VMWare Image
https://www.offensive-security.com/kali-linux-vmware-virtualbox-image-download/

Convert VMWare Image to VMDWare Fusion
http://blog.greggant.com/post/103218302428/install-an-os-from-a-vmdk-image-in-vmware-fusion

File > New
Install from disc of Image
Create a custom virtual machine
i took a few screen updates

# 1 Update Kali

## start aircrack / terminal

### List the usb devices

root@kali:~# lsusb
Bus 002 Device 005: ID 0bda:8187 Realtek Semiconductor Corp. RTL8187 Wireless Adapter
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 006: ID 0e0f:0008 VMware, Inc.
Bus 001 Device 003: ID 0e0f:0002 VMware, Inc. Virtual USB Hub
Bus 001 Device 002: ID 0e0f:0003 VMware, Inc. Virtual Mouse
Bus 001 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub


craig@cn:~/aircrack$ lsusb
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 005: ID 04f3:2494 Elan Microelectronics Corp. 
Bus 001 Device 003: ID 8087:0a2a Intel Corp. 
Bus 001 Device 002: ID 0bda:58c2 Realtek Semiconductor Corp. 
Bus 001 Device 006: ID 0bda:8187 Realtek Semiconductor Corp. RTL8187 Wireless Adapter
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub



### Check for interfaces
root@kali:~# airmon-ng
PHY	Interface	Driver		Chipset

phy32	wlan0		rtl8187		Realtek Semiconductor Corp. RTL8187

## Modes of Wireless -Six
Monitor mode is one of the seven modes that 802.11 wireless cards can operate in: Master (acting as an access point), Managed (client, also known as station), Ad hoc, Mesh, Repeater, Promiscuous, and Monitor mode.

Monitor mode is a special mode that allows your PC to listen to every wireless packet. This monitor mode also allows you to optionally inject packets into a network.

###  Monitor Mode  
* Access Point  
* Base Station  


Monitor mode can sniff packets from access points the radio is not associated with.

Not all wireless cards have monitor mode.


>>
  ```Shell
  root@kali:~# iwconfig

  wlan0mon  IEEE 802.11bg  ESSID:off/any
            Mode:Managed  Access Point: Not-Associated   Tx-Power=20 dBm
            Retry short limit:7   RTS thr:off   Fragment thr:off
            Encryption key:off
            Power Management:off

    root@kali:~# iw phy phy32 info | grep -A8 modes         
  ```
### Master Mode  
Typically a
Access Point - wifi pinapple
Base Station

### Managed Mode  (Infrastructure)
* Clients  
* Stations  
which connect to access points, your laptop, phone, xbox, roku, apple tv...

iwconfig wlna1 mode managed
iwconfig wlan1 essid Pineapple
iwconfig wlan1
we see this is not associated with the Pineapple endpoint
we told this device to specifically use this wifi endpoint

Types of Management Frames
* beacons
* probes {requests and responses}
* association {requests and responses and disassocations}
* authentication {deauthorization}



### Ad-hoc Mode (Peer to Peer)
* Peer to Peer
All devices must have the same essid, so if we have lots of small devices in close
proxmity, this will work well.

### Mesh Mode
It's a mesh network...

### Repeater Mode
Repeats the single or extend the range of a single access point


## Monitor Mode
https://en.wikipedia.org/wiki/Monitor_mode
Put the interface in monitor mode.

# Example
root@kali:~# airmon-ng start wlan0
Found 5 processes that could cause trouble.
If airodump-ng, aireplay-ng or airtun-ng stops working after
a short period of time, you may want to kill (some of) them!

  PID Name
  748 NetworkManager
 1069 avahi-daemon
 1070 avahi-daemon
 1079 wpa_supplicant
 1867 dhclient

PHY	Interface	Driver		Chipset

phy32	wlan0		rtl8187		Realtek Semiconductor Corp. RTL8187
		(mac80211 monitor mode vif enabled for [phy32]wlan0 on [phy32]wlan0mon)
		(mac80211 station mode vif disabled for [phy32]wlan0)


root@kali:~# iwconfig
eth0      no wireless extensions.

wlan0mon  IEEE 802.11bg  ESSID:off/any
          Mode:Managed  Access Point: Not-Associated   Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Encryption key:off
          Power Management:off

lo        no wireless extensions.

root@kali:~# airodump-ng wlan0mon
ioctl(SIOCSIWMODE) failed: Device or resource busy

ARP linktype is set to 1 (Ethernet) - expected ARPHRD_IEEE80211,
ARPHRD_IEEE80211_FULL or ARPHRD_IEEE80211_PRISM instead.  Make
sure RFMON is enabled: run 'airmon-ng start wlan0mon <#>'
Sysfs injection support was not found either.

root@kali:~# ifconfig wlan0mon down
root@kali:~# iwconfig wlan0mon mode monitor
root@kali:~# ifconfig wlan0mon up
root@kali:~# iwconfig
eth0      no wireless extensions.

wlan0mon  IEEE 802.11bg  Mode:Monitor  Frequency:2.457 GHz  Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:off

lo        no wireless extensions.

root@kali:~# airodump-ng wlan0mon


 CH  7 ][ Elapsed: 12 s ][ 2016-02-01 23:25

 BSSID              PWR  Beacons    #Data, #/s  CH  MB   ENC  CIPHER AUTH ESSID

 00:25:00:FF:94:73   -1        0        0    0  -1  -1                    <length:  0>
 B8:3E:59:38:D2:53  -34        5        0    0   1  54e  WPA2 CCMP   PSK  <length: 15>
 E0:B7:0A:91:15:30  -41       13        1    0   9  54e  WPA2 CCMP   PSK  ATT5pwfivS
 74:9D:DC:EB:D8:E1  -43       14        2    0   6  54 . WPA2 CCMP   PSK  2WIRE678
 AC:5D:10:FB:BA:E9  -48       15        1    0   8  54 . WPA2 CCMP   PSK  2WIRE733
 64:0F:29:06:C5:A1  -49       12        2    0  11  54 . WPA2 CCMP   PSK  2WIRE413
 00:25:3C:66:EE:09  -57        6        0    0  11  54 . WPA2 CCMP   PSK  2WIRE737
 1C:1B:68:55:FB:80  -62        3        0    0   6  54e  WPA2 CCMP   PSK  ATT4s6Y3e3
 F0:99:BF:0C:9D:0E  -62        8        3    0  11  54e  WPA2 CCMP   PSK  Aggie Apple
 94:62:69:28:EB:70  -63        8        0    0   6  54e  WPA2 CCMP   PSK  GolanHouse


## Notes
An SSID is the Name of a Network
BSSIDs Identify Access Points and Their Clients

Handshakes.... demo....


# Deauth Wireless Clients with Aircrack-ng
4-way handshake and WEP vs WPA Crack
https://www.youtube.com/watch?v=75LEQEEOfXo


# Promiscuous Mode
assumes hub based networks
