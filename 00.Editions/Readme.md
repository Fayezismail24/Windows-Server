# Windows Server Editions

A comprehensive reference for Windows Server editions — covering key differences, use cases, licensing rights, and virtualization entitlements.

---

## Quick Comparison

| Feature | Essentials | Standard | Datacenter | Azure Edition | Evaluation |
|---|---|---|---|---|---|
| **Target** | Small business | General purpose | Highly virtualized | Azure-only | Lab / Testing |
| **Cost** | Paid | Paid | Paid | Azure billing | Free |
| **Duration** | Perpetual | Perpetual | Perpetual | Subscription | 180 days (extendable) |
| **Max Users** | 25 | Unlimited | Unlimited | Unlimited | Unlimited |
| **Max Devices** | 50 | Unlimited | Unlimited | Unlimited | Unlimited |
| **CALs Required** | ❌ No | ✅ Yes | ✅ Yes | ❌ No (Azure billing) | ❌ No |
| **Production Use** | ✅ | ✅ | ✅ | ✅ | ❌ Not permitted |
| **VM Rights (OSEs)** | 1 (physical only) | 2 VMs per license | Unlimited VMs | Unlimited (Azure) | Unlimited (Datacenter-based) |
| **Hyper-V Host** | ❌ | ✅ | ✅ | ❌ | ✅ |
| **Failover Clustering** | ❌ | ✅ | ✅ | ✅ | ✅ |
| **Storage Spaces Direct** | ❌ | ❌ | ✅ | ✅ | ✅ |
| **Shielded VMs** | ❌ | ❌ | ✅ | ✅ | ✅ |
| **Software-Defined Networking** | ❌ | ❌ | ✅ | ✅ | ✅ |
| **Hotpatch (no-reboot updates)** | ❌ | ❌ | ❌ | ✅ | ❌ |
| **SMB over QUIC** | ❌ | ❌ | ❌ | ✅ | ❌ |
| **Available On-Premises** | ✅ | ✅ | ✅ | ❌ | ✅ |
| **Available on Azure** | ❌ | ✅ | ✅ | ✅ | ❌ |
| **Convertible to Full License** | N/A | N/A | N/A | N/A | ✅ In-place |

---

## Editions — Detailed Breakdown

### 1. Essentials

> Designed for small businesses that need a simple, affordable server without complex licensing.

**Key characteristics:**
- Supports up to **25 users** and **50 devices**
- **No CALs required** — the edition license covers all users/devices within the limits
- Can only run on a **single physical server** (no virtualization rights)
- Provides built-in integration with **Microsoft 365 / Azure** for hybrid scenarios
- Includes a connector tool for automatically joining client PCs to the domain

**Common roles:**
- File and print server
- Domain controller for small offices
- Basic application hosting

**Limitations:**
- Cannot be used as a Hyper-V host for running other VMs
- No failover clustering or high-availability features
- Hard cap of 25 users — exceeding this requires upgrading to Standard

**Licensing:**
- Licensed per server (not per core)
- One license per physical server, no stacking

---

### 2. Standard

> The go-to edition for most on-premises workloads — physical servers or lightly virtualized environments.

**Key characteristics:**
- Supports all standard server roles (AD DS, DNS, DHCP, File Services, IIS, RDS, etc.)
- Includes rights to run **2 Virtual Machines (OSEs)** per license
- To run more VMs on the same host, additional Standard licenses can be stacked (e.g., 2 licenses = 4 VMs)
- Supports Hyper-V, but **not** Storage Spaces Direct or Shielded VMs

**Common roles:**
- Active Directory Domain Controller
- File and Print Server
- Web Server (IIS)
- Remote Desktop Services (with RDS CALs)
- DNS / DHCP

**Virtualization rights:**
- 2 OSEs (OS Environments) per license
- Stack licenses on the same host for more VMs
- Example: 3 Standard licenses on one host = 6 licensed VMs

**Licensing:**
- Licensed **per physical core** (minimum 16 cores per server, 8 per processor)
- Requires **Windows Server CALs** for every user or device accessing the server
- Software Assurance (SA) optional but recommended for upgrade rights

**When to choose Standard over Datacenter:**
- Running 1–2 VMs per host
- Physical server workloads with no heavy virtualization
- Budget-conscious environments

---

### 3. Datacenter

> Built for cloud-scale, heavily virtualized, and software-defined infrastructure.

**Key characteristics:**
- **Unlimited virtual machines** on the licensed physical host
- All features of Standard, plus exclusive enterprise features
- The preferred edition for **Hyper-V hosts, HCI clusters, and private cloud**

**Exclusive features (not in Standard):**
| Feature | Description |
|---|---|
| **Storage Spaces Direct (S2D)** | Software-defined storage for HCI clusters |
| **Shielded VMs** | Encrypted VMs protected from compromised fabric admins |
| **Software-Defined Networking (SDN)** | Full network virtualization stack |
| **Network Controller** | Centralized SDN management |
| **Host Guardian Service (HGS)** | Attestation service for Shielded VM fabric |
| **Azure Stack HCI integration** | Deep integration with Azure Stack HCI clusters |

**Common roles:**
- Hyper-V virtualization host
- HCI (Hyper-Converged Infrastructure) nodes
- Private cloud / SCVMM-managed fabric
- Environments requiring Shielded VMs for tenant isolation

**Licensing:**
- Licensed **per physical core** (same minimum rules as Standard)
- Requires **Windows Server CALs** (same as Standard)
- More expensive per license, but cost-effective when running 3+ VMs per host

**Standard vs Datacenter — break-even point:**
- Each Standard license = 2 VMs
- If you need more than 2 VMs per host → stacking Standard licenses becomes more expensive than a single Datacenter license
- **General rule: 3+ VMs per host = Datacenter is cheaper**

---

### 4. Azure Edition

> A cloud-exclusive edition available only via the Azure Marketplace, with Azure-native enhancements.

**Key characteristics:**
- Only available as an **Azure VM** — cannot be installed on-premises or in other clouds
- Includes exclusive features not available in any other edition
- Billing is consumption-based through Azure (no separate license purchase)
- No traditional CALs — access licensing is handled through Azure

**Exclusive features:**
| Feature | Description |
|---|---|
| **Hotpatch** | Apply security patches without rebooting the VM |
| **SMB over QUIC** | Access file shares securely over the internet without VPN |
| **Azure Extended Network** | Stretch on-prem subnets into Azure seamlessly |
| **Azure Automanage** | Automated best-practice configuration and management |

**Common use cases:**
- Azure-hosted workloads requiring minimal downtime (Hotpatch)
- File servers accessible over the internet without VPN (SMB over QUIC)
- Enterprise workloads fully committed to Azure

**Licensing:**
- Included in Azure VM pricing (pay-as-you-go or Reserved Instances)
- Azure Hybrid Benefit can be applied if you have existing on-prem licenses with SA
- No on-premises deployment rights

---

## Choosing the Right Edition

```
Is this a small office with ≤25 users and no virtualization needs?
  └── YES → Essentials

Is this an Azure-only deployment?
  └── YES → Azure Edition

How many VMs will run on this physical host?
  ├── 0–2 VMs (or physical workload) → Standard
  └── 3+ VMs → Datacenter
```

---

## Version History

| Version | Release Year | End of Mainstream Support | End of Extended Support |
|---|---|---|---|
| Windows Server 2025 | 2024 | 2029-10-09 | 2034-10-09 |
| Windows Server 2022 | 2021 | 2026-10-13 | 2031-10-14 |
| Windows Server 2019 | 2018 | 2024-01-09 | 2029-01-09 |
| Windows Server 2016 | 2016 | 2022-01-11 | 2027-01-12 |

> ⚠️ Windows Server 2019 is past mainstream support. Plan upgrades accordingly.

---

## Evaluation Edition

Microsoft provides a **free 180-day trial** of Windows Server (Standard and Datacenter) through the Microsoft Evaluation Center. It is fully functional with no feature restrictions — the only limitation is the time window.

| Property | Details |
|---|---|
| **Duration** | 180 days |
| **Editions available** | Standard, Datacenter |
| **Feature restrictions** | None |
| **Extendable** | Yes — up to 5 times via `slmgr /rearm` |
| **Convertible to full license** | Yes — in-place, no reinstall needed |
| **Production use allowed** | ❌ Not permitted per EULA |
| **Requires Microsoft account** | ✅ Yes (for download) |
| **Available versions** | Windows Server 2022, 2025 |

---

### Download

1. Go to **[microsoft.com/evalcenter](https://www.microsoft.com/en-us/evalcenter)**
2. Select **Windows Server 2025** or **Windows Server 2022**
3. Sign in with a Microsoft account (free account is sufficient)
4. Fill in a short registration form
5. Choose your download format:

| Format | Description | Best for |
|---|---|---|
| **ISO** | Bootable installer image | Bare-metal installs, VMs via ISO mount |
| **VHDX** | Pre-built virtual hard disk | Hyper-V — fastest way to spin up a test VM |

> 💡 **Tip:** The VHDX is the quickest option for lab environments — attach it to a new Hyper-V VM and boot directly, no installation wizard needed.

---

### Installation Options

During setup, you will be prompted to choose an installation type:

| Option | Description | Recommended? |
|---|---|---|
| **Server Core** | CLI only, no GUI | ✅ Microsoft's recommended direction — lower attack surface, less resource usage |
| **Desktop Experience** | Full GUI (like Windows) | Better for learning/lab environments |

> ⚠️ You cannot switch between Core and Desktop Experience after installation without reinstalling. Choose carefully.

---

### Activation Status

Check your current evaluation status at any time:

```cmd
slmgr /xpr
```

This shows the license expiry date in a dialog box.

To see detailed license info:

```cmd
slmgr /dlv
```

---

### Extending the Evaluation

The evaluation can be extended using the **rearm** command. Each rearm adds another 180 days.

```cmd
slmgr /rearm
```

- Maximum of **5 rearms** allowed
- Requires a **reboot** after each rearm
- Gives up to ~**3 years** of evaluation time total (180 days × 6 periods)

**Check remaining rearm count:**

```cmd
slmgr /dlv
```

Look for the line: `Remaining Windows rearm count`

> ⚠️ Once all rearms are exhausted, the system will nag on login and the screen may dim. It will not automatically shut down or delete data, but it is not suitable for any use at that point.

---

### What Happens at Expiry

| Behavior | Details |
|---|---|
| Login warning | Displayed on every login |
| Screen dimming | Desktop background turns black |
| Auto shutdown | ❌ Does not occur (Server 2019+) |
| Data loss | ❌ Does not occur |
| Services stop | ❌ Services keep running |

> The system remains technically operational after expiry but is non-compliant. Convert or rearm before expiry in any active lab environment.

---

### Converting to a Full License

Once you purchase a license, you can activate in-place — **no reinstall required**.

**Standard Edition:**

```cmd
DISM /online /Set-Edition:ServerStandard /ProductKey:XXXXX-XXXXX-XXXXX-XXXXX-XXXXX /AcceptEula
```

**Datacenter Edition:**

```cmd
DISM /online /Set-Edition:ServerDatacenter /ProductKey:XXXXX-XXXXX-XXXXX-XXXXX-XXXXX /AcceptEula
```

> ⚠️ You can only convert **upward** (Eval → Standard or Eval → Datacenter). You cannot downgrade using DISM.

Alternatively, inject the product key directly if the edition already matches your license:

```cmd
slmgr /ipk XXXXX-XXXXX-XXXXX-XXXXX-XXXXX
slmgr /ato
```

---

### Evaluation vs Full License

| Aspect | Evaluation | Full License |
|---|---|---|
| Cost | Free | Paid |
| Duration | 180 days (extendable) | Perpetual or subscription |
| Windows Update | ⚠️ Limited during eval period | ✅ Full access |
| Production use | ❌ Not permitted (EULA) | ✅ |
| Domain join | ✅ Allowed | ✅ |
| All server roles | ✅ Available | ✅ |
| Azure Hybrid Benefit | ❌ | ✅ (with SA) |

---

### Quick Reference — slmgr Commands

| Task | Command |
|---|---|
| Check expiry date | `slmgr /xpr` |
| View detailed license info | `slmgr /dlv` |
| Extend evaluation (rearm) | `slmgr /rearm` |
| Inject a product key | `slmgr /ipk <key>` |
| Activate online | `slmgr /ato` |
| Convert edition via DISM | `DISM /online /Set-Edition:<edition> /ProductKey:<key> /AcceptEula` |
| Uninstall current key | `slmgr /upk` |
| Clear key from registry | `slmgr /cpky` |

---

## Related Topics

- [Licensing Models](../licensing/README.md)
- [Client Access Licenses (CALs)](../cals/README.md)
- [Core Licensing Rules](../licensing/core-licensing.md)

---

*Last updated: June 2026 | Based on Microsoft official documentation*
