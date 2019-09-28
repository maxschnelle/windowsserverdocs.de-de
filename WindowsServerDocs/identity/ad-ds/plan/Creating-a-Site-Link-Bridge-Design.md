---
ms.assetid: 64142026-07b5-4601-840a-c8dcf6ab9814
title: Erstellen eines Entwurfs für Standortverknüpfungsbrücken
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 79e91481c357d05617ee0ddc716e2bf6e90b8b27
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408960"
---
# <a name="creating-a-site-link-bridge-design"></a>Erstellen eines Entwurfs für Standortverknüpfungsbrücken

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Eine Standort Verknüpfungs Brücke verbindet zwei oder Mehrstandort Verknüpfungen und ermöglicht Transitivität Zwischenstandort Verknüpfungen. Jede Standort Verknüpfung in einer Bridge muss über einen gemeinsamen Standort mit einer anderen Standort Verknüpfung in der Bridge verfügen. Die Konsistenzprüfung (KCC) verwendet die Informationen an den einzelnen Standort Verknüpfungen, um die Kosten für die Replikation Zwischenstand Orten in einer Standort Verknüpfung und Standorte in den anderen Standort Verknüpfungen der Bridge zu berechnen. Ohne eine gemeinsame Site Zwischenstandort Verknüpfungen kann die KCC auch keine direkten Verbindungen zwischen Domänen Controllern an den Standorten einrichten, die über dieselbe Standort Verknüpfungs Brücke verbunden sind.  
  
Standardmäßig sind alle Standort Verknüpfungen transitiv. Es wird empfohlen, die Transitivität zu aktivieren, indem Sie nicht den Standardwert **Bridge alle Standort Verknüpfungen überbrücken** (standardmäßig aktiviert) ändern. Allerdings müssen Sie **alle Standort Verknüpfungen überbrücken** deaktivieren und den Entwurf einer Standort Verknüpfungs Brücke durchführen, wenn Folgendes gilt:  

- Ihr IP-Netzwerk wird nicht vollständig weitergeleitet. Wenn Sie **alle Standort Verknüpfungen überbrücken**deaktivieren, werden alle Standort Verknüpfungen als nicht transitiv betrachtet, und Sie können Standort Verknüpfungs Brücken-Objekte erstellen und konfigurieren, um das tatsächliche Routing Verhalten Ihres Netzwerks zu modellieren.  
- Sie müssen den Replikations Fluss der in Active Directory Domain Services vorgenommenen Änderungen (AD DS) steuern. Durch Deaktivieren der **Bridge aller Standort Verknüpfungen** für den IP-Transport der Standort Verknüpfung und Konfigurieren einer Standort Verknüpfungs Brücke wird die Standort Verknüpfungs Brücke zum Äquivalent zu einem separaten Netzwerk. Alle Standort Verknüpfungen innerhalb der Standort Verknüpfungs Brücke können transitiv weitergeleitet werden, Sie werden jedoch nicht außerhalb der Standort Verknüpfungs Brücke weitergeleitet.  

Weitere Informationen zur Verwendung des Snap-Ins "Active Directory Standorte und Dienste" zum Deaktivieren der Einstellung " **alle Standort Verknüpfungen überbrücken** " finden Sie im Artikel [Aktivieren oder Deaktivieren von Standort](https://go.microsoft.com/fwlink/?LinkId=107073)Verknüpfungs Brücken.  
  
## <a name="controlling-ad-ds-replication-flow"></a>Steuern AD DS Replikations Flusses

Zwei Szenarios, in denen Sie einen Standort Verknüpfungs Brücken-Entwurf zum Steuern des Replikations Flusses benötigen, umfassen das Steuern des Replikations Failovers und das Steuern der  
  
### <a name="controlling-replication-failover"></a>Steuern des Replikations Failovers

Wenn Ihre Organisation über eine Hub-und-Sprachnetzwerk Topologie verfügt, sollten Sie im Allgemeinen nicht möchten, dass die Satellitenstandorte Replikations Verbindungen mit anderen Satellitenstandorten herstellen, wenn alle Domänen Controller am Hub-Standort ausfallen. In solchen Szenarien müssen Sie **alle Standort Verknüpfungen überbrücken** deaktivieren und Standort Verknüpfungs Brücken erstellen, damit Replikations Verbindungen zwischen dem Satelliten Standort und einem anderen Hub-Standort hergestellt werden, der nur ein oder zwei Hops vom Satelliten Standort entfernt ist.  
  
### <a name="controlling-replication-through-a-firewall"></a>Steuern der Replikation über eine Firewall

Wenn zwei Domänen Controller, die dieselbe Domäne auf zwei verschiedenen Standorten darstellen, ausdrücklich miteinander kommunizieren dürfen, können Sie **alle Standort Verknüpfungen überbrücken und Standort Verknüpfungs** Brücken für Standorte auf der gleichen Seite des Brand. Wenn Ihr Netzwerk durch Firewalls getrennt ist, wird daher empfohlen, die Transitivität von Standort Verknüpfungen zu deaktivieren und Standort Verknüpfungs Brücken für das Netzwerk auf einer Seite der Firewall zu erstellen. Informationen zum Verwalten der Replikation über Firewalls finden Sie im Artikel [Active Directory in von Firewalls segmentierten Netzwerken](https://go.microsoft.com/fwlink/?LinkId=107074).
