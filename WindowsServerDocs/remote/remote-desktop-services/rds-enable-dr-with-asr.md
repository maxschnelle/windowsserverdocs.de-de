---
title: Aktivieren der notfallwiederherstellung von RDS mit Azure Site Recovery
description: Erfahren Sie, wie Sie die notfallwiederherstellung von RDS mit Azure Site Recovery aktivieren.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 05/05/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 7aa25602c71e5d114be7ae59c5e3ce168844d700
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446550"
---
# <a name="enable-disaster-recovery-of-rds-using-azure-site-recovery"></a>Aktivieren der notfallwiederherstellung von RDS mit Azure Site Recovery

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2019, WindowsServer 2016

Um sicherzustellen, dass Ihre RDS-Bereitstellung für die notfallwiederherstellung ordnungsgemäß konfiguriert ist, müssen Sie alle Komponenten, aus denen Ihre RDS-Bereitstellung zu schützen:

- Active Directory
- SQL Server-Ebene
- RDS-Komponenten
- Netzwerkkomponenten

## <a name="configure-active-directory-and-dns-replication"></a>Konfigurieren der Active Directory und DNS-Replikation

Sie benötigen eine Active Directory am Standort notfallwiederherstellung für Ihre RDS-Bereitstellung funktioniert. Sie haben zwei Möglichkeiten, die basierend auf der Komplexität die RDS-Bereitstellung ist:

- Option 1: Wenn Sie eine kleine Anzahl von Anwendungen und ein einzelnen Domänencontroller für den gesamten Standorts gleichzeitig, Ihre gesamten lokalen Standort und Failover werden wird verwenden Sie ASR-Replikation zum Replizieren des Domänencontrollers am sekundären Standort ("true" für beide Standort-zu-Standort und Standort-zu-Azure-Szenarien).
- Option 2: Sie haben eine große Anzahl von Anwendungen und führen Sie eine Active Directory-Gesamtstruktur müssen Sie Failover verschiedener Anwendungen zu einem Zeitpunkt, richten Sie einen zusätzlichen Domänencontroller am Standort notfallwiederherstellung (entweder ein sekundärer Standort oder in Azure).

Finden Sie unter [Schützen von Active Directory und DNS mit Azure Site Recovery](/azure/site-recovery/site-recovery-active-directory) ausführliche Informationen zum Verfügbarmachen von eines Domänencontrollers am Standort notfallwiederherstellung. Bei der Rest dieses Leitfadens wird davon ausgegangen, dass Sie diese Schritte befolgt haben und den Domänencontroller zur Verfügung steht.

## <a name="set-up-sql-server-replication"></a>Einrichten von SQL Server-Replikation

Finden Sie unter [Schützen von SQL Server mit SQL Server-Wiederherstellung und Azure Site Recovery](/azure/site-recovery/site-recovery-sql) die Schritte zum Einrichten von SQL Server-Replikation.

## <a name="enable-protection-for-the-rds-application-components"></a>Aktivieren des Schutzes für die RDS-Anwendungskomponenten

Je nach den Typ der RDS-Bereitstellung können Sie Schutz für die andere Komponente-VMs (wie in der folgenden Tabelle aufgeführt) in Azure Site Recovery aktivieren. Konfigurieren Sie die relevante Azure Site Recovery-Elemente, die basierend auf dem, ob Ihre virtuellen Computer auf Hyper-V oder VMWare bereitgestellt werden.


|               Bereitstellungstyp                |                                                                                                     Schutz-Schritte                                                                                                     |
|----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     Persönlicher virtueller Desktop (nicht verwaltet)     | 1. Stellen Sie sicher, dass alle Virtualisierungshosts über den RDVH-Rolle installiert sind.    </br>2. Verbindungsbroker.  </br>3. Persönliche Desktops. </br>4. Gold-Vorlagen-VM. </br>5. Webzugriff, Lizenzserver und Gatewayserver |
| In einem Pool zusammengefassten virtuellen Desktops, die (mit kein Benutzerprofil-Datenträger verwaltet) |                    1. Alle Virtualisierungshosts sind über den RDVH-Rolle installiert.  </br>2. Verbindungsbroker.  </br>3. Gold-Vorlagen-VM. </br>4. Webzugriff, Lizenzserver und Gatewayserver.                    |
|   RemoteApps und Remotedesktopsitzungen (ohne UPD)   |                                                          1. Sitzung hostet.  </br>2. Verbindungsbroker. </br>3. Webzugriff, Lizenzserver und Gatewayserver.                                                           |

