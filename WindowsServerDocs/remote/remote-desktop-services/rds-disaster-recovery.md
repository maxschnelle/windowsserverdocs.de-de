---
title: 'Schützen deiner RDS-Bereitstellung: Notfallwiederherstellung'
description: Hier erfährst du mehr über die Notfallwiederherstellungsoptionen für die Remotedesktopdienste.
ms.topic: article
ms.assetid: 9ff6a3b0-ea14-424e-9524-209252e9f1a8
author: lizap
ms.author: elizapo
ms.date: 06/12/2017
ms.openlocfilehash: e9270c6d1609e67d4875afb2a9ba971de14c1c7c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87936894"
---
# <a name="configure-disaster-recovery-for-remote-desktop-services"></a>Konfigurieren der Notfallwiederherstellung für die Remotedesktopdienste

Wenn du die Remotedesktopdienste (Remote Desktop Services, RDS) in deiner Umgebung bereitstellst, werden diese zu einem entscheidenden Bestandteil deiner Infrastruktur – insbesondere die Apps und Ressourcen, die du für deine Benutzer freigibst. Wenn die RDS-Bereitstellung aus irgendeinem Grund ausfällt – sei es durch einen Netzwerkausfall oder eine Naturkatastrophe –, können Benutzer nicht mehr auf diese Apps und Ressourcen zugreifen, und die Geschäftsabläufe deines Unternehmens sind beeinträchtigt. Um dies zu vermeiden, kannst du eine Lösung zur Notfallwiederherstellung konfigurieren, über die du ein Failover deiner Bereitstellung durchführen kannst: Wenn deine RDS-Bereitstellung – aus welchem Grund auch immer – ausfällt, ist eine Sicherungslösung verfügbar, die automatisch übernehmen kann.

Um den Betrieb deiner RDS-Bereitstellung beim Ausfall einer einzelnen Komponente oder eines einzelnen Computers aufrechtzuerhalten, empfiehlt es sich, die RDS-Bereitstellung für Hochverfügbarkeit zu konfigurieren. Zu diesem Zweck richtest du eine [RDSH-Farm](rds-scale-rdsh-farm.md) ein und stellst sicher, dass deine [Verbindungsbroker im Hinblick auf Hochverfügbarkeit gruppiert sind](rds-connection-broker-cluster.md).

Die hier empfohlene Lösung für die Notfallwiederherstellung dient dazu, deine Bereitstellung bei schwerwiegenden Ausfällen zu schützen, also bei Ereignissen, die dazu führen, dass deine gesamte RDS-Bereitstellung ausfällt (einschließlich für Hochverfügbarkeit konfigurierter redundanter Rollen). Wenn du eine Lösung für die Notfallwiederherstellung in deine Bereitstellung integriert hast, kannst du im Fall eines solchen Ereignisses ein Failover der gesamten Bereitstellung durchführen und Apps und Ressourcen schnell wieder für deine Benutzer in Betrieb nehmen.

Verwende folgende Informationen, um Lösungen für die Notfallwiederherstellung in RDS bereitzustellen:

- [Nutzen mehrerer Azure-Rechenzentren, um den Zugriff auf deine RDS-Bereitstellung durch Benutzer sicherzustellen, auch wenn ein Azure-Rechenzentrum ausfällt (Georedundanz)](rds-multi-datacenter-deployment.md)
- [Bereitstellen von Azure Site Recovery für ein Failover von RDS-Komponenten bei einem Site-to-Site- oder Site-to-Azure-Failover](rds-disaster-recovery-with-azure.md)


