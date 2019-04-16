---
title: "Migrieren der Rollendienste für Active Directory Federation Services zu WindowsServer 2012"
description: "Enthält Anweisungen zum Migrieren des AD FS-Rollendiensts zu Windows Server 2012."
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2b44ed504c2b3dc8a8ac0ca9648f1db9e362e075
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012"></a>Migrieren der Rollendienste für Active Directory Federation Services zu WindowsServer 2012

Im folgenden finden Sie Anweisungen zur Migration die folgenden Rollendienste zu Active Directory-Verbunddienste (AD FS) unter Windows Server 2012:  
  
-   AD FS 1.1-Windows-Token-basierter Agent und AD FS 1.1 Ansprüche unterstützenden Agent installiert mit Windows Server 2008 oder Windows Server 2008 R2  
  
-   AD FS 2.0-Verbundserver und AD FS 2.0-Verbundserverproxys unter Windows Server 2008 oder Windows Server 2008 R2 installiert    
  
## <a name="supported-migration-scenarios"></a>Unterstützte Migrationsszenarien  
 Die Anweisungen zur Migration enthält die folgenden Aufgaben:  
  
-   Exportieren der AD FS 2.0-Konfigurationsdaten von Ihrem Server, auf der Windows Server 2008 ausgeführt wird oder Windows Server 2008 R2  
  
-   Ausführen von ein direktes Upgrade des Betriebssystems dieses Servers von Windows Server 2008 oder Windows Server 2008 R2 zu Windows Server 2012.
  
-   Neuerstellen der ursprünglichen AD FS-Konfiguration und Wiederherstellen der übrigen AD FS-diensteinstellungen auf dem Server, auf dem nun die AD FS-Serverrolle ausgeführt wird, die mit Windows Server 2012 installiert ist.  
  
 Dieses Handbuch enthält keine Anweisungen zum Migrieren eines Servers, das mehrere Rollen ausgeführt werden. Wenn Ihr Server mehrere Rollen ausgeführt wird, wird empfohlen, dass ein benutzerdefiniertes Migrationsverfahren für die serverumgebung anhand der Informationen in anderen Handbüchern für die Migration zu entwickeln. Migrationshandbücher für weitere Rollen sind verfügbar, auf die [Windows Server Migration Portal](https://go.microsoft.com/fwlink/?LinkId=247608).  
  
## <a name="supported-operating-systems"></a>Unterstützte Betriebssysteme  
 **Betriebssystem des Zielservers:**  
  

-  Windows Server 2012 oder Windows Server 2008 R2 (Server Core und vollständige Installation)  
  
 **Prozessor des Zielservers:**  
  

-  X64-basierte  
  
|Prozessor des Quellservers|Betriebssystem des Quellservers|  
|-----|-----|  
|x86- oder x 64-basierte|WindowsServer 2003 mit Servicepack 2|  
|x86- oder x 64-basierte|Windows Server 2003 R2|  
|x86- oder x 64-basierte|Windows Server 2008, vollständige Installation und Server Core-Installationsoptionen|  
|X64-basierte|Windows Server2008 R2|  
|X64-basierte|Server Core-Installationsoption von Windows Server 2008 R2|  
|X64-basierte|Server Core-Installation und vollständige Installation von Windows Server 2012|  
  
> [!NOTE]
>  -   Die Versionen der Betriebssysteme, die in der obigen Tabelle aufgeführt sind, werden die ältesten Kombinationen von Betriebssystemen und Servicepacks, die unterstützt werden.  
> -   Die Foundation, Standard, Enterprise und Datacenter-Editionen des Windows Server-Betriebssystems werden als Quell- oder Zielserver unterstützt.  
> -   Migrationen zwischen physischen und virtuellen Betriebssystemen werden unterstützt.  
  
### <a name="supported-ad-fs-role-services-and-features"></a>Unterstützte AD FS-Rollendienste und features  
 Die folgende Tabelle enthält die Migrationsszenarien der AD FS-Rollendienste und die entsprechenden Einstellungen, die in diesem Handbuch beschrieben werden.  
  
|Von|Zu AD FS, installiert mit Windows Server 2012|  
|----------|-----|  
|AD FS 1.0-Verbundserver installiert mit Windows Server 2003 R2|Die Migration wird nicht unterstützt.|  
|AD FS 1.0-Verbundserverproxy installiert mit Windows Server 2003 R2|Die Migration wird nicht unterstützt.|  
|AD FS 1.0-Windows-Token-basierte Agent, installiert mit Windows Server 2003 R2|Die Migration wird nicht unterstützt.|  
|AD FS 1.0 Ansprüche unterstützenden Agent, installiert mit Windows Server 2003 R2)|Die Migration wird nicht unterstützt.|  
|AD FS 1.1-Verbundserver installiert mit Windows Server 2008 oder Windows Server 2008 R2|Die Migration wird nicht unterstützt.|  
|AD FS 1.1-Verbundserverproxy installiert mit Windows Server 2008 oder Windows Server 2008 R2|Die Migration wird nicht unterstützt.|  
|AD FS 1.1-Windows-Token-basierte Agent, installiert mit Windows Server 2008 oder Windows Server 2008 R2|Die Migration auf demselben Server wird unterstützt, aber der migrierte AD FS-Windows-Token-basierter Agent funktioniert nur mit einem AD FS 1.1-Verbunddienst mit Windows Server 2008 oder Windows Server 2008 R2 installiert. Weitere Informationen finden Sie unter:<br /><br /> [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)<br /><br /> [Interaktion mit AD FS 1.x](Interoperating-with-AD-FS-1.x.md)|  
|AD FS 1.1 Ansprüche unterstützenden Agent, installiert mit Windows Server 2008 oder Windows Server 2008 R2)|Die Migration auf demselben Server wird unterstützt. Der migrierte Ansprüche unterstützende 1.1-Web-Agent von AD FS funktioniert mit folgendem:<br /><br /> AD FS 1.1-Verbunddienst installiert mit Windows Server 2008 oder Windows Server 2008 R2<br /><br /> Auf Windows Server 2008 oder Windows Server 2008 R2 installierten AD FS 2.0-Verbunddienst<br /><br /> AD FS-Verbunddienst installiert mit Windows Server 2012<br /><br /> Weitere Informationen finden Sie unter:<br /><br /> [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)<br /><br /> [Interaktion mit AD FS 1.x](Interoperating-with-AD-FS-1.x.md)|  
|AD FS 2.0-Verbundserver installiert unter Windows Server 2008 oder Windows Server 2008 R2|Die Migration auf demselben Server wird unterstützt. Weitere Informationen finden Sie unter:<br /><br /> [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)<br /><br /> [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)|  
|AD FS 2.0-Verbundserverproxys unter Windows Server 2008 oder Windows Server 2008 R2 installiert|Die Migration auf demselben Server wird unterstützt.  Weitere Informationen finden Sie unter:<br /><br /> [Vorbereiten der Migration der AD FS 2.0-Verbundserver-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)<br /><br /> [Migrieren der AD FS 2.0-Verbundserver-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration der AD FS 2.0-Verbundserver-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren der AD FS 2.0-Verbundserver-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)