---
ms.assetid: eeb919de-e21e-48d8-8186-e42adec6933f
title: Entwerfen der Standorttopologie
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e1d9323ceda478369973f959687d46c9ca3cb88f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888491"
---
# <a name="designing-the-site-topology"></a>Entwerfen der Standorttopologie

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Eine Dienst Directory-Standorttopologie ist eine logische Darstellung Ihres physischen Netzwerks. Entwerfen einer Standorttopologie für Active Directory Domain Services (AD DS) umfasst das Planen der Domänencontrollerkapazität und Entwerfen von Standorten, Subnetzen, standortverknüpfungen und Standortverknüpfungsbrücken, um sicherzustellen, effizientes routing von Datenverkehr für Abfrage und die Replikation.  
  
Entwerfen einer Standorttopologie hilft Ihnen, effizient Abfragen von Clients und Active Directory-Replikations-Datenverkehr weiterleiten. Eine gut entworfene Standorttopologie Ihrer Organisation dabei hilft die folgenden Vorteile erzielen:  
  
-   Minimieren Sie die Kosten für die Replikation von Active Directory-Daten.  
  
-   Minimieren der Verwaltungsaufwand, die zum Verwalten der Standorttopologie erforderlich sind.  
  
-   Planen der Replikation, die Speicherorte, langsame oder DFÜ Netzwerk-Links zum Replizieren von Active Directory-Daten während der Spitzenzeiten ermöglicht.  
  
-   Optimieren Sie die Fähigkeit von Clientcomputern, die nächsten Ressourcen, z. B. Domänencontroller und verteilten Dateisystems (Distributed File System, DFS)-Server zu suchen. Dieses dient als Hilfe zur Reduzierung des Netzwerkverkehrs über langsame Netzwerkverbindungen (WAN), an- und Abmeldung Prozesse verbessern und Downloadvorgängen zu beschleunigen.  
  
Bevor Sie beginnen, Ihre Website-Topologie zu entwerfen, müssen Sie die Struktur der physischen Netzwerk verstehen. Darüber hinaus müssen Sie zuerst Ihre logischen Struktur von Active Directory, einschließlich der Verwaltungshierarchie, Gesamtstrukturplan und Domänenplan für jede Gesamtstruktur entwerfen. Sie müssen außerdem den Domain Name System (DNS)-Infrastruktur-Entwurf für AD DS ausführen. Weitere Informationen zum Entwerfen der logischen Struktur von Active Directory und DNS-Infrastruktur finden Sie unter [Entwerfen der logischen Struktur für Windows Server 2008 AD DS](https://technet.microsoft.com/library/cc770806.aspx).  
  
Nachdem Sie die Gestaltung Ihrer Site Topologie abgeschlossen haben, müssen Sie sicherstellen, dass Ihre Domänencontroller die Hardware erfüllen, die für Windows Server 2008 Standard, Windows Server 2008 Enterprise und Windows Server 2008 Datacenter.  
  
## <a name="in-this-guide"></a>Inhalt dieser Anleitung  
  
-   [Grundlegendes zu Active Directory-Standorttopologie](../../ad-ds/plan/Understanding-Active-Directory-Site-Topology.md)  
  
-   [Sammeln von Netzwerkinformationen](../../ad-ds/plan/Collecting-Network-Information.md)  
  
-   [Planen der Domänencontrollerkapazität](../../ad-ds/plan/Planning-Domain-Controller-Placement.md)  
  
-   [Erstellen eines Standortentwurfs](../../ad-ds/plan/Creating-a-Site-Design.md)  
  
-   [Erstellen eines Entwurfs für Standortverknüpfungen](../../ad-ds/plan/Creating-a-Site-Link-Design.md)  
  
-   [Erstellen eines Entwurfs für Standortverknüpfungs-Bridge](../../ad-ds/plan/Creating-a-Site-Link-Bridge-Design.md)  
  
-   [Suchen zusätzlicher Ressourcen für Windows Server 2008 Active Directory-Standorttopologieentwurf](../../ad-ds/plan/Finding-Additional-Resources-for-Windows-Server-2008-Active-Directory-Site-Topology-Design.md)  
  


