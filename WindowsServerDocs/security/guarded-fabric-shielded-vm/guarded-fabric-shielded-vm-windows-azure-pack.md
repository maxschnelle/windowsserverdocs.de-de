---
title: 'Abgeschirmte VMs für Mandanten: Bereitstellen einer abgeschirmten VM mithilfe von Windows Azure Pack'
ms.topic: article
ms.assetid: 095315e4-c4a7-4b80-91d8-528119b62c4c
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 613082bcc5cfefa0c7abb0011762c3d283ea98aa
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87989989"
---
# <a name="shielded-vms--for-tenants---deploying-a-shielded-vm-by-using-windows-azure-pack"></a>Abgeschirmte VMs für Mandanten: Bereitstellen einer abgeschirmten VM mithilfe von Windows Azure Pack

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Wenn Ihr hostingdienstanbieter dies unterstützt, können Sie Windows Azure Pack verwenden, um eine abgeschirmte VM bereitzustellen.

Führen Sie die folgenden Schritte aus:

1. Abonnieren Sie mindestens einen Plan, der in Windows Azure Pack angeboten wird.

2. Erstellen Sie mithilfe Windows Azure Pack eine abgeschirmte VM.

    [Verwenden Sie abgeschirmte virtuelle](/previous-versions/azure/windows-server-azure-pack/mt720674(v=technet.10))Computer, die in den folgenden Themen beschrieben werden:

   - [Erstellen](/previous-versions/azure/windows-server-azure-pack/mt720672(v=technet.10)) Sie Schutz Daten (und laden Sie die geschützte Datendatei hoch, wie im zweiten Verfahren im Thema beschrieben).

     > [!NOTE]
     > Als Teil der Erstellung von Schutz Daten laden Sie die Datei mit dem Überwachungs Schlüssel herunter. dabei handelt es sich um eine XML-Datei im UTF-8-Format. Ändern Sie die Datei nicht in UTF-16.

   - [Erstellen Sie einen abgeschirmten virtuellen Computer](/previous-versions/azure/windows-server-azure-pack/mt720673(v=technet.10)) mit **schneller**Fassung, über eine geschützte Vorlage oder über eine reguläre Vorlage.

       > [!WARNING]
       > Wenn Sie [einen abgeschirmten virtuellen Computer mithilfe einer regulären Vorlage erstellen](/previous-versions/azure/windows-server-azure-pack/mt720673(v=technet.10)#Anchor_2), ist es wichtig zu beachten, dass der virtuelle Computer *nicht geschützt bereitgestellt wird.* Dies bedeutet, dass der Vorlagen Datenträger nicht anhand der Liste der vertrauenswürdigen Datenträger in der geschützten Datendatei überprüft wird, und dass es sich nicht um die geheimen Daten in der Schutz Datendatei handelt Wenn eine geschützte Vorlage verfügbar ist, empfiehlt es sich, einen abgeschirmten virtuellen Computer mit einer abgeschirmten Vorlage bereitzustellen, um den End-to-End-Schutz ihrer geheimen Schlüssel zu gewährleisten.

   - [Konvertieren einer virtuellen Maschine der Generation 2 in eine abgeschirmte virtuelle Maschine](/previous-versions/azure/windows-server-azure-pack/mt720670(v=technet.10))

       > [!NOTE]
       > Wenn Sie eine virtuelle Maschine in einen abgeschirmten virtuellen Computer konvertieren, werden vorhandene Prüfpunkte und Sicherungen nicht verschlüsselt. Wenn möglich, sollten Sie alte Prüfpunkte löschen, um den Zugriff auf Ihre alten, entschlüsselten Daten zu verhindern.

## <a name="additional-references"></a>Weitere Verweise

- [Geschützte Hosts und abgeschirmte VMs: Konfigurationsschritte für Hosting-Anbieter](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)