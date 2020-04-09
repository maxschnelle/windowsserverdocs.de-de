---
title: Migrieren von Rollendiensten der Active Directory Federation zu Windows Server 2012 R2
description: Enthält Anweisungen zum Migrieren des AD FS Dienstanbieter zu Windows Server 2012 R2.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6c2f9c8079eb2dfaf208c8835940351a925d0a16
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857503"
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012-r2"></a>Migrieren von Rollendiensten der Active Directory Federation zu Windows Server 2012 R2
 Dieses Dokument enthält Anweisungen zum Migrieren der folgenden Rollen Dienste zu Active Directory-Verbunddienste (AD FS) (AD FS), der mit Windows Server 2012 R2 installiert wird:  
  
-   AD FS 2,0-Verbund Server, installiert unter Windows Server 2008 oder Windows Server 2008 R2  
  
-   AD FS Verbund Server, installiert unter Windows Server 2012  
  
## <a name="supported-migration-scenarios"></a>Unterstützte Migrationsszenarien  
 Die Anweisungen zur Migration in diesem Handbuch beinhalten die folgenden Aufgaben:  
  
- Exportieren der AD FS 2,0-Konfigurationsdaten von Ihrem Server, auf dem Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 ausgeführt wird  
  
- Ausführen eines direkten Upgrades des Betriebssystems des Servers von Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 auf Windows Server 2012 R2. 
  
- Neuerstellen der ursprünglichen AD FS Konfiguration und Wiederherstellen der verbleibenden AD FS Dienst Einstellungen auf diesem Server, auf dem nun die AD FS Server-Rolle ausgeführt wird, die mit Windows Server 2012 R2 installiert wird.  
  
  Dieses Handbuch enthält keine Anweisungen zum Migrieren eines Servers, auf dem mehrere Rollen ausgeführt werden. Wenn auf dem Server mehrere Rollen ausgeführt werden, wird empfohlen, anhand der Informationen in anderen Handbüchern für die Rollenmigration ein benutzerdefiniertes Migrationsverfahren für die Serverumgebung zu entwickeln. Migrationsanweisungen für weitere Rollen sind im [Windows Server-Migrationsportal](https://go.microsoft.com/fwlink/?LinkId=247608)verfügbar.  
  
### <a name="supported-operating-systems"></a>Unterstützte Betriebssysteme  
 Betriebssystem des Zielservers:  
  
 Windows Server 2012 R2 (Optionen für Server Core und vollständige Installation)  
  
 Zielserver Prozessor:  
  
 x64-basiert  
  
|Prozessor des Quellservers|Betriebssystem des Quellservers|  
|-----------------------------|------------------------------------|  
|x86- oder x64-basiert| Windows Server 2008, vollständige Installation und Server Core-Installation|  
|x64-basiert|Windows Server 2008 R2|  
|x64-basiert|Server Core-Installationsoption von Windows Server 2008 R2|  
|x64-basiert|Server Core-und vollständige Installationsoptionen von Windows Server 2012|  
  
> [!NOTE]
> - Die in der obigen Tabelle aufgeführten Betriebssystemversionen sind die ältesten unterstützten Kombinationen von Betriebssystemen und Service Packs.  
>   -   Die Foundation-, Standard-, Enterprise-und Datacenter-Editionen des Windows Server-Betriebssystems werden als Quell-oder Ziel Server unterstützt.  
>   -   Migrationen zwischen physischen und virtuellen Betriebssystemen werden unterstützt.  
  
### <a name="supported-ad-fs-role-services-and-features"></a>Unterstützte AD FS Rollen Dienste und-Features  
 In der folgenden Tabelle werden die Migrationsszenarien der AD FS-Rollen Dienste und ihre entsprechenden Einstellungen beschrieben, die in diesem Handbuch beschrieben werden.  
  
|Von|So AD FS mit Windows Server 2012 R2 installiert|  
|----------|----------------------------------------------------------------------------------------------|  
|AD FS 2,0-Verbund Server, installiert unter Windows Server 2008 oder Windows Server 2008 R2|Die Migration auf demselben Server wird unterstützt. Weitere Informationen finden Sie unter:<p> [Vorbereiten der Migration des AD FS Verbund Servers](prepare-migrate-ad-fs-server-r2.md)<p> [Migrieren des AD FS Verbund Servers](migrate-ad-fs-fed-server-r2.md)|  
|AD FS Verbund Server, installiert unter Windows Server 2012|Die Migration auf demselben Server wird unterstützt.  Weitere Informationen finden Sie unter folgenden Themen:<p> [Vorbereiten der Migration des AD FS Verbund Servers](prepare-migrate-ad-fs-server-r2.md)<p> [Migrieren des AD FS Verbund Servers](migrate-ad-fs-fed-server-r2.md)|  
  
## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS Verbund Servers](prepare-migrate-ad-fs-server-r2.md)   
 [Migrieren des AD FS Verbund Servers](migrate-ad-fs-fed-server-r2.md)   
 [Migrieren des AD FS Verbund Server Proxys](migrate-fed-server-proxy-r2.md)   
 [Überprüfen der AD FS Migration zu Windows Server 2012 R2](verify-ad-fs-migration.md)