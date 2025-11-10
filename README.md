# 🌐 Network Planning & Design for Folds, Fins & Welders Company

This repository contains the documentation for a **Network Planning Assignment**, detailing the industry-standard design, IP addressing scheme, and estimated costs for the Folds, Fins & Welders Company network infrastructure.

## Project Details

Network Planning


---

## 1. Departmental Network Design (Administration, Amenities, and Warehouse 1)

This section outlines the industry-standard design for the three key departments, focusing on structure, security, and scalability.

### 1.1 Design Steps & Rationale

| Component | Configuration Steps | Rationale (Industry Standard) |
| :--- | :--- | :--- |
| **VLAN Configuration** | Configured VLANs for Administration (Payroll, Reception, Accounts, Sales, Finance, Management) and a segregated Guest IP for Wireless Access Points (WAPs). | **Enhances network security and management** by segregating traffic based on departments and isolating guest traffic. Allows for future expansion. |
| **Layer 2 Switches** | Introduced Layer 2 switches (Switch A and Switch B) to create distinct broadcast domains. Ports assigned to specific departmental VLANs. | **Controls broadcast traffic** and manages network traffic efficiently within the local segment. |
| **Trunk Link** | Established a trunk link between Switch A and Switch B. | Essential for **transporting VLAN traffic** between switches. |
| **Layer 3 Switch (IDF)** | Installed a Layer 3 switch in the Administration Intermediate Distribution Frame (IDF) for **Inter-VLAN Routing**. Configured VLAN interfaces with assigned IP addresses. | Improves **network performance and security** by handling routing locally, recommended for medium to large-scale networks. |
| **Structured Cabling** | Used **Category 6 (Cat6) Ethernet cabling**. | Ensures **high-speed data transmission** (Gigabit Ethernet speeds) for modern network installations. |
| **Network Switches** | Installed 48-port Gigabit Ethernet switches with **stacking capabilities**. | Provides **scalability and facilitates future expansion** by allowing easy addition of more ports. |
| **Wireless Access Points (WAPs)** | Deployed at least two dual-band WAPs. Used a separate Guest IP VLAN. | Ensures secure wireless connectivity and separation of guest devices from sensitive departmental data. |
| **IP Cameras** | Installed IP cameras for surveillance, connected to the network, with centralized monitoring. | Standard approach for **enhancing security and surveillance** capabilities. |

***Note:** The same design principles are applied to the Amenities and Warehouse 1 departments.*

### 1.2 IP Addressing Scheme

The network uses **IPv4** for all devices.

#### Building LANs Summary

| Building | Network | No. of Usable Hosts | Hosts + Expansion | Subnet ID/Mask | First Host | Last Host | Broadcast |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Administration** | 192.168.15.128/25 | 32 | 126 | .128/25 | .129 | .254 | .255 |
| **Amenities** | 192.168.16.0/26 | 10 | 62 | .0/26 | .1 | .62 | .63 |
| **Warehouse 1** | 192.168.16.112/28 | 1 | 14 | .112/28 | .113 | .126 | .127 |

#### Administration Building VLANs (Network: 192.168.15.128/25)

| VLAN | Hosts + Expansion | Subnet ID/Mask | First Host | Last Host | Broadcast |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Guest WAP** | 30 | .128/27 | .129 | .158 | .159 |
| **Payroll Section** | 14 | .160/28 | .161 | .174 | .175 |
| **Admin/Reception** | 14 | .176/28 | .177 | .190 | .191 |
| **Management** | 14 | .192/28 | .193 | .206 | .207 |
| **Account** | 14 | .208/28 | .209 | .222 | .223 |
| **Finance** | 6 | .224/29 | .225 | .230 | .231 |
| **Sales** | 6 | .232/29 | .233 | .238 | .239 |
| **IP Camera** | 6 | .240/29 | .241 | .246 | .247 |

#### Amenities Building VLANs (Network: 192.168.16.0/26)

| VLAN | Hosts + Expansion | Subnet ID/Mask | First Host | Last Host | Broadcast |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Guest WAP** | 30 | .0/27 | .1 | .30 | .31 |
| **Staff Sitting Room** | 14 | .32/28 | .33 | .46 | .47 |
| **Catering Kitchen** | 6 | .48/29 | .49 | .54 | .55 |
| **Staff Canteen** | 6 | .56.29 | .57 | .62 | .63 |

---

## 2. All-Site Network Design with Redundancy

This section details the design of the entire site network, incorporating redundancy, media selection, and a comprehensive IP scheme.

### 2.1 Redundancy & Media Considerations

The design emphasizes **redundancy** and strategic use of different media types to ensure reliability and performance.

* **Core Infrastructure:** Dual ISP connection to a redundant pair of **Cisco ISR 4000 Series Routers** and **Cisco ASA 5506-X Firewalls**.
* **MDF Setup:** A Main Distribution Frame (MDF) with redundant switches is established. The main MDF is suggested for the **Administration Department** for easy access by IT personnel and proximity to decision-makers. The redundant MDF is suggested for the **Amenities Department** as a strategic backup location in case of an emergency affecting the primary location.
* **Inter-Building Connectivity:** **Armored Single-mode Fiber Optic Cable** is used between the MDF and each department's IDF switch. This is crucial for **longer distances** and to withstand potential **electromagnetic interference** on the site.
* **Industrial Connectivity:** Fiber optic cable is recommended for connecting industrial devices like Lathe machines in the Manufacturing Department to withstand harsh environments and ensure reliable, high-performance connectivity.
* **Intra-Building Connectivity:** Standard **Cat6 Ethernet cables** are used for connecting devices to the IDF switches within each building.

### 2.2 All-Site IPv4 Network Scheme

The following table provides the complete IPv4 subnetting plan for the entire site, including inter-device links for redundancy.

| Building/Link | Network | Hosts + Expansion | Subnet ID/Mask | First Host | Last Host | Broadcast |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Testing Floor** | 192.168.15.0/25 | 126 | .0/25 | .1 | .126 | .127 |
| **Administration** | 192.168.15.128/25 | 126 | .128/25 | .129 | .254 | .255 |
| **Amenities** | 192.168.16.0/26 | 62 | .0/26 | .1 | .62 | .63 |
| **Manufacturing** | 192.168.16.64/27 | 30 | .64/27 | .65 | .94 | .95 |
| **Security** | 192.168.16.96/28 | 14 | .96/28 | .97 | .110 | .111 |
| **Warehouse 1** | 192.168.16.112/28 | 14 | .112/28 | .113 | .126 | .127 |
| **Warehouse 2** | 192.168.16.128/28 | 14 | .128/28 | .129 | .142 | .143 |
| **MDF S1 to FW1** | 192.168.16.144/30 | 2 | .144/30 | .145 | .146 | .147 |
| **MDF S1 to FW2** | 192.168.16.148/30 | 2 | .148/30 | .149 | .150 | .151 |
| **MDF S2 to FW1** | 192.168.16.152/30 | 2 | .152/30 | .153 | .154 | .155 |
| **MDF S2 to FW2** | 192.168.16.156/30 | 2 | .156/30 | .157 | .158 | .159 |
| **FW1 to Router 1** | 192.168.16.160/30 | 2 | .160/30 | .161 | .162 | .163 |
| **FW2 to Router 2** | 192.168.16.172/30 | 2 | .172/30 | .173 | .174 | .175 |
| **Admin IDF S1 to MDF S1** | 192.168.16.192/30 | 2 | .192/30 | .193 | .194 | .195 |
| *... (Other Inter-IDF/MDF Links)* | *...* | *...* | *...* | *...* | *...* | *...* |

### 2.3 IPv4 Over IPv6 Rationale

**IPv4** was chosen over IPv6 for the following reasons:

1.  **Limited Device Count:** The company has a limited number of devices, making the vast address space of IPv6 unnecessary.
2.  **Compatibility & Ubiquity:** IPv4 is the most extensively used protocol, ensuring compatibility with the existing majority of networking hardware, operating systems, and software.
3.  **Cost of Upgrade:** Supporting IPv6 might require expensive upgrades to the current network infrastructure (firewalls, switches, routers).
4.  **Familiarity & Troubleshooting:** IT experts are typically more familiar with IPv4, simplifying troubleshooting due to decades of widespread use and extensive available resources.

---

## 3. Estimated Network Cost Analysis

The following table provides the estimated costs for the essential networking components to implement the design.

| Component | Description | Quantity | Unit Price (£) | Total Cost (£) | Justification |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Cisco Catalyst 3850 L3 Switch (48 ports)** | All Building IDF Switch | 7 | 2300 | 16100 | Robust security measures, best price/performance for Layer 3 (routing capabilities) at IDF points. |
| **Cisco Catalyst 3650 L2 Switch (48 ports)** | Admin Building IDF Switch | 2 | 3292 | 6584 | Provides essential Layer 2 security features (ACLs, port security) for a primary location. |
| **Cisco Catalyst 3850 L3 Switch (48 ports)** | MDF Switch (Redundancy) | 2 | 2300 | 4600 | Used as core redundant distribution layer switches. |
| **Cisco ISR 4000 Series Router** | MDF Router (Dual ISP) | 2 | 3900 | 7800 | Provides robust security (firewall, VPN, encryption) and integrated wireless capability. |
| **Cisco ASA 5506-X Firewall** | MDF Firewall (Redundancy) | 2 | 1330 | 2660 | Stateful firewall, IPS, and advanced threat protection for critical asset protection. |
| **Armored Single-mode Fiber Optic Cable** | Inter-building connectivity | 2000m | 3.5 | 7000 | Physical protection, ideal for long distances, and resistance to EMI. |
| **Cat6 Ethernet Cables** | Intra-building connectivity | 5000m | 0.45 | 2250 | High performance and faster data transmission within buildings. |
| **Underground Cable Ducting** | Inter-building connectivity | 1000m | 4 | 4000 | Protects underground cables from crushing, chemicals, and water. |
| **PVC Trunking Pipe** | All building cable management | 1500m | 3 | 4500 | Hides cables, eliminates clutter, and ensures a clean, organized installation. |
| **Network Equipment Racks (22U)** | IDF Racks/Cabinets | 7 | 284 | 1988 | Cable management options, improved airflow, and organization. |
| **Network Equipment Rack (22U)** | MDF Racks/Cabinets | 2 | 284 | 568 | Cable management for core network gear. |
| **Wall Sockets (RJ45)** | All Building | 255 | 12 | 3060 | Provides neat, dedicated, and organized network connection points. |
| **Ethernet Patch Panels (24-Port Cat6)** | All Building | 13 | 43 | 559 | Simplifies cable management, troubleshooting, and provides rack-mountable organization. |
| **Fiber Optic Patch Panels** | All Building | 13 | 40 | 520 | Modular design for customization, scalability, and organized fiber termination. |
| **Fiber Optic Connector (LC)** | All Building | 30 | 7 | 210 | Small, slim design for high-density installations in equipment. |
| **10G SFP+ LC Multi-Mode Transceiver Module** | All Building | 17 | 15 | 255 | Provides 10 Gbps bandwidth for demanding applications. |
| **Cable Ties (Panduit)** | All Building (20 packs of 750) | 20 | 10 | 7500 | Durable and reliable for securing and organizing cables. |
| **Total Estimated Cost (Excluding Labor)** | | | | **70,064** | |

---

If you need any specific section of this README formatted differently or have further documentation to add, please let me know!
