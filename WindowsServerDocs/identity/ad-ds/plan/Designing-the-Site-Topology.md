---
ms.assetid: eeb919de-e21e-48d8-8186-e42adec6933f
title: Entwerfen der Standorttopologie
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3f16b5b941ef9c3bd8f4bf742d432afc1b3f559a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="designing-the-site-topology"></a>Entwerfen der Standorttopologie

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Eine Dienst Topologie ist eine logische Darstellung des physischen Netzwerks. Entwerfen einer Standorttopologie für Active Directory-Domänendienste (AD DS) umfasst das Planen der Platzierung der Stammdomänencontroller der und Entwerfen von Standorten, Subnetzen, standortverknüpfungen und Standortverknüpfungsbrücken, um sicherzustellen, dass effizientes Routing von Abfragen und Replikations-Datenverkehr.  
  
Entwerfen einer Standorttopologie hilft Ihnen bei effizient Weiterleiten von Clientanforderungen und Active Directory-Replikations-Datenverkehr. Eine gut entworfene Standorttopologie kann Ihre Organisation die folgenden Vorteile:  
  
-   Minimieren Sie die Kosten für die Replikation von Active Directory-Daten.  
  
-   Reduzieren Sie Verwaltungsaufwands, die zum Verwalten der Standorttopologie erforderlich sind.  
  
-   Planen der Replikation, mit der Speicherorte langsam oder DFÜ-Netzwerk-Links zu Spitzenzeiten Active Directory-Daten repliziert werden kann.  
  
-   Optimieren Sie die Möglichkeit von Clientcomputern, die am nächsten gelegenen Ressourcen, z.B. Domänencontrollern und Servern (Distributed File System, DFS) zu finden. Dadurch reduziert den Netzwerkverkehr über langsame WAN network (WAN) Links, die Anmelde- und Abmeldeskripts Prozesse und Datei-Download-Vorgänge beschleunigen.  
  
Bevor Sie mit dem Entwerfen der Standorttopologie beginnen, müssen Sie die Struktur des physischen Netzwerks kennen. Darüber hinaus müssen Sie zunächst die logische Struktur Active Directory, einschließlich der Verwaltungshierarchie, Planen der Gesamtstruktur und Domänenplan für jede Gesamtstruktur entwerfen. Sie müssen außerdem den Domain Name System (DNS)-Infrastruktur-Entwurf für AD DS ausführen. Weitere Informationen zum Entwerfen der logischen Struktur von Active Directory und DNS-Infrastruktur finden Sie unter [Entwerfen der logischen Struktur für Windows Server2008 AD DS](https://technet.microsoft.com/library/cc770806.aspx).  
  
Nach Abschluss des Entwurfs der Standorttopologie müssen Sie sicherstellen, dass Ihre Domänencontroller die Hardware erfüllen, die für Windows Server2008 Standard, Windows Server2008 Enterprise und Windows Server2008 Datacenter.  
  
## <a name="in-this-guide"></a>In diesem Handbuch  
  
-   [Grundlegendes zu Active Directory-Standorttopologie](../../ad-ds/plan/Understanding-Active-Directory-Site-Topology.md)  
  
-   [Sammeln von Netzwerkinformationen](../../ad-ds/plan/Collecting-Network-Information.md)  
  
-   [Planen der Domänencontrollerkapazität](../../ad-ds/plan/Planning-Domain-Controller-Placement.md)  
  
-   [Erstellen eines Standortentwurfs](../../ad-ds/plan/Creating-a-Site-Design.md)  
  
-   [Erstellen eines Entwurfs für Standortverknüpfungen](../../ad-ds/plan/Creating-a-Site-Link-Design.md)  
  
-   [Erstellen eines Entwurfs für Standortverknüpfungsbrücke](../../ad-ds/plan/Creating-a-Site-Link-Bridge-Design.md)  
  
-   [Suchen zusätzlicher Ressourcen für Windows Server2008 Active Directory-Topologie-Standortentwurfs](../../ad-ds/plan/Finding-Additional-Resources-for-Windows-Server-2008-Active-Directory-Site-Topology-Design.md)  
  


