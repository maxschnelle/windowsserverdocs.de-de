---
ms.assetid: 64142026-07b5-4601-840a-c8dcf6ab9814
title: Erstellen eines Entwurfs für Standortverknüpfungsbrücken
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4a194aa2fe2594c518d310cd86549945487d101e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813991"
---
# <a name="creating-a-site-link-bridge-design"></a>Erstellen eines Entwurfs für Standortverknüpfungsbrücken

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Eine Standortverknüpfungsbrücke verbindet zwei oder mehr Standort verknüpft und ermöglicht die Transitivität zwischen standortverknüpfungen. Jede standortverknüpfung in einer Bridge muss es sich um einen Standort enthält, die auch einen anderen Standort-Link in der Bridge verfügen. Die Konsistenzprüfung (KCC) verwendet die Informationen für jede standortverknüpfung, um die Kosten für die Replikation zwischen Standorten in einer standortverknüpfung und Standorte in der anderen standortverknüpfungen, die von der Bridge zu berechnen. Ohne die das Vorhandensein von einem gemeinsamen Standort zwischen standortverknüpfungen kann die konsistenzprüfung (KCC) auch direkte Verbindungen zwischen Domänencontrollern am Standort herstellen, die durch die gleichen Standortverknüpfungsbrücke verbunden sind.  
  
Standardmäßig sind alle standortverknüpfungen transitiv. Es wird empfohlen, die Sie durch die Änderung nicht auf des Standardwerts Transitivität halten **überbrücken aller standortverknüpfungen** (standardmäßig aktiviert). Sie müssen jedoch deaktivieren **überbrücken aller standortverknüpfungen** und ein Entwurfs für standortverknüpfungen Bridge abgeschlossen, wenn:  

- Ihre IP-Netzwerk ist nicht vollständig weitergeleitet. Wenn Sie deaktivieren **überbrücken aller standortverknüpfungen**, alle standortverknüpfungen gelten nicht transitiv, und Sie können erstellen, und Standortverknüpfungsbrücken-Objekte zum Modellieren von der tatsächlichen Routingverhalten Ihres Netzwerks zu konfigurieren.  
- Sie müssen den Datenfluss für Replikation Änderungen in Active Directory Domain Services (AD DS) zu steuern. Durch Deaktivierung **überbrücken aller standortverknüpfungen** für den Website-Link-IP-Transport und eine Standortverknüpfungsbrücke konfigurieren, wird die Standortverknüpfungsbrücke das Äquivalent von einem separaten Netzwerk. Alle standortverknüpfungen in der Standortverknüpfungsbrücke transitiv weiterleiten können, aber sie nicht außerhalb der Standortverknüpfungsbrücke weiterleiten.  

Weitere Informationen dazu, wie Sie das Active Directory-Standorte und -Dienste-Snap-in verwenden Sie zum Deaktivieren der **überbrücken aller standortverknüpfungen** festlegen, finden Sie im Artikel [aktivieren oder deaktivieren Sie Standortverknüpfungsbrücken](https://go.microsoft.com/fwlink/?LinkId=107073).  
  
## <a name="controlling-ad-ds-replication-flow"></a>Steuern des Ablaufs von AD DS-Replikation

Zwei Szenarien, in denen Sie eine Brücke Entwurfs für standortverknüpfungen zum Steuern der Datenfluss für Replikation benötigen, enthalten Steuern der Replikation, Failover und Steuern der Replikation über eine Firewall.  
  
### <a name="controlling-replication-failover"></a>Steuern der Failover der Replikation

Wenn Ihre Organisation eine Hub-Spoke-Netzwerktopologie ist, in der Regel sollten Sie nicht die Satelliten-Standorte replikationsverbindungen an andere Standorte Satelliten erstellen, wenn alle Domänencontroller in der Hubwebsite ein Fehler auftritt. In solchen Szenarien müssen Sie deaktivieren **überbrücken aller standortverknüpfungen** , und Standortverknüpfungsbrücken erstellen, sodass replikationsverbindungen zwischen Satellitenstandort und einem anderen Hubstandort, der nur ein oder zwei Hops von Satellitenstandort erstellt werden.  
  
### <a name="controlling-replication-through-a-firewall"></a>Steuern der Replikation über eine firewall

Wenn zwei Domänencontroller, die die gleiche Domäne in zwei verschiedenen Standorten darstellt ausdrücklich zugelassen sind, für die Kommunikation untereinander nur über eine Firewall, können Sie deaktivieren, **überbrücken aller standortverknüpfungen** , und Standortverknüpfungsbrücken für erstellen Websites auf derselben Seite der Firewall. Wenn Ihr Netzwerk durch Firewalls voneinander getrennt sind, empfehlen wir, Transitivität von standortverknüpfungen deaktivieren und Standortverknüpfungsbrücken für das Netzwerk auf einer Seite der Firewall zu erstellen. Informationen zum Verwalten der Replikation über Firewalls finden Sie im Artikel [Active Directory in Netzwerken durch Firewalls segmentiert](https://go.microsoft.com/fwlink/?LinkId=107074).
