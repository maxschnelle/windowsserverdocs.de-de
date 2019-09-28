---
title: Migrieren des AD FS 2,0-Verbund Server Proxys
description: Bietet Informationen zum Migrieren des AD FS Verbund Server Proxys zu Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e97a1b3b66d7c12c96570022b7e69caaf0e92f65
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408227"
---
# <a name="migrate-the-ad-fs-20-federation-server-proxy"></a>Migrieren des AD FS 2,0-Verbund Server Proxys
Dieses Dokument enthält ausführliche Informationen zum Migrieren eines AD FS 2,0-Verbund Proxyservers zu Windows Server 2012.

## <a name="migrate-the-proxy"></a>Den Proxy migrieren

Führen Sie das folgende Verfahren aus, um einen AD FS 2,0-Verbund Server Proxy zu Windows Server 2012 zu migrieren:  
  
1.  Überprüfen Sie für jeden Verbund Server Proxy, den Sie zu Windows Server 2012 migrieren möchten, die Verfahren unter [Vorbereiten der Migration des AD FS 2,0-Verbund Server Proxys](prepare-to-migrate-ad-fs-fed-proxy.md).  
  
2.  Entfernen Sie einen Verbundserverproxy aus dem Lastenausgleich.  
  
3.  Führen Sie ein direktes Upgrade des Betriebssystems auf diesem Server von Windows Server 2008 R2 oder Windows Server 2008 auf Windows Server 2012 aus. Weitere Informationen finden Sie unter [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx).  
  
> [!IMPORTANT]
>  Durch das Upgrade des Betriebssystems geht die AD FS-Proxykonfiguration auf diesem Server verloren und die AD FS 2.0-Serverrolle wird entfernt. Stattdessen wird die Windows Server 2012 AD FS Server-Rolle installiert, aber Sie ist nicht konfiguriert. Sie müssen die ursprüngliche AD FS-Proxykonfiguration manuell erstellen und die verbleibenden AD FS-Proxyeinstellungen wiederherstellen, um die Verbundserverproxymigration abzuschließen.  
  
4. Erstellen Sie die ursprüngliche AD FS-Proxykonfiguration mithilfe des **Assistenten für die Konfiguration eines AD FS-Verbundserverproxys**. Weitere Informationen finden Sie unter [Konfigurieren eines Computers für die Verbundserverproxy-Rolle](configure-a-computer-for-the-federation-server-proxy-role.md). Wenn Sie den Assistenten ausführen, verwenden Sie die Informationen, die Sie in Vorbereitung auf die Migration des AD FS 2.0-Verbundserverproxys gesammelt haben, wie folgt:  
  
 
|**Eingabeoption für den Verbund Server Proxy-Assistenten**|**Folgenden Wert verwenden**|
|-----|-----|  
|**Verbunddienst Name**|Geben Sie den Wert "BaseHostName" aus der Datei proxyproperties.txt ein.|  
|**Beim Senden von Anfragen an diesen Verbunddienst HTTP-Proxyserver verwenden**, Kontrollkästchen|Aktivieren Sie dieses Kontrollkästchen, wenn die Datei proxyproperties.txt einen Wert für die Eigenschaft "ForwardProxyUrl" enthält.|  
|**Adresse des HTTP-Proxy Servers**|Geben Sie den Wert "ForwardProxyUrl" aus der Datei proxyproperties.txt ein.|  
|Anmeldeaufforderung|Geben Sie die Anmeldeinformationen für ein Konto ein, das entweder ein Administrator des AD FS-Verbundservers ist, oder das Dienstkonto, unter dem der AD FS-Verbunddienst ausgeführt wird.|  
  
5. Aktualisieren Sie Ihre AD FS-Webseiten auf diesem Server. Wenn Sie Ihre angepassten AD FS Proxy Webseiten während der Vorbereitung des Verbund Server Proxys für die Migration gesichert haben, verwenden Sie die Sicherungsdaten, um die standardmäßigen AD FS Webseiten zu überschreiben, die standardmäßig im Verzeichnis **%systemdrive%\inetpub\adfs\ls** erstellt wurden. als Ergebnis der Konfiguration des AD FS-Proxys in Windows Server 2012.  
  
6. Fügen Sie diesen Server wieder dem Lastenausgleich hinzu.  
  
7. Wenn Sie andere AD FS 2.0-Verbundserverproxys migriert haben, wiederholen Sie die Schritte 2 bis 6 für die verbleibenden Verbundserverproxycomputer.  
  
  
## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md)-Verbund Servers    
 [Vorbereiten der Migration des AD FS 2,0-Verbund Server Proxys](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren Sie den AD FS 2,0](migrate-the-ad-fs-fed-server.md)-Verbund Server  .  
 [Migrieren Sie den AD FS 2,0-Verbund Server Proxy](migrate-the-ad-fs-2-fed-server-proxy.md) .  
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)