# 🔒 Secure Remote Access Infrastructure — VPN, SSH, RDP & Wake-on-LAN

A practical project focused on building secure, private remote access to home lab devices **without using unsafe port forwarding**. The setup uses overlay VPN networking, cross-platform remote administration, and remote power management — combining real infrastructure concepts in one project.

---

## 🎯 Project Goals

- Build secure remote access to home lab devices without exposing services to the public internet
- Use a private VPN overlay network instead of router port forwarding
- Test cross-platform remote administration (Linux + Windows)
- Explore Wake-on-LAN for remote power management
- Understand the difference between network connectivity and service availability

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| Tailscale | Private VPN overlay network between trusted devices |
| Raspberry Pi 4 Model B | Always-on internal home lab device |
| SSH | Remote Linux command-line administration |
| Windows Remote Desktop (RDP) | Graphical remote access to Windows systems |
| Samba / SMB | Network file sharing |
| Wake-on-LAN | Remote power-on testing |
| Fing mobile app | WoL packet sending from mobile |
| iPhone / mobile clients | Cross-device access testing |

---

## 📋 What I Did

### 1. Raspberry Pi as Always-On Lab Device
Set up the Raspberry Pi as a low-power, always-on device on the home network using Ethernet for stability. Verified its local IP address before doing anything else — addressing mistakes early always cost time later.

### 2. SSH Remote Administration
Configured SSH access to the Pi so it could be managed entirely from another device — no monitor, keyboard, or mouse required. This turned the Pi into a small, headless server suitable for hosting services.

### 3. Tailscale VPN Deployment
Installed and configured Tailscale to create a **private overlay network** between trusted devices. Instead of opening ports on the router (the unsafe traditional approach), Tailscale creates an encrypted, authenticated mesh between authorised devices.

The Tailscale network ended up containing **8 trusted devices** across Windows, iOS, and Linux — all able to reach each other privately regardless of which physical network they were on.

### 4. Remote Connectivity Testing
Verified connectivity across the VPN using ping tests and service-level checks. A key learning: **a working VPN doesn't mean working services**. Each service (SSH, file sharing, RDP) had to be configured individually — the VPN just provides the path.

### 5. Network File Sharing
Configured shared folder access (`\\192.168.0.22`) so files could be accessed both locally and remotely through the VPN. Mounted the share as a drive letter on Windows clients (Z:) for easy access. Total share capacity: 457 GB with 430 GB free.

### 6. Mobile Access Testing
Verified the setup worked from an iPhone via the Tailscale mobile app, confirming the architecture supports flexible access from any client device — not just laptops.

### 7. Windows Remote Desktop (RDP)
Configured RDP on the Windows machine and tested graphical remote access. Troubleshot connection issues that came down to:
- Windows firewall rules
- Account permissions
- Service status checks
- RDP-specific Windows settings

This proved that remote access is a **layered problem** — networking, OS configuration, and service settings all have to align.

### 8. Wake-on-LAN Testing
Tested two different Wake-on-LAN methods:
- **Fing mobile app** — successfully woke the device
- **Heimdall dashboard / web-based WoL tool** — did not work reliably

Learned that WoL behaviour depends on:
- BIOS/UEFI configuration
- Network adapter power settings
- Magic packet delivery path (some methods don't broadcast properly)
- Target device power state

### 9. Security Considerations
Deliberately avoided port forwarding because exposing services to the public internet creates real attack surfaces. Tailscale's authentication model (tied to identity, not IP) made the setup both more secure and easier to manage long-term.

---

## 🧠 Key Skills Demonstrated

- VPN architecture and overlay networking (Tailscale)
- SSH server configuration and remote Linux administration
- Windows Remote Desktop (RDP) configuration and troubleshooting
- Network file sharing (SMB/Samba)
- Wake-on-LAN concepts and BIOS-level configuration
- Cross-platform remote administration (Linux, Windows, iOS)
- Mobile remote access testing
- Layered troubleshooting (network → OS → service)
- Secure access design (avoiding unsafe port forwarding)
- IP addressing and device verification

---

## 💡 What I Took Away

The single most important lesson: **secure remote access is a layered system**. A VPN connection doesn't mean working services. A reachable device doesn't mean a configured one. Real infrastructure involves the VPN, OS settings, service config, firewall rules, and routing all aligning — and each layer has to be checked individually.

This project moved my understanding from "how do I connect to my Pi remotely" to "how do I design secure remote access properly" — which is a much more useful question for real IT work.
