---
title: Übersicht über den Speicher Migrationsdienst
description: Storage Migration Service vereinfacht die Migration von Speicher zu Windows Server oder zu Azure. Es bietet ein grafisches Tool, das Daten auf Windows-und Linux-Servern inventarisiert und die Daten dann auf neuere Server oder virtuelle Azure-Computer überträgt. Storage Migration Service bietet auch die Möglichkeit, die Identität eines Servers auf den Zielserver zu übertragen, sodass apps und Benutzer auf Ihre Daten zugreifen können, ohne dass Links oder Pfade geändert werden müssen.
author: jasongerend
ms.author: jgerend
manager: elizapo
ms.date: 01/17/2020
ms.topic: article
ms.prod: windows-server
ms.technology: storage
ms.openlocfilehash: 1a98de21e91fc7bdc431e7413c44089ce750bc05
ms.sourcegitcommit: 840d1d8851f68936db3934c80796fb8722d3c64a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519472"
---
# <a name="storage-migration-service-overview"></a>Übersicht über den Speicher Migrationsdienst

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server (halbjährlicher Kanal)

Storage Migration Service vereinfacht die Migration von Speicher zu Windows Server oder zu Azure. Es bietet ein grafisches Tool, das Daten auf Windows-und Linux-Servern inventarisiert und die Daten dann auf neuere Server oder virtuelle Azure-Computer überträgt. Storage Migration Service bietet auch die Möglichkeit, die Identität eines Servers auf den Zielserver zu übertragen, sodass apps und Benutzer auf Ihre Daten zugreifen können, ohne dass Links oder Pfade geändert werden müssen.

In diesem Thema wird erläutert, warum Sie Storage Migration Service verwenden möchten, wie der Migrationsprozess funktioniert und welche Anforderungen für Quell-und Zielserver gelten.

## <a name="why-use-storage-migration-service"></a>Gründe für die Verwendung von Storage Migration Service

Verwenden Sie den Speicher Migrationsdienst, weil Sie einen Server (oder viele Server) haben, den Sie zu neueren Hardware oder virtuellen Computern migrieren möchten. Der Speicher Migrationsdienst wurde entwickelt, um Folgendes zu unterstützen:

- Inventarisieren mehrerer Server und der zugehörigen Daten
- Schnelles übertragen von Dateien, Dateifreigaben und Sicherheits Konfigurationen von den Quell Servern
- Übernehmen Sie optional die Identität der Quell Server (auch als "überspringen" bezeichnet), sodass Benutzer und apps nichts ändern müssen, um auf vorhandene Daten zuzugreifen.
- Verwalten einer oder mehrerer Migrationen über die Benutzeroberfläche des Windows Admin Centers

![Das Diagramm zeigt den Speicher Migrationsdienst, der Dateien & Konfiguration von Quell Servern zu Ziel Servern, Azure-VMS oder Azure-Dateisynchronisierung migriert.](media/overview/storage-migration-service-diagram.png)

**Abbildung 1: Quellen und Ziele des Speicher Migrations Dienstanbieter**

## <a name="how-the-migration-process-works"></a>Funktionsweise des Migrationsprozesses

Die Migration ist ein dreistufiger Prozess:

1. **Inventur Server** zum Erfassen von Informationen über Ihre Dateien und die Konfiguration (siehe Abbildung 2).
2. **Übertragen (kopieren) von Daten** von den Quell Servern auf die Zielserver.
3. **Überschneiden Sie die neuen Server** (optional).<br>Die Zielserver übernehmen die früheren Identitäten der Quell Server, damit apps und Benutzer nichts ändern müssen. <br>Die Quell Server wechseln in einen Wartungszustand, in dem Sie immer noch dieselben Dateien enthalten, die Sie immer besitzen (es werden niemals Dateien von den Quell Servern entfernt), sind aber für Benutzer und apps nicht verfügbar. Anschließend können Sie die Server in ihrer freundlichen Zeit außer Betrieb setzen.

![Screenshot, der einen zu scannenden Server anzeigt](media/migrate/inventory.png)
**Abbildung 2: Inventarisierung von Servern durch den Speicher Migrationsdienst**

Im folgenden Video wird gezeigt, wie Sie Storage Migration Service verwenden, um einen Server zu erstellen, z. b. einen Windows Server 2008 R2-Server, der jetzt nicht mehr unterstützt wird, und den Speicher auf einen neueren Server zu verschieben.

> [!VIDEO https://www.youtube.com/embed/h-Xc9j1w144]

## <a name="requirements"></a>Anforderungen

Um Storage Migration Service verwenden zu können, benötigen Sie Folgendes:

- Einen **Quell Server** oder **Failovercluster** zum Migrieren von Dateien und Daten aus
- Ein **Zielserver** , auf dem Windows Server 2019 (gruppiert oder eigenständig) ausgeführt wird, um zu zu migrieren. Windows Server 2016 und Windows Server 2012 R2 funktionieren ebenso gut, sind aber um 50% langsamer.
- Ein **Orchestrator-Server** , auf dem Windows Server 2019 zum Verwalten der Migration ausgeführt wird  <br>Wenn Sie nur wenige Server migrieren und auf einem der Server Windows Server 2019 ausgeführt wird, können Sie diesen als Orchestrator verwenden. Wenn Sie weitere Server migrieren, empfiehlt es sich, einen separaten Orchestrator-Server zu verwenden.
- Ein **PC oder Server, auf dem [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md)**  ausgeführt wird, um die Benutzeroberfläche von Storage Migration Service auszuführen, es sei denn, Sie verwenden lieber PowerShell zum Verwalten der Migration. Die Version Windows Admin Center und Windows Server 2019 muss mindestens Version 1809 aufweisen.

Es wird dringend empfohlen, dass Orchestrator-und Zielcomputer über mindestens zwei Kerne oder zwei vCPUs und mindestens 2 GB Arbeitsspeicher verfügen. Inventur-und Übertragungs Vorgänge werden mit mehr Prozessoren und Arbeitsspeicher erheblich beschleunigt.

### <a name="security-requirements-the-storage-migration-service-proxy-service-and-firewall-ports"></a>Sicherheitsanforderungen, Speicher Migrationsdienst-Proxy Dienst und Firewallports

- Ein Migrations Konto, das Administratorrechte auf den Quell Computern und dem Orchestrator-Computer ist.
- Ein Migrations Konto, bei dem es sich um einen Administrator auf den Ziel Computern und dem Orchestrator-Computer handelt.
- Auf dem Orchestrator-Computer muss die Firewallregel für die Datei-und Druckerfreigabe (SMB-in) *eingehend aktiviert sein*.
- Auf den Quell-und Ziel Computern müssen die folgenden Firewallregeln in *eingehender* Richtung aktiviert sein (obwohl Sie diese möglicherweise bereits aktiviert haben):
  - Datei- und Druckerfreigabe (SMB eingehend)
  - Anmeldedienst (NP-in)
  - Windows Management Instrumentation (DCOM-In)
  - Windows-Verwaltungsinstrumentation (WMI-In)
  
  > [!TIP]
  > Bei der Installation des Speicher Migrationsdienst-Proxy Dienstanbieter auf einem Computer mit Windows Server 2019 werden automatisch die erforderlichen Firewallports auf diesem Computer geöffnet. To do so, connect to the destination server in Windows Admin Center and then go to **Server Manager** (in Windows Admin Center) > **Roles and features**, select **Storage Migration Service Proxy**, and then select **Install**.


- If the computers belong to an Active Directory Domain Services domain, they should all belong to the same forest. The destination server must also be in the same domain as the source server if you want to transfer the source's domain name to the destination when cutting over. Cutover technically works across domains, but the fully-qualified domain name of the destination will be different from the source...

### <a name="requirements-for-source-servers"></a>Requirements for source servers

The source server must run one of the following operating systems:

- Windows Server (halbjährlicher Kanal)
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2
- WindowsServer 2012
- Windows Server 2008 R2
- Windows Server 2008
- Windows Server 2003 R2
- Windows Server 2003
- Windows Small Business Server 2003 R2
- Windows Small Business Server 2008
- Windows Small Business Server 2011
- Windows Server 2012 Essentials
- Windows Server 2012 R2 Essentials
- Windows Server 2016 Essentials
- Windows Server 2019 Essentials
- Windows Storage Server 2008
- Windows Storage Server 2008 R2
- Windows Storage Server 2012
- Windows Storage Server 2012 R2
- Windows Storage Server 2016

Note: Windows Small Business Server and Windows Server Essentials are domain controllers. Storage Migration Service can't yet cut over from domain controllers, but can inventory and transfer files from them.   

You can migrate the following additional source types if the orchestrator is running Windows Server, version 1903 or later, or if the orchestrator is running an earlier version of Windows Server with [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) installed:

- Failover clusters running Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, Windows Server 2019
- Linux servers that use Samba. We've tested the following:
    - CentOS 7
    - Debian GNU/Linux 8
    - RedHat Enterprise Linux 7.6
    - SUSE Linux Enterprise Server (SLES) 11 SP4
    - Ubuntu 16.04 LTS and 12.04.5 LTS
    - Samba 4.8, 4.7, 4.3, 4.2, and 3.6

### <a name="requirements-for-destination-servers"></a>Requirements for destination servers

The destination server must run one of the following operating systems:

- Windows Server (halbjährlicher Kanal)
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2

> [!TIP]
> Destination servers running Windows Server 2019 or Windows Server, Semi-Annual Channel or later have double the transfer performance of earlier versions of Windows Server. This performance boost is due to the inclusion of a built-in Storage Migration Service proxy service, which also opens the necessary firewall ports if they're not already open.

## <a name="whats-new-in-storage-migration-service"></a>What's new in Storage Migration Service

The following new features are available when running the Storage Migration Server orchestrator on Windows Server, version 1903 or later, or an earlier version of Windows Server with [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) installed:

- Migrieren lokaler Benutzer und Gruppen zum neuen Server
- Migrate storage from failover clusters, migrate to failover clusters, and migrate between standalone servers and failover clusters
- Migrieren von Speicher von einem Linux-Server, der Samba verwendet
- Vereinfachte Synchronisierung von migrierten Freigaben zu Azure mithilfe von Azure-Dateisynchronisierung
- Migrieren zu neuen Netzwerken wie etwa Azure

## <a name="see-also"></a>Weitere Informationen:

- [Migrate a file server by using Storage Migration Service](migrate-data.md)
- [Storage Migration Services frequently asked questions (FAQ)](faq.md)
- [Storage Migration Service known issues](known-issues.md)
