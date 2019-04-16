---
title: Begleithandbücher zum Hauptnetzwerk
description: Dieses Thema enthält eine Übersicht über die Begleithandbücher zu Windows Server2016 Core Network Guide
manager: brianlic
ms.technology: networking
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: d57af0bd-9301-4f62-9888-f528cd10451d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3c272c51cc69017b75e50e79e58186c0ea7c6391
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="core-network-companion-guides"></a>Begleithandbücher zum Hauptnetzwerk

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Während der Windows Server2016 [Kernnetzwerkhandbuch](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide) enthält Anweisungen zum Bereitstellen einer neuen Active Directory&reg; Gesamtstruktur mit einer neuen Stammdomäne und der unterstützenden Netzwerkinfrastruktur Begleithandbücher bieten Ihnen die Möglichkeit, mit dem Netzwerk Features hinzuzufügen.

Jede Begleithandbuch können Sie ein bestimmtes Ziel zu erreichen, nachdem Sie Ihre Hauptnetzwerk bereitgestellt haben. Können Sie in einigen Fällen, dass mehrere Begleitgeräte führt, die bei der Bereitstellung von zusammen und in der richtigen Reihenfolge stehen sehr komplexe Ziele in einer gemessenen, kostengünstige und sinnvolle Weise erreichen.

Wenn Sie Ihre Active Directory-Domäne und Core-Netzwerk ohne das Handbuch zum Hauptnetzwerk bereitgestellt haben, weiterhin können die Begleithandbücher Sie zum Hinzufügen von Features zum Netzwerk. Einfach das Kernnetzwerkhandbuch als eine Liste der erforderlichen Komponenten, und wissen Sie, um zusätzliche Features mit der Begleithandbücher bereitzustellen, Ihr Netzwerk die Voraussetzungen erfüllt werden müssen, die durch das Handbuch zum Hauptnetzwerk bereitgestellt werden.

## <a name="core-network-companion-guide-deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>Kernnetzwerk-Begleithandbuch: Bereitstellen von Serverzertifikaten für 802.1X-authentifizierte Kabel- und Drahtlosnetzwerke Bereitstellungen 

Diesem Begleithandbuch wird beschrieben, wie auf dem Hauptnetzwerk durch Bereitstellen von Serverzertifikaten für Computer, auf denen der Netzwerkrichtlinienserver \(NPS\) und/oder \(RAS\) RAS-Dienst ausgeführt werden.

Serverzertifikate sind erforderlich, wenn Sie zertifikatbasierte Authentifizierungsmethoden mit Extensible Authentication Protocol \(EAP\) und geschütztes EAP \(PEAP\) für die Netzwerkzugriffsauthentifizierung bereitstellen. Bereitstellen von Serverzertifikaten mit Active Directory Certificate Services bietet \(AD CS\) für EAP und PEAP zertifikatbasierte Authentifizierungsmethoden die folgenden Vorteile:

- Die Identität des NPS- oder RAS-Servers Binden an einen privaten Schlüssel.
- Eine effiziente und sichere Methode für die automatische Registrierung von Zertifikaten auf NPS- und RAS-Servern
- Eine effiziente Methode zum Verwalten von Zertifikaten und Zertifizierungsstellen
- Sicherheit durch zertifikatbasierte Authentifizierung
- Die Möglichkeit, erweitern Sie die Verwendung von Zertifikaten für weitere Zwecke
  
Eine Anleitung zum Bereitstellen von Serverzertifikaten finden Sie [Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen](server-certs/Deploy-Server-Certificates-for-802.1X-Wired-and-Wireless-Deployments.md).  
## <a name="core-network-companion-guide-deploy-password-based-8021x-authenticated-wireless-access"></a>Kernnetzwerk-Begleithandbuch: Bereitstellung Kennwort-basierte 802.1X-authentifizierten drahtlosen Zugriff

Diesem Begleithandbuch wird beschrieben, wie Sie auf dem Hauptnetzwerk erstellen, durch die Bereitstellung von Anweisungen zum Bereitstellen von Institute of Electrical und Electronics Engineers \(IEEE\) 802.1X\-authentifizierten IEEE 802.11-Drahtloszugriff mit Protected Extensible Authentication Protocol\ – Microsoft Challenge Handshake Authentication Protocol Version 2 \ (PEAP\-MS\-CHAP v2\).

Die Authentifizierungsmethode PEAP\-MS\-CHAP v2 erfordert, dass die Authentifizierung von Servern mit Netzwerkrichtlinienserver \(NPS\) vorhanden drahtlose Clients mit einem Serverzertifikat, um die Identität des NPS-Servers an den Client zu beweisen, jedoch die Benutzerauthentifizierung erfolgt nicht mit einem Zertifikat - Benutzern stattdessen ermöglichen, ihre Domäne Kombination aus Benutzername und Kennwort.

Da PEAP\-MS\-CHAP v2 erforderlich ist, dass Benutzer während der Authentifizierung ein Zertifikat, anstatt Kennwörtern basierende Anmeldeinformationen angeben, ist es in der Regel einfacher und kostengünstiger als EAP\-TLS oder PEAP\-TLS bereitstellen.

Bevor Sie diese Anleitung zum Bereitstellen von drahtlosen Zugriff mit der PEAP\-MS\-CHAP v2-Authentifizierungsmethode verwenden, müssen Sie Folgendes tun:

1. Folgen Sie den Anweisungen des Kernnetzwerkhandbuchs Ihrer Netzwerkinfrastruktur Core bereitstellen oder die Technologien haben bereits angezeigt, in diesem Handbuch in Ihrem Netzwerk bereitgestellt.
2. Folgen Sie den Anweisungen in Core Network Companion Guide bereitstellen Serverzertifikate für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen oder bereits die Technologien gestellt sind in dieser Anleitung in Ihrem Netzwerk bereitgestellt.

Eine Anleitung zum Bereitstellen von drahtlosen Zugriff mit PEAP\-MS\-CHAP v2 finden Sie [Bereitstellung Kennwort-basierte Drahtloszugriff mit 802.1X-Authentifizierung ](wireless/a-deploy-8021X-wireless-access.md).

## <a name="core-network-companion-guide-deploy-branchcache-hosted-cache-mode"></a>Kernnetzwerk-Begleithandbuch: Bereitstellen von BranchCache-Modus für gehostete Caches

Diesem Begleithandbuch wird beschrieben, wie Sie BranchCache im Modus für gehostete Caches in einen oder mehrere Filialen bereitstellen.

BranchCache ist eine Technologie wide Area Network (WAN)-Bandbreite Optimierung, die in einigen Editionen der Betriebssysteme Windows Server2016 und Windows10 sowie in früheren Versionen von Windows und Windows Server verfügbar ist.

Wenn Sie BranchCache im Modus für gehostete Caches bereitstellen, Cache-Inhalte in einer Filiale befindet sich auf einem oder mehreren Servercomputern, die aufgerufen werden, gehostete Cacheserver. Gehostete Cacheserver können ausführen Arbeitslasten zusätzlich zum Hosten von Cache, in der Sie den Server für mehrere Zwecke in der Filiale verwenden kann.

BranchCache-gehosteten Cachemodus erhöht die Effizienz des Caches, da der Inhalt verfügbar ist, auch wenn der Client, der ursprünglich angefordert und zwischengespeichert, und die Daten offline ist. Da der gehostete Cacheserver immer verfügbar ist, wird mehr Inhalt zwischengespeichert werden, und größere einsparungen von WAN-Bandbreite, und BranchCache-Effizienz.

Wenn Sie den Modus für gehostete Caches bereitstellen, können alle Clients in einer Filiale mit mehreren Subnetzen einen einzigen Cache zugreifen, die auf dem Cacheserver gehosteten gespeichert wird, auch wenn die Clients in unterschiedlichen Subnetzen befinden.

Informationen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" finden Sie unter [Bereitstellen von BranchCache Hosted Cache Mode ](bc-hcm/1-Deploy-Bc-Hcm.md).
