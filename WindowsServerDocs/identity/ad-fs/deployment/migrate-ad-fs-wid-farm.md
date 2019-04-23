---
title: Migrieren Sie eine AD FS 2.0-Verbundserver Server WID-farm
description: Enthält Informationen zur Migration von Windows-datenbankfarm ein AD FS 2.0-Server zu Windows Server 2012
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: dbef7d07041a1fd32656c95947d5202b566c068a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868321"
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>Migrieren einer AD FS 2.0-WID-farm  
Dieses Dokument enthält ausführliche Informationen zum Migrieren eines AD FS 2.0 Windows Internal Database (WID)-Farm zu Windows Server 2012.

## <a name="migrate-an-ad-fs-wid-farm"></a>Migrieren einer AD FS-WID-farm
Um eine WID-Farm zu Windows Server 2012 zu migrieren, führen Sie die folgenden Schritte aus:  
  
1.  Klicken Sie für jeden Knoten (Server) in der Windows-datenbankfarm, überprüfen Sie, und führen Sie die Verfahren in [Vorbereiten der Migration von einer Windows-datenbankfarm](prepare-to-migrate-a-wid-farm.md).  
  
2.  Entfernen Sie alle nicht primären Knoten aus dem Lastenausgleich.  
  
3.  Ein Upgrade des Betriebssystems Ihres Servers von Windows Server 2008 R2 oder Windows Server 2008 zu Windows Server 2012. Weitere Informationen finden Sie unter [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx).  
  
> [!IMPORTANT]
>  Als Ergebnis der Aktualisierung des Betriebssystems die AD FS-Konfiguration auf diesem Server verloren und die AD FS 2.0-Serverrolle wird entfernt. Wird stattdessen die Windows Server 2012 AD FS-Serverrolle installiert, aber nicht konfiguriert ist. Sie müssen die ursprüngliche AD FS-Konfiguration erstellen und Wiederherstellen der verbleibenden AD FS-Einstellungen, um die verbundservermigration abzuschließen.  
  
4.  Erstellen Sie die ursprüngliche AD FS-Konfiguration auf diesem Server an.  
  
Sie können die ursprüngliche AD FS-Konfiguration erstellen, mit der **AD FS-Verbundserverkonfigurations-Assistenten** eine WID-Farm einen Verbundserver hinzu. Weitere Informationen finden Sie unter [Hinzufügen eines Verbundservers zu einer Verbundserverfarm](add-a-federation-server-to-a-federation-server-farm.md).  
  
> [!NOTE]
> Wenn Sie erreichen die **angeben des primären Verbundservers und des Dienstkontos** auf der Seite die **AD FS-Verbundserverkonfigurations-Assistenten**, geben Sie den Namen des primären Verbundservers der WID-Farm und achten Sie darauf, dass Sie die Dienstkontoinformationen eingeben, die Sie beim Vorbereiten der AD FS-Migration notiert haben. Weitere Informationen finden Sie unter [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-a-wid-farm.md). 
>  
> Sie beim Erreichen der **Geben Sie dem Namen des Verbunddiensts** Seite, wählen Sie dasselbe SSL-Zertifikat, das Sie in der "Vorbereiten der Migration eine WID-Farm" aufgezeichnet [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-a-wid-farm.md).  
  
5.  Aktualisieren Sie Ihre AD FS-Webseiten auf diesem Server. Wenn Sie Ihre angepassten AD FS-Webseiten während der Vorbereitung der Migration gesichert, müssen Sie Ihre Sicherungsdaten zu verwenden, um die AD FS-Standardwebseiten zu überschreiben, die standardmäßig erstellt wurden die **%systemdrive%\inetpub\adfs\ls** als Verzeichnis ein Ergebnis von der AD FS-Konfiguration unter Windows Server 2012.  
  
6.  Fügen Sie den Server, den Sie für den Load Balancer nur auf Windows Server 2012 aktualisiert.  
  
7.  Wiederholen Sie die Schritte 1 bis 6 für die restlichen sekundären Server in Ihrer Windows-datenbankfarm.  
  
8.  Stufen Sie einen der sekundären Server, für die ein Upgrade ausgeführt wurde, zum primären Server in der internen Windows-Datenbankfarm herauf. Öffnen Sie dazu Windows PowerShell, und führen Sie den folgenden Befehl aus: `PSH:> Set-AdfsSyncProperties –Role PrimaryComputer`.  
  
9. Entfernen Sie den ursprünglichen primären Server Ihrer internen Windows-Datenbankfarm aus dem Lastenausgleich.  
  
10. Stufen Sie den ursprünglichen primären Server in der internen Windows-Datenbankfarm mithilfe von Windows PowerShell zum sekundären Server herab. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung aus: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um den ursprünglichen primären Server zum sekundären Server herabzustufen: `PSH:> Set-AdfsSyncProperties – Role SecondaryComputer –PrimaryComputerName <FQDN of the Primary Federation Server>`.  
  
11. Das Upgrade des Betriebssystems auf diesem letzten Knoten (Server) auf Ihrem-datenbankfarm von Windows Server 2008 R2 oder Windows Server 2008 zu Windows Server 2012. Weitere Informationen finden Sie unter [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx).  
  
> [!IMPORTANT]
>  Das Ergebnis des Upgrades des Betriebssystems die AD FS-Konfiguration auf diesem Server verloren und die AD FS 2.0-Serverrolle wird entfernt. Wird stattdessen die Windows Server 2012 AD FS-Serverrolle installiert, aber nicht konfiguriert ist. Sie müssen manuell die ursprüngliche AD FS-Konfiguration erstellen und Wiederherstellen der verbleibenden AD FS-Einstellungen, um die verbundservermigration abzuschließen.  
  
12. Erstellen Sie die ursprüngliche AD FS-Konfiguration auf diesem letzten Knoten (Server) in Ihrer Windows-datenbankfarm.  
  
Sie können die ursprüngliche AD FS-Konfiguration erstellen, mit der **AD FS-Verbundserverkonfigurations-Assistenten** eine WID-Farm einen Verbundserver hinzu. Weitere Informationen finden Sie unter [Hinzufügen eines Verbundservers zu einer Verbundserverfarm](add-a-federation-server-to-a-federation-server-farm.md).  
  
> [!NOTE]
> Wenn Sie erreichen die **angeben des primären Verbundservers und des Dienstkontos** auf der Seite die **AD FS-Verbundserverkonfigurations-Assistenten**, geben Sie die Dienstkontoinformationen, die Sie notiert während Vorbereiten der AD FS-Migration. Weitere Informationen finden Sie unter [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-a-wid-farm.md). 
>  
> Sie beim Erreichen der **Geben Sie dem Namen des Verbunddiensts** Seite, achten Sie darauf, dass Sie dasselbe SSL-Zertifikat wählen Sie im notiert [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-a-wid-farm.md).  
  
13. Aktualisieren Sie Ihre AD FS-Webseiten auf diesem letzten Server in Ihrer Windows-datenbankfarm. Wenn Sie Ihre angepassten AD FS-Webseiten während der Vorbereitung der Migration gesichert, verwenden Sie Ihre gesicherten Daten, um die AD FS-Standardwebseiten zu überschreiben, die standardmäßig erstellt wurden die **%systemdrive%\inetpub\adfs\ls** Verzeichnis als Ergebnis des die AD FS-Konfiguration unter Windows Server 2012.  
  
14. Fügen Sie diesen letzten Server Ihrer WID-Farm, die Sie für den Load Balancer nur auf Windows Server 2012 aktualisiert.  
  
15. Stellen Sie alle verbleibenden AD FS-Anpassungen wieder her, z. B. benutzerdefinierte Attributspeicher.  
  
## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration von AD FS 2.0-Verbundserver-Server-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren der AD FS 2.0-Verbundserver-Server-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)