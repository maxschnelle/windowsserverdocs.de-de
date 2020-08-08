---
title: Migrieren von Rollendiensten der Active Directory-Verbunddienste (AD FS) zu Windows Server 2012 R2
description: Enthält Anweisungen zum Migrieren des AD FS Dienstanbieter zu Windows Server 2012 R2.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.openlocfilehash: 49c75fadcbc1284f23b490eb6ee48813ef40f781
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970907"
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012-r2"></a>Migrieren von Rollendiensten der Active Directory-Verbunddienste (AD FS) zu Windows Server 2012 R2
 Dieses Dokument enthält Anweisungen zum Migrieren der folgenden Rollen Dienste zu Active Directory-Verbunddienste (AD FS) (AD FS), der mit Windows Server 2012 R2 installiert wird:

-   AD FS 2.0-Verbundserver, installiert unter Windows Server 2008 oder Windows Server 2008 R2

-   AD FS-Verbundserver, installiert unter Windows Server 2012

## <a name="supported-migration-scenarios"></a>Unterstützte Migrationsszenarien
 Die Anweisungen zur Migration in diesem Handbuch beinhalten die folgenden Aufgaben:

- Exportieren der AD FS 2.0-Konfigurationsdaten von Ihrem Server, auf dem Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 ausgeführt wird

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
|x64-basiert|Server Core-Installation von Windows Server 2008 R2|
|x64-basiert|Server Core-und vollständige Installationsoptionen von Windows Server 2012|

> [!NOTE]
> - Die in der obigen Tabelle aufgeführten Betriebssystemversionen sind die ältesten unterstützten Kombinationen von Betriebssystemen und Service Packs.
>   -   Die Foundation-, Standard-, Enterprise- und Datacenter-Editionen des Windows Server-Betriebssystems werden als Quell- oder als Zielserver unterstützt.
>   -   Migrationen zwischen physischen und virtuellen Betriebssystemen werden unterstützt.

### <a name="supported-ad-fs-role-services-and-features"></a>Unterstützte AD FS-Rollendienste und -Features
 In der folgenden Tabelle werden die Migrationsszenarien der AD FS-Rollendienste und ihre entsprechenden, in diesem Handbuch beschriebenen Einstellungen erläutert:

|Von|So AD FS mit Windows Server 2012 R2 installiert|
|----------|----------------------------------------------------------------------------------------------|
|AD FS 2.0-Verbundserver, installiert unter Windows Server 2008 oder Windows Server 2008 R2|Die Migration auf demselben Server wird unterstützt. Weitere Informationen finden Sie unter:<p> [Vorbereiten der Migration des AD FS-Verbundservers](prepare-migrate-ad-fs-server-r2.md)<p> [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md)|
|AD FS-Verbundserver, installiert unter Windows Server 2012|Die Migration auf demselben Server wird unterstützt.  Weitere Informationen finden Sie unter:<p> [Vorbereiten der Migration des AD FS-Verbundservers](prepare-migrate-ad-fs-server-r2.md)<p> [Migrieren des AD FS-Verbundservers](migrate-ad-fs-fed-server-r2.md)|

## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS Verbund Servers migrieren](prepare-migrate-ad-fs-server-r2.md) des [AD FS](migrate-ad-fs-fed-server-r2.md) Verbund Servers migrieren des AD FS Verbund Server [Proxy](migrate-fed-server-proxy-r2.md) [Überprüfen der AD FS Migration zu Windows Server 2012 R2](verify-ad-fs-migration.md)