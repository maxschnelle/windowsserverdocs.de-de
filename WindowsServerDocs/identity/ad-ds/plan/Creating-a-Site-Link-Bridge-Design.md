---
ms.assetid: 64142026-07b5-4601-840a-c8dcf6ab9814
title: "Erstellen eines Entwurfs für Standortverknüpfungsbrücke"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 58dda7c1f56fa3799b902ab5458e71323047ec73
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="creating-a-site-link-bridge-design"></a>Erstellen eines Entwurfs für Standortverknüpfungsbrücke

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Eine Standortverknüpfungsbrücke verbindet zwei oder mehr Standort verknüpft und ermöglicht die Transitivität zwischen standortverknüpfungen. Jeder Standort Link in eine Brücke muss einen Standort mit einem anderen Standort Link in der Brücke verfügen. (Knowledge Consistency Checker, KCC) verwendet die Informationen für jede standortverknüpfung, die Kosten der Replikation zwischen Standorten in einer standortverknüpfung und Standorte in anderen standortverknüpfungen der Brücke zu berechnen. Ohne das Vorhandensein von einem gemeinsamen Standort zwischen standortverknüpfungen kann die Konsistenzprüfung (KCC) auch direkte Verbindungen zwischen Domänencontrollern an den Standorten herstellen, die über die gleichen Standortverknüpfungsbrücke verbunden sind.  
  
Standardmäßig sind alle standortverknüpfungen transitiv. Es wird empfohlen, dass durch das Ändern nicht des Standardwert Transitivität stets **Brücke zwischen allen standortverknüpfungen** (standardmäßig aktiviert). Sie müssen jedoch deaktivieren **Brücke zwischen allen standortverknüpfungen** und führen Sie eine Entwurfs der Standortverknüpfungsbrücken, wenn:  
  
-   IP-Netzwerk ist nicht vollständig weitergeleitet. Wenn Sie deaktivieren **Brücke zwischen allen standortverknüpfungen**, gelten alle standortverknüpfungen nicht transitiv, und erstellen und konfigurieren Sie Standortverknüpfungsbrücken-Objekte zum Modellieren, um die tatsächlichen Routing Verhaltens Ihres Netzwerks können.  
  
-   In diesem Fall müssen Sie eine Replikation Steuerung des Änderungen im Active Directory-Domänendienste (AD DS). Durch die Deaktivierung **Brücke zwischen allen standortverknüpfungen** für den Standort Link IP-Transport und eine Standortverknüpfungsbrücke konfigurieren, die Standortverknüpfungsbrücke wird die Entsprechung von einem separaten Netzwerk. Alle standortverknüpfungen in der Standortverknüpfungsbrücke transitiv weiterleiten können, aber keine außerhalb der Standortverknüpfungsbrücke weiterleiten.  
  
Weitere Informationen dazu, wie Sie das Active Directory-Standorte und -Dienste-Snap-In verwenden, um Deaktivieren der **Brücke zwischen allen standortverknüpfungen** festlegen, finden Sie unter Aktivieren oder deaktivieren Sie Standortverknüpfungsbrücken ([https://go.microsoft.com/fwlink/?LinkId=107073](https://go.microsoft.com/fwlink/?LinkId=107073)).  
  
## <a name="controlling-ad-ds-replication-flow"></a>Steuern der Fluss der AD DS-Replikation  
Zwei Szenarien, in denen Sie eine Entwurfs der Standortverknüpfungsbrücken, die Steuerung der Replikation erforderlich, sind Steuern des Replikations-Failovers und Steuern der Replikation über eine Firewall.  
  
### <a name="controlling-replication-failover"></a>Steuern des Replikations-Failovers  
Wenn Ihre Organisation eine Hub-and-Spoke-Netzwerktopologie verfügt, in der Regel sollten Sie nicht Satellitensites replikationsverbindungen an andere Standorte Satelliten erstellen, wenn alle Domänencontroller am Hubstandort fehlschlagen. In solchen Szenarien müssen Sie deaktivieren **Brücke zwischen allen standortverknüpfungen**, und erstellen Sie Standortverknüpfungsbrücken, damit replikationsverbindungen zwischen dem Satelliten und einen anderen Hubstandort, die nur ein oder zwei Hops Weg der Satelliten-Website erstellt werden.  
  
### <a name="controlling-replication-through-a-firewall"></a>Steuern der Replikation über eine Firewall  
Wenn zwei Domänencontroller, die die gleiche Domäne in zwei verschiedenen Standorten darstellen ausdrücklich zugelassen werden, um miteinander kommunizieren nur mit einer Firewall befindet, können Sie deaktivieren **Brücke zwischen allen standortverknüpfungen**, und erstellen Sie Standortverknüpfungsbrücken für Standorte auf derselben Seite der Firewall. Wenn Ihr Netzwerk durch Firewalls getrennt ist, empfehlen wir deaktivieren Transitivität der standortverknüpfungen, und erstellen Standortverknüpfungsbrücken für das Netzwerk auf einer Seite der Firewall. Informationen zum Verwalten der Replikation durch Firewalls finden Sie in Active Directory in Netzwerken durch Firewalls segmentiert ([https://go.microsoft.com/fwlink/?LinkId=107074](https://go.microsoft.com/fwlink/?LinkId=107074)).  
  


