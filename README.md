# Technical Infrastructure Portfolio: Hybrid Lab Architecture

## Project Overview
Design, assembly, and configuration of a multi-node hybrid lab environment for focused cybersecurity research, system administration, and vulnerability testing. The architecture emphasizes high availability, secure remote access, and clear segregation of duties between host and guest systems.

### 1. Lab Architecture & Remote Access

The environment utilizes powerful Windows 11 hosts for high-performance workloads, a dedicated "sandbox" host for virtualization, and a lean laptop for mobile access and documentation.

#### **Remote Orchestration: Sunshine + Moonlight**
*   **Implementation:** Configured Sunshine (host) and Moonlight (client) to enable seamless access from a repaired laptop client. Utilized **Tailscale** VPN to create a secure "Tailnet" between devices across different physical locations.
*   **Objective:** Achieved "anywhere-in-the-world" capability, demonstrating hardware repair skills alongside software configuration.

### 2. Virtualization Host Configuration (Build-002 Rig)

Optimized an Intel i7-7700 system to reliably host isolated virtual machines using Oracle VM VirtualBox. Ubuntu 24.04 LTS VM successfully provisioned using **LVM (Logical Volume Management)** for scalable storage, installed with a minimal attack surface configuration.

### 3. Deployment Challenges & Resolutions Log

This log documents key obstacles encountered during setup and the professional resolutions implemented across both the Hybrid Lab and the recent GitHub/Email configuration.

| Challenge Area | Problem Description | Resolution Strategy |
| :--- | :--- | :--- |
| **Hypervisor Lock** | VirtualBox failed to launch VMs; red status indicator on CPU icon (VT-x lock). | Disabled Windows Hyper-V via `bcdedit /set hypervisorlaunchtype off` and enabled `Intel Virtualization Technology` in ASUS UEFI BIOS. |
| **Graphics Failure** | Ubuntu installer displayed a purple screen with DRM/vmwgfx errors. | Changed VirtualBox Graphics Controller to **VMSVGA** and increased Video Memory to 128MB. |
| **Installer Freeze** | Ubuntu installer stalled/froze during "copying files" phase. | Increased VM CPU allocation to **4 cores** in VM settings to prevent resource starvation. |
| **Application Block** | Windows 11 **Smart App Control** blocked the Sunshine installer. | Temporarily disabled SAC via Windows Security panel; immediately re-enabled SAC post-installation. |
| **Connectivity** | Host PC not discoverable in Moonlight client search (different subnets). | Implemented **Tailscale** VPN and used manual IP entry for direct connectivity. |
| **Firewall/Download Block** | Tailscale installer stuck at 0% download on client laptop due to network security policies. | Bypassed restrictions using **PowerShell `winget install`** command. |
| **Email Auth Failure** | DMARC check failed despite SPF passing in initial tests (SPF/DKIM misalignment). | Ensured emails were sent via Zoho SMTP to include the DKIM signature; confirmed `DKIM: PASS` and `DMARC: PASS` via original message headers. |
| **HTTPS Activation** | "Enforce HTTPS" button was unclickable after successful DNS check. | Resolved temporary browser caching issue by activating the setting via an **incognito window**. |

### 4. Status & Future Work
The hybrid lab is operational. This setup validates understanding of virtualization, RDP alternatives, VPN tunneling, and hardware-level security configuration.

## Infrastructure & Stack
This portfolio demonstrates foundational skills in **DNS Management**, **Email Authentication**, and **Version Control/DevOps**. The entire system is built and maintained with a total cost of ownership of **$11.08 per year**.

| Component | Service Used | Purpose |
| :--- | :--- | :--- |
| **Domain Registrar** | Porkbun | Domain purchase and DNS management. |
| **Web Hosting** | GitHub Pages | Static site hosting directly from this repository. |
| **Email Hosting** | Zoho Mail | Professional, free "forever" mailbox (`chris@qfwllc.com`). |
| **Email Auth** | SPF, DKIM, DMARC | Domain security protocols verified and enforced. |

---

## Security & DNS Configuration
*   **HTTPS:** Enforced via GitHub Pages SSL certificates (**Active**).
*   **DNS Management:** A-Records and CNAMEs configured in Porkbun pointing traffic here.
*   **Email Security:** MX, SPF, DKIM, and DMARC records are configured, verified, and passing security audits for optimal email deliverability and authentication.

> [!SUCCESS]
> The website is fully active and securely reachable via HTTPS at **`https://qfwlc.com`**.

