---
title: Übersicht über den Speicher Migrationsdienst
description: Mit dem Speichermigrationsdienst können Server einfacher zu einer neueren Version von Windows Server migriert werden. Er bietet ein grafisches Tool, das Daten auf Servern inventarisiert und anschließend die Daten und die Konfiguration auf neuere Server überträgt – ganz ohne Apps oder die Notwendigkeit für Benutzer, irgendetwas zu ändern.
author: jasongerend
ms.author: jgerend
manager: elizapo
ms.date: 08/16/2019
ms.topic: article
ms.prod: windows-server
ms.technology: storage
ms.openlocfilehash: 022b0c3445c007960c490159f6580a702233ee41
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402976"
---
# <a name="storage-migration-service-overview"></a>Übersicht über den Speicher Migrationsdienst

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server (halbjährlicher Kanal)

Mit dem Speichermigrationsdienst können Server einfacher zu einer neueren Version von Windows Server migriert werden. Er bietet ein grafisches Tool, das Daten auf Servern inventarisiert und anschließend die Daten und die Konfiguration auf neuere Server überträgt – ganz ohne Apps oder die Notwendigkeit für Benutzer, irgendetwas zu ändern.

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
3. **An die neuen Server über** springen (optional).<br>Die Zielserver übernehmen die früheren Identitäten der Quell Server, damit apps und Benutzer nichts ändern müssen. <br>Die Quell Server wechseln in einen Wartungszustand, in dem Sie immer noch dieselben Dateien enthalten, die Sie immer besitzen (es werden niemals Dateien von den Quell Servern entfernt), sind aber für Benutzer und apps nicht verfügbar. Anschließend können Sie die Server in ihrer freundlichen Zeit außer Betrieb setzen.

![Screenshot, der einen zu überprüfenden](media/migrate/inventory.png)
**Server anzeigt Abbildung 2: Speicher Migrationsdienst-Inventur Server**

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
  - Windows-Verwaltungsinstrumentation (DCOM-in)
  - Windows-Verwaltungsinstrumentation (WMI-In)
  
  > [!TIP]
  > Bei der Installation des Speicher Migrationsdienst-Proxy Dienstanbieter auf einem Computer mit Windows Server 2019 werden automatisch die erforderlichen Firewallports auf diesem Computer geöffnet. Stellen Sie hierzu im Windows Admin Center eine Verbindung mit dem Zielserver her, und navigieren Sie dann zu **Server-Manager** (im Windows Admin Center) > **Rollen und Features**, wählen Sie **Speicher Migrationsdienst-Proxy**aus, und klicken Sie dann auf **Installieren**.


- Wenn die Computer zu einer Active Directory Domain Services Domäne gehören, sollten Sie alle zur selben Gesamtstruktur gehören. Der Zielserver muss sich auch in derselben Domäne befinden wie der Quell Server, wenn Sie beim überspringen den Domänen Namen der Quelle an das Ziel übertragen möchten. Die Umstellung erfolgt in technischer Hinsicht über Domänen übergreifend, aber der voll qualifizierte Domänen Name des Ziels unterscheidet sich von der Quelle...

### <a name="requirements-for-source-servers"></a>Anforderungen für Quell Server

Auf dem Quell Server muss eines der folgenden Betriebssysteme ausgeführt werden:

- Windows Server (halbjährlicher Kanal)
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2
- WindowsServer 2008
- Windows Server 2003 R2
- Windows Server 2003
- Windows Small Business Server 2003 R2
- Windows Small Business Server 2008
- Windows Small Business Server 2011
- Windows Server 2012 Essentials
- Windows Server 2012 R2 Essentials
- Windows Server 2016 Essentials
- Windows Server 2019 Essentials

Hinweis: Windows Small Business Server und Windows Server Essentials sind Domänen Controller. Der Speicher Migrationsdienst kann noch nicht von Domänen Controllern entfernt werden, kann jedoch Dateien inventarisieren und übertragen.   

Sie können die folgenden zusätzlichen Quell Typen migrieren, wenn der Orchestrator unter Windows Server, Version 1903 oder höher, ausgeführt wird, oder wenn der Orchestrator eine frühere Version von Windows Server mit installiertem [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) ausgeführt hat:

- Failovercluster
- Linux-Server, die Samba verwenden. Wir haben Folgendes getestet:
    - CentOS 7
    - Debian GNU/Linux 8
    - RedHat Enterprise Linux 7,6
    - SUSE Linux Enterprise Server (SLES) 11 SP4
    - Ubuntu 16,04 LTS und 12.04.5 LTS
    - Samba 4,8, 4,7, 4,3, 4,2 und 3,6

### <a name="requirements-for-destination-servers"></a>Anforderungen für Zielserver

Auf dem Zielserver muss eines der folgenden Betriebssysteme ausgeführt werden:

- Windows Server (halbjährlicher Kanal)
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2

> [!TIP]
> Zielserver, auf denen Windows Server 2019 oder Windows Server, ein halbjährlicher Kanal oder höher ausgeführt wird, haben eine doppelte Übertragungsleistung früherer Versionen von Windows Server. Diese Leistungssteigerung ist auf die Einbindung eines integrierten Speicher Migrationsdienst-Proxy Dienstanbieter zurückzuführen, der auch die erforderlichen Firewallports öffnet, sofern diese noch nicht geöffnet sind.

## <a name="whats-new-in-storage-migration-service"></a>Neuerungen bei Storage Migration Service

Die folgenden neuen Funktionen sind verfügbar, wenn Sie den Speicher Migrations Server-Orchestrator unter Windows Server, Version 1903 oder höher oder eine frühere Version von Windows Server mit installierter [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) ausführen:

- Migrieren lokaler Benutzer und Gruppen zum neuen Server
- Migrieren von Speicher von Failoverclustern, Migrieren zu Failoverclustern und Migrieren zwischen eigenständigen Servern und Failoverclustern
- Migrieren von Speicher von einem Linux-Server, der Samba verwendet
- Vereinfachte Synchronisierung von migrierten Freigaben zu Azure mithilfe von Azure-Dateisynchronisierung
- Migrieren zu neuen Netzwerken wie etwa Azure

## <a name="see-also"></a>Siehe auch

- [Migrieren eines Dateiservers mithilfe von Storage Migration Service](migrate-data.md)
- [Häufig gestellte Fragen (FAQ) zu Storage Migration Services](faq.md)
- [Bekannte Probleme bei Storage Migration Service](known-issues.md)
