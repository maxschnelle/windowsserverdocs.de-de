---
title: Migrieren einer AD FS 2,0-Verbund Server-wid-Farm
description: Enthält Informationen zum Migrieren einer AD FS 2,0-Server-wid-Farm zu Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 89da3de4bc626e12a1fc34752841f2de1afb5322
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408240"
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>Migrieren einer AD FS 2,0-wid-Farm  
Dieses Dokument enthält ausführliche Informationen zum Migrieren einer AD FS 2,0-internen Windows-Daten Bank Farm (WID) zu Windows Server 2012.

## <a name="migrate-an-ad-fs-wid-farm"></a>Migrieren einer AD FS wid-Farm
Führen Sie das folgende Verfahren aus, um eine wid-Farm zu Windows Server 2012 zu migrieren:  
  
1.  Überprüfen Sie für jeden Knoten (Server) in der wid-Farm die Verfahren unter [Vorbereiten der Migration einer wid-Farm](prepare-to-migrate-a-wid-farm.md).  
  
2.  Entfernen Sie alle nicht primären Knoten aus dem Lastenausgleich.  
  
3.  Führen Sie ein Upgrade des Betriebssystems auf diesem Server von Windows Server 2008 R2 oder Windows Server 2008 auf Windows Server 2012 aus. Weitere Informationen finden Sie unter [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx).  
  
> [!IMPORTANT]
>  Aufgrund des Betriebssystem Upgrades geht die AD FS Konfiguration auf diesem Server verloren, und die Server Rolle AD FS 2,0 wird entfernt. Stattdessen wird die Windows Server 2012 AD FS Server-Rolle installiert, aber Sie ist nicht konfiguriert. Sie müssen die ursprüngliche AD FS Konfiguration erstellen und die verbleibenden AD FS Einstellungen wiederherstellen, um die Verbund Servermigration abzuschließen.  
  
4. Erstellen Sie die ursprüngliche AD FS Konfiguration auf diesem Server.  
  
Sie können die ursprüngliche AD FS Konfiguration erstellen, indem Sie mithilfe des **AD FS-Assistenten zum Konfigurieren** von Verbund Servern einen Verbund Server zu einer wid-Farm hinzufügen. Weitere Informationen finden Sie unter [Hinzufügen eines Verbundservers zu einer Verbundserverfarm](add-a-federation-server-to-a-federation-server-farm.md).  
  
> [!NOTE]
> Wenn Sie die Seite **primären Verbund Server und Dienst Konto angeben** des Assistenten für die **Konfiguration des AD FS**-Verbund Servers erreichen, geben Sie den Namen des primären Verbund Servers der wid-Farm ein, und stellen Sie sicher, dass Sie das Dienst Konto eingeben. Informationen, die Sie beim Vorbereiten der AD FS Migration aufgezeichnet haben. Weitere Informationen finden Sie unter [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-a-wid-farm.md)-Verbund Servers. 
>  
> Wenn Sie die Seite **Verbunddienst Namen angeben** erreichen, achten Sie darauf, dass Sie das gleiche SSL-Zertifikat auswählen, das Sie im Abschnitt "Vorbereiten der Migration einer wid-Farm" unter [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-a-wid-farm.md)-Verbund Servers notiert haben.  
  
5. Aktualisieren Sie Ihre AD FS-Webseiten auf diesem Server. Wenn Sie die benutzerdefinierten AD FS Webseiten während der Vorbereitung auf die Migration gesichert haben, müssen Sie die standardmäßigen AD FS Webseiten, die standardmäßig im AD FS Verzeichnis **%systemdrive%\inetpub\adfs\ls** erstellt wurden, mithilfe der Sicherungsdaten überschreiben. Konfiguration auf Windows Server 2012.  
  
6. Fügen Sie den Server, den Sie soeben für Windows Server 2012 aktualisiert haben, dem Load Balancer hinzu.  
  
7. Wiederholen Sie die Schritte 1 bis 6 für die verbleibenden sekundären Server in ihrer wid-Farm.  
  
8. Stufen Sie einen der sekundären Server, für die ein Upgrade ausgeführt wurde, zum primären Server in der internen Windows-Datenbankfarm herauf. Öffnen Sie dazu Windows PowerShell, und führen Sie den folgenden Befehl aus: `PSH:> Set-AdfsSyncProperties –Role PrimaryComputer`.  
  
9. Entfernen Sie den ursprünglichen primären Server Ihrer internen Windows-Datenbankfarm aus dem Lastenausgleich.  
  
10. Stufen Sie den ursprünglichen primären Server in der internen Windows-Datenbankfarm mithilfe von Windows PowerShell zum sekundären Server herab. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung aus: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um den ursprünglichen primären Server auf einen sekundären Server herabzusetzen: `PSH:> Set-AdfsSyncProperties – Role SecondaryComputer –PrimaryComputerName <FQDN of the Primary Federation Server>`.  
  
11. Führen Sie ein Upgrade des Betriebssystems auf diesem letzten Knoten (Server) in der wid-Farm von Windows Server 2008 R2 oder Windows Server 2008 auf Windows Server 2012 aus. Weitere Informationen finden Sie unter [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx).  
  
> [!IMPORTANT]
>  Aufgrund der Aktualisierung des Betriebssystems geht die AD FS Konfiguration auf diesem Server verloren, und die Server Rolle AD FS 2,0 wird entfernt. Stattdessen wird die Windows Server 2012 AD FS Server-Rolle installiert, aber Sie ist nicht konfiguriert. Sie müssen die ursprüngliche AD FS Konfiguration manuell erstellen und die verbleibenden AD FS Einstellungen wiederherstellen, um die Verbund Servermigration abzuschließen.  
  
12. Erstellen Sie die ursprüngliche AD FS Konfiguration auf diesem letzten Knoten (Server) in der wid-Farm.  
  
Sie können die ursprüngliche AD FS Konfiguration erstellen, indem Sie mithilfe des **AD FS-Assistenten zum Konfigurieren** von Verbund Servern einen Verbund Server zu einer wid-Farm hinzufügen. Weitere Informationen finden Sie unter [Hinzufügen eines Verbundservers zu einer Verbundserverfarm](add-a-federation-server-to-a-federation-server-farm.md).  
  
> [!NOTE]
> Wenn Sie im Assistenten für die **Konfiguration des AD FS**-Verbund Servers auf die Seite primären Verbund **Server und Dienst Konto angeben** zugreifen, geben Sie die Dienst Kontoinformationen ein, die Sie beim Vorbereiten der AD FS Migration notiert haben. Weitere Informationen finden Sie unter [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-a-wid-farm.md)-Verbund Servers. 
>  
> Wenn Sie die Seite **Verbunddienst Namen angeben** erreichen, achten Sie darauf, dass Sie das gleiche SSL-Zertifikat auswählen, das Sie unter [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-a-wid-farm.md)-Verbund Servers notiert haben.  
  
13. Aktualisieren Sie Ihre AD FS Webseiten auf diesem letzten Server in ihrer wid-Farm. Wenn Sie Ihre angepassten AD FS Webseiten beim Vorbereiten der Migration gesichert haben, verwenden Sie Ihre Sicherungsdaten, um die standardmäßigen AD FS Webseiten zu überschreiben, die standardmäßig im Verzeichnis **%systemdrive%\inetpub\adfs\ls** als Ergebnis des AD FS Konfiguration auf Windows Server 2012.  
  
14. Fügen Sie den letzten Server Ihrer wid-Farm, den Sie soeben auf Windows Server 2012 aktualisiert haben, auf den Load Balancer hinzu.  
  
15. Stellen Sie alle verbleibenden AD FS-Anpassungen wieder her, z. B. benutzerdefinierte Attributspeicher.  
  
## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md)-Verbund Servers    
 [Vorbereiten der Migration des AD FS 2,0-Verbund Server Proxys](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren Sie den AD FS 2,0](migrate-the-ad-fs-fed-server.md)-Verbund Server  .  
 [Migrieren Sie den AD FS 2,0-Verbund Server Proxy](migrate-the-ad-fs-2-fed-server-proxy.md) .  
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)