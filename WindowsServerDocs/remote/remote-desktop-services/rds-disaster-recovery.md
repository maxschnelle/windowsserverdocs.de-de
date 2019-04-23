---
title: Schützen Sie Ihre RDS-Bereitstellung – notfallwiederherstellung
description: Erfahren Sie mehr über Ihre Optionen für notfallwiederherstellung für Remote Desktop Services
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9ff6a3b0-ea14-424e-9524-209252e9f1a8
author: lizap
ms.author: elizapo
ms.date: 06/12/2017
ms.openlocfilehash: a6eac3a50999633d15b1b6dc28608f60f6fef6c7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834081"
---
# <a name="configure-disaster-recovery-for-remote-desktop-services"></a>Konfigurieren der notfallwiederherstellung für Remote Desktop Services

Wenn Sie Remote Desktop Services in Ihrer Umgebung bereitstellen, wird es ein wichtiger Bestandteil der Infrastruktur, insbesondere die apps und Ressourcen, die Sie für Benutzer freigeben. Wenn die RDS-Bereitstellung aufgrund von etwas nach einem Netzwerkausfall, einer Naturkatastrophe ausfällt, Benutzer keinen Zugriff auf diese apps und Ressourcen, und Ihr Unternehmen wird beeinträchtigt. Um dies zu vermeiden, können Sie konfigurieren, eine Lösung zur notfallwiederherstellung, die Ihnen, ein Failover Ihrer Bereitstellung ermöglicht – Wenn Ihre RDS-Bereitstellung aus irgendeinem Grund nicht verfügbar ist, besteht eine Sicherung verfügbar ist, automatisch übernehmen.

Damit bleiben Ihre RDS-Bereitstellung ausgeführt wird, bei dem eine einzelne Komponente oder ein Computer ausfällt, wird empfohlen, das Konfigurieren der RDS-Bereitstellung für hochverfügbarkeit. Hierzu können Sie das Einrichten einer [RDSH-Farm](rds-scale-rdsh-farm.md) und stellen Sie sicher Ihre [Verbindungsbroker für hochverfügbarkeit gruppiert werden](rds-connection-broker-cluster.md). 

Die elementarste notfallwiederherstellungslösung, die uns hier empfohlene werden zum Schützen Ihrer Bereitstellung nach schwerwiegenden Notfall - etwas, die Sie die gesamte RDS-Bereitstellung (einschließlich redundante Rollen für hohe Verfügbarkeit konfiguriert) verwendet. Wenn solcher Notfall stößt, werden eine Lösung zur notfallwiederherstellung in Ihrer Bereitstellung integriert können Sie die gesamte Bereitstellung für das Failover und schnell apps und Ressourcen einrichten und ausführen für Ihre Benutzer.

Verwenden Sie die folgende Informationen, um Lösungen für die notfallwiederherstellung in RDS bereitzustellen:

- [Nutzen Sie mehrere Azure-Rechenzentren, um sicherzustellen, dass Benutzer Ihre RDS-Bereitstellung zugreifen können, selbst wenn (Geo-Redundanz) ein Azure-Rechenzentrum ausfällt](rds-multi-datacenter-deployment.md)
- [Bereitstellen von Azure Site Recovery zum Failover für RDS-Komponenten in der Standort-zu-Standort oder Standort-zu-Azure-Failover bereit.](rds-disaster-recovery-with-azure.md)


