---
title: Bereitstellen des Host-Überwachungs Diensts
ms.topic: article
ms.assetid: 310b63d9-5ac7-4961-98ef-103af45d706a
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 01/14/2020
ms.openlocfilehash: e8077655717db3f6700b0e0a3d12792465b41299
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939771"
---
# <a name="deploying-the-host-guardian-service"></a>Bereitstellen des Host-Überwachungs Diensts

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Eines der wichtigsten Ziele bei der Bereitstellung einer gehosteten Umgebung besteht darin, die Sicherheit der virtuellen Computer zu gewährleisten, die in der Umgebung ausgeführt werden. Als Cloud-Dienstanbieter oder privater Cloud-Administrator im Unternehmen können Sie ein geschütztes Fabric verwenden, um eine sicherere Umgebung für VMs bereitzustellen. Ein geschütztes Fabric besteht aus einem Host Guardian Service (Host-Überwachungsdienst) – in der Regel ein Cluster mit drei Knoten – sowie einem oder mehreren geschützten Hosts und einer Reihe von abgeschirmten virtuellen Computern (VMs).

## <a name="video-deploying-a-guarded-fabric"></a>Video: Bereitstellen eines geschützten Fabrics

> [!VIDEO https://www.microsoft.com/videoplayer/embed/dcd8e99f-36f1-4bc8-b3d2-9576da38d9f1?autoplay=false]

## <a name="deployment-tasks-for-guarded-fabrics-and-shielded-vms"></a>Bereitstellungs Aufgaben für geschützte Fabrics und abgeschirmte VMS

In der folgenden Tabelle werden die Aufgaben zum Bereitstellen eines geschützten Fabrics und zum Erstellen von abgeschirmten VMS entsprechend den verschiedenen Administrator Rollen aufgegliedert. Beachten Sie Folgendes: Wenn der HGS-Administrator HGS mit autorisierten Hyper-V-Hosts konfiguriert, sammelt ein Fabric-Administrator Informationen zu den Hosts gleichzeitig und stellt diese bereit.

| Schritt und Verknüpfung mit Inhalt | Image |
|--|--|--|
| 1: [Überprüfen der HGS-Voraussetzungen](guarded-fabric-prepare-for-hgs.md) | ![Schritt 1: Überprüfen der Voraussetzungen](../media/Guarded-Fabric-Shielded-VM/guarded-host-verify.png) |
| 2. [Konfigurieren des ersten HGS-Knotens](guarded-fabric-choose-where-to-install-hgs.md) | ![Schritt 2: Konfigurieren des ersten HGS-Knotens](../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-first-hgs-node.png) |
| 3: [Konfigurieren zusätzlicher HGS-Knoten](guarded-fabric-configure-additional-hgs-nodes.md) | ![Schritt 3: Konfigurieren zusätzlicher HGS-Knoten](../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-secondary-hgs-nodes.png) |
| 4: [Konfigurieren von Fabric-DNS](guarded-fabric-configuring-fabric-dns.md) | ![Schritt 4: Konfigurieren von Fabric-DNS](../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-fabric-dns.png) |
| 5: [Überprüfen der Host Voraussetzungen (Schlüssel)](guarded-fabric-guarded-host-prerequisites.md#host-key-attestation) und [Überprüfen der Host Voraussetzungen (TPM)](guarded-fabric-guarded-host-prerequisites.md#tpm-trusted-attestation) | ![Schritt 5: Überprüfen des erforderlichen Host Schlüssels und des Host Voraussetzungen für das TPM](../media/Guarded-Fabric-Shielded-VM/guarded-host-verify.png) |
| 6: [Erstellen eines Host Schlüssels (Schlüssel)](guarded-fabric-create-host-key.md) und[Sammeln von Hostinformationen (TPM)](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md) | ![Schritt 6: Erstellen eines Host Schlüssels und Sammeln von Hostinformationen](../media/Guarded-Fabric-Shielded-VM/guarded-host-collect-info-from-hosts.png) |
| 7: [Konfigurieren von HGS mit Hostinformationen](guarded-fabric-add-host-information-to-hgs.md) | ![Schritt 7: Hinzufügen von Hostinformationen zu HGS](../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-hgs-with-host-info.png) |
| 8- [bestätigen, dass Hosts bestätigen können](guarded-fabric-confirm-hosts-can-attest-successfully.md) | ![Schritt 8: bestätigen, dass der Host bestätigen kann](../media/Guarded-Fabric-Shielded-VM/guarded-host-confirm-hosts-attest.png) |
| 9: [Konfigurieren von VMM (optional)](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-overview) | ![Schritt 9: Konfigurieren von VMM (optional)](../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-vmm.png) |
| 10 [Erstellen von Vorlagen](guarded-fabric-create-a-shielded-vm-template.md) Datenträgern | ![Schritt 10: Erstellen von Vorlagen Datenträgern](../media/Guarded-Fabric-Shielded-VM/guarded-host-create-template-disk.png) |
| 11: Erstellen eines VM-schutzhilfsobjekts [für VMM (optional)](guarded-fabric-vm-shielding-helper-vhd.md) | ![Schritt 11: Erstellen eines VM-Schutz-Hilfe Datenträgers für VMM](../media/Guarded-Fabric-Shielded-VM/guarded-host-create-helper-disk.png) |
| 12: [Einrichten Windows Azure Pack (optional)](guarded-fabric-shielded-vm-windows-azure-pack.md) | ![Schritt 12: Einrichten Windows Azure Pack (optional)](../media/Guarded-Fabric-Shielded-VM/guarded-host-windows-azure-pack.png) |
| 13-geschützte [Datendatei erstellen](guarded-fabric-tenant-creates-shielding-data.md) | ![Schritt 13: Erstellen einer Schutz Datendatei](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-file.png) |
| 14. [Erstellen von abgeschirmten VMS mithilfe Windows Azure Pack](guarded-fabric-shielded-vm-windows-azure-pack.md) | ![Schritt 14: Erstellen von abgeschirmten VMS mithilfe Windows Azure Pack](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielded-vms.png) |
| 15. [Erstellen von abgeschirmten VMS mithilfe von VMM](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-vms) | ![Schritt 15: Erstellen von abgeschirmten VMS mithilfe von VMM](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielded-vms.png) |

## <a name="additional-references"></a>Weitere Verweise

- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
