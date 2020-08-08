---
title: Migrieren von Rollendiensten der Active Directory-Verbunddienste zu Windows Server 2012
description: Enthält Anweisungen zum Migrieren des AD FS Dienstanbieter zu Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.openlocfilehash: abbd51daea374eb4684f5416bed45fb0aaf315d4
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938210"
---
# <a name="migrate-active-directory-federation-services-role-services-to-windows-server-2012"></a>Migrieren von Rollendiensten der Active Directory-Verbunddienste zu Windows Server 2012

Im folgenden finden Sie Anweisungen zum Migrieren der folgenden Rollen Dienste zu Active Directory-Verbunddienste (AD FS) (AD FS) unter Windows Server 2012:

-   Der Windows-Token-basierte Agent für AD FS 1.1 und der Ansprüche unterstützende AD FS 1.1-Agent werden mit Windows Server 2008 oder Windows Server 2008 R2 installiert.

-   Der AD FS 2.0-Verbundserver und der AD FS 2.0-Verbundserverproxy sind unter Windows Server 2008 oder Windows Server 2008 R2 installiert.

## <a name="supported-migration-scenarios"></a>Unterstützte Migrationsszenarien
 Die Migrations Anweisungen enthalten die folgenden Aufgaben:

- Exportieren der AD FS 2.0-Konfigurationsdaten von Ihrem Server, auf dem Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird

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
|x64-basiert|Server Core-Installation von Windows Server 2008 R2|
|x64-basiert|Server Core-und vollständige Installationsoptionen von Windows Server 2012|

> [!NOTE]
> - Die in der obigen Tabelle aufgeführten Betriebssystemversionen sind die ältesten unterstützten Kombinationen von Betriebssystemen und Service Packs.
>   -   Die Foundation-, Standard-, Enterprise- und Datacenter-Editionen des Windows Server-Betriebssystems werden als Quell- oder als Zielserver unterstützt.
>   -   Migrationen zwischen physischen und virtuellen Betriebssystemen werden unterstützt.

### <a name="supported-ad-fs-role-services-and-features"></a>Unterstützte AD FS-Rollendienste und -Features
 In der folgenden Tabelle werden die Migrationsszenarien der AD FS-Rollendienste und ihre entsprechenden, in diesem Handbuch beschriebenen Einstellungen erläutert:

|Von|So AD FS mit Windows Server 2012 installiert|
|----------|-----|
|AD FS 1.0-Verbundserver, installiert mit Windows Server 2003 R2|Migration wird nicht unterstützt|
|AD FS 1.0-Verbundserverproxy, installiert mit Windows Server 2003 R2|Migration wird nicht unterstützt|
|Windows-Token-basierter Agent für AD FS 1.0, installiert mit Windows Server 2003 R2|Migration wird nicht unterstützt|
|Ansprüche unterstützender AD FS 1.1-Agent, installiert mit Windows Server 2003 R2|Migration wird nicht unterstützt|
|AD FS 1.1-Verbundserver, installiert mit Windows Server 2008 oder Windows Server 2008 R2|Migration wird nicht unterstützt|
|AD FS 1.1-Verbundserverproxy, installiert mit Windows Server 2008 oder Windows Server 2008 R2|Migration wird nicht unterstützt|
|Windows-Token-basierter Agent für AD FS 1.1, installiert mit Windows Server 2008 oder Windows Server 2008 R2|Die Migration auf demselben Server wird unterstützt, aber der migrierte Windows-Token-basierte Agent für AD FS funktioniert nur mit einem AD FS 1.1-Verbunddienst, der mit Windows Server 2008 oder Windows Server 2008 R2 installiert wurde. Weitere Informationen finden Sie unter:<p> [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)<p> [Interagieren mit AD FS 1.x](Interoperating-with-AD-FS-1.x.md)|
|Ansprüche unterstützender AD FS 1.1-Agent, installiert mit Windows Server 2008 oder Windows Server 2008 R2|Die Migration auf demselben Server wird unterstützt. Der migrierte Ansprüche unterstützende AD FS 1.1-Agent funktioniert mit Folgendem:<p> AD FS 1.1-Verbunddienst, installiert mit Windows Server 2008 oder Windows Server 2008 R2<p> AD FS 2.0-Verbunddienst, installiert unter Windows Server 2008 oder Windows Server 2008 R2<p> AD FS Verbund Dienst, der mit Windows Server 2012 installiert wurde<p> Weitere Informationen finden Sie unter:<p> [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)<p> [Interagieren mit AD FS 1.x](Interoperating-with-AD-FS-1.x.md)|
|AD FS 2.0-Verbundserver, installiert unter Windows Server 2008 oder Windows Server 2008 R2|Die Migration auf demselben Server wird unterstützt. Weitere Informationen finden Sie unter:<p> [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)<p> [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)|
|AD FS 2.0-Verbundserverproxy, installiert unter Windows Server 2008 oder Windows Server 2008 R2|Die Migration auf demselben Server wird unterstützt.  Weitere Informationen finden Sie unter:<p> [Vorbereiten der Migration des AD FS 2.0-Verbundserverproxys](prepare-to-migrate-ad-fs-fed-proxy.md)<p> [Migrieren des AD FS 2.0-Verbundserverproxys](migrate-the-ad-fs-2-fed-server-proxy.md)|

## <a name="see-also"></a>Weitere Informationen
 [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md) -Verbund Servers [Vorbereiten der Migration des Verbund Server Proxys von AD FS 2,0](prepare-to-migrate-ad-fs-fed-proxy.md) [Migrieren des AD FS 2,0](migrate-the-ad-fs-fed-server.md) Verbund Servers migrieren des [AD FS 2,0](migrate-the-ad-fs-2-fed-server-proxy.md) Verbund Server Proxy [Migrieren der AD FS 1,1-Web-Agents](migrate-the-ad-fs-web-agent.md)