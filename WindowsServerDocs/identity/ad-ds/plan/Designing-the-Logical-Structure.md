---
ms.assetid: 9ad81367-f3fe-4b2e-bd7c-5900b2b9f77f
title: Entwerfen der logischen Struktur
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 82184fe678c05b1d7458584de8eecd0c07ece02f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832331"
---
# <a name="designing-the-logical-structure"></a>Entwerfen der logischen Struktur

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory-Domänendienste (AD DS) können Organisationen eine skalierbare, sichere und verwaltbare Infrastruktur für Benutzer- und ressourcenverwaltung erstellen. Außerdem können sie zur Unterstützung von verzeichnisfähigen Anwendungen.  
  
Eine gut entworfene logische Struktur von Active Directory bietet die folgenden Vorteile:  
  
-   Vereinfachte Verwaltung von Microsoft Windows-basierte Netzwerke, die große Anzahl von Objekten enthalten.  
  
-   Eine konsolidierte Domänenstruktur und geringere Verwaltungskosten  
  
-   Die Möglichkeit, die administrative Kontrolle über Ressourcen, die nach Bedarf zu delegieren.  
  
-   Geringere Auswirkungen auf die Netzwerkbandbreite  
  
-   Vereinfachte Ressourcenfreigabe  
  
-   Optimale suchleistung  
  
-   Niedrige Gesamtbetriebskosten  
  
Eine gut entworfene logische Struktur von Active Directory ermöglicht die effiziente Integration von Features wie Gruppenrichtlinien; Desktopsperre softwareverteilung und Benutzer, Gruppe, Arbeitsstationen und Server-Verwaltung in Ihrem System. Darüber hinaus eine sorgfältig entworfene logische Struktur ermöglicht die Integration von Microsoft und nicht-Microsoft-Anwendungen und Dienste, z. B. Microsoft Exchange Server public Key-Infrastruktur (PKI), und ein domänenbasiertes verteiltes Dateisystem (DFS).  
  
Wenn Sie eine logische Struktur von Active Directory entwerfen, bevor Sie AD DS bereitstellen, können Sie den Bereitstellungsprozess, um Active Directory-Features am besten nutzen optimieren. Informationen zum Entwerfen der logischen Struktur von Active Directory Ihr Entwicklungsteam zuerst identifiziert die Anforderungen für Ihre Organisation und, basierend auf diesen Informationen, entscheidet die Gesamtstruktur und Domäne Grenzen zu platzieren. Klicken Sie dann entscheidet das Entwurfsteam, wie die Domain Name System (DNS)-Umgebung entsprechend den Bedürfnissen der Gesamtstruktur konfigurieren. Schließlich gibt das Entwurfsteam die Organisationseinheit (OU)-Struktur, die erforderlich ist, um die Verwaltung von Ressourcen in Ihrer Organisation zu delegieren.  
  
## <a name="in-this-guide"></a>Inhalt dieser Anleitung  
  
-   [Grundlegendes zum logischen Active Directory-Modell](../../ad-ds/plan/Understanding-the-Active-Directory-Logical-Model.md)  
  
-   [Identifizieren der Teilnehmer am Bereitstellungsprojekt](../../ad-ds/plan/Identifying-the-Deployment-Project-Participants.md)  
  
-   [Erstellen eines Gesamtstrukturentwurfs](../../ad-ds/plan/Creating-a-Forest-Design.md)  
  
-   [Erstellen eines Domänenentwurfs](../../ad-ds/plan/Creating-a-Domain-Design.md)  
  
-   [Erstellen einen DNS-Infrastruktur-Entwurf](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md)  
  
-   [Erstellen eines Organisationseinheitsentwurfs](../../ad-ds/plan/Creating-an-Organizational-Unit-Design.md)  
  
-   [Anhang A: DNS-Inventur](../../ad-ds/plan/Appendix-A--DNS-Inventory.md)  
  


