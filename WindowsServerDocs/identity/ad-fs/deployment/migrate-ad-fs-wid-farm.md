---
title: Migrieren einer AD FS 2.0-Verbundserver-WID-Serverfarm
description: "Enthält Informationen zur Migration von Windows-datenbankfarm ein AD FS 2.0-Server zu Windows Server 2012"
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: dbef7d07041a1fd32656c95947d5202b566c068a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>Migrieren einer AD FS 2.0 WID-farm  
Dieses Dokument enthält ausführliche Informationen zur Migration einer AD FS 2.0 Windows Internal Database (WID)-Farm zu Windows Server 2012.

## <a name="migrate-an-ad-fs-wid-farm"></a>Migrieren Sie eine AD FS-datenbankfarm
Um ein Windows-datenbankfarm zu Windows Server 2012 migrieren, führen Sie die folgenden Schritte aus:  
  
1.  Für jeden Knoten (Server) in der Windows-datenbankfarm, überprüfen Sie, und führen Sie die Verfahren in [Vorbereiten der Migration von einer Windows-datenbankfarm](prepare-to-migrate-a-wid-farm.md).  
  
2.  Entfernen Sie alle nicht primären Knoten aus dem Lastenausgleich.  
  
3.  Aktualisieren des Betriebssystems Ihres Servers von Windows Server 2008 R2 oder Windows Server 2008 zu Windows Server 2012. Weitere Informationen finden Sie unter [Installieren von Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx).  
  
> [!IMPORTANT]
>  Als Ergebnis einer Aktualisierung des Betriebssystems der AD FS-Konfiguration auf diesem Server verloren und die AD FS 2.0-Serverrolle wird entfernt. Wird stattdessen die Windows Server 2012 AD FS-Serverrolle installiert, aber es ist nicht konfiguriert. Sie müssen die ursprüngliche AD FS-Konfiguration erstellen und Wiederherstellen der verbleibenden AD FS-Einstellungen, um die verbundservermigration abzuschließen.  
  
4.  Erstellen Sie die ursprüngliche AD FS-Konfiguration auf diesem Server.  
  
Sie können die ursprüngliche AD FS-Konfiguration erstellen, mit der **AD FS-Verbundserverkonfigurations-Assistenten** zum Hinzufügen eines Verbundservers zu einer WID-Farm. Weitere Informationen finden Sie unter [Hinzufügen eines Verbundservers zu einer Verbundserverfarm](add-a-federation-server-to-a-federation-server-farm.md).  
  
> [!NOTE]
> Wenn Sie so lange die **angeben des primären Verbundservers und des Dienstkontos** Seite der **AD FS-Verbundserverkonfigurations-Assistenten**, geben Sie den Namen des primären Verbundservers der WID-Farm, und achten Sie darauf, dass Sie die Dienstkontoinformationen eingeben, die Sie beim Vorbereiten der AD FS-Migration notiert haben. Weitere Informationen finden Sie unter [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-a-wid-farm.md). 
>  
> Wenn Sie so lange die **angeben eines Verbunddienstnamens** Seite, wählen Sie dasselbe SSL-Zertifikat, das Sie in der "Vorbereiten der Migration eine WID-Farm" aufgezeichnet [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-a-wid-farm.md).  
  
5.  Aktualisieren Sie Ihre AD FS-Webseiten auf diesem Server. Wenn Sie Ihre angepassten AD FS-Webseiten während der Vorbereitung der Migration gesichert, müssen Sie Ihre Sicherungsdaten verwenden, um die AD FS-Standardwebseiten zu überschreiben, die standardmäßig erstellt wurden die **%systemdrive%\inetpub\adfs\ls** Verzeichnis aufgrund der AD FS-Konfiguration unter Windows Server 2012.  
  
6.  Fügen Sie den Server, den Sie gerade auf Windows Server 2012 auf das Lastenausgleichsmodul aktualisiert.  
  
7.  Wiederholen Sie die Schritte 1 bis 6 für die restlichen sekundären Server in Ihrer Windows-datenbankfarm.  
  
8.  Stufen Sie einen aktualisierten sekundären Server zum primären Server in Ihrer Windows-datenbankfarm. Zu diesem Zweck öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl: `PSH:> Set-AdfsSyncProperties –Role PrimaryComputer`.  
  
9. Entfernen Sie den ursprünglichen primären Server von Ihrem Windows-datenbankfarm aus dem Lastenausgleich.  
  
10. Herabstufen Sie, den ursprünglichen primären Server in Ihrer Windows-datenbankfarm ein sekundärer Server werden mithilfe von Windows PowerShell. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie den folgenden Befehl, den ursprünglichen primären Server zum sekundären Server herabzustufen: `PSH:> Set-AdfsSyncProperties – Role SecondaryComputer –PrimaryComputerName <FQDN of the Primary Federation Server>`.  
  
11. Das Upgrade des Betriebssystems auf diesem letzten Knoten (Server) auf Ihre datenbankfarm von Windows Server 2008 R2 oder Windows Server 2008 zu Windows Server 2012. Weitere Informationen finden Sie unter [Installieren von Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx).  
  
> [!IMPORTANT]
>  Als Ergebnis einer Aktualisierung des Betriebssystems der AD FS-Konfiguration auf diesem Server verloren und die AD FS 2.0-Serverrolle wird entfernt. Wird stattdessen die Windows Server 2012 AD FS-Serverrolle installiert, aber es ist nicht konfiguriert. Sie müssen manuell erstellen die ursprüngliche AD FS-Konfiguration und Wiederherstellen der verbleibenden AD FS-Einstellungen, um die verbundservermigration abzuschließen.  
  
12. Erstellen Sie die ursprüngliche AD FS-Konfiguration auf diesem letzten Knoten (Server) in Ihrer Windows-datenbankfarm.  
  
Sie können die ursprüngliche AD FS-Konfiguration erstellen, mit der **AD FS-Verbundserverkonfigurations-Assistenten** zum Hinzufügen eines Verbundservers zu einer WID-Farm. Weitere Informationen finden Sie unter [Hinzufügen eines Verbundservers zu einer Verbundserverfarm](add-a-federation-server-to-a-federation-server-farm.md).  
  
> [!NOTE]
> Wenn Sie so lange die **angeben des primären Verbundservers und des Dienstkontos** Seite der **AD FS-Verbundserverkonfigurations-Assistenten**, geben Sie die Dienstkontoinformationen ein, die Sie beim Vorbereiten der AD FS-Migration notiert haben. Weitere Informationen finden Sie unter [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-a-wid-farm.md). 
>  
> Wenn Sie so lange die **angeben eines Verbunddienstnamens** Seite, achten Sie darauf, dass Sie dasselbe SSL-Zertifikat wählen Sie im aufgezeichnet [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-a-wid-farm.md).  
  
13. Aktualisieren Sie Ihre AD FS-Webseiten auf diesem letzten Server in Ihrer Windows-datenbankfarm. Wenn Sie Ihre angepassten AD FS-Webseiten während der Vorbereitung der Migration gesichert, verwenden Sie Ihre Sicherungsdaten, um die AD FS-Standardwebseiten zu überschreiben, die standardmäßig erstellt wurden die **%systemdrive%\inetpub\adfs\ls** Verzeichnis aufgrund der AD FS-Konfiguration unter Windows Server 2012.  
  
14. Fügen Sie diesen letzten Server Ihrer WID-Farm, die Sie gerade auf Windows Server 2012 auf das Lastenausgleichsmodul aktualisiert.  
  
15. Stellen Sie alle verbleibenden AD FS-Anpassungen, z. B. benutzerdefinierte Attributspeicher wieder her.  
  
## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration der AD FS 2.0-Verbundserver-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren der AD FS 2.0-Verbundserver-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)