# Proxmox Infrastructure

Here’s a tailored `README.md` for my **homelab / Proxmox infra project**:

---

## 🏠 Homelab Infrastructure — Proxmox & Beyond

This repository documents my journey of building a **homelab from scratch**, starting with a **single Proxmox node** on bare metal and expanding towards a multi-node cluster, shared storage (NFS), automation, and monitoring.

I have had one for a long time(2yrs +) but  thought it will be a good idea to document it so that i can refer back to it in the future and to help others who are trying to do the same.

The goal is to create a **real-world environment** for learning DevOps, Cloud, and infrastructure automation while showcasing hands-on experience.

---

## 📖 Table of Contents

1. [Overview](#-overview)  
2. [Current Setup](#-current-setup)  
3. [Network Topology](#-network-topology)  
4. [Proxmox Configuration](#-proxmox-configuration)  
5. [Roadmap](#-roadmap)  
6. [Lessons Learned](#-lessons-learned)  

---

## 🔎 Overview

- **Purpose**: Learn, experiment, and simulate production-grade infrastructure. I am by no means a professional sysadmin but i am trying to learn as much as i can.
- **Platform**: Proxmox VE (bare-metal virtualization).  
- **Scope**:  
  - Virtualization (VMs, LXC)  
  - Networking (CIDR blocks, VLANs, bridges)  
  - Storage (local, NFS, Ceph)  
  - Monitoring (Grafana, Prometheus)  
  - Automation (Ansible, Terraform)  
  - Kubernetes (K3s/k8s clusters)  

---

## 🖥 Current Setup
- **Hardware**: Custom-built bare metal server  
- **Hypervisor**: Proxmox VE 8.x  
- **Networking**:  
  - CIDR: `192.168.1.0/24`  check your network settings to confirm your CIDR block. make sure to use a range that is not used by your router.
  - Gateway: `192.168.1.254` Make sure to confirm your default gateway. Mine is `.254` not `.1` 
  - Proxmox datacenter IP: `192.168.1.73:8006` the port `8006` is the default port for Proxmox. paste on your browser to access the Proxmox web interface. you have to use the one you have reserved for Proxmox. 

---

## 🌐 Network Topology

### Current State (Single Node)
![Single Node Homelab](diagrams/single_node_homelab_gw254.png)

**Details:**  
- 🌐 Internet → 📡 Router (`192.168.1.254`) → 🔀 LAN Switch  
- 🖥 Proxmox Node (`192.168.1.73:8006`)  
- 💾 NAS / Shared Storage (`192.168.1.50`) *(future)*  
- 📦 PBS Backup Server (`192.168.1.80`) *(future)*  
- 📊 Monitoring Stack *(future)*  

---

## ⚙️ Proxmox Configuration
### Static IP (`/etc/network/interfaces`)
```bash
auto lo
iface lo inet loopback

auto enp3s0
iface enp3s0 inet manual

auto vmbr0
iface vmbr0 inet static
    address 192.168.1.73/24
    gateway 192.168.1.254
    bridge-ports enp3s0
    bridge-stp off
    bridge-fd 0
````

---

## 🛠 Roadmap

* [x] Setup Proxmox on bare metal
* [x] Configure static IP and gateway
* [ ] Add shared storage (NAS / NFS / ZFS)
* [ ] Deploy Proxmox Backup Server (PBS)
* [ ] Expand to multi-node cluster
* [ ] Install Kubernetes (K3s) cluster
* [ ] Setup monitoring (Prometheus + Grafana)
* [ ] Automate with Ansible + Terraform

---

## 📚 Lessons Learned

* Always confirm your **default gateway** (my setup uses `.254`, not `.1`).
* Reserve Proxmox’s IP outside of DHCP pool to avoid conflicts.
* Start small — a single node with a stable IP is better than rushing into clustering.
* Documentation + diagrams are just as valuable as the infra itself.

---

## 📜 License

MIT License © 2025
