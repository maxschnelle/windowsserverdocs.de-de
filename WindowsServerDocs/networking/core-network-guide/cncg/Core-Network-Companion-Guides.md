---
title: Begleithandbücher zum Hauptnetzwerk
description: Dieses Thema enthält eine Übersicht über die Begleit Handbücher zum Windows Server 2016-Kern Netzwerk Handbuch.
manager: brianlic
ms.technology: networking
ms.prod: windows-server
ms.topic: article
ms.assetid: d57af0bd-9301-4f62-9888-f528cd10451d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c0895cfd62d462ef6d158dc39ef59a9ee10a7c98
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406302"
---
# <a name="core-network-companion-guidance"></a>Core-Netzwerk-Begleithandbuch

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Im Windows Server 2016- [Kern Netzwerk Handbuch](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide) finden Sie Anweisungen zum Bereitstellen einer neuen Active Directory @ no__t-1-Gesamtstruktur mit einer neuen Stamm Domäne und der unterstützenden Netzwerkinfrastruktur. Begleit Handbücher bieten Ihnen jedoch die Möglichkeit, Funktionen für Ihr Netzwerk.

Mit den einzelnen Handbüchern können Sie nach dem Bereitstellen des Hauptnetzwerks jeweils ein bestimmtes Ziel erreichen. In einigen Fällen gibt es mehrere Begleithandbücher, mit deren Hilfe Sie sehr komplexe Ziele auf wohlüberlegte, kostengünstige und sinnvolle Weise erreichen können, sofern Sie die Handbücher zusammen und in der richtigen Reihenfolge anwenden.

Wenn Sie die Active Directory-Domäne und das Hauptnetzwerk ohne das Handbuch zum Hauptnetzwerk bereitgestellt haben, können Sie dennoch mithilfe der Begleithandbücher dem Netzwerk Features hinzuzufügen. Verwenden Sie das Handbuch zum Hauptnetzwerk einfach als Liste mit Voraussetzungen, und denken Sie daran, dass das Netzwerk zum Hinzufügen weiterer Features mit den Begleithandbüchern die im Handbuch zum Hauptnetzwerk genannten Voraussetzungen erfüllen muss.

## <a name="core-network-companion-guide-deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>Core Network Companion Guide: Bereitstellen von Serverzertifikaten für drahtgebundene und drahtlose 802.1X-Bereitstellungen 

In diesem Begleit Handbuch wird erläutert, wie Sie das zentrale Netzwerk durch Bereitstellen von Server Zertifikaten für Computer, auf denen der Netzwerk Richtlinien Server \(nps @ no__t-1, RAS-Dienst \(ras @ no__t-3 oder beides ausgeführt wird, erstellen.

Server Zertifikate sind erforderlich, wenn Sie Zertifikat basierte Authentifizierungsmethoden mit dem Extensible Authentication-Protokoll \(eap @ no__t-1 und Protected EAP \(peap @ no__t-3 für die Netzwerk Zugriffs Authentifizierung bereitstellen. Das Bereitstellen von Server Zertifikaten mit Active Directory Zertifikat Diensten \(ad CS @ no__t-1 für EAP-und PEAP-Zertifikat basierte Authentifizierungsmethoden bietet die folgenden Vorteile:

- Binden der Identität des NPS-oder RAS-Servers an einen privaten Schlüssel
- Eine kosteneffiziente und sichere Methode zum automatischen Anmelden von Zertifikaten für NPS-und RAS-Server in Domänen Mitgliedern
- Eine effiziente Methode zum Verwalten von Zertifikaten und Zertifizierungsstellen
- Sicherheit durch zertifikatbasierte Authentifizierung
- Möglichkeit zum Erweitern der Verwendung von Zertifikaten für weitere Zwecke
  
Anweisungen zum Bereitstellen von Server Zertifikaten finden Sie unter Bereitstellen von [Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen](server-certs/Deploy-Server-Certificates-for-802.1X-Wired-and-Wireless-Deployments.md).  
## <a name="core-network-companion-guide-deploy-password-based-8021x-authenticated-wireless-access"></a>Core Network Companion Guide: Bereitstellung des kennwortbasierten authentifizierten 802.1X-Funkzugriffs

In diesem Begleit Handbuch wird erläutert, wie Sie auf dem Kern Netzwerk aufbauen, indem Sie Anweisungen zum Bereitstellen von Technikern von Elektro-und Elektronik Technikern \(ieee @ no__t-1 802.1 x @ no__t-2authenticated IEEE 802,11-drahtlos Zugriff mithilfe von geschützt bereitstellen. Extensible Authentication Protocol \ – Microsoft Challenge Handshake Authentication Protocol Version 2 \(pap @ no__t-4ms @ no__t-5chap v2 @ no__t-6.

Die Authentifizierungsmethode "ETAP @ no__t-0ms @ no__t-1chap V2" erfordert, dass für die Authentifizierung von Servern, auf denen der Netzwerk Richtlinien Server \(nps @ no__t-3 ausgeführt wird, drahtlose Clients mit einem Server Zertifikat vorhanden sind, um die NPS-Identität für den Client zu beweisen, aber Benutzer die Authentifizierung erfolgt nicht mithilfe eines Zertifikats. stattdessen geben Benutzer ihren Domänen Benutzernamen und das zugehörige Kennwort an.

Da für PEAP @ no__t-0ms @ no__t-1chap v2 die Angabe von Kenn Wort basierten Anmelde Informationen anstelle eines Zertifikats während des Authentifizierungsprozesses erforderlich ist, ist es in der Regel einfacher und kostengünstiger, als EAP @ no__t-2tls oder PEAP @ no__t-3tls bereitzustellen.

Vor der Verwendung dieses Handbuchs zum Bereitstellen des drahtlosen Zugriffs mit der Authentifizierungsmethode "ETAP @ no__t-0ms @ no__t-1chap V2" müssen Sie die folgenden Schritte ausführen:

1. Befolgen Sie die Anweisungen im Handbuch zum Hauptnetzwerk, um Ihre zentrale Netzwerkinfrastruktur bereitzustellen, oder stellen Sie die in diesem Handbuch bereitgestellten Technologien bereits in Ihrem Netzwerk bereit.
2. Befolgen Sie die Anweisungen im Begleit Handbuch zum Hauptnetzwerk Bereitstellen von Server Zertifikaten für Kabel-und drahtlos Bereitstellungen mit 802.1 x, oder verfügen Sie bereits über die Technologien, die in diesem Handbuch in Ihrem Netzwerk bereitgestellt werden.

Anweisungen zum Bereitstellen des drahtlosen Zugriffs mit "Peer-no__t-0ms @ no__t-1chap V2" finden Sie unter Bereitstellen von Kenn [Wort basiertem 802.1 x-authentifizierten drahtlosen Zugriff](wireless/a-deploy-8021X-wireless-access.md).

## <a name="core-network-companion-guide-deploy-branchcache-hosted-cache-mode"></a>Core Network Companion Guide: Bereitstellen des BranchCache-Modus „Gehosteter Cache“

In diesem Begleit Handbuch wird erläutert, wie Sie BranchCache im Modus "gehosteter Cache" in einer oder mehreren Zweigstellen bereitstellen.

BranchCache ist eine Technologie zur Optimierung der Bandbreite in einem WAN (Wide Area Network), die in einigen Editionen der Windows Server 2016-und Windows 10-Betriebssysteme sowie in früheren Versionen von Windows und Windows Server enthalten ist.

Bei der Bereitstellung von BranchCache im Modus für gehostete Caches wird der Inhaltscache in einer Filiale auf einem oder mehreren Servercomputern, so genannten gehosteten Cacheservern, gehostet. Gehostete Cache Server können Arbeits Auslastungen zusätzlich zum Hosten des Caches ausführen, sodass Sie den Server in der Zweigstelle für mehrere Zwecke verwenden können.

BranchCache-Modus für gehostete Caches erhöht die Effizienz des Caches, da Inhalte auch dann verfügbar sind, wenn der Client, der die Daten ursprünglich angefordert und zwischengespeichert hat, offline ist Da der gehostete Cacheserver immer verfügbar ist, kann mehr Inhalt zwischengespeichert werden, und dies führt zu größeren WAN-Bandbreiteneinsparungen und zur Verbesserung der BranchCache-Effizienz.

Wenn Sie den Modus "gehosteter Cache" bereitstellen, können alle Clients in einer Zweigniederlassung mit mehreren Subnetzen auf einen einzelnen Cache zugreifen, der auf dem gehosteten Cache Server gespeichert ist, auch wenn sich die Clients in unterschiedlichen Subnetzen befinden.

Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" finden Sie unter Bereitstellen von [BranchCache im Modus "gehosteter Cache](bc-hcm/1-Deploy-Bc-Hcm.md)".
