---
title: Bereitstellen des Host-Überwachungs Diensts
ms.prod: windows-server
ms.topic: article
ms.assetid: 310b63d9-5ac7-4961-98ef-103af45d706a
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 01/14/2020
ms.openlocfilehash: 9244dd8c9a567813c5732571de5dddc42d23be2a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475587"
---
# <a name="deploying-the-host-guardian-service"></a>Bereitstellen des Host-Überwachungs Diensts

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Eines der wichtigsten Ziele bei der Bereitstellung einer gehosteten Umgebung besteht darin, die Sicherheit der virtuellen Computer zu gewährleisten, die in der Umgebung ausgeführt werden. Als Cloud-Dienstanbieter oder privater Cloud-Administrator im Unternehmen können Sie ein geschütztes Fabric verwenden, um eine sicherere Umgebung für VMs bereitzustellen. Ein geschütztes Fabric besteht aus einem Host Guardian Service (Host-Überwachungsdienst) – in der Regel ein Cluster mit drei Knoten – sowie einem oder mehreren geschützten Hosts und einer Reihe von abgeschirmten virtuellen Computern (VMs).

## <a name="video-deploying-a-guarded-fabric"></a>Video: Bereitstellen eines geschützten Fabrics

> [!VIDEO https://www.microsoft.com/videoplayer/embed/dcd8e99f-36f1-4bc8-b3d2-9576da38d9f1?autoplay=false]

## <a name="deployment-tasks-for-guarded-fabrics-and-shielded-vms"></a>Bereitstellungs Aufgaben für geschützte Fabrics und abgeschirmte VMS

In der folgenden Tabelle werden die Aufgaben zum Bereitstellen eines geschützten Fabrics und zum Erstellen von abgeschirmten VMS entsprechend den verschiedenen Administrator Rollen aufgegliedert. Beachten Sie Folgendes: Wenn der HGS-Administrator HGS mit autorisierten Hyper-V-Hosts konfiguriert, sammelt ein Fabric-Administrator Informationen zu den Hosts gleichzeitig und stellt diese bereit.

|<img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-hgs-administrator-tasks.png" alt="Host Guardian Service administrator tasks" width="238" height="62" align="left" /> | <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-fabric-administrator-tasks.png" alt="Fabric administrator tasks" width="300" height="62" align="left" /> | <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-tenant-administrator-tasks.png" alt="Tenant administrator tasks" width="184" height="66" align="left" /> |
|-------------------------------------|--------------------------------|-----------------------------------------|
|(1) [Überprüfen der HGS-Voraussetzungen](guarded-fabric-prepare-for-hgs.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-verify.png" alt="Step 1" hspace="8" align="right" />| | |
|(2) [Konfigurieren des ersten HGS- &nbsp; Knotens](guarded-fabric-choose-where-to-install-hgs.md)&nbsp;<img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-first-hgs-node.png" alt="Step 2" hspace="8" align="right" />| | |
|(3) [zusätzliche HGS- &nbsp; Knoten konfigurieren](guarded-fabric-configure-additional-hgs-nodes.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-secondary-hgs-nodes.png" alt="Step 3" hspace="8" align="right" />| | |
| &nbsp; |(4) [Konfigurieren des Fabric-DNS](guarded-fabric-configuring-fabric-dns.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-fabric-dns.png" alt="Step 4" hspace="8" align="right" />| |
| &nbsp; |(5) [Überprüfen der Host &nbsp; Voraussetzungen (Schlüssel)](guarded-fabric-guarded-host-prerequisites.md#host-key-attestation)<br>[Überprüfen der Host &nbsp; Voraussetzungen (TPM)](guarded-fabric-guarded-host-prerequisites.md#tpm-trusted-attestation)<img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-verify.png" alt="Step 5" hspace="8" align="right" />| |
|(7) [Konfigurieren von HGS mit Hostinformationen](guarded-fabric-add-host-information-to-hgs.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-hgs-with-host-info.png" alt="Step 7" hspace="8" align="right" />|(6) [Erstellen eines Host Schlüssels (Schlüssel)](guarded-fabric-create-host-key.md)<br>[Sammeln von Hostinformationen (TPM)](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-collect-info-from-hosts.png" alt="Step 6" hspace="8" align="right" />| |
| &nbsp; |(8) [bestätigen, dass Hosts bestätigen können](guarded-fabric-confirm-hosts-can-attest-successfully.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-confirm-hosts-attest.png" alt="Step 8" hspace="8" align="right" />| |
| &nbsp; |(9) [Konfigurieren von VMM (optional)](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-overview) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-vmm.png" alt="Step 9" hspace="8" align="right" />| |
| &nbsp; |(10) [Erstellen von Vorlagen](guarded-fabric-create-a-shielded-vm-template.md) Datenträgern <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-create-template-disk.png" alt="Step 10" hspace="8" align="right" />| |
| &nbsp; |(11) Erstellen eines VM-schutzhilfsobjekts [für VMM (optional)](guarded-fabric-vm-shielding-helper-vhd.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-create-helper-disk.png" alt="Step 11" hspace="8" align="right" />| |
| &nbsp; |(12) [Einrichten Windows Azure Pack (optional)](guarded-fabric-shielded-vm-windows-azure-pack.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-windows-azure-pack.png" alt="Step 12" hspace="8" align="right" />| |
| &nbsp; | &nbsp; |(13) Schutz [Datendatei erstellen](guarded-fabric-tenant-creates-shielding-data.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-file.png" alt="Step 13" hspace="8" align="right" />|
| &nbsp; | &nbsp; |(14) [Erstellen von abgeschirmten VMS mithilfe Windows Azure Pack](guarded-fabric-shielded-vm-windows-azure-pack.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-shielded-vms.png" alt="Step 14" hspace="8" align="right" /><br>[Erstellen von abgeschirmten VMS mithilfe von VMM](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-vms) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-shielded-vms.png" alt="Step 15" hspace="8" align="right" />|


## <a name="additional-references"></a>Zusätzliche Referenzen

- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
