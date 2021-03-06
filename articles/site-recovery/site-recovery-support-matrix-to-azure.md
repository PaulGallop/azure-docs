---
title: Azure Site Recovery support matrix for replicating to Azure | Microsoft Docs
description: Summarizes the supported operating systems and components for Azure Site Recovery
services: site-recovery
documentationcenter: ''
author: Rajani-Janaki-Ram
manager: rochakm
editor: ''

ms.assetid:
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 01/25/2017
ms.author: rajanaki

---
# Azure Site Recovery support matrix for replicating to Azure

> [!div class="op_single_selector"]
> * [Replicate to Azure](site-recovery-support-matrix-to-azure.md)
> * [Replicate to customer-owned secondary site](site-recovery-support-matrix-to-sec-site.md)


This article summarizes supported configurations and components for Azure Site Recovery when replicating and recovering to Azure. For more about prerequisites for Azure Site Recovery, see [Site Recovery best practices](site-recovery-best-practices.md).


## Support for deployment options

**Deployment** | **VMware/physical server** | **Hyper-V (no Virtual Machine Manager)** | **Hyper-V (with Virtual Machine Manager)**
--- | --- | --- | ---
**Azure portal** | On-premises VMware VMs to Azure storage, with Azure Resource Manager or classic storage and networks.<br/><br/> Failover to Resource Manager-based or classic VMs. | On-premises Hyper-V VMs (not in Virtual Machine Manager clouds) to Azure storage, with Resource Manager or classic storage and networks.<br/><br/> Failover to Resource Manager-based or classic VMs. | On-premises Hyper-V (VMs in Virtual Machine Manager clouds) to Azure storage, with Resource Manager or classic storage and networks.<br/><br/> Failover to Resource Manager-based or classic VMs.
**Classic portal** | Maintenance mode only. New vaults can't be created. | Maintenance mode only. | Maintenance mode only.
**PowerShell** | Not currently supported. | Supported | Supported


## Support for datacenter management servers

### Virtualization management entities

**Deployment** | **Support**
--- | ---
**VMware VM/physical server** | vSphere 6.0, 5.5, or 5.1 with latest update
**Hyper-V (with Virtual Machine Manager)** | System Center Virtual Machine Manager 2016 and System Center Virtual Machine Manager 2012 R2

  >[!Note]
  > A System Center Virtual Machine Manager 2016 cloud with a mixture of Windows Server 2016 and 2012 R2 hosts isn't currently supported.

### Host servers

**Deployment** | **Support**
--- | ---
**VMware VM/physical server** | vCenter 5.5 or 6.0 (support for 5.5 features only)
**Hyper-V (no Virtual Machine Manager)** | Windows Server 2016, Windows Server 2012 R2 with latest updates
**Hyper-V (with Virtual Machine Manager)** | Windows Server 2016, Windows Server 2012 R2 with latest updates.<br/><br/> Windows Server 2016 hosts should be managed by System Center Virtual Machine Manager 2016.

  >[!Note]
  >A Hyper-V site that mixes hosts running Windows Server 2016 and 2012 R2 isn't currently supported.

## Support for replicated machine OS versions

Virtual machines that are protected must meet [Azure requirements](site-recovery-best-practices.md#azure-virtual-machine-requirements) when replicating to Azure.
The following table summarizes replicated operating system support in various deployment scenarios while using Azure Site Recovery. This support is applicable for any workload running on the mentioned OS.

 **VMware/physical server** | **Hyper-V (no Virtual Machine Manager)** | **Hyper-V (with Virtual Machine Manager)**
--- | --- | ---
64-bit Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 with at least SP1<br/><br/> Red Hat Enterprise Linux 6.7, 6.8, 7.1, 7.2 <br/><br/> CentOS 6.5, 6.6, 6.7, 6.8, 7.0, 7.1, 7.2 <br/><br/> Oracle Enterprise Linux 6.4, 6.5 running either the Red Hat compatible kernel or Unbreakable Enterprise Kernel Release 3 (UEK3) <br/><br/> SUSE Linux Enterprise Server 11 SP3 | Any guest OS [supported by Azure](https://technet.microsoft.com/library/cc794868.aspx) | Any guest OS [supported by Azure](https://technet.microsoft.com/library/cc794868.aspx)


>[!Note]
>Storage support for Linux versions
>file system (EXT3, ETX4, ReiserFS, XFS),
>Multipath software-Device Mapper,
>Volume manager (LVM2), and
>physical servers with HP CCISS controller storage are *not* supported.
>The ReiserFS file system is supported only on SUSE Linux Enterprise Server 11 SP3.

## Support for network configuration
The following tables summarize network configuration support in various deployment scenarios that use Azure Site Recovery to replicate to Azure.

### Host network configuration

**Configuration** | **VMware/physical server** | **Hyper-V (no Virtual Machine Manager)** | **Hyper-V (with Virtual Machine Manager)**
--- | --- | --- | ---
NIC teaming | Yes<br/><br/>Not supported in physical machines| Yes | Yes
VLAN | Yes | Yes | Yes
IPv4 | Yes | Yes | Yes
IPv6 | No | No | No

### Guest VM network configuration

**Configuration** | **VMware/physical server** | **Hyper-V (no Virtual Machine Manager)** | **Hyper-V (with Virtual Machine Manager)**
--- | --- | --- | ---
NIC teaming | No | No | No
IPv4 | Yes | Yes | Yes
IPv6 | No | No | No
Static IP (Windows) | Yes | Yes | Yes
Static IP (Linux) | No | No | No
Multi-NIC | Yes | Yes | Yes

### Failed-over Azure VM network configuration

**Azure networking** | **VMware/physical server** | **Hyper-V (no Virtual Machine Manager)** | **Hyper-V (with Virtual Machine Manager)**
--- | --- | --- | ---
Express Route | Yes | Yes | Yes
ILB | Yes | Yes | Yes
ELB | Yes | Yes | Yes
Traffic Manager | Yes | Yes | Yes
Multi-NIC | Yes | Yes | Yes
Reserved IP | Yes | Yes | Yes
IPv4 | Yes | Yes | Yes
Retain source IP | Yes | Yes | Yes


## Support for storage
The following tables summarize storage configuration support in various deployment scenarios that use Azure Site Recovery to replicate to Azure.

### Host storage configuration

**Configuration** | **VMware/physical server** | **Hyper-V (no Virtual Machine Manager)** | **Hyper-V (with Virtual Machine Manager)**
--- | --- | --- | ---
NFS | Yes for VMware<br/><br/> No for physical servers | N/A | N/A
SMB 3.0 | N/A | Yes | Yes
SAN (ISCSI) | Yes | Yes | Yes
Multi-path (MPIO)<br></br>Tested with: Microsoft DSM, EMC PowerPath 5.7 SP4, EMC PowerPath DSM for CLARiiON | Yes | Yes | Yes

### Guest or physical server storage configuration

**Configuration** | **VMware/physical server** | **Hyper-V (no Virtual Machine Manager)** | **Hyper-V (with Virtual Machine Manager)**
--- | --- | --- | ---
VMDK | Yes | N/A | N/A
VHD/VHDX | N/A | Yes | Yes
Gen 2 VM | N/A | Yes | Yes
EFI/UEFI| No | Yes | Yes
Shared cluster disk | Yes for VMware<br/><br/> N/A for physical servers | No | No
Encrypted disk | No | No | No
NFS | No | N/A | N/A
SMB 3.0 | No | No | No
RDM | Yes<br/><br/> N/A for physical servers | N/A | N/A
Disk > 1 TB | No | No | No
Volume with striped disk > 1 TB<br/><br/> LVM-Logical Volume Management | Yes | Yes | Yes
Storage Spaces | No | Yes | Yes
Hot add/remove disk | No | No | No
Exclude disk | Yes | Yes | Yes
Multi-path (MPIO) | N/A | Yes | Yes

**Azure storage** | **VMware/physical server** | **Hyper-V (no Virtual Machine Manager)** | **Hyper-V (with Virtual Machine Manager)**
--- | --- | --- | ---
LRS | Yes | Yes | Yes
GRS | Yes | Yes | Yes
Cool storage | No | No | No
Hot storage| No | No | No
Encryption at rest(SSE)| Yes | Yes | Yes
Premium storage | Yes | No | No
Import/export service | No | No | No


## Support for Azure compute configuration

**Compute feature** | **VMware/physical server** | **Hyper-V (no Virtual Machine Manager)** | **Hyper-V (with Virtual Machine Manager)**
--- | --- | --- | ---
Availability sets | No | No | No
HUB | Yes | Yes | Yes

## Failed-over Azure VM requirements

You can deploy Site Recovery to replicate virtual machines and physical servers running any operating system supported by Azure. This includes most versions of Windows and Linux. On-premises VMs that you want to replicate must conform with the following Azure requirements while replicating to Azure.

**Entity** | **Requirements** | **Details**
--- | --- | ---
**Guest operating system** | For Hyper-V to Azure replication, Site Recovery supports all operating systems that are [supported by Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx). <br/><br/> For VMware and physical server replication, check the Windows and Linux [prerequisites](site-recovery-vmware-to-azure-classic.md#before-you-start-deployment). | The prerequisites check will fail if unsupported.
**Guest operating system architecture** | 64-bit | The prerequisites check will fail if unsupported.
**Operating system disk size** | Up to 1023 GB | The prerequisites check will fail if unsupported.
**Operating system disk count** | 1 | The prerequisites check will fail if unsupported.
**Data disk count** | 16 or fewer (Maximum value is a function of the size of the virtual machine being created. 16 = XL.) | The prerequisites check will fail if unsupported.
**Data disk VHD size** | Up to 1023 GB | The prerequisites check will fail if unsupported.
**Network adapters** | Multiple adapters are supported. |
**Shared VHD** | Not supported | The prerequisites check will fail if unsupported.
**FC disk** | Not supported | The prerequisites check will fail if unsupported.
**Hard disk format** | VHD <br/><br/> VHDX | Although VHDX isn't currently supported in Azure, Site Recovery automatically converts VHDX to VHD when you failover to Azure. When you failback to on-premises, the virtual machines continue to use the VHDX format.
**Bitlocker** | Not supported | Bitlocker must be disabled before protecting a virtual machine.
**VM name** | Between 1 and 63 characters. Restricted to letters, numbers, and hyphens. The VM name must start and end with a letter or number. | Update the value in the virtual machine properties in Site Recovery.
**VM type** | Generation 1<br/><br/> Generation 2 -- Windows | Generation 2 VMs with an OS disk type of basic (which includes one or two data volumes formatted as VHDX) and less than 300 GB of disk space are supported.<br></br>Linux Generation 2 VMs aren't supported. [Learn more](https://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/)|

## Support for Recovery Services vault actions

**Action** | **VMware/physical server** | **Hyper-V (no Virtual Machine Manager)** | **Hyper-V (with Virtual Machine Manager)**
--- | --- | --- | ---
Move vault across resource groups<br/><br/> Within and across subscriptions | No | No | No
Move storage, network, Azure VMs across resource groups<br/><br/> Within and across subscriptions | No | No | No


## Support for Provider and Agent

**Name** | **Description** | **Latest version** | **Details**
--- | --- | --- | --- | ---
**Azure Site Recovery Provider** | Coordinates communications between on-premises servers and Azure <br/><br/> Installed on on-premises Virtual Machine Manager servers, or on Hyper-V servers if there's no Virtual Machine Manager server | 5.1.19 ([available from portal](http://aka.ms/downloaddra)) | [Latest features and fixes](https://support.microsoft.com/kb/3155002)
**Azure Site Recovery Unified Setup (VMware to Azure)** | Coordinates communications between on-premises VMware servers and Azure <br/><br/> Installed on on-premises VMware servers | 9.3.4246.1 (available from portal) | [Latest features and fixes](https://support.microsoft.com/kb/3155002)
**Mobility service** | Coordinates replication between on-premises VMware servers/physical servers and Azure/secondary site<br/><br/> Installed on VMware VM or physical servers you want to replicate  | N/A (available from portal) | N/A
**Microsoft Azure Recovery Services (MARS) agent** | Coordinates replication between Hyper-V VMs and Azure<br/><br/> Installed on on-premises Hyper-V servers (with or without a Virtual Machine Manager server) | Latest agent ([available from portal](http://aka.ms/latestmarsagent)) |






## Next steps
[Prepare for deployment](site-recovery-best-practices.md)
