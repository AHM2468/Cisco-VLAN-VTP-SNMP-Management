# Enterprise Network Design: VLAN, VTP & SNMP Management

An advanced enterprise-level network simulation designed in Cisco Packet Tracer utilizing a Star Topology. This project focuses on efficient local area network segmentation through Virtual LANs (VLANs), automated management via VLAN Trunking Protocol (VTP), and centralized infrastructure monitoring utilizing simple network management protocol methodologies.

## 🌐 Topology & IP Addressing Scheme

The architecture is deployed via 1 Centralized Router (Cisco 2911), 3 Switches (Cisco 2960), 6 End-User PCs, and 2 Dedicated Servers organized into three distinct corporate departments:

- **VLAN 10 (Sales Department):** Network `192.168.10.0/24` | Default Gateway: `192.168.10.1`
- **VLAN 20 (HR Department):** Network `192.168.20.0/24` | Default Gateway: `192.168.20.1`
- **VLAN 30 (IT Department):** Network `192.168.30.0/24` | Default Gateway: `192.168.30.1`

### **Infrastructure Endpoints Mapping:**
- **Server 1 (Network Monitoring Station):** Assigned to **VLAN 30** (`192.168.30.2`)
- **Server 2 (Testing Server):** Assigned to **VLAN 20** (`192.168.20.2`)

## 🚥 Switch & VTP Domain Configuration

To simplify network administration and avoid manual database mismatches, the VLAN Trunking Protocol was deployed with the following parameters:
- **VTP Domain Name:** `AKM_Network`
- **VTP Password:** `02468`
- **Switch 1 (Core):** Configured in **VTP Server Mode** to broadcast configuration changes.
- **Switch 2 & Switch 3:** Configured in **VTP Client Mode** to dynamically synchronize database records across IEEE 802.1Q trunk links.

*Security Best Practice:* **VLAN 1** was strictly isolated and restricted from hosting active production, host, or native management traffic to eliminate security threats such as VLAN hopping and excessive broadcast storm domain saturation.

## 🛠️ SNMP Troubleshooting Framework

The project includes an optimization analysis for handling Simple Network Management Protocol (SNMP) tracking constraints:
1. **"SNMP Is Not Enabled" Faults:** Resolved by adjusting access control lists (ACLs), matching community string parameters (`public`/`private`), and opening UDP inbound ports **161** and **162**.
2. **`RESPONSE_DELAYED` Errors:** Managed by adjusting NMS timeout metrics, analyzing baseline link saturation, and prioritizing protocol traffic on switches via the `snmp-server ip precedence 7` command execution.
3. **`noSuchName` / `noSuchObject` Faults:** Fixed by validating active OID identifiers against enterprise MIB definition rules using automated native diagnostic walks (`snmpwalk`).

## 📂 Repository Contents
- `IT363 Project.pkt`: Original Cisco Packet Tracer live environment layout.
