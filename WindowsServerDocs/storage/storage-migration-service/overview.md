---
Title: Übersicht über Storage-Migration Service
description: Storage-Migration-Dienst erleichtert es, für die Migration der Server auf eine neuere Version von Windows Server. Es bietet ein grafisches Tool, die inventarisiert, die Daten auf Servern und dann die Daten und die Konfiguration auf neueren Servern übertragen – alles ohne Anwendungen oder Benutzer Änderungen vornehmen müssen.
author: jasongerend
ms.author: jgerend
manager: elizapo
ms.date: 05/21/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: ce4cbdc291d98a180ee6f5b597d322620fa1b19f
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66453171"
---
# <a name="storage-migration-service-overview"></a>Übersicht über Storage-Migration Service

>Gilt für: WindowsServer 2019, Windows Server 2016, Windows Server 2012 R2, WindowsServer (Halbjährlicher Kanal)

Storage-Migration-Dienst erleichtert es, für die Migration der Server auf eine neuere Version von Windows Server. Es bietet ein grafisches Tool, die inventarisiert, die Daten auf Servern und dann die Daten und die Konfiguration auf neueren Servern übertragen – alles ohne Anwendungen oder Benutzer Änderungen vornehmen müssen.

In diesem Thema wird erläutert, warum Sie Storage-Migration-Dienst verwenden möchten, wie während der Migration funktioniert und was die Anforderungen für die Quell-und Zielserver sind.

## <a name="why-use-storage-migration-service"></a>Gründe für die Verwendung Storage Migration-Dienst

Verwenden Sie Storage-Migration-Dienst, da Sie haben einen Server (oder viele Server), die Sie zu neuer Hardware oder virtuellen Computern migrieren möchten. Storage-Migration-Dienst soll helfen, indem Sie wie folgt vorgehen:

- Inventarisieren Sie mehrere Server und ihre Daten
- Schnell übertragen von Dateien, Dateifreigaben und Security-Konfiguration aus der Quellserver
- Optional, damit Benutzer und apps keine Änderungen vornehmen, für den Zugriff auf vorhandene Daten haben Sie die Identität der Source Server (auch bekannt als Ausschneiden über)
- Verwalten Sie eine oder mehrere Migrationen über die Benutzeroberfläche von Windows Admin Center

![Das Diagramm zeigt die Speicherdienst-Migration Migrieren von Dateien und die Konfiguration vom Quellserver auf den Zielserver, Azure-VMs und Azure File Sync.](media/overview/storage-migration-service-diagram.png)

**Abbildung 1: Speicherung Datenbankmigrationsdienst Quellen und Ziele**

## <a name="how-the-migration-process-works"></a>Wie funktioniert während der migration

Migration ist ein dreistufiger Prozess:

1. **Inventarisieren von Servern** zum Sammeln von Informationen zu den Dateien und die Konfiguration (siehe Abbildung 2).
2. **Übertragen von Daten (Kopieren)** aus den Quellservern, auf dem Zielserver.
3. **Zu den neuen Servern Übernahme** (optional).<br>Dem Zielserver davon aus der Quelle Server frühere Identitäten, damit apps und Benutzer keine Änderungen vornehmen. <br>Der Quellserver Geben Sie in einem Wartungszustand, in dem sie immer noch die gleichen enthalten, Dateien, die bislang (wir nie Dateien entfernen aus der Quellserver), aber nicht für Benutzer und apps verfügbar sind. Sie können dann die Server nach Wunsch außer Betrieb setzen.

![Screenshot mit einem Server bereit, die überprüft werden](media/migrate/inventory.png)
**Abbildung 2: Speicherung Datenbankmigrationsdienst Inventarisierung von Servern**

## <a name="requirements"></a>Anforderungen

Um Speicherung Datenbankmigrationsdienst verwenden zu können, benötigen Sie Folgendes:

- Ein **Quellserver** zum Migrieren von Dateien und Daten aus
- Ein **Zielserver** unter Windows Server-2019 zu migrieren – Windows Server 2016 und Windows Server 2012 R2, gut geeignet, aber sind ca. 50 % langsamer
- Ein **Orchestrator-Server** unter Windows Server-2019 zum Verwalten der Migrations  <br>Wenn Sie nur ein paar Server migrieren, und einen der Server die Windows Server-2019 ausgeführt wird, können Sie, die als Orchestrator. Wenn Sie weitere Server migrieren, wird empfohlen, mit einem separaten OrchestratorServer.
- Ein **PC oder Server mit [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md)**  die Benutzeroberfläche für die Speicherung Datenbankmigrationsdienst, ausgeführt werden, es sei denn, Sie mithilfe von PowerShell zum Verwalten der Migrations möchten. Die Version des Windows Admin Center und Windows Server-2019 müssen mindestens Version 1809.

Es wird dringend empfohlen, die der Orchestrator und dem Ziel Computer verfügen über mindestens zwei Kerne oder zwei vCPUs und über mindestens 2 GB Arbeitsspeicher. Inventar und Übertragung sind wesentlich schneller mit mehr Prozessoren und Arbeitsspeicher.

### <a name="security-requirements"></a>Sicherheitsanforderungen

- Eine Migrationskonto, das ein Administrator auf dem Quellcomputer und dem Orchestrator-Computer ist.
- Eine Migrationskonto, das ein Administrator auf dem Zielcomputer und dem Orchestrator-Computer ist.
- Der Orchestrator-Computer müssen die Datei- und Druckerfreigabe (SMB eingehend) aktivierte Firewallregel *eingehende*.
- Die Quelle und Ziel-Computer müssen die folgenden Firewallregeln aktiviert *eingehende* (auch wenn Sie bereits diese aktiviert haben können):
  - Datei- und Druckerfreigabe (SMB eingehend)
  - Der Netlogon-Dienst (NP eingehend)
  - Windows-Verwaltungsinstrumentation (DCOM-in)
  - Windows-Verwaltungsinstrumentation (WMI-In)
  
  > [!TIP]
  > Den Proxydienst von Storage Migration-Dienst automatisch auf einem 2019 für Windows Server-Computer installieren, wird die erforderlichen Firewallports auf diesem Computer geöffnet.
- Wenn die Computer einer Active Directory Domain Services-Domäne gehören, sollten sie alle zur selben Gesamtstruktur gehören. Der Zielserver muss auch in der gleichen Domäne wie der Quellserver sein, wenn Sie den Domänennamen von der Quelle in die Zieldatenbank übertragen werden, wenn über ausschneiden möchten. Aus technischer Sicht Umstellung funktioniert, domänenübergreifend, aber der vollqualifizierten Domänennamen des Ziels unterscheiden sich von der Quelle...

### <a name="requirements-for-source-servers"></a>Anforderungen für den Quellserver

Der Quellserver muss es sich um eines der folgenden Betriebssysteme ausgeführt:

- WindowsServer Halbjährlicher Kanal
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2
- WindowsServer 2008
- Windows Server 2003 R2
- Windows Server 2003

Wenn der Orchestrator 1903 oder höher, Windows Server ausgeführt wird, können Sie die folgenden Typen von zusätzlichen Quell-migrieren:

- Failovercluster
- Linux-Server, die Samba verwenden. Wir haben die folgenden getestet:
    - RedHat Enterprise Linux 7.6, CentOS 7, Debian 8, Ubuntu 16.04 and 12.04.5, SUSE Linux Enterprise Server (SLES) 11 SP4
    - Samba 4.x, 3.6.x

### <a name="requirements-for-destination-servers"></a>Anforderungen für den Zielserver

Der Zielserver muss es sich um eines der folgenden Betriebssysteme ausgeführt:

- WindowsServer Halbjährlicher Kanal
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2

> [!TIP]
> Der Zielserver unter Windows Server-2019 oder Windows Server, haben Halbjährlicher Kanal 1809 oder höher doppelte die übertragungsleistung früherer Versionen von Windows Server. Diese Leistungssteigerung wurde für den integrierten Speicherung Datenbankmigrationsdienst Proxydienst, der wird auch die erforderlichen Firewall geöffnet werden, die Ports, wenn sie nicht bereits sind öffnen.

## <a name="whats-new-in-storage-migration-service"></a>Neuerungen im Storage-Migration-Dienst

Windows Server-Version 1903 fügt die folgenden neuen Features, die bei Ausführung auf dem Orchestrator-Server:

- Migrieren Sie lokale Benutzer und Gruppen mit dem neuen server
- Migrieren des Speichers von Failoverclustern
- Migrieren des Speichers von einem Linux-Server, der Samba verwendet
- Synchronisieren Sie leichter migrierte Dateifreigaben in Azure mithilfe von Azure File Sync
- Migrieren Sie zu neuen wie z. B. Azure-Netzwerken

## <a name="see-also"></a>Siehe auch

- [Migrieren eines Dateiservers mit Storage-Migration-Dienst](migrate-data.md)
- [Storage Migration Services: häufig gestellte Fragen (FAQ)](faq.md)
- [Speicherung Datenbankmigrationsdienst bekannte Probleme](known-issues.md)
