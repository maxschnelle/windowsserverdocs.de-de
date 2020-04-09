---
title: Geschütztes Fabric und abgeschirmte VMs
ms.prod: windows-server
ms.topic: article
ms.assetid: 5c7ada81-2d97-41d4-87cf-1a7ccf06cd20
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 9e76b3081438ae38c6b83b7cdd179d47b1e21a70
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856913"
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
- Blog: [Daten Center-und Private Cloud-Sicherheitsblog](https://blogs.technet.microsoft.com/datacentersecurity/)
- Übersicht: [Übersicht über geschützte Fabric-und abgeschirmte VMS](Guarded-Fabric-and-Shielded-VMs.md)

## <a name="planning-topics"></a>Themen zur Planung

- [Planungs Handbuch für Hoster](guarded-fabric-planning-for-hosters.md)
- [Planungs Handbuch für Mandanten](guarded-fabric-shielded-vm-planning-for-tenants.md)

## <a name="deployment-topics"></a>Themen zur Bereitstellung

- [Bereitstellungs Handbuch](guarded-fabric-deploying-hgs-overview.md)
    - [Schnellstart](guarded-fabric-deployment-overview.md)
    - [Bereitstellen von HGS](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)
    - [Bereitstellen geschützter Hosts](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)
        - [Konfigurieren des Fabric-DNS für Hosts, die zu überwachten Hosts werden](guarded-fabric-configuring-fabric-dns.md)
        - [Bereitstellen eines überwachten Hosts im AD-Modus](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)
        - [Bereitstellen eines überwachten Hosts mit dem TPM-Modus](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)
        - [Bestätigen, dass geschützte Hosts bestätigen können](guarded-fabric-confirm-hosts-can-attest-successfully.md)
        - [Abgeschirmte VMS: der hostingdienstanbieter stellt überwachte Hosts in VMM bereit.](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-hosts)
    - [Bereitstellen von abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
        - [Erstellen einer abgeschirmten VM-Vorlage](guarded-fabric-create-a-shielded-vm-template.md)
        - [Vorbereiten einer VHD für ein VM-Schutz Hilfsprogramm](guarded-fabric-vm-shielding-helper-vhd.md)
        - [Einrichten des Windows Azure Packs](guarded-fabric-hoster-sets-up-windows-azure-pack.md)
        - [Erstellen einer Schutz Datendatei](guarded-fabric-tenant-creates-shielding-data.md)
        - [Bereitstellen einer abgeschirmten VM mithilfe Windows Azure Pack](guarded-fabric-shielded-vm-windows-azure-pack.md)
        - [Bereitstellen einer abgeschirmten VM mithilfe Virtual Machine Manager](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)

## <a name="operations-and-management-topic"></a>Themen zur Betriebs-und Verwaltungsaufgaben

- [Verwalten des Host-Überwachungs Diensts](guarded-fabric-manage-hgs.md)
