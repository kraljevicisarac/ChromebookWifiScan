# ChromebookWifiScan
Shell script to list Wi-Fi networks from Chromebook CLI (Dev Mode Required) 

chromebook_wifi_scan.sh - script to list wifi networks

 Author: Nigel Bowden
 Version: v0.1 - 7th Jan 2018

 This script parses the output of the cli command "iw dev <adapter> scan"
 to determine all wi-fi networks that can be heard by a chromebook client. It
 uses grep to parse/scrape the command output. It will run in a loop
 giving output until you hit Ctrl-C to stop it.

 You will need to drop the Chromebook in to developer mode to access the shell
 and run this script. Note that going in to developer mode wipes all current data
 on the machine (...but it's all in the cloud...right?) See the following for 
 more details:

  1. https://framebyframewifi.net/2016/05/10/chrome-os-wifi-diagnostics/
  2. https://www.howtogeek.com/210817/how-to-enable-developer-mode-on-your-chromebook/

 (Note: this script is liable to break if command output changes over time - sorry)

```
  grep output:

  BSS 5a:83:bf:34:67:e5
  freq: 2412
  signal: -83.00
  SSID: BTWifi-X
```

  Standard output from running script on cli:
```
 . ./chromebook_wif_scan/sh

 Output:

  BSSID              RSSI     CH    Freq    SSID
                     (dBm)          (Mhz)
  ===============================================================
  ac:86:74:64:a1:91  -45.00    1    2412
  ac:86:74:64:a1:82  -45.00    1    2412    VM202651-2G
  ae:86:74:64:a1:95  -57.00   44    5220    VM202651-5G
  28:76:10:01:ac:00  -59.00   44    5220
  e8:fc:af:2e:1e:88  -75.00    6    2437    VM202651-2G
  c0:05:c2:5f:1c:61  -79.00    6    2437    HomeWifi2G
  28:76:10:01:ac:08  -83.00   44    5220    VM202651-5G
  80:2a:a8:d2:20:69  -89.00   36    5180    HomeWifi5G
  f6:6b:ef:28:ee:8d  -91.00   11    2462    Virgin Media
  d2:05:c2:5f:1c:61  -91.00   11    2462    VM3668793
  e8:fc:af:14:5a:38  -93.00   11    2462    BTWifi-with-FON
  ===============================================================

```
  With "-csv" command line option, output as follows (all networks detected
  will be listed in this format):
```
. ./chromebook_wifi_scan.sh  -csv

  "ssid_name", "bssid_mac", "sig_level", "channel_num", "hh:mm:ss"

  Example: "Virgin Media", "D2:08:C2:5F:74:23", -57", "36", "19:47:05"
```
  This can be imported in to the MAC application:  Wifi Explorer
  for further analysis

  Notes:

   1. This will only run if the laptop is in developer mode and the 
      shell has been accessed (Ctrl-Alt-T - enter 'shell' at the 
      crosh prompt)
   2. Store this script in the user home directory (cd ~/)
   3. If piping out to a local csv file using tee, the file
      being created must be in the local (home) directory
   4. Once a csv file has been created, use the copy command 
      to copy to the downloads folder to pull off via the Files
      app to Google Drive


