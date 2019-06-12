---
title: Migrieren des AD FS 2.0-Verbundserverproxys
description: Enthält Informationen zum Migrieren des AD FS-Verbundserverproxys zu Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: eddb0d3432c69ecff4542ff1b8f2204b96ce0820
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445662"
---
# <a name="migrate-the-ad-fs-20-federation-server-proxy"></a>Migrieren des AD FS 2.0-Verbundserverproxys
Dieses Dokument enthält ausführliche Informationen zur Migration von AD FS 2.0-Verbundserver-Proxy-Server zu Windows Server 2012.

## <a name="migrate-the-proxy"></a>Migrieren Sie den proxy

Um einen AD FS 2.0-Verbundserverproxy zu Windows Server 2012 zu migrieren, führen Sie die folgenden Schritte aus:  
  
1.  Klicken Sie für jeden Verbundserverproxy, die Sie zu Windows Server 2012 migrieren möchten, überprüfen Sie, und führen Sie die Verfahren in [Vorbereiten der Migration des AD FS 2.0-Verbundserverproxys](prepare-to-migrate-ad-fs-fed-proxy.md).  
  
2.  Entfernen Sie einen Verbundserverproxy aus dem Lastenausgleich.  
  
3.  Führen Sie ein direktes Upgrade des Betriebssystems Ihres Servers von Windows Server 2008 R2 oder Windows Server 2008 zu Windows Server 2012. Weitere Informationen finden Sie unter [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx).  
  
> [!IMPORTANT]
>  Durch das Upgrade des Betriebssystems geht die AD FS-Proxykonfiguration auf diesem Server verloren und die AD FS 2.0-Serverrolle wird entfernt. Wird stattdessen die Windows Server 2012 AD FS-Serverrolle installiert, aber nicht konfiguriert ist. Sie müssen die ursprüngliche AD FS-Proxykonfiguration manuell erstellen und die verbleibenden AD FS-Proxyeinstellungen wiederherstellen, um die Verbundserverproxymigration abzuschließen.  
  
4. Erstellen Sie die ursprüngliche AD FS-Proxykonfiguration mithilfe des **Assistenten für die Konfiguration eines AD FS-Verbundserverproxys**. Weitere Informationen finden Sie unter [Configure a Computer for the Federation Server Proxy Role](configure-a-computer-for-the-federation-server-proxy-role.md). Wenn Sie den Assistenten ausführen, verwenden Sie die Informationen, die Sie in Vorbereitung auf die Migration des AD FS 2.0-Verbundserverproxys gesammelt haben, wie folgt:  
  
 
|**Eingabeoption für den Assistenten für Verbundserverproxys**|**Verwenden Sie den folgenden Wert**|
|-----|-----|  
|**Name des Verbunddiensts**|Geben Sie den Wert "BaseHostName" aus der Datei proxyproperties.txt ein.|  
|**Beim Senden von Anfragen an diesen Verbunddienst HTTP-Proxyserver verwenden**, Kontrollkästchen|Aktivieren Sie dieses Kontrollkästchen, wenn die Datei proxyproperties.txt einen Wert für die Eigenschaft "ForwardProxyUrl" enthält.|  
|**HTTP-Proxyserveradresse**|Geben Sie den Wert "ForwardProxyUrl" aus der Datei proxyproperties.txt ein.|  
|Anmeldeaufforderung|Geben Sie die Anmeldeinformationen für ein Konto ein, das entweder ein Administrator des AD FS-Verbundservers ist, oder das Dienstkonto, unter dem der AD FS-Verbunddienst ausgeführt wird.|  
  
5. Aktualisieren Sie Ihre AD FS-Webseiten auf diesem Server. Wenn Sie Ihre angepassten AD FS-proxywebseiten während der Vorbereitung des Verbundserverproxys für die Migration gesichert, verwenden Sie Ihre gesicherten Daten, um die AD FS-Standardwebseiten zu überschreiben, die standardmäßig erstellt wurden die **%systemdrive%\inetpub\adfs\ls** Verzeichnis aufgrund der Konfiguration des AD FS-Proxy unter Windows Server 2012.  
  
6. Fügen Sie diesen Server wieder dem Lastenausgleich hinzu.  
  
7. Wenn Sie andere AD FS 2.0-Verbundserverproxys migriert haben, wiederholen Sie die Schritte 2 bis 6 für die verbleibenden Verbundserverproxycomputer.  
  
  
## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration von AD FS 2.0-Verbundserver-Server-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren der AD FS 2.0-Verbundserver-Server-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)