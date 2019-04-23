---
title: Aktualisieren Ihre Remote Desktop Services-Bereitstellungen auf Windows Server 2016
description: Dieser Artikel beschreibt, wie Sie Ihre vorhandenen Remote Desktop Services-Bereitstellungen auf Windows Server 2016 aktualisieren.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: spatnaik
ms.date: 03/20/2018
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f7b1f1f6-57c8-40ab-a235-e36240dcc1f8
author: spatnaik
manager: scottman
notes: https://social.technet.microsoft.com/wiki/contents/articles/22069.remote-desktop-services-upgrade-guidelines-for-windows-server-2012-r2.aspx
ms.openlocfilehash: f683a7d9346494e7f1fb6faf716ca9c90cfef8d3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875751"
---
# <a name="upgrading-your-remote-desktop-services-deployments-to-windows-server-2016"></a>Aktualisieren Ihre Remote Desktop Services-Bereitstellungen auf Windows Server 2016

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

## <a name="supported-os-upgrades-with-rds-role-installed"></a>Unterstützt Upgrades des Betriebssystems mit Remotedesktopdienste-Rolle installiert
Upgrades auf Windows Server 2016 werden nur von Windows Server 2012 R2 und Windows Server 2016 unterstützt.

## <a name="flow-for-deployment-upgrades"></a>Der Ablauf für die Bereitstellung upgrades
Um die Ausfallzeit auf ein Minimum zu halten, empfiehlt es sich um die folgenden Schritte ausführen:

1. **RD-Verbindungsbrokerserver** muss die erste aktualisiert werden. Wenn in der Bereitstellung aktiv/aktiv-Konfiguration vorhanden ist, entfernen Sie alle bis auf einen Server aus der Bereitstellung, und führen Sie ein direktes Upgrade. Führen Sie Upgrades für die übrigen RD Connection Broker Server offline, und klicken Sie dann erneut auf die Bereitstellung hinzufügen. Die Bereitstellung wird während des Upgrades von RD Connection Broker Server nicht verfügbar sein.

   > [!NOTE] 
   > Es ist erforderlich, um RD Connection Broker Server zu aktualisieren. Windows Server 2012 R2 RD Connection Broker Server unterstützt in einer gemischten Bereitstellung mit Windows Server 2016-Servern nicht. Sobald die RD Connection Broker Server Windows Server 2016 ausgeführt werden wird die Bereitstellung funktionsfähig ist, auch wenn die übrigen Server in der Bereitstellung mehr Windows Server 2012 R2 ausgeführt werden.

2. **Remotedesktop-Lizenzserver** muss aktualisiert werden, vor dem upgrade von Remotedesktop-Sitzungshostserver.
   > [!NOTE] 
   > Windows Server 2012 und 2012 R2-Remotedesktop-Lizenzserver mit der Windows Server 2016-Bereitstellung funktioniert, aber sie können nur Clientzugriffslizenzen, die von Windows Server 2012 R2 und älteren verarbeiten. Sie können keine Clientzugriffslizenzen für Windows Server 2016. Finden Sie unter [lizenzieren Sie Ihre RDS-Bereitstellung mit Clientzugriffslizenzen (CALs)](rds-client-access-license.md) für Weitere Informationen zum Remotedesktop-Lizenzserver.

3. **RD-Sitzungshostservern** anschließend aktualisiert werden können. Der Administrator kann die Server in 2 Schritten wie nachstehend beschrieben aktualisiert werden aufteilen, um Ausfallzeiten während des Upgrades zu vermeiden. Alle werden funktionalen nach dem Upgrade. Um zu aktualisieren, verwenden Sie die Schritte in [Upgrade Remote Desktop Session Host-Server auf Windows Server 2016](upgrade-to-rdsh.md).

4. **Remotedesktop-Virtualisierungshostserver** anschließend aktualisiert werden können. Um zu aktualisieren, verwenden Sie die Schritte in [Aktualisieren von Remotedesktop-Virtualisierungshost-Server auf Windows Server 2016](upgrade-to-rdvh.md).

5. **Server mit Web Access für Remotedesktop** können jederzeit aktualisiert werden.
   > [!NOTE]
   > Aktualisieren von RD-Web kann IIS-Eigenschaften (z. B. alle Konfigurationsdateien) zurückgesetzt. Um die nicht der Fall ist, stellen Sie Hinweise oder Kopien von Anpassungen, die an den RD-Web-Website in IIS ausgeführt.

   > [!NOTE] 
   > Windows Server 2012 und 2012 R2 Web Access für Remotedesktop-Server funktionieren mit Windows Server 2016-Bereitstellungen.

6. **Remotedesktop-Gatewayservern** können jederzeit aktualisiert werden.
   > [!NOTE]
   > Windows Server 2016 enthält keine-Richtlinien (Network Access Protection, NAP) - müssen entfernt werden soll. So entfernen Sie die richtigen Richtlinien die einfachste Möglichkeit ist durch den Upgrade-Assistenten ausführen. Wenn es alle NAP-Richtlinien, die Sie löschen müssen sind, das Upgrade blockiert und erstellen eine Textdatei auf dem Desktop, der die spezifischen Richtlinien enthält. Um NAP-Richtlinien zu verwalten, öffnen Sie die Netzwerkrichtlinienserver-Tool. Nach dem Löschen, klicken Sie auf **aktualisieren** im Setup-Tool, um den Upgradevorgang fortzusetzen. 

   > [!NOTE] 
   > Windows Server 2012 und 2012 R2 Remotedesktop-Gatewayservern funktionieren mit Windows Server 2016-Bereitstellungen.

## <a name="vdi-deployment--supported-guest-os-upgrade"></a>VDI-Bereitstellung – unterstützten Gastbetriebssystem-Upgrades
Administratoren müssen die folgenden Optionen zum Aktualisieren der VM-Sammlungen:

### <a name="upgrade-managed-shared-vm-collections"></a>Aktualisieren von verwalteten freigegebenen VM-Sammlungen 
Administratoren müssen zum Erstellen von VM-Vorlagen mit der gewünschten Betriebssystemversion aus, und verwenden, um alle virtuellen Computer im Pool zu patchen. 

Wir unterstützen die folgenden Patchen Szenarien:
- Windows 7 SP1 kann gepatcht werden, um Windows 8 oder Windows 8.1
- Windows 8 kann gepatcht werden, um Windows 8.1
- Windows 8.1 kann gepatcht werden, auf Windows 10

### <a name="upgrade-unmanaged-shared-vm-collections"></a>Upgrade von nicht verwalteten freigegebenen VM-Auflistungen 
Endbenutzer können nicht ihre persönliche Desktops aktualisieren. Administratoren sollten das Upgrade ausführen. Die genauen Schritte sind immer noch bestimmt werden soll.