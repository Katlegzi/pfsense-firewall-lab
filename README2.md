# NAT, Port Forwarding, and OpenVPN Lab

# Overview
This project extends our pfSense firewall lab by configuring Network Address Translation (NAT) rules, establishing port forwarding to route external traffic to an internal client, and deploying a secure OpenVPN remote access server.

---

# Lab Architecture & Services
- Port Forwarding: Configured WAN-to-LAN redirection mapping external port requests to internal client services on Client-01 (192.168.1.100).
- OpenVPN Server: Deployed a remote access VPN instance utilizing a dedicated Certificate Authority (CA), custom server certificates, and local database user authentication.
- Client Export: Generated and exported secure inline configuration profiles (.ovpn) for authenticated remote users.

---

# Step-by-Step Implementation

# Phase 1: Port Forwarding
- Configured inbound NAT rule on the WAN interface to forward incoming TCP traffic to the designated internal target IP (192.168.1.100).
- Verified automatic firewall rule generation by pfSense to permit forwarded traffic through the WAN filter.

# Phase 2: OpenVPN Setup Wizard
- Executed the OpenVPN Server Setup Wizard via the WebGUI (VPN > OpenVPN > Wizards).
- Established a dedicated Local User Access authentication scheme, generated a private Certificate Authority, and configured the server tunnel network (10.8.0.0/24) with LAN routing rules.

# Phase 3: User Management & Client Export
- Created a dedicated test user account (vpnuser) under System > User Manager and bound a unique user certificate signed by the lab CA.
- Installed the OpenVPN Client Export package to generate downloadable client configuration bundles for secure remote connections.

---

# Evidence & Screenshots

| Evidence Item | Description | Status |
| :--- | :--- | :--- |
| 1. Port Forward Rule | WAN NAT rule configuration directing traffic to internal client | Captured |
| 2. OpenVPN Server Status | Active OpenVPN server instance running on UDP port 1194 | Captured |
| 3. User Manager | Created test user account with paired cryptographic certificate | Captured |
| 4. Client Export Options | Generated OpenVPN configuration bundles and inline export profiles | Captured |
