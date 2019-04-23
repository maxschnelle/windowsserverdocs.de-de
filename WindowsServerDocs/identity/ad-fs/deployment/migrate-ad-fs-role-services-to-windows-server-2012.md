---
title: Migrieren von Rollendiensten der Active Directory-Verbunddienste zu Windows Server 2012
description: Enthält Anweisungen zum Migrieren von AD FS-Diensts in Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2b44ed504c2b3dc8a8ac0ca9648f1db9e362e075
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850301"
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012"></a>Migrieren von Rollendiensten der Active Directory-Verbunddienste zu Windows Server 2012

Im folgenden finden Anweisungen zum Migrieren die folgenden Rollendienste zu Active Directory Federation Services (AD FS) unter Windows Server 2012:  
  
-   Token-basierter AD FS 1.1-Windows-Agent und AD FS 1.1-Ansprüche unterstützender Agent installiert mit Windows Server 2008 oder Windows Server 2008 R2  
  
-   AD FS 2.0-Verbundserver und AD FS 2.0-Verbundserverproxys auf Windows Server 2008 oder Windows Server 2008 R2 installiert    
  
## <a name="supported-migration-scenarios"></a>Unterstützte Migrationsszenarien  
 Die Anweisungen zur Migration enthält die folgenden Aufgaben:  
  
-   Exportieren der AD FS 2.0-Konfigurationsdaten von Ihrem Server, der Windows Server 2008 ausgeführt wird, oder Windows Server 2008 R2  
  
-   Ausführen von ein direktes Upgrade des Betriebssystems dieses Servers von Windows Server 2008 oder Windows Server 2008 R2 auf Windows Server 2012.
  
-   Neuerstellen der ursprünglichen AD FS-Konfiguration und Wiederherstellen der übrigen AD FS-diensteinstellungen auf dem Server, der jetzt die AD FS-Serverrolle ausgeführt wird, die mit Windows Server 2012 installiert ist.  
  
 Dieses Handbuch enthält keine Anweisungen zum Migrieren eines Servers, auf dem mehrere Rollen ausgeführt werden. Wenn auf dem Server mehrere Rollen ausgeführt werden, wird empfohlen, anhand der Informationen in anderen Handbüchern für die Rollenmigration ein benutzerdefiniertes Migrationsverfahren für die Serverumgebung zu entwickeln. Migrationsanweisungen für weitere Rollen sind im [Windows Server-Migrationsportal](https://go.microsoft.com/fwlink/?LinkId=247608)verfügbar.  
  
## <a name="supported-operating-systems"></a>Unterstützte Betriebssysteme  
 **Betriebssystem des Zielservers:**  
  

-  Windows Server 2012 oder Windows Server 2008 R2 (Server Core und vollständige Installation)  
  
 **Prozessor des Zielservers:**  
  

-  x64-basiert  
  
|Prozessor des Quellservers|Betriebssystem des Quellservers|  
|-----|-----|  
|x86- oder x64-basiert|Windows Server 2003 mit Service Pack 2|  
|x86- oder x64-basiert|Windows Server 2003 R2|  
|x86- oder x64-basiert|Windows Server 2008, vollständige Installation und Server Core-Installationsoptionen|  
|x64-basiert|Windows Server 2008 R2|  
|x64-basiert|Server Core-Installationsoption von Windows Server 2008 R2|  
|x64-basiert|Server Core "und" vollständige Installation von Windows Server 2012|  
  
> [!NOTE]
>  -   Die in der obigen Tabelle aufgeführten Betriebssystemversionen sind die ältesten unterstützten Kombinationen von Betriebssystemen und Service Packs.  
> -   Die Foundation, Standard, Enterprise und Datacenter-Editionen des Betriebssystems Windows Server werden als die Quelle oder als Zielserver unterstützt.  
> -   Migrationen zwischen physischen und virtuellen Betriebssystemen werden unterstützt.  
  
### <a name="supported-ad-fs-role-services-and-features"></a>Unterstützte AD FS-Rollendienste und features  
 Die folgende Tabelle beschreibt die Migrationsszenarien der AD FS-Rollendienste und ihre entsprechenden Einstellungen, die in diesem Handbuch beschrieben werden.  
  
|Von|Um AD FS, installiert mit Windows Server 2012|  
|----------|-----|  
|AD FS 1.0-Verbundserver installiert mit Windows Server 2003 R2|Migration wird nicht unterstützt|  
|AD FS 1.0-Verbundserverproxy mit Windows Server 2003 R2 installiert|Migration wird nicht unterstützt|  
|AD FS 1.0-Windows-Token-basierte Agent, installiert mit Windows Server 2003 R2|Migration wird nicht unterstützt|  
|AD FS 1.0 Ansprüche unterstützenden Agent, installiert mit Windows Server 2003 R2)|Migration wird nicht unterstützt|  
|AD FS 1.1-Verbundserver installiert mit Windows Server 2008 oder Windows Server 2008 R2|Migration wird nicht unterstützt|  
|AD FS 1.1-Verbundserverproxy mit Windows Server 2008 oder Windows Server 2008 R2 installiert|Migration wird nicht unterstützt|  
|AD FS 1.1-Windows-Token-basierte Agent, installiert mit Windows Server 2008 oder Windows Server 2008 R2|Die Migration auf dem gleichen Server wird unterstützt, aber der migrierte Token-basierter AD FS-Windows-Agent funktioniert nur mit einem AD FS 1.1-Verbunddienst mit Windows Server 2008 oder Windows Server 2008 R2 installiert. Weitere Informationen finden Sie in den folgenden Themen:<br /><br /> [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)<br /><br /> [Interaktion mit AD FS 1.x](Interoperating-with-AD-FS-1.x.md)|  
|AD FS 1.1 Ansprüche unterstützenden Agent, installiert mit Windows Server 2008 oder Windows Server 2008 R2)|Die Migration auf demselben Server wird unterstützt. Der migrierte AD FS 1.1-Ansprüche unterstützende-Web-Agent funktioniert mit folgendem:<br /><br /> AD FS 1.1-Verbunddienst, die mit Windows Server 2008 oder Windows Server 2008 R2 installiert<br /><br /> Auf Windows Server 2008 oder Windows Server 2008 R2 installierten AD FS 2.0-Verbunddienst<br /><br /> AD FS-Verbunddienst installiert mit Windows Server 2012<br /><br /> Weitere Informationen finden Sie in den folgenden Themen:<br /><br /> [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)<br /><br /> [Interaktion mit AD FS 1.x](Interoperating-with-AD-FS-1.x.md)|  
|AD FS 2.0-Verbundserver installiert unter Windows Server 2008 oder Windows Server 2008 R2|Die Migration auf demselben Server wird unterstützt. Weitere Informationen finden Sie in den folgenden Themen:<br /><br /> [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)<br /><br /> [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)|  
|AD FS 2.0-Verbundserverproxys auf Windows Server 2008 oder Windows Server 2008 R2 installiert|Die Migration auf demselben Server wird unterstützt.  Weitere Informationen finden Sie unter:<br /><br /> [Vorbereiten der Migration von AD FS 2.0-Verbundserver-Server-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)<br /><br /> [Migrieren der AD FS 2.0-Verbundserver-Server-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)|  
  
## <a name="see-also"></a>Siehe auch  
 [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration von AD FS 2.0-Verbundserver-Server-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren der AD FS 2.0-Verbundserver-Server-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)