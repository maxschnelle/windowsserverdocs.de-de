---
title: "Migrieren der Rollendienste für Active Directory Federation Services zu Windows Server 2012 R2"
description: "Enthält Anweisungen zum Migrieren des AD FS-Diensts zu Windows Server 2012 R2."
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 478729a7b6560beba5f04a1a15ad035561ad31f0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012-r2"></a>Migrieren der Rollendienste für Active Directory Federation Services zu Windows Server 2012 R2
 Dieses Dokument enthält Anweisungen zum Migrieren die folgenden Rollendienste zu Active Directory-Verbunddienste (AD FS), die mit Windows Server 2012 R2 installiert ist:  
  
-   AD FS 2.0-Verbundserver installiert unter Windows Server 2008 oder Windows Server 2008 R2  
  
-   AD FS-Verbundservers installiert unter Windows Server 2012  
  
## <a name="supported-migration-scenarios"></a>Unterstützte Migrationsszenarien  
 Die Anweisungen zur Migration in diesem Handbuch umfassen die folgenden Aufgaben:  
  
-   Exportieren der AD FS 2.0-Konfigurationsdaten von Ihrem Server, auf denen Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 ausgeführt wird  
  
-   Ausführen von ein direktes Upgrade des Betriebssystems dieses Servers von Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 für Windows Server 2012 R2. 
  
-   Neuerstellen der ursprünglichen AD FS-Konfiguration und Wiederherstellen der übrigen AD FS-diensteinstellungen auf dem Server, auf dem nun die AD FS-Serverrolle ausgeführt wird, die mit Windows Server 2012 R2 installiert ist.  
  
 Dieses Handbuch enthält keine Anweisungen zum Migrieren eines Servers, das mehrere Rollen ausgeführt werden. Wenn Ihr Server mehrere Rollen ausgeführt wird, wird empfohlen, dass ein benutzerdefiniertes Migrationsverfahren für die serverumgebung anhand der Informationen in anderen Handbüchern für die Migration zu entwickeln. Migrationshandbücher für weitere Rollen sind verfügbar, auf die [Windows Server Migration Portal](https://go.microsoft.com/fwlink/?LinkId=247608).  
  
### <a name="supported-operating-systems"></a>Unterstützte Betriebssysteme  
 Betriebssystem des Zielservers:  
  
 Windows Server 2012 R2 (Server Core und vollständige Installation)  
  
 Prozessor des Zielservers:  
  
 X64-basierte  
  
|Prozessor des Quellservers|Betriebssystem des Quellservers|  
|-----------------------------|------------------------------------|  
|x86- oder x 64-basierte| Windows Server 2008, vollständige Installation und Server Core-Installationsoptionen|  
|X64-basierte|Windows Server2008 R2|  
|X64-basierte|Server Core-Installationsoption von Windows Server 2008 R2|  
|X64-basierte|Server Core-Installation und vollständige Installation von Windows Server 2012|  
  
> [!NOTE]
>  -   Die Versionen der Betriebssysteme, die in der obigen Tabelle aufgeführt sind, werden die ältesten Kombinationen von Betriebssystemen und Servicepacks, die unterstützt werden.  
> -   Die Foundation, Standard, Enterprise und Datacenter-Editionen des Windows Server-Betriebssystems werden als Quell- oder Zielserver unterstützt.  
> -   Migrationen zwischen physischen und virtuellen Betriebssystemen werden unterstützt.  
  
### <a name="supported-ad-fs-role-services-and-features"></a>Unterstützte AD FS-Rollendienste und features  
 Die folgende Tabelle enthält die Migrationsszenarien der AD FS-Rollendienste und die entsprechenden Einstellungen, die in diesem Handbuch beschrieben werden.  
  
|Von|Zu AD FS, installiert mit Windows Server 2012 R2|  
|----------|----------------------------------------------------------------------------------------------|  
|AD FS 2.0-Verbundserver installiert unter Windows Server 2008 oder Windows Server 2008 R2|Die Migration auf demselben Server wird unterstützt. Weitere Informationen finden Sie unter:<br /><br /> [Vorbereiten der Migration des AD FS-Verbundservers](prepare-migrate-ad-fs-server-r2.md)<br /><br /> [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md)|  
|AD FS-Verbundservers installiert unter Windows Server 2012|Die Migration auf demselben Server wird unterstützt.  Weitere Informationen finden Sie unter:<br /><br /> [Vorbereiten der Migration des AD FS-Verbundservers](prepare-migrate-ad-fs-server-r2.md)<br /><br /> [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md)|  
  
## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS-Verbundservers](prepare-migrate-ad-fs-server-r2.md)   
 [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md)   
 [Migrieren des AD FS-Verbundserverproxys](migrate-fed-server-proxy-r2.md)   
 [Überprüfen der AD FS-Migrations zu Windows Server 2012 R2](verify-ad-fs-migration.md)