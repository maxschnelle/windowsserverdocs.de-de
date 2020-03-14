---
title: Upgrade Ihrer Remotedesktopdienste-Bereitstellungen auf Windows Server 2016
description: In diesem Artikel wird beschrieben, wie Sie Ihre vorhandenen Bereitstellungen der Remotedesktopdienste auf Windows Server 2016 aktualisieren.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 29648db89b61a9d22aad6d5aa814cfe7f425a970
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79323362"
---
# <a name="upgrading-your-remote-desktop-services-deployments-to-windows-server-2016"></a>Upgrade Ihrer Remotedesktopdienste-Bereitstellungen auf Windows Server 2016

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

## <a name="supported-os-upgrades-with-rds-role-installed"></a>Unterstützte Betriebssystemupgrades mit installierter RDS-Rolle
Upgrades auf Windows Server 2016 werden nur von Windows Server 2012 R2 und Windows Server 2016 unterstützt.

## <a name="flow-for-deployment-upgrades"></a>Ablauf für Upgrades von Bereitstellungen
Um die Ausfallzeit so kurz wie möglich zu halten, sollten Sie die unten beschriebenen Schritte ausführen:

1. Für **RD-Verbindungsbrokerserver** sollte zuerst ein Upgrade ausgeführt werden. Wenn in der Bereitstellung eine aktiv/aktiv-Konfiguration vorliegt, entfernen Sie alle Server bis auf einen aus der Bereitstellung, und führen Sie ein direktes Upgrade durch. Führen Sie Upgrades auf den verbleibenden RD-Verbindungsbrokerservern offline durch, und fügen Sie sie anschließend der Bereitstellung wieder hinzu. Die Bereitstellung ist während des Upgrades der RD-Verbindungsbrokerserver nicht verfügbar.

   > [!NOTE] 
   > Es ist erforderlich, ein Upgrade der RD-Verbindungsbrokerserver durchzuführen. Windows Server 2012 R2-RD-Verbindungsbrokerserver werden in einer gemischten Bereitstellung mit Windows Server 2016-Servern nicht unterstützt. Sobald die RD-Verbindungsbrokerserver Windows Server 2016 ausführen, ist die Bereitstellung betriebsbereit, auch wenn der Rest der Server in der Bereitstellung noch Windows Server 2012 R2 ausführt.

2. **RD-Lizenzserver** sollten aktualisiert werden, bevor Sie das Upgrade Ihrer RD-Sitzungshostserver durchführen.
   > [!NOTE] 
   > Windows Server 2012- und 2012 R2 RD-Lizenzserver arbeiten mit Windows Server 2016-Bereitstellungen zusammen, sie können aber nur CALs von Windows Server 2012 R2 und älter verarbeiten. Sie können keine CALs von Windows Server 2016 verwenden. Weitere Informationen zu RD-Lizenzservern finden Sie unter [Lizenzieren Ihrer RDS-Bereitstellung mit Clientzugriffslizenzen (CALs)](rds-client-access-license.md).

3. Für **RD-Sitzungshostserver** kann als nächstes ein Upgrade ausgeführt werden. Um Ausfallzeiten während des Upgrades zu vermeiden, kann der Administrator die Server für das Upgrade in zwei Schritte aufteilen, wie unten ausführlich beschrieben. Nach dem Upgrade sind alle betriebsbereit. Führen Sie für das Upgrade die in [Upgrade von Remotedesktop-Sitzungshostservern auf Windows Server 2016](upgrade-to-rdsh.md) beschriebenen Schritte aus.

4. Für **RD-Virtualisierungshostserver** kann als nächstes das Upgrade ausgeführt werden. Führen Sie für das Upgrade die in [Upgrade von Remotedesktop-Virtualisierungshostservern auf Windows Server 2016](upgrade-to-rdvh.md) beschriebenen Schritte aus.

5. Für **RD-Webzugriffsserver** kann jederzeit ein Upgrade durchgeführt werden.
   > [!NOTE]
   > Beim Upgrade von RD Web werden möglicherweise IIS-Eigenschaften (wie etwa alle Konfigurationsdateien) zurückgesetzt. Um Ihre Änderungen nicht zu verlieren, notieren oder kopieren Sie an der RD-Website in IIS vorgenommene Anpassungen.

   > [!NOTE] 
   > Windows Server 2012 und 2012 R2 RD-Webzugriffsserver funktionieren in Kombination mit Windows Server 2016-Bereitstellungen.

6. Für **RD-Gatewayserver** kann jederzeit ein Upgrade ausgeführt werden.
   > [!NOTE]
   > Windows Server 2016 enthält keine Richtlinien zum Netzwerkzugriffsschutz (Network Access Protection, NAP) – diese müssen entfernt werden. Die einfachste Möglichkeit zum Entfernen der richtigen Richtlinien besteht im Ausführen des Upgrade-Assistenten. Wenn NAP-Richtlinien vorhanden sind, die Sie löschen müssen, blockiert das Upgrade und erstellt eine Textdatei auf dem Desktop, die die spezifischen Richtlinien enthält. Öffnen Sie zum Verwalten von NAP-Richtlinien das Netzwerkrichtlinienserver-Tool. Klicken Sie nach ihrem Löschen im Setuptool auf **Aktualisieren**, um den Upgradevorgang fortzusetzen. 

   > [!NOTE] 
   > Windows Server 2012 und 2012 R2 RD-Gatewayserver funktionieren in Kombination mit Windows Server 2016-Bereitstellungen.

## <a name="vdi-deployment--supported-guest-os-upgrade"></a>VDI-Bereitstellung: Upgrade des unterstützten Gastbetriebssystems
Administratoren bieten sich die folgenden Optionen zum Aktualisieren von VM-Sammlungen:

### <a name="upgrade-managed-shared-vm-collections"></a>Upgrade von verwalteten freigegebenen VM-Sammlungen 
Die Administratoren müssen VM-Vorlagen mit der gewünschten Betriebssystemversion erstellen und sie verwenden, um alle VMs im Pool zu patchen. 

Wir unterstützen die folgenden Patchszenarien:
- Windows 7 SP1 kann auf Windows 8 oder Windows 8.1 gepatcht werden
- Windows 8 kann auf Windows 8.1 gepatcht werden
- Windows 8.1 kann auf Windows 10 gepatcht werden

### <a name="upgrade-unmanaged-shared-vm-collections"></a>Upgrade von nicht verwalteten freigegebenen VM-Sammlungen 
Endbenutzer können kein Upgrade ihrer persönlichen Desktopcomputer durchführen. Das Upgrade sollte durch Administratoren ausgeführt werden. Die Schritte sind im Einzelnen noch nicht festgelegt worden.