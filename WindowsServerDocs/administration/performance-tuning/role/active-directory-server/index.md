---
title: Optimierung der Leistung von Active Directory-Servern
description: Optimierung der Leistung von Active Directory-Servern
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: TimWi; ChrisRob; HerbertM; KenBrumf;  MLeary; ShawnRab; v-tea
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: b8ab1eed003294e3396bcea21b31b7c084180b9c
ms.sourcegitcommit: 02f1e11ba37a83e12d8ffa3372e3b64b20d90d00
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68863449"
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

Die ordnungsgemäße Bereitstellung einer ausreichenden Anzahl von Domänencontrollern in der richtigen Domäne und an den richtigen Orten sowie für Redundanz zu sorgen ist entscheidend, um sicherzustellen, dass Clientanforderungen rechtzeitig verarbeitet werden. Dieses ausführliche Thema überschreitet den Rahmen dieses Handbuchs. Leser sollten sich zu Beginn der Active Directory-Leistungsoptimierung mit den Empfehlungen und Anleitungen in [Kapazitätsplanung für Active Directory Domain Services](capacity-planning-for-active-directory-domain-services.md) vertraut machen.

>[!Important]
> Ordnungsgemäße Konfiguration und Dimensionierung von Active Directory hat wesentliche potenzielle Auswirkungen auf die gesamte System- und Workloadleistung. Leser sollten zu Beginn unbedingt [Kapazitätsplanung für Active Directory Domain Services](capacity-planning-for-active-directory-domain-services.md) lesen.

## <a name="updates-and-evolving-recommendations"></a>Updates und resultierende Empfehlungen

Während der letzten Generationen des Betriebssystems waren enorme Verbesserungen sowohl der Leistungsoptimierung bei Active Directory als auch Clients zu verzeichnen, und diese Bestrebungen dauern unvermindert an. Sie sollten die neuesten Versionen der Plattform bereitstellen, um die Vorteile zu genießen, wie etwa:

- Erhöhte Zuverlässigkeit
- Bessere Leistung
- Bessere Protokollierung und Tools zur Problembehandlung

Allerdings ist uns klar, dass dies zeitintensiv ist, und viele Umgebungen werden in einem Szenario betrieben, wo es unmöglich ist, die aktuelle Plattform zu 100% zu realisieren. Mit einigen Verbesserungen wurden ältere Versionen der Plattform ergänzt, und wir werden weitere hinzufügen.

Du solltest dich kontinuierlich über die neuesten Nachrichten, Anleitungen und bewährten Methoden zur Verwaltung von ADDS informieren und hierzu unseren Teamblog [„Ask the Directory Services Team“](https://techcommunity.microsoft.com/t5/Ask-the-Directory-Services-Team/bg-p/AskDS) (Das Directory Services-Team fragen) verfolgen.

## <a name="see-also"></a>Weitere Informationen

- [Kapazitätsplanung für AD DS](capacity-planning-for-active-directory-domain-services.md)
- [Hardwareaspekte](hardware-considerations.md)
- [Überlegungen zur Speicherauslastung](memory-usage-considerations.md)
- [Überlegungen zu LDAP](ldap-considerations.md)
- [Ordnungsgemäße Platzierung von Domänencontrollern und Überlegungen zum Standort](site-definition-considerations.md)
- [Problembehandlung bezüglich der AD DS-Leistung](troubleshoot.md)  
  
