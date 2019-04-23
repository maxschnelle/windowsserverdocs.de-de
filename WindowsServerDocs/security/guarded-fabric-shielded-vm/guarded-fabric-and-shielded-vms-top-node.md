---
title: Geschütztes Fabric und abgeschirmte VMs
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 5c7ada81-2d97-41d4-87cf-1a7ccf06cd20
manager: dongill
author: rpsqrd
ms.author: justinha
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: c2c16574439569eeb1181977f23bae238f43865c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857431"
---
# <a name="guarded-fabric-and-shielded-vms"></a>Geschütztes Fabric und abgeschirmte VMs

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Eines der wichtigsten Ziele für die Bereitstellung einer gehosteten Umgebung werden gewährleisten die Sicherheit der virtuellen Computer in der Umgebung ausgeführt. Als Cloud-Dienstanbieter oder privater Cloud-Administrator in Unternehmen können Sie eine geschützte Fabric verwenden, um eine sicherere Umgebung für VMs bereitzustellen. Ein geschütztes Fabric besteht aus einem Host Guardian Service (Host-Überwachungsdienst) – in der Regel ein Cluster mit drei Knoten – sowie einem oder mehreren geschützten Hosts und einer Reihe von abgeschirmten virtuellen Computern (VMs).

> [!IMPORTANT]
> Stellen Sie sicher, dass Sie das neueste kumulative Update installiert haben, bevor Sie die geschützten virtuellen Maschinen in der Produktion bereitstellen.

## <a name="videos-blog-and-overview-topic-about-guarded-fabrics-and-shielded-vms"></a>Videos, Blogs und Übersichtsthema zu überwachten Fabrics und abgeschirmte VMs

- Video: [Schützen Sie Ihr virtualisierungsfabric vor Bedrohungen von innen mit Windows Server-2019](https://myignite.techcommunity.microsoft.com/sessions/64690)
- Video: [Einführung in abgeschirmte VMs unter WindowsServer 2016](https://channel9.msdn.com/Shows/Mechanics/Introduction-to-Shielded-Virtual-Machines-in-Windows-Server-2016)
- Video: [Einführung in abgeschirmte VMs mit Windows Server 2016 Hyper-V](https://channel9.msdn.com/events/Ignite/2016/BRK3124)
- Video: [Bereitstellen abgeschirmter VMs sowie eines geschützten Fabrics mit WindowsServer 2016](https://mva.microsoft.com/en-US/training-courses/deploying-shielded-vms-and-a-guarded-fabric-with-windows-server-2016-17131?l=WFLef7vUD_4604300474)
- Blog: [Datacenter and Private Cloud Security-Blog](https://blogs.technet.microsoft.com/datacentersecurity/)
- Übersicht: [Geschütztes Fabric und abgeschirmte VMs-Übersicht](Guarded-Fabric-and-Shielded-VMs.md)

## <a name="planning-topics"></a>Themen zur Planung

- [Leitfaden zur kapazitätsplanung für Hoster](guarded-fabric-planning-for-hosters.md)
- [Leitfaden zur kapazitätsplanung für Mandanten](guarded-fabric-shielded-vm-planning-for-tenants.md)

## <a name="deployment-topics"></a>Themen zur Bereitstellung

- [Handbuch für die Bereitstellung](guarded-fabric-deploying-hgs-overview.md)
    - [Schnellstart](guarded-fabric-deployment-overview.md)
    - [Bereitstellen des Host-Überwachungsdienst](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)
    - [Bereitstellen überwachter hosts](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)
        - [Konfigurieren des Fabrics-DNS für Hosts, die überwachten Hosts werden](guarded-fabric-configuring-fabric-dns.md)
        - [Bereitstellen von überwachten Host mithilfe von AD-Modus](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)
        - [Bereitstellen Sie einen überwachten Host mit dem TPM-Modus](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)
        - [Vergewissern Sie sich, überwachte Hosts nachweisen können](guarded-fabric-confirm-hosts-can-attest-successfully.md)
        - [Abgeschirmte VMs: stellt die Hosting-Anbieter überwachten Hosts in VMM](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-hosts)
    - [Bereitstellen von abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
        - [Erstellen einer abgeschirmten VM-Vorlage](guarded-fabric-create-a-shielded-vm-template.md)
        - [Vorbereiten einer VM-Schutz Hilfsprogramms-VHD](guarded-fabric-vm-shielding-helper-vhd.md)
        - [Richten Sie Windows Azure Pack](guarded-fabric-hoster-sets-up-windows-azure-pack.md)
        - [Erstellen Sie eine geschützte Datendatei](guarded-fabric-tenant-creates-shielding-data.md)
        - [Bereitstellen einer abgeschirmten VM mithilfe von Windows Azure Pack](guarded-fabric-shielded-vm-windows-azure-pack.md)
        - [Bereitstellen einer abgeschirmten VM mithilfe von Virtual Machine Manager](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)

## <a name="operations-and-management-topic"></a>Vorgänge und -verwaltungsthema

- [Verwalten von Host-Überwachungsdienst](guarded-fabric-manage-hgs.md)
