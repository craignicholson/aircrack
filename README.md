# Aircrack-ng

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
### Managed Mode  
* Clients  
* Stations  
which connect to access points

### Ad-hoc Mode (Peer to Peer)
* Peer to Peer
All devices must have the same essid

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
