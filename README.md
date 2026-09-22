# pfSense Firewall Installation, Configuration & Testing Lab

# Overview
This project documents the successful deployment, network configuration, and security rule enforcement of a pfSense Firewall virtual appliance in a simulated lab environment using VirtualBox. A client virtual machine (`Client-01`) was routed through the firewall to test packet filtering, custom firewall rule evaluation, and protocol analysis.

---

# Lab Architecture & Topology
* Firewall VM (pfSense-FW): 
  * WAN Interface (`em0`): Bridged/NAT network for upstream connectivity.
  * LAN Interface (`em1`): Internal Network (`LabNet`) configured with static IP `192.168.1.1/24` acting as the default gateway for internal clients.
* Client VM (`Client-01`): Xubuntu Linux instance attached to `LabNet`, dynamically assigned an IP address via pfSense's built-in DHCP server (`192.168.1.100` - `192.168.1.199`).

---

# Step-by-Step Implementation

# Phase 3: Interface Assignment & Configuration
* Configured network interface mappings during initial installation: assigned `em0` as WAN and `em1` as LAN.
* Established internal subnet routing and verified basic console status metrics.

# Phase 5: WebGUI Setup & Verification
* Completed the initial pfSense setup wizard via the client browser (`https://192.168.1.1`).
* Configured system hostname (`pfsense-lab`), upstream DNS servers (`8.8.8.8` / `1.1.1.1`), and secured admin credentials.
* Verification: Confirmed both WAN and LAN interfaces were active and reporting as `[UP]` on the dashboard.

# Phase 6: Firewall Rules & Traffic Control
* ICMP Filtering: Created a custom LAN rule blocking outbound ICMP traffic originating from the local subnet. Verified failure via terminal ping tests (100% packet loss).
* Destination-Specific Blocking: Implemented a TCP block rule targeting a specific external host (`example.com` / `93.184.216.34`) across ports 80 and 443 while ensuring unrestricted access to alternate sites like `neverssl.com`
* Top-Down Evaluation: Confirmed the importance of rule ordering, noting that custom block rules must sit above the default allow rule to take effect.

# Phase 7: Packet Analysis & Logging
* Inspected real-time firewall event logs under Status > System Logs > Firewall to trace blocked traffic entries.
* Utilized Wireshark on `Client-01` to capture and verify filtered ICMP requests versus successful HTTP/TLS sessions.

---

# Evidence & Screenshots

| Evidence Item | Description | Status |
| :--- | :--- | :--- |
| 1. Interface Assignment | Console output showing `em0` (WAN) and `em1` (LAN) bindings. | Captured |
| 2. WebGUI Dashboard | Interfaces widget showing WAN and LAN status as `[UP]`. | Captured |
| 3. Firewall Rule Table | Custom ICMP and destination block rules placed above the default allow rule. | Captured |
| 4. ICMP Block Test | Terminal output demonstrating 100% packet loss on ping. | Captured |
| **5. Web Block Test** | Browser error page confirming successful interception of `example.com`[cite: 1]. | Captured |
| **6. Firewall Logs** | System log entries displaying dropped packet events[cite: 1]. | Captured |
| **7. Wireshark Capture** | Packet capture analysis verifying blocked versus allowed traffic streams[cite: 1]. | Captured |
