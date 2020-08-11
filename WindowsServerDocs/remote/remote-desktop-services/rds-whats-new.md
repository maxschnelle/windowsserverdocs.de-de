---
title: Neues in den Remotedesktopdiensten
description: Enthält eine Beschreibung neuer RDS-Features in Windows Server 2016.
ms.author: chrimo
ms.date: 10/11/2016
ms.topic: article
ms.assetid: 04d52dff-e61b-4633-9908-be8600abc2ba
author: ChristianMontoya
manager: scottman
ms.openlocfilehash: 2048b78e17b4888492e252fb4b5454f9428a5e34
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961594"
---
# <a name="whats-new-in-remote-desktop-services"></a>Neues in den Remotedesktopdiensten

Remotedesktopdienste (Remote Desktop Services, RDS) basieren auf Windows Server 2016 und sind eine Virtualisierungsplattform für ein breites Spektrum von Kundenszenarien. An der Verbesserung der RDS-Lösung sind neben dem Remotedesktopteam auch andere Technologiepartner bei Microsoft beteiligt. Die folgenden Szenarien und Technologien wurden in Windows Server 2016 neu hinzugefügt oder verbessert.

Sieh dir dazu auch das folgende Video von der Ignite 2016 an: [Harness RDS improvements in Windows Server 2016](https://channel9.msdn.com/Events/Ignite/2016/BRK3098) (Nutzen von RDS-Verbesserungen in Windows Server 2016). In diesem Video geht das Produktteam auf alle neuen und verbesserten Features der Remotedesktopdienste ein (einschließlich vGPU-Unterstützung).

## <a name="app-compatibility---windows-server-2016-and-windows-10"></a>App-Kompatibilität: Windows Server 2016 und Windows 10
Windows Server 2016 hat das gleiche Fundament wie Windows 10, wodurch es so aussieht und sich so verhält, wie du es von einem Desktop erwartest. Darüber hinaus können damit größtenteils die gleichen Anwendungen ausgeführt werden. In Kombination mit den Grafikfunktionen (weiter unten) bietet Windows Server 2016 eine Umgebung, in der alle Benutzer produktiv arbeiten können.

## <a name="azure-sql-database---the-new-database-for-your-highly-available-environment"></a>Azure SQL-Datenbank: die neue Datenbank für eine hoch verfügbare Umgebung
Der Remotedesktop-Verbindungsbroker kann alle Bereitstellungsinformationen (wie etwa Verbindungszustände und Benutzer-/Hostzuordnungen) in einer gemeinsam genutzten SQL-Datenbank speichern – beispielsweise in einer Azure SQL-Datenbank. Vergiss das Bereitstellungshandbuch für SQL Server-Always On-Verfügbarkeitsgruppen, schnapp dir die Verbindungszeichenfolge für die Azure SQL-Datenbank, und nutze deine hoch verfügbare Umgebung.

Weitere Informationen: [New Windows Server 2016 Capability: Use Azure SQL DB for your Remote Desktop Connection Broker high availability en...](https://techcommunity.microsoft.com/t5/microsoft-security-and/new-windows-server-2016-capability-use-azure-sql-db-for-your/ba-p/249787) (Neue Windows Server 2016-Funktion: Verwenden von Azure SQL-Datenbank für deine Hochverfügbarkeitsumgebung mit dem Remotedesktop-Verbindungsbroker)

## <a name="graphics---solving-graphics-needs-across-various-scenarios"></a>Grafik: Erfüllung der Grafikanforderungen verschiedenster Szenarien
Dank der diskreten Gerätezuweisung von Hyper-V kannst du nun GPUs auf einem Hostcomputer direkt einem virtuellen Computer zuordnen, damit sie von dessen Anwendungen mit GPU-Bedarf genutzt werden können. Die RemoteFX-vGPU unterstützt nun OpenGL 4.4, OpenCL 1.1, 4K-Auflösung und virtuelle Windows Server-Computer.

Weitere Informationen: [Diskrete Gerätezuweisung](https://techcommunity.microsoft.com/t5/virtualization/bg-p/Virtualization)

## <a name="rd-connection-broker---improved-connection-handling-during-logon-storms"></a>RD-Verbindungsbroker: verbesserte Verbindungsverarbeitung bei hohem Anmeldeaufkommen
Dank der verbesserten Verbindungsverarbeitung kann der RD-Verbindungsbroker nun mehr als 10.000 gleichzeitige Anmeldeanforderungen verarbeiten und kommt somit auch mit Anmeldespitzen zurecht. Der verbesserte RD-Verbindungsbroker vereinfacht auch die Wartung der Bereitstellung, da Server schneller wieder der Umgebung hinzugefügt werden können.

Weitere Informationen: [Improved Remote Desktop Connection Broker Performance with Windows Server 2016 and Windows Server 2012 R2 Hotfix](https://techcommunity.microsoft.com/t5/microsoft-security-and/improved-remote-desktop-connection-broker-performance-with/ba-p/249559) (Leistungsverbesserung für den Remotedesktop-Verbindungsbroker mit Hotfix für Windows Server 2016 and Windows Server 2012 R2)

## <a name="rdp-10---new-capabilities-built-into-the-protocol"></a>RDP 10: neue, in das Protokoll integrierte Funktionen
RDP 10 verwendet jetzt den H.264/AVC 444-Codec zur angemessenen Optimierung von Videos und Text. Ab diesem Release wird auch die Verwendung eines Stifts in Remotedesktopsitzungen unterstützt. Mit diesen Funktionen kommen deine Remotesitzungen noch näher an eine lokale Sitzung heran.

Weitere Informationen: [Remote Desktop Protocol (RDP) 10 AVC/H.264 improvements in Windows 10 and Windows Server 2016 Technical Preview](https://techcommunity.microsoft.com/t5/microsoft-security-and/remote-desktop-protocol-rdp-10-avc-h-264-improvements-in-windows/ba-p/249588) (RDP 10 (Remotedesktopprotokoll): AVC/H.264-Verbesserungen in Windows 10 und Windows Server 2016)

## <a name="personal-session-desktops---providing-individual-desktops-to-any-end-user"></a>Persönliche Sitzungsdesktops: individuelle Desktops für jeden Endbenutzer
Persönliche Sitzungsdesktops sind eine neue Möglichkeit zum Hosten eigener persönlicher Desktops in der Cloud. Administratorrechte und dedizierte Sitzungshosts tragen zur Vereinfachung von Hostingumgebungen bei und ermöglichen es den Benutzern, den Desktop wie ihren eigenen zu verwalten.

Weitere Informationen: [Verwenden von persönlichen Sitzungsdesktops mit Remotedesktopdiensten](rds-personal-session-desktops.md)
