---
title: Begleithandbücher zum Hauptnetzwerk
description: Dieses Thema enthält eine Übersicht über die Begleit Handbücher zum Windows Server 2016-Kern Netzwerk Handbuch.
manager: brianlic
ms.topic: article
ms.assetid: d57af0bd-9301-4f62-9888-f528cd10451d
ms.author: lizross
author: eross-msft
ms.openlocfilehash: e7595cc91f1bf3c4b2b631398bc97accba8930cc
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997122"
---
# <a name="core-network-companion-guidance"></a>Begleithandbuch zum Kernnetzwerk

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Im Windows Server 2016- [Kern Netzwerk Handbuch](../core-network-guide.md) finden Sie Anweisungen zum Bereitstellen einer neuen Active Directory &reg; -Gesamtstruktur mit einer neuen Stamm Domäne und der unterstützenden Netzwerkinfrastruktur. Begleit Handbücher bieten Ihnen jedoch die Möglichkeit, Ihrem Netzwerk Features hinzuzufügen.

Mit den einzelnen Handbüchern können Sie nach dem Bereitstellen des Hauptnetzwerks jeweils ein bestimmtes Ziel erreichen. In einigen Fällen gibt es mehrere Begleithandbücher, mit deren Hilfe Sie sehr komplexe Ziele auf wohlüberlegte, kostengünstige und sinnvolle Weise erreichen können, sofern Sie die Handbücher zusammen und in der richtigen Reihenfolge anwenden.

Wenn Sie die Active Directory-Domäne und das Hauptnetzwerk ohne das Handbuch zum Hauptnetzwerk bereitgestellt haben, können Sie dennoch mithilfe der Begleithandbücher dem Netzwerk Features hinzuzufügen. Verwenden Sie das Handbuch zum Hauptnetzwerk einfach als Liste mit Voraussetzungen, und denken Sie daran, dass das Netzwerk zum Hinzufügen weiterer Features mit den Begleithandbüchern die im Handbuch zum Hauptnetzwerk genannten Voraussetzungen erfüllen muss.

## <a name="core-network-companion-guide-deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>Begleit Handbuch zum Hauptnetzwerk: Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen

In diesem Begleit Handbuch wird erläutert, wie Sie das zentrale Netzwerk durch Bereitstellen von Server Zertifikaten für Computer, auf denen der Netzwerk Richtlinien Server \( NPS \) , RAS-Dienst- \( RAS \) oder beides ausgeführt wird, erstellen.

Server Zertifikate sind erforderlich, wenn Sie Zertifikat basierte Authentifizierungsmethoden mit dem Extensible Authentication Protocol \( EAP \) und dem geschützten EAP- \( PEAP \) für die Netzwerk Zugriffs Authentifizierung bereitstellen. Das Bereitstellen von Server Zertifikaten mit den Active Directory Zertifikat Diensten \( AD CS \) für EAP-und PEAP-Zertifikat basierte Authentifizierungsmethoden bietet die folgenden Vorteile:

- Binden der Identität des NPS-oder RAS-Servers an einen privaten Schlüssel
- Eine kosteneffiziente und sichere Methode zum automatischen Anmelden von Zertifikaten für NPS-und RAS-Server in Domänen Mitgliedern
- Eine effiziente Methode zum Verwalten von Zertifikaten und Zertifizierungsstellen
- Sicherheit durch zertifikatbasierte Authentifizierung
- Möglichkeit zum Erweitern der Verwendung von Zertifikaten für weitere Zwecke

Anweisungen zum Bereitstellen von Server Zertifikaten finden Sie unter Bereitstellen von [Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen](server-certs/Deploy-Server-Certificates-for-802.1X-Wired-and-Wireless-Deployments.md).
## <a name="core-network-companion-guide-deploy-password-based-8021x-authenticated-wireless-access"></a>Begleit Handbuch zum Hauptnetzwerk: Bereitstellen von Kenn Wort basiertem 802.1 x-authentifizierten drahtlosen Zugriff

In diesem Begleit Handbuch wird erläutert, wie Sie auf dem Kern Netzwerk aufbauen, indem Sie Anweisungen zur Bereitstellung von "Institute of Electrical and Electronics Engineers \( \) 802.1 x \- authentifiziert IEEE 802,11 Wireless Access using Protected Extensible Authentication Protocol \ – Microsoft Challenge Handshake Authentication Protocol Version 2 \( PAP \- MS \- CHAP v2 \) " bereitstellen.

Die Authentifizierungsmethode "Peer- \- MS- \- CHAP v2" erfordert, dass bei der Authentifizierung von Servern, auf denen Netzwerk Richtlinien Server \( -NPS ausgeführt \) wird, drahtlose Clients mit einem Server Zertifikat vorhanden sind, um die NPS-Identität für den Client zu beweisen. die Benutzerauthentifizierung erfolgt jedoch nicht über ein Zertifikat

Da \- es bei PEAP MS \- CHAP v2 erforderlich ist, dass Benutzer Kenn Wort basierte Anmelde Informationen anstelle eines Zertifikats während der Authentifizierung bereitstellen, ist es in der Regel einfacher und kostengünstiger, als EAP \- TLS oder PEAP TLS bereitzustellen \- .

Bevor Sie diesen Leitfaden zum Bereitstellen des drahtlosen Zugriffs mit der \- Authentifizierungsmethode "PAP MS \- CHAP v2" verwenden, müssen Sie die folgenden Schritte ausführen:

1. Befolgen Sie die Anweisungen im Handbuch zum Hauptnetzwerk, um Ihre zentrale Netzwerkinfrastruktur bereitzustellen, oder stellen Sie die in diesem Handbuch bereitgestellten Technologien bereits in Ihrem Netzwerk bereit.
2. Befolgen Sie die Anweisungen im Begleit Handbuch zum Hauptnetzwerk Bereitstellen von Server Zertifikaten für Kabel-und drahtlos Bereitstellungen mit 802.1 x, oder verfügen Sie bereits über die Technologien, die in diesem Handbuch in Ihrem Netzwerk bereitgestellt werden.

Anweisungen zum Bereitstellen des drahtlosen Zugriffs mithilfe von PAP \- MS \- CHAP v2 finden Sie unter Bereitstellen von Kenn [Wort basiertem 802.1 x-authentifizierten drahtlosen Zugriff](wireless/a-deploy-8021X-wireless-access.md).

## <a name="core-network-companion-guide-deploy-branchcache-hosted-cache-mode"></a>Begleit Handbuch zum Hauptnetzwerk: Bereitstellen von BranchCache-Modus für gehostete Caches

In diesem Begleit Handbuch wird erläutert, wie Sie BranchCache im Modus "gehosteter Cache" in einer oder mehreren Zweigstellen bereitstellen.

BranchCache ist eine Technologie zur Optimierung der Bandbreite in einem WAN (Wide Area Network), die in einigen Editionen der Windows Server 2016-und Windows 10-Betriebssysteme sowie in früheren Versionen von Windows und Windows Server enthalten ist.

Bei der Bereitstellung von BranchCache im Modus für gehostete Caches wird der Inhaltscache in einer Filiale auf einem oder mehreren Servercomputern, so genannten gehosteten Cacheservern, gehostet. Gehostete Cache Server können Arbeits Auslastungen zusätzlich zum Hosten des Caches ausführen, sodass Sie den Server in der Zweigstelle für mehrere Zwecke verwenden können.

BranchCache-Modus für gehostete Caches erhöht die Effizienz des Caches, da Inhalte auch dann verfügbar sind, wenn der Client, der die Daten ursprünglich angefordert und zwischengespeichert hat, offline ist Da der gehostete Cacheserver immer verfügbar ist, kann mehr Inhalt zwischengespeichert werden, und dies führt zu größeren WAN-Bandbreiteneinsparungen und zur Verbesserung der BranchCache-Effizienz.

Wenn Sie den Modus "gehosteter Cache" bereitstellen, können alle Clients in einer Zweigniederlassung mit mehreren Subnetzen auf einen einzelnen Cache zugreifen, der auf dem gehosteten Cache Server gespeichert ist, auch wenn sich die Clients in unterschiedlichen Subnetzen befinden.

Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" finden Sie unter Bereitstellen von [BranchCache im Modus "gehosteter Cache](bc-hcm/1-Deploy-Bc-Hcm.md)".