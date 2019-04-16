---
title: Migrieren des AD FS 2.0-Verbundserverproxys
description: "Enthält Informationen zum Migrieren des AD FS-Verbundserverproxys zu Windows Server 2012."
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 98e28c9be808f63ed39a3ac24dd95014b388d001
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-the-ad-fs-20-federation-server-proxy"></a>Migrieren des AD FS 2.0-Verbundserverproxys
Dieses Dokument enthält ausführliche Informationen zur Migration einer AD FS 2.0-Verbundserver-Proxyserver zu Windows Server 2012.

## <a name="migrate-the-proxy"></a>Migrieren des Proxys

Um einen AD FS 2.0-Verbundserverproxy zu Windows Server 2012 migrieren, führen Sie die folgenden Schritte aus:  
  
1.  Überprüfen Sie, für jeden Verbundserverproxy, die Sie in Windows Server 2012 migrieren möchten, und führen Sie die Verfahren in [Vorbereiten der Migration des AD FS 2.0-Verbundserverproxys](prepare-to-migrate-ad-fs-fed-proxy.md).  
  
2.  Entfernen Sie einen Verbundserverproxy aus dem Lastenausgleich.  
  
3.  Führen Sie ein direktes Upgrade des Betriebssystems auf diesem Server von Windows Server 2008 R2 oder Windows Server 2008 zu Windows Server 2012. Weitere Informationen finden Sie unter [Installieren von Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx).  
  
> [!IMPORTANT]
>  Als Ergebnis einer Aktualisierung des Betriebssystems die AD FS-Proxykonfiguration auf diesem Server verloren und die AD FS 2.0-Serverrolle wird entfernt. Wird stattdessen die Windows Server 2012 AD FS-Serverrolle installiert, aber es ist nicht konfiguriert. Sie müssen manuell die ursprüngliche AD FS-Proxykonfiguration erstellen und Wiederherstellen der verbleibenden AD FS-Proxyeinstellungen, um die verbundserverproxymigration abzuschließen.  
  
4.  Erstellen Sie die ursprüngliche AD FS-Proxykonfiguration mithilfe der **AD FS-Konfigurationsassistenten für den Verbundserverproxy**. Weitere Informationen finden Sie unter [Konfigurieren eines Computers für die Verbundserverproxy-Rolle](configure-a-computer-for-the-federation-server-proxy-role.md). Wie Sie den Assistenten ausführen, verwenden Sie die Informationen, die Sie in Vorbereitung auf die Migration des AD FS 2.0-Verbundserverproxys wie folgt erfasst:  
  
 
|**Eingabeoption für den Assistenten für den Verbundserverproxy**|**Verwenden Sie den folgenden Wert**|
|-----|-----|  
|**Verbunddienstname**|Geben Sie den Wert "basehostname" aus der Datei proxyproperties.txt ein.|  
|**Verwenden Sie einen HTTP-Proxyserver beim Senden von Anfragen an diesen Verbunddienst** das Kontrollkästchen eines Diensts|Aktivieren Kontrollkästchen Sie dieses, wenn die Datei proxyproperties.txt einen Wert für die Eigenschaft "forwardproxyurl" enthält|  
|**HTTP-Proxyserveradresse**|Geben Sie den Wert "forwardproxyurl" aus der Datei proxyproperties.txt ein.|  
|Administratoranmeldeaufforderung|Geben Sie die Anmeldeinformationen des Kontos ein, ist entweder ein Administrator des AD FS-Verbundservers, oder das Dienstkonto, unter dem die AD FS-Verbunddienst ausgeführt wird.|  
  
5.  Aktualisieren Sie Ihre AD FS-Webseiten auf diesem Server. Wenn Sie Ihre angepassten AD FS-proxywebseiten während der Vorbereitung des Verbundserverproxys für die Migration gesichert, verwenden Sie Ihre Sicherungsdaten, um die AD FS-Standardwebseiten zu überschreiben, die standardmäßig erstellt wurden die **%systemdrive%\inetpub\adfs\ls** Verzeichnis aufgrund der AD FS-Proxy-Konfiguration in Windows Server 2012.  
  
6.  Fügen Sie diesen Server wieder in das Lastenausgleichsmodul.  
  
7.  Wenn Sie andere AD FS 2.0-Verbundserverproxys migriert haben, wiederholen Sie die Schritte 2 bis 6 für die verbleibenden verbundserverproxycomputer.  
  
  
## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration der AD FS 2.0-Verbundserver-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren der AD FS 2.0-Verbundserver-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)