---
title: Migrieren von Rollendiensten der Active Directory-Verbunddienste (AD FS) zu Windows Server 2012
description: Enthält Anweisungen zum Migrieren des AD FS Dienstanbieter zu Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: cdb5523ade5c3c7572656d62d1b4f744683ec96e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408274"
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012"></a>Migrieren von Rollendiensten der Active Directory-Verbunddienste (AD FS) zu Windows Server 2012

Im folgenden finden Sie Anweisungen zum Migrieren der folgenden Rollen Dienste zu Active Directory-Verbunddienste (AD FS) (AD FS) unter Windows Server 2012:  
  
-   AD FS 1,1 Windows-Token-basierter Agent und AD FS 1,1 Ansprüche unterstützender Agent, installiert mit Windows Server 2008 oder Windows Server 2008 R2  
  
-   AD FS 2,0-Verbund Server und AD FS 2,0-Verbund Server Proxy, installiert unter Windows Server 2008 oder Windows Server 2008 R2    
  
## <a name="supported-migration-scenarios"></a>Unterstützte Migrationsszenarien  
 Die Migrations Anweisungen enthalten die folgenden Aufgaben:  
  
- Exportieren der AD FS 2,0-Konfigurationsdaten von Ihrem Server, auf dem Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird  
  
- Ausführen eines direkten Upgrades des Betriebssystems des Servers von Windows Server 2008 oder Windows Server 2008 R2 auf Windows Server 2012.
  
- Neuerstellen der ursprünglichen AD FS Konfiguration und Wiederherstellen der verbleibenden AD FS Dienst Einstellungen auf diesem Server, auf dem nun die AD FS Server-Rolle ausgeführt wird, die mit Windows Server 2012 installiert wird.  
  
  Dieses Handbuch enthält keine Anweisungen zum Migrieren eines Servers, auf dem mehrere Rollen ausgeführt werden. Wenn auf dem Server mehrere Rollen ausgeführt werden, wird empfohlen, anhand der Informationen in anderen Handbüchern für die Rollenmigration ein benutzerdefiniertes Migrationsverfahren für die Serverumgebung zu entwickeln. Migrationsanweisungen für weitere Rollen sind im [Windows Server-Migrationsportal](https://go.microsoft.com/fwlink/?LinkId=247608)verfügbar.  
  
## <a name="supported-operating-systems"></a>Unterstützte Betriebssysteme  
 **Betriebssystem des Zielservers:**  
  

- Windows Server 2012 oder Windows Server 2008 R2 (Optionen für Server Core und vollständige Installation)  
  
  **Zielserver Prozessor:**  
  

- x64-basiert  
  
|Prozessor des Quellservers|Betriebssystem des Quellservers|  
|-----|-----|  
|x86- oder x64-basiert|Windows Server 2003 mit Service Pack 2|  
|x86- oder x64-basiert|Windows Server 2003 R2|  
|x86- oder x64-basiert|Windows Server 2008, vollständige Installation und Server Core-Installation|  
|x64-basiert|Windows Server 2008 R2|  
|x64-basiert|Server Core-Installationsoption von Windows Server 2008 R2|  
|x64-basiert|Server Core-und vollständige Installationsoptionen von Windows Server 2012|  
  
> [!NOTE]
> - Die in der obigen Tabelle aufgeführten Betriebssystemversionen sind die ältesten unterstützten Kombinationen von Betriebssystemen und Service Packs.  
>   -   Die Foundation-, Standard-, Enterprise-und Datacenter-Editionen des Windows Server-Betriebssystems werden als Quell-oder Ziel Server unterstützt.  
>   -   Migrationen zwischen physischen und virtuellen Betriebssystemen werden unterstützt.  
  
### <a name="supported-ad-fs-role-services-and-features"></a>Unterstützte AD FS Rollen Dienste und-Features  
 In der folgenden Tabelle werden die Migrationsszenarien der AD FS-Rollen Dienste und ihre entsprechenden Einstellungen beschrieben, die in diesem Handbuch beschrieben werden.  
  
|Von|So AD FS mit Windows Server 2012 installiert|  
|----------|-----|  
|AD FS 1,0-Verbund Server, installiert mit Windows Server 2003 R2|Migration wird nicht unterstützt|  
|AD FS 1,0-Verbund Server Proxy, installiert mit Windows Server 2003 R2|Migration wird nicht unterstützt|  
|AD FS 1,0 Windows-Token-basierter Agent, installiert mit Windows Server 2003 R2|Migration wird nicht unterstützt|  
|AD FS 1,0-Agent, der Ansprüche unterstützt und mit Windows Server 2003 R2 installiert wurde)|Migration wird nicht unterstützt|  
|AD FS 1,1-Verbund Server, installiert mit Windows Server 2008 oder Windows Server 2008 R2|Migration wird nicht unterstützt|  
|AD FS 1,1-Verbund Server Proxy, installiert mit Windows Server 2008 oder Windows Server 2008 R2|Migration wird nicht unterstützt|  
|AD FS 1,1 Windows-Token-basierter Agent, installiert mit Windows Server 2008 oder Windows Server 2008 R2|Die Migration auf demselben Server wird unterstützt, aber der migrierte AD FS Windows-Token-basierte Agent funktioniert nur mit einem AD FS 1,1-Verbund Dienst, der mit Windows Server 2008 oder Windows Server 2008 R2 installiert ist. Weitere Informationen finden Sie unter:<br /><br /> [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)<br /><br /> [Interagieren mit AD FS 1.x](Interoperating-with-AD-FS-1.x.md)|  
|AD FS 1,1-Agent, der Ansprüche unterstützt und mit Windows Server 2008 oder Windows Server 2008 R2 installiert wurde)|Die Migration auf demselben Server wird unterstützt. Der migrierte AD FS 1,1-Web-Agent funktioniert mit folgendem:<br /><br /> AD FS 1,1-Verbund Dienst, installiert mit Windows Server 2008 oder Windows Server 2008 R2<br /><br /> AD FS 2,0-Verbund Dienst, installiert unter Windows Server 2008 oder Windows Server 2008 R2<br /><br /> AD FS Verbund Dienst, der mit Windows Server 2012 installiert wurde<br /><br /> Weitere Informationen finden Sie unter:<br /><br /> [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)<br /><br /> [Interagieren mit AD FS 1.x](Interoperating-with-AD-FS-1.x.md)|  
|AD FS 2,0-Verbund Server, installiert unter Windows Server 2008 oder Windows Server 2008 R2|Die Migration auf demselben Server wird unterstützt. Weitere Informationen finden Sie unter:<br /><br /> [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)<br /><br /> [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)|  
|AD FS 2,0-Verbund Server Proxy, installiert unter Windows Server 2008 oder Windows Server 2008 R2|Die Migration auf demselben Server wird unterstützt.  Weitere Informationen finden Sie unter:<br /><br /> [Vorbereiten der Migration des AD FS 2.0-Verbundserverproxys](prepare-to-migrate-ad-fs-fed-proxy.md)<br /><br /> [Migrieren des AD FS 2.0-Verbundserverproxys](migrate-the-ad-fs-2-fed-server-proxy.md)|  
  
## <a name="see-also"></a>Weitere Informationen  
 [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md) -Verbund Servers   
 [Vorbereiten der Migration des AD FS 2,0-Verbund Server Proxys](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren Sie den AD FS 2,0](migrate-the-ad-fs-fed-server.md) -Verbund Server   
 [Migrieren Sie den AD FS 2,0-Verbund Server Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)