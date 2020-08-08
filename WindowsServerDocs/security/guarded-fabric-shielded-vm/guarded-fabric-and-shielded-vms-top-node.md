---
title: Geschütztes Fabric und abgeschirmte VMs
ms.topic: article
ms.assetid: 5c7ada81-2d97-41d4-87cf-1a7ccf06cd20
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: c3f17320432d44a84be05040e23e7af30995c969
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997561"
---
# <a name="guarded-fabric-and-shielded-vms"></a>Geschütztes Fabric und abgeschirmte VMs

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Eines der wichtigsten Ziele bei der Bereitstellung einer gehosteten Umgebung besteht darin, die Sicherheit der virtuellen Computer zu gewährleisten, die in der Umgebung ausgeführt werden. Als Cloud-Dienstanbieter oder privater Cloud-Administrator im Unternehmen können Sie ein geschütztes Fabric verwenden, um eine sicherere Umgebung für VMs bereitzustellen. Ein geschütztes Fabric besteht aus einem Host Guardian Service (Host-Überwachungsdienst) – in der Regel ein Cluster mit drei Knoten – sowie einem oder mehreren geschützten Hosts und einer Reihe von abgeschirmten virtuellen Computern (VMs).

> [!IMPORTANT]
> Stellen Sie sicher, dass Sie das neueste kumulative Update installiert haben, bevor Sie geschützte virtuelle Computer in der Produktion bereitstellen.

## <a name="videos-blog-and-overview-topic-about-guarded-fabrics-and-shielded-vms"></a>Videos, Blog und Übersichts Thema zu geschützten Fabrics und abgeschirmten VMS

- Video: [Schützen Ihres virtualisierungsfabrics vor Insider Bedrohungen mit Windows Server 2019](https://myignite.techcommunity.microsoft.com/sessions/64690)
- Video: [Einführung in abgeschirmte Virtual Machines in Windows Server 2016](https://channel9.msdn.com/Shows/Mechanics/Introduction-to-Shielded-Virtual-Machines-in-Windows-Server-2016)
- Video: [Einblicke in abgeschirmte VMS mit Windows Server 2016 Hyper-V](https://channel9.msdn.com/events/Ignite/2016/BRK3124)
- Video: bereitstellen [von abgeschirmten VMS und einem geschützten Fabric mit Windows Server 2016](https://mva.microsoft.com/training-courses/deploying-shielded-vms-and-a-guarded-fabric-with-windows-server-2016-17131?l=WFLef7vUD_4604300474)
- Blog: [Daten Center-und Private Cloud-Sicherheitsblog](/archive/blogs/datacentersecurity/)
- Übersicht: [Übersicht über geschützte Fabric-und abgeschirmte VMS](Guarded-Fabric-and-Shielded-VMs.md)

## <a name="planning-topics"></a>Themen zur Planung

- [Planungs Handbuch für Hoster](guarded-fabric-planning-for-hosters.md)
- [Planungs Handbuch für Mandanten](guarded-fabric-shielded-vm-planning-for-tenants.md)

## <a name="deployment-topics"></a>Themen zur Bereitstellung

- [Bereitstellungs Handbuch](guarded-fabric-deploying-hgs-overview.md)
    - [Schnellstart](guarded-fabric-deployment-overview.md)
    - [Bereitstellen von HGS](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)
    - [Bereitstellen überwachter Hosts](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)
        - [Konfigurieren des Fabric-DNS für Hosts, die als geschützte Hosts verwendet werden sollen](guarded-fabric-configuring-fabric-dns.md)
        - [Bereitstellen eines überwachten Hosts im AD-Modus](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)
        - [Bereitstellen eines überwachten Hosts mit dem TPM-Modus](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)
        - [Bestätigen, dass geschützte Hosts bestätigen können](guarded-fabric-confirm-hosts-can-attest-successfully.md)
        - [Abgeschirmte VMs: Hosting-Anbieter stellt geschützte Hosts in VMM bereit](/system-center/vmm/guarded-deploy-host?view=sc-vmm-2019)
    - [Bereitstellen von abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
        - [Erstellen einer Vorlage für eine abgeschirmte VM](guarded-fabric-create-a-shielded-vm-template.md)
        - [Vorbereiten einer VHD für ein VM-Schutz Hilfsprogramm](guarded-fabric-vm-shielding-helper-vhd.md)
        - [Einrichten des Windows Azure Packs](guarded-fabric-hoster-sets-up-windows-azure-pack.md)
        - [Erstellen einer Schutz Datendatei](guarded-fabric-tenant-creates-shielding-data.md)
        - [Bereitstellen einer abgeschirmten VM mithilfe Windows Azure Pack](guarded-fabric-shielded-vm-windows-azure-pack.md)
        - [Bereitstellen einer abgeschirmten VM mithilfe Virtual Machine Manager](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)

## <a name="operations-and-management-topic"></a>Themen zur Betriebs-und Verwaltungsaufgaben

- [Verwalten des Host-Überwachungs Diensts](guarded-fabric-manage-hgs.md)