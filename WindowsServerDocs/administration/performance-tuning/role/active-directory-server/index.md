---
title: Optimierung der Leistung von Active Directory-Servern
description: Optimierung der Leistung von Active Directory-Servern
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: TimWi; ChrisRob; HerbertM; KenBrumf;  MLeary; ShawnRab
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 04c9683c3d14291d5dc2682c6836657313865866
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891941"
---
# <a name="performance-tuning-active-directory-servers"></a>Optimierung der Leistung von Active Directory-Servern

Die Active Directory-Leistungsoptimierung konzentriert sich auf zwei Ziele:
- Active Directory ist optimal konfiguriert, um die Last so effizient wie möglich zu bewältigen
- An Active Directory übermittelte Workloads sollten so effizient wie möglich sein

Dies erfordert die ordnungsgemäße Beachtung von drei separaten Bereichen:
- Ordnungsgemäße Kapazitätsplanung – Sicherstellen, dass ausreichende Hardwareressourcen zur Unterstützung der gegebenen Last vorhanden sind
- Serverseitige Optimierung – Konfigurieren von Domänencontrollern, sodass sie die Last so effizient wie möglich bewältigen
- Optimierung von Active Directory-Client/-Anwendung – Sicherstellen, dass Clients und Anwendungen Active Directory optimal nutzen

## <a name="start-with-capacity-planning"></a>Starten mit Kapazitätsplanung
Die ordnungsgemäße Bereitstellung einer ausreichenden Anzahl von Domänencontrollern in der richtigen Domäne und an den richtigen Orten sowie für Redundanz zu sorgen ist entscheidend, um sicherzustellen, dass Clientanforderungen rechtzeitig verarbeitet werden. Dieses ausführliche Thema überschreitet den Rahmen dieses Handbuchs. Sie sollten sich zu Beginn Ihrer Active Directory-Leistungsoptimierung mit den Empfehlungen und Anleitungen in [Capacity Planning for Active Directory Domain Services](https://go.microsoft.com/fwlink/?LinkId=324566) (Kapazitätsplanung für Active Directory Domain Services) vertraut machen.

>[!Important]
> Ordnungsgemäße Konfiguration und Dimensionierung von Active Directory hat wesentliche potenzielle Auswirkungen auf die gesamte System- und Workloadleistung. Sie sollten zu Beginn unbedingt [Capacity Planning for Active Directory Domain Services](https://go.microsoft.com/fwlink/?LinkId=324566) lesen.

## <a name="updates-and-evolving-recommendations"></a>Updates und resultierende Empfehlungen

Während der letzten Generationen des Betriebssystems waren enorme Verbesserungen sowohl der Leistungsoptimierung bei Active Directory als auch Clients zu verzeichnen, und diese Bestrebungen dauern unvermindert an. Sie sollten die neuesten Versionen der Plattform bereitstellen, um die Vorteile zu genießen, wie etwa:

- Erhöhte Zuverlässigkeit
- Bessere Leistung
- Bessere Protokollierung und Tools zur Problembehandlung

Allerdings ist uns klar, dass dies zeitintensiv ist, und viele Umgebungen werden in einem Szenario betrieben, wo es unmöglich ist, die aktuelle Plattform zu 100% zu realisieren. Mit einigen Verbesserungen wurden ältere Versionen der Plattform ergänzt, und wir werden weitere hinzufügen.

Sie sollten sich kontinuierlich über die neuesten Nachrichten, Anleitungen und bewährten Methoden zur Verwaltung von ADDS informieren und hierzu unseren Teamblog [„Ask the Directory Services Team“](https://blogs.technet.microsoft.com/askds) (Fragen Sie das Directory Services-Team) verfolgen.

## <a name="see-also"></a>Siehe auch
- [Überlegungen zur Hardware](hardware-considerations.md)
- [Überlegungen zu LDAP](ldap-considerations.md)
- [Ordnungsgemäße Platzierung von Domänencontrollern und Überlegungen zum Standort](site-definition-considerations.md)
- [Problembehandlung bezüglich der ADDS-Leistung](troubleshoot.md) 
- [Kapazitätsplanung für Active Directory Domain Services](https://go.microsoft.com/fwlink/?LinkId=324566)
