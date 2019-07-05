---
title: Aktivieren der Notfallwiederherstellung von RDS mithilfe von Azure Site Recovery
description: Hier erfährst du, wie du die Notfallwiederherstellung von RDS mithilfe von Azure Site Recovery aktivierst.
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
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "66446550"
---
# <a name="enable-disaster-recovery-of-rds-using-azure-site-recovery"></a>Aktivieren der Notfallwiederherstellung von RDS mithilfe von Azure Site Recovery

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Um sicherzustellen, dass deine RDS-Bereitstellung hinreichend für die Notfallwiederherstellung konfiguriert ist, musst du alle Komponenten deiner RDS-Bereitstellung schützen:

- Active Directory
- SQL Server-Ebene
- RDS-Komponenten
- Netzwerkkomponenten

## <a name="configure-active-directory-and-dns-replication"></a>Konfigurieren von Active Directory und DNS-Replikation

Du benötigst Active Directory am Notfallwiederherstellungsstandort, damit deine RDS-Bereitstellung funktioniert. Du hast basierend auf der Komplexität deiner RDS-Bereitstellung zwei Möglichkeiten:

- Option 1: Wenn du eine geringe Anzahl von Anwendungen und einen einzelnen Domänencontroller für deinen gesamten lokalen Standort besitzt und ein Failover für den ganzen Standort ausführst, verwende die ASR-Replikation für das Replizieren des Domänencontrollers am sekundären Standort. (Dies gilt sowohl für Site-to-Site-Szenarien als auch für Site-to-Azure-Szenarien).
- Option 2: Wenn du über eine große Anzahl von Anwendungen und eine Active Directory-Gesamtstruktur verfügst und jeweils nur für wenige Anwendungen ein Failover ausführst, richte einen zusätzlichen Domänencontroller am Notfallwiederherstellungsstandort (sekundärer Standort oder in Azure) ein.

Ausführliche Informationen zum Verfügbarmachen eines Domänencontrollers am Notfallwiederherstellungsstandort findest du unter [Einrichten der Notfallwiederherstellung für Active Directory und DNS](/azure/site-recovery/site-recovery-active-directory). In der übrigen Anleitung wird davon ausgegangen, dass du diese Schritte ausgeführt hast und der Domänencontroller verfügbar ist.

## <a name="set-up-sql-server-replication"></a>Einrichten der SQL Server-Replikation

Schritte zum Einrichten der SQL Server-Replikation findest du unter [Einrichten der Notfallwiederherstellung für SQL Server](/azure/site-recovery/site-recovery-sql).

## <a name="enable-protection-for-the-rds-application-components"></a>Aktivieren des Schutzes für die RDS-Anwendungskomponenten

Abhängig vom Typ deiner RDS-Bereitstellung kannst du in Azure Site Recovery den Schutz virtueller Computer für verschiedene Komponenten aktivieren (siehe Tabelle weiter unten). Konfiguriere die relevanten Azure Site Recovery-Elemente basierend darauf, ob deine virtuellen Computer unter Hyper-V oder VMWare bereitgestellt werden.


|               Bereitstellungstyp                |                                                                                                     Schritte für den Schutz                                                                                                     |
|----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     Persönlicher virtueller Desktop (nicht verwaltet)     | 1. Stelle sicher, dass alle Virtualisierungshosts bereit sind und die RDVH-Rolle installiert ist.    </br>2. Verbindungsbroker  </br>3. Persönliche Desktops </br>4. Virtueller Computer mit Gold-Vorlage </br>5. Webzugriff, Lizenzserver und Gatewayserver |
| Virtueller Desktop in einem Pool (ohne UPD verwaltet) |                    1. Alle Virtualisierungshosts sind bereit, und die RDVH-Rolle ist installiert.  </br>2. Verbindungsbroker  </br>3. Virtueller Computer mit Gold-Vorlage </br>4. Webzugriff, Lizenzserver und Gatewayserver                    |
|   RemoteApps und Desktopsitzungen (ohne UPD)   |                                                          1. Sitzungshosts  </br>2. Verbindungsbroker </br>3. Webzugriff, Lizenzserver und Gatewayserver                                                           |

