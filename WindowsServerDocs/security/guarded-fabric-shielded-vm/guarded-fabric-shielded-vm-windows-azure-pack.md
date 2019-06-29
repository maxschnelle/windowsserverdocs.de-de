---
title: Abgeschirmte virtuelle Computer für Mandanten – Bereitstellen eines abgeschirmten virtuellen Computers mit Windows Azure Pack
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 095315e4-c4a7-4b80-91d8-528119b62c4c
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 4cb5ed3433e04b7a5fe7004e517eb4cc38c7eb53
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469662"
---
# <a name="shielded-vms--for-tenants---deploying-a-shielded-vm-by-using-windows-azure-pack"></a>Abgeschirmte virtuelle Computer für Mandanten – Bereitstellen eines abgeschirmten virtuellen Computers mit Windows Azure Pack

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2019, WindowsServer 2016

Wenn Ihre hosting-Anbieter unterstützt wird, können Sie Windows Azure Pack verwenden, zum Bereitstellen eines abgeschirmten virtuellen Computers.

Führen Sie die folgenden Schritte aus:

1. Abonnieren von einem oder mehreren Plänen, die in Windows Azure Pack angeboten.

2. Erstellen Sie eine abgeschirmte VM, indem Sie mit Windows Azure Pack.

    [Verwenden von geschützten virtuellen Maschinen](https://technet.microsoft.com/library/mt720674.aspx), die in den folgenden Themen beschrieben wird:

   - [Erstellen Sie Schutzdaten](https://technet.microsoft.com/library/mt720672.aspx) (und die geschützte Datendatei hochladen, wie im zweiten Verfahren im Thema beschrieben).
    
     > [!NOTE]
     > Im Rahmen der Erstellung von geschützten Daten werden Sie Ihre wächterschlüsseldatei herunterladen, die eine XML-Datei in UTF-8-Format. Ändern Sie die Datei nicht in UTF-16.
    
   - [Erstellen einer abgeschirmte VM](https://technet.microsoft.com/library/mt720673.aspx) – mit **Schnellerfassung**, einer geschützten Vorlage oder über eine reguläre Vorlage.
    
       > [!WARNING]
       > Wenn Sie [erstellen Sie eine geschützte virtuelle Maschine mit einer regulären Vorlage](https://technet.microsoft.com/library/mt720673.aspx#Anchor_2), es ist wichtig zu beachten, dass es sich bei der Bereitstellung der VM *bei nicht geschirmten*. Dies bedeutet, dass der vorlagendatenträger wird anhand der Liste der vertrauenswürdigen Datenträgers in der geschützten Datendatei nicht überprüft, und die geheimen Schlüssel in der geschützten Datendatei verwendet werden, sind um den virtuellen Computer bereitzustellen. Wenn eine geschützte Vorlage verfügbar ist, ist es vorzuziehen, zum Bereitstellen einer abgeschirmten VM mit einer geschützten Vorlage zum Schutz Ihrer Geheimnisse von End-to-End bereitstellen.
    
   - [Konvertieren Sie eine virtuelle Maschine der Generation 2 in eine geschützte virtuelle Maschine](https://technet.microsoft.com/library/mt720670.aspx)
    
       > [!NOTE]
       > Wenn Sie einen virtuellen Computer in eine geschützte virtuelle Maschine konvertieren, werden vorhandene Prüfpunkte und Sicherungen nicht verschlüsselt. Löschen Sie alte Prüfpunkte, sofern möglich, um den Zugriff auf Ihre alten, entschlüsselten die Daten zu verhindern.

## <a name="see-also"></a>Siehe auch

- [Hosten von Service Provider-Konfigurationsschritte für die überwachten Hosts und abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
