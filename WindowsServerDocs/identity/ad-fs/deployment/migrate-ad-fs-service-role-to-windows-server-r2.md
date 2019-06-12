---
title: Migrieren von Rollendiensten der Active Directory Federation zu Windows Server 2012 R2
description: Enthält Anweisungen zum Migrieren von AD FS-Diensts in Windows Server 2012 R2.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 34eab7d5e0325a4ad8268a900738eea30b944ebb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444561"
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012-r2"></a>Migrieren von Rollendiensten der Active Directory Federation zu Windows Server 2012 R2
 Dieses Dokument enthält Anweisungen zum Migrieren von die folgenden Rollendienste zu Active Directory-Verbunddienste (AD FS), die mit Windows Server 2012 R2 installiert ist:  
  
-   AD FS 2.0-Verbundserver installiert unter Windows Server 2008 oder Windows Server 2008 R2  
  
-   AD FS-Verbundserver installiert unter Windows Server 2012  
  
## <a name="supported-migration-scenarios"></a>Unterstützte Migrationsszenarien  
 Die Anweisungen zur Migration in diesem Handbuch beinhalten die folgenden Aufgaben:  
  
- Exportieren der AD FS 2.0-Konfigurationsdaten von Ihrem Server, auf denen Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 ausgeführt wird  
  
- Ausführen von ein direktes Upgrade des Betriebssystems dieses Servers von Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 auf Windows Server 2012 R2. 
  
- Neuerstellen der ursprünglichen AD FS-Konfiguration und Wiederherstellen der übrigen AD FS-diensteinstellungen auf dem Server, der jetzt die AD FS-Serverrolle ausgeführt wird, die mit Windows Server 2012 R2 installiert ist.  
  
  Dieses Handbuch enthält keine Anweisungen zum Migrieren eines Servers, auf dem mehrere Rollen ausgeführt werden. Wenn auf dem Server mehrere Rollen ausgeführt werden, wird empfohlen, anhand der Informationen in anderen Handbüchern für die Rollenmigration ein benutzerdefiniertes Migrationsverfahren für die Serverumgebung zu entwickeln. Migrationsanweisungen für weitere Rollen sind im [Windows Server-Migrationsportal](https://go.microsoft.com/fwlink/?LinkId=247608)verfügbar.  
  
### <a name="supported-operating-systems"></a>Unterstützte Betriebssysteme  
 Betriebssystem des Zielservers:  
  
 Windows Server 2012 R2 (Server Core und vollständige Installation)  
  
 Prozessor des Zielservers:  
  
 x64-basiert  
  
|Prozessor des Quellservers|Betriebssystem des Quellservers|  
|-----------------------------|------------------------------------|  
|x86- oder x64-basiert| Windows Server 2008, vollständige Installation und Server Core-Installationsoptionen|  
|x64-basiert|Windows Server 2008 R2|  
|x64-basiert|Server Core-Installationsoption von Windows Server 2008 R2|  
|x64-basiert|Server Core "und" vollständige Installation von Windows Server 2012|  
  
> [!NOTE]
> - Die in der obigen Tabelle aufgeführten Betriebssystemversionen sind die ältesten unterstützten Kombinationen von Betriebssystemen und Service Packs.  
>   -   Die Foundation, Standard, Enterprise und Datacenter-Editionen des Betriebssystems Windows Server werden als die Quelle oder als Zielserver unterstützt.  
>   -   Migrationen zwischen physischen und virtuellen Betriebssystemen werden unterstützt.  
  
### <a name="supported-ad-fs-role-services-and-features"></a>Unterstützte AD FS-Rollendienste und features  
 Die folgende Tabelle beschreibt die Migrationsszenarien der AD FS-Rollendienste und ihre entsprechenden Einstellungen, die in diesem Handbuch beschrieben werden.  
  
|Von|Um AD FS, installiert mit Windows Server 2012 R2|  
|----------|----------------------------------------------------------------------------------------------|  
|AD FS 2.0-Verbundserver installiert unter Windows Server 2008 oder Windows Server 2008 R2|Die Migration auf demselben Server wird unterstützt. Weitere Informationen finden Sie in den folgenden Themen:<br /><br /> [Vorbereiten der Migration des AD FS-Verbundservers](prepare-migrate-ad-fs-server-r2.md)<br /><br /> [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md)|  
|AD FS-Verbundserver installiert unter Windows Server 2012|Die Migration auf demselben Server wird unterstützt.  Weitere Informationen finden Sie unter:<br /><br /> [Vorbereiten der Migration des AD FS-Verbundservers](prepare-migrate-ad-fs-server-r2.md)<br /><br /> [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md)|  
  
## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS-Verbundservers](prepare-migrate-ad-fs-server-r2.md)   
 [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md)   
 [Migrieren des AD FS-Verbundserverproxys](migrate-fed-server-proxy-r2.md)   
 [Überprüfen der AD FS-Migrations zu Windows Server 2012 R2](verify-ad-fs-migration.md)