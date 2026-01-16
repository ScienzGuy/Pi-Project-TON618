# TON618: The S-Tier Network Black Hole 🕳️

Named after the most massive black hole known to science, **TON618** is a Raspberry Pi-powered network appliance designed to pull every ad, tracker, and malicious domain into an unescapable singularity. This project combines **Pi-hole** and **PiVPN (WireGuard)** to provide aggressive, surgical-grade filtering for a residential network and mobile devices.

## 🚀 Overview
TON618 serves as the primary DNS gateway for a high-performance home network (anchored by a Nest Wifi Pro mesh system). It extends this protection to mobile devices via an encrypted WireGuard tunnel, ensuring an ad-free experience even on 5G/cellular networks.

### Core Stats
* **Blocklist Density:** 1,123,000+ domains.
* **Primary List:** HaGeZi Ultimate (High-Fidelity Filtering).
* **Block Rate:** ~22.8% of total network traffic (normalized).
* **Protocol:** WireGuard (UDP 51820).

## 🛠️ Hardware Stack
* **Controller:** Raspberry Pi 4 Model B.
* **Storage:** SanDisk Max Endurance MicroSD (optimized for high-frequency database writes to `gravity.db`).
* **Network:** Gigabit Ethernet (Hardwired to primary mesh node).

## ⚙️ Surgical Configurations
This repository documents the specific "Day 2" fixes required to stabilize high-density filtering on Android 16 and enterprise-grade mesh environments.

### 1. The VPN-to-WAN Bridge (Masquerade)
To allow VPN clients to access the internet through the Pi's Ethernet interface, a manual NAT masquerade was required:
```bash
sudo iptables -t nat -A POSTROUTING -s 10.228.35.0/24 -o eth0 -j MASQUERADE
sudo netfilter-persistent save
