---
title: Migrieren einer AD FS 2,0-Verbund Server-wid-Farm
description: Enthält Informationen zum Migrieren einer AD FS 2,0-Server-wid-Farm zu Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.openlocfilehash: 8ee9d015b56dfec59e1d13a9ffa51f6297d60787
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87962754"
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>Migrieren einer AD FS 2,0-wid-Farm
Dieses Dokument enthält ausführliche Informationen zum Migrieren einer AD FS 2,0-internen Windows-Daten Bank Farm (WID) zu Windows Server 2012.

## <a name="migrate-an-ad-fs-wid-farm"></a>Migrieren einer AD FS wid-Farm
Führen Sie das folgende Verfahren aus, um eine wid-Farm zu Windows Server 2012 zu migrieren:

1.  Überprüfen Sie für jeden Knoten (Server) in der wid-Farm die Verfahren unter [Vorbereiten der Migration einer wid-Farm](prepare-to-migrate-a-wid-farm.md).

2.  Entfernen Sie alle nicht primären Knoten aus dem Lastenausgleich.

3.  Führen Sie ein Upgrade des Betriebssystems auf diesem Server von Windows Server 2008 R2 oder Windows Server 2008 auf Windows Server 2012 aus. Weitere Informationen finden Sie unter [Installieren von Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134246(v=ws.11)).

> [!IMPORTANT]
>  Durch das Upgrade des Betriebssystems geht die AD FS-Konfiguration auf diesem Server verloren und die AD FS 2.0-Serverrolle wird entfernt. Stattdessen wird die Windows Server 2012 AD FS Server-Rolle installiert, aber Sie ist nicht konfiguriert. Sie müssen die ursprüngliche AD FS-Konfiguration erstellen und die verbleibenden AD FS-Einstellungen wiederherstellen, um die Verbundservermigration abzuschließen.

4. Erstellen Sie die ursprüngliche AD FS-Konfiguration auf diesem Server.

Sie können die ursprüngliche AD FS-Konfiguration mithilfe des **Assistenten zum Konfigurieren von AD FS-Verbundservern** erstellen, um einen Verbundserver zu einer internen Windows-Datenbankfarm hinzuzufügen. Weitere Informationen finden Sie unter [Hinzufügen eines Verbundservers zu einer Verbundserverfarm](add-a-federation-server-to-a-federation-server-farm.md).

> [!NOTE]
> Wenn Sie die Seite **Angeben des primären Verbundservers und des Dienstkontos** des **Assistenten zum Konfigurieren von AD FS-Verbundservern** erreichen, geben Sie den Namen des primären Verbundservers der internen Windows-Datenbankfarm ein, und stellen Sie sicher, dass Sie die Dienstkontoinformationen eingeben, die Sie beim Vorbereiten der AD FS-Migration notiert haben. Weitere Informationen finden Sie unter [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-a-wid-farm.md)-Verbund Servers.
>
> Wenn Sie die Seite **Verbunddienst Namen angeben** erreichen, achten Sie darauf, dass Sie das gleiche SSL-Zertifikat auswählen, das Sie im Abschnitt "Vorbereiten der Migration einer wid-Farm" unter [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-a-wid-farm.md)-Verbund Servers notiert haben.

5. Aktualisieren Sie Ihre AD FS-Webseiten auf diesem Server. Wenn Sie Ihre angepassten AD FS Webseiten während der Vorbereitung auf die Migration gesichert haben, müssen Sie Ihre Sicherungsdaten verwenden, um die standardmäßigen AD FS Webseiten zu überschreiben, die standardmäßig im Verzeichnis **%systemdrive%\inetpub\adfs\ls** erstellt wurden, als Ergebnis der AD FS Konfiguration auf Windows Server 2012.

6. Fügen Sie den Server, den Sie soeben für Windows Server 2012 aktualisiert haben, dem Load Balancer hinzu.

7. Wiederholen Sie die Schritte 1 bis 6 für die restlichen sekundären Server in der internen Windows-Datenbankfarm.

8. Stufen Sie einen der sekundären Server, für die ein Upgrade ausgeführt wurde, zum primären Server in der internen Windows-Datenbankfarm herauf. Öffnen Sie dazu Windows PowerShell, und führen Sie den folgenden Befehl aus: `PSH:> Set-AdfsSyncProperties –Role PrimaryComputer`.

9. Entfernen Sie den ursprünglichen primären Server Ihrer internen Windows-Datenbankfarm aus dem Lastenausgleich.

10. Stufen Sie den ursprünglichen primären Server in der internen Windows-Datenbankfarm mithilfe von Windows PowerShell zum sekundären Server herab. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung aus: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um den ursprünglichen primären Server auf einen sekundären Server herabzusetzen: `PSH:> Set-AdfsSyncProperties – Role SecondaryComputer –PrimaryComputerName <FQDN of the Primary Federation Server>` .

11. Führen Sie ein Upgrade des Betriebssystems auf diesem letzten Knoten (Server) in der wid-Farm von Windows Server 2008 R2 oder Windows Server 2008 auf Windows Server 2012 aus. Weitere Informationen finden Sie unter [Installieren von Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134246(v=ws.11)).

> [!IMPORTANT]
>  Durch das Upgrade des Betriebssystems geht die AD FS-Konfiguration auf diesem Server verloren und die AD FS 2.0-Serverrolle wird entfernt. Stattdessen wird die Windows Server 2012 AD FS Server-Rolle installiert, aber Sie ist nicht konfiguriert. Sie müssen die ursprüngliche AD FS-Konfiguration manuell erstellen und die verbleibenden AD FS-Einstellungen wiederherstellen, um die Verbundservermigration abzuschließen.

12. Erstellen Sie die ursprüngliche AD FS-Konfiguration auf diesem letzten Knoten (Server) in Ihrer internen Windows-Datenbankfarm.

Sie können die ursprüngliche AD FS-Konfiguration mithilfe des **Assistenten zum Konfigurieren von AD FS-Verbundservern** erstellen, um einen Verbundserver zu einer internen Windows-Datenbankfarm hinzuzufügen. Weitere Informationen finden Sie unter [Hinzufügen eines Verbundservers zu einer Verbundserverfarm](add-a-federation-server-to-a-federation-server-farm.md).

> [!NOTE]
> Wenn Sie die Seite **Angeben des primären Verbundservers und des Dienstkontos** des **Assistenten zum Konfigurieren von AD FS-Verbundservern** erreichen, geben Sie die Dienstkontoinformationen ein, die Sie beim Vorbereiten der AD FS-Migration notiert haben. Weitere Informationen finden Sie unter [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-a-wid-farm.md)-Verbund Servers.
>
> Wenn Sie die Seite **Verbunddienst Namen angeben** erreichen, achten Sie darauf, dass Sie das gleiche SSL-Zertifikat auswählen, das Sie unter [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-a-wid-farm.md)-Verbund Servers notiert haben.

13. Aktualisieren Sie Ihre AD FS-Webseiten auf diesem letzten Server in Ihrer internen Windows-Datenbankfarm. Wenn Sie die benutzerdefinierten AD FS Webseiten beim Vorbereiten der Migration gesichert haben, verwenden Sie Ihre Sicherungsdaten, um die standardmäßigen AD FS Webseiten zu überschreiben, die standardmäßig im Verzeichnis **%systemdrive%\inetpub\adfs\ls** erstellt wurden, als Ergebnis der AD FS Konfiguration auf Windows Server 2012.

14. Fügen Sie den letzten Server Ihrer wid-Farm, den Sie soeben auf Windows Server 2012 aktualisiert haben, auf den Load Balancer hinzu.

15. Stellen Sie alle verbleibenden AD FS-Anpassungen wieder her, z. B. benutzerdefinierte Attributspeicher.

## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md) -Verbund Servers [Vorbereiten der Migration des Verbund Server Proxys von AD FS 2,0](prepare-to-migrate-ad-fs-fed-proxy.md) [Migrieren des AD FS 2,0](migrate-the-ad-fs-fed-server.md) Verbund Servers migrieren des [AD FS 2,0](migrate-the-ad-fs-2-fed-server-proxy.md) Verbund Server Proxy [Migrieren der AD FS 1,1-Web-Agents](migrate-the-ad-fs-web-agent.md)
