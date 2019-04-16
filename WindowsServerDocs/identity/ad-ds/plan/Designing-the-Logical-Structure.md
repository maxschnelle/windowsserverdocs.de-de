---
ms.assetid: 9ad81367-f3fe-4b2e-bd7c-5900b2b9f77f
title: Entwerfen der logischen Struktur
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 8d1b9c27f05faef49f7fd4228f4ebe689b75d30f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="designing-the-logical-structure"></a>Entwerfen der logischen Struktur

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Active Directory-Domänendienste (AD DS) ermöglicht Organisationen eine skalierbare, sichere und verwaltbare Infrastruktur für Benutzer- und Ressourcenverwaltung erstellen. Darüber hinaus können sie die AD-aktivierte Anwendungen unterstützen.  
  
Eine gut entworfene logische Active Directory-Struktur bietet die folgenden Vorteile:  
  
-   Vereinfachte Verwaltung von Microsoft Windows-basierten Netzwerken, die große Anzahl von Objekten enthalten.  
  
-   Eine konsolidierte Domänenstruktur und geringere Verwaltungskosten  
  
-   Die Möglichkeit, administrative Kontrolle über Ressourcen, nach Bedarf  
  
-   Reduzierte Auswirkungen auf die Netzwerkbandbreite  
  
-   Vereinfachte Ressourcenfreigabe  
  
-   Suche optimale Leistung  
  
-   Niedrige Gesamtbetriebskosten  
  
Eine gut entworfene logische Active Directory-Struktur ermöglicht das effiziente Integration von Features wie Gruppenrichtlinien; Desktop-Sperrung; Verteilung von Software; und Benutzer, Gruppen, Arbeitsstationen und Server in Ihrem System. Darüber hinaus eine sorgfältig entworfene logische Struktur erleichtert die Integration von Microsoft und von Microsoft stammenden Anwendungen und Dienste wie Microsoft Exchange Server public Key-Infrastruktur (PKI), und einer domänenbasierten verteiltes Dateisystem (DFS).  
  
Wenn Sie vor der Bereitstellung von AD DS logische Active Directory-Struktur entwerfen, können Sie während des Bereitstellungsprozesses, um am besten von Active Directory-Features nutzen zu optimieren. Zum Entwerfen der logischen Struktur von Active Directory Ihrem Entwicklungsteam zunächst identifiziert die Anforderungen für Ihre Organisation und anhand dieser Informationen, entscheidet die Gesamtstruktur und Domäne Grenzen zu platzieren. Das Entwurfsteam entscheidet anschließend, die Domain Name System (DNS)-Umgebung die Anforderungen der Gesamtstruktur konfigurieren. Schließlich gibt das Entwurfsteam die Organisationseinheit (OU)-Struktur, die zum Delegieren der Verwaltung von Ressourcen in Ihrer Organisation erforderlich ist.  
  
## <a name="in-this-guide"></a>In diesem Handbuch  
  
-   [Grundlegendes zum logischen Active Directory-Modell](../../ad-ds/plan/Understanding-the-Active-Directory-Logical-Model.md)  
  
-   [Identifizieren der Teilnehmer am Bereitstellungsprojekt](../../ad-ds/plan/Identifying-the-Deployment-Project-Participants.md)  
  
-   [Erstellen eines Gesamtstrukturentwurfs](../../ad-ds/plan/Creating-a-Forest-Design.md)  
  
-   [Erstellen eines Domänenentwurfs](../../ad-ds/plan/Creating-a-Domain-Design.md)  
  
-   [Erstellen einen DNS-Infrastruktur-Entwurf](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md)  
  
-   [Erstellen eines Organisationseinheitsentwurfs](../../ad-ds/plan/Creating-an-Organizational-Unit-Design.md)  
  
-   [Anhang A: DNS-Inventur](../../ad-ds/plan/Appendix-A--DNS-Inventory.md)  
  


