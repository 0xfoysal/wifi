# Enable Monitor Mode on a Wireless Adapter

This guide explains how to enable **Monitor Mode** on a wireless adapter in Linux.

## Prerequisites
- A wireless adapter that supports monitor mode.
- Linux with `aircrack-ng` installed.
- Root or sudo access.

## Step 1: Identify Your Wireless Interface
Run the following command to list network interfaces:
```bash
ip a | grep wl
```
Or:
```bash
iw dev
```
Example output:
```
wlx00117f1b8884  IEEE 802.11  ESSID:off/any  
Mode:Managed  Access Point: Not-Associated   Tx-Power=20 dBm   
```
Note the interface name (e.g., `wlx00117f1b8884`).

## Step 2: Kill Interfering Processes
Before enabling monitor mode, stop interfering network processes:
```bash
sudo airmon-ng check kill
```

## Step 3: Enable Monitor Mode
Run the following command to enable monitor mode:
```bash
sudo airmon-ng start wlx00117f1b8884
```
This should create a new interface (e.g., `wlx00117f1b8884mon`).

## Step 4: Verify Monitor Mode
To check if monitor mode is enabled, run:
```bash
iwconfig
```
Look for `Mode: Monitor` in the output.

## Alternative Method (Manual)
If `airmon-ng` does not work, enable monitor mode manually:
```bash
sudo ip link set wlx00117f1b8884 down
sudo iw dev wlx00117f1b8884 set type monitor
sudo ip link set wlx00117f1b8884 up
```
Then verify with:
```bash
iwconfig
```

## Step 5: Restart Network Manager (If Needed)
If your internet stops working, restart NetworkManager:
```bash
sudo systemctl restart NetworkManager
```

## Troubleshooting
- **Check if your adapter supports monitor mode:**
  ```bash
  iw list | grep -A 10 "Supported interface modes"
  ```
  If `monitor` is missing, your adapter does not support monitor mode.
- **Check for driver issues:**
  ```bash
  dmesg | grep wlan
  ```
- **For USB adapters, ensure proper drivers are installed:**
  ```bash
  lsusb
  ```
