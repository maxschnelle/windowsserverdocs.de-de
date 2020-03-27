---
title: Begleithandbücher zum Hauptnetzwerk
description: Dieses Thema enthält eine Übersicht über die Begleit Handbücher zum Windows Server 2016-Kern Netzwerk Handbuch.
manager: brianlic
ms.technology: networking
ms.prod: windows-server
ms.topic: article
ms.assetid: d57af0bd-9301-4f62-9888-f528cd10451d
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 5f3ae4f9c22e61a8428a257d9324fe164eeaa04b
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319108"
---
# <a name="core-network-companion-guidance"></a>Core-Netzwerk-Begleithandbuch

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Im Windows Server 2016- [Kern Netzwerk Handbuch](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide) finden Sie Anweisungen zum Bereitstellen einer neuen Active Directory&reg;-Gesamtstruktur mit einer neuen Stamm Domäne und der unterstützenden Netzwerkinfrastruktur. Begleit Handbücher bieten Ihnen jedoch die Möglichkeit, dem Netzwerk Features hinzuzufügen.

Mit den einzelnen Handbüchern können Sie nach dem Bereitstellen des Hauptnetzwerks jeweils ein bestimmtes Ziel erreichen. In einigen Fällen gibt es mehrere Begleithandbücher, mit deren Hilfe Sie sehr komplexe Ziele auf wohlüberlegte, kostengünstige und sinnvolle Weise erreichen können, sofern Sie die Handbücher zusammen und in der richtigen Reihenfolge anwenden.

Wenn Sie die Active Directory-Domäne und das Hauptnetzwerk ohne das Handbuch zum Hauptnetzwerk bereitgestellt haben, können Sie dennoch mithilfe der Begleithandbücher dem Netzwerk Features hinzuzufügen. Verwenden Sie das Handbuch zum Hauptnetzwerk einfach als Liste mit Voraussetzungen, und denken Sie daran, dass das Netzwerk zum Hinzufügen weiterer Features mit den Begleithandbüchern die im Handbuch zum Hauptnetzwerk genannten Voraussetzungen erfüllen muss.

## <a name="core-network-companion-guide-deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>Begleit Handbuch zum Hauptnetzwerk: Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen 

In diesem Begleit Handbuch wird erläutert, wie Sie das zentrale Netzwerk durch Bereitstellen von Server Zertifikaten für Computer, auf denen der Netzwerk Richtlinien Server \(NPS-\), RAS-Dienst \(RAS-\)oder beides erstellt wird, erstellen.

Server Zertifikate sind erforderlich, wenn Sie Zertifikat basierte Authentifizierungsmethoden mit Extensible Authentication Protocol \(EAP\) und geschützten EAP-\(PEAP-\) für die Netzwerk Zugriffs Authentifizierung bereitstellen. Das Bereitstellen von Server Zertifikaten mit Active Directory Zertifikat Diensten \(AD CS\) für EAP-und PEAP-Zertifikat basierte Authentifizierungsmethoden bietet die folgenden Vorteile:

- Binden der Identität des NPS-oder RAS-Servers an einen privaten Schlüssel
- Eine kosteneffiziente und sichere Methode zum automatischen Anmelden von Zertifikaten für NPS-und RAS-Server in Domänen Mitgliedern
- Eine effiziente Methode zum Verwalten von Zertifikaten und Zertifizierungsstellen
- Sicherheit durch zertifikatbasierte Authentifizierung
- Möglichkeit zum Erweitern der Verwendung von Zertifikaten für weitere Zwecke
  
Anweisungen zum Bereitstellen von Server Zertifikaten finden Sie unter Bereitstellen von [Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen](server-certs/Deploy-Server-Certificates-for-802.1X-Wired-and-Wireless-Deployments.md).  
## <a name="core-network-companion-guide-deploy-password-based-8021x-authenticated-wireless-access"></a>Begleit Handbuch zum Hauptnetzwerk: Bereitstellen von Kenn Wort basiertem 802.1 x-authentifizierten drahtlosen Zugriff

In diesem Begleit Handbuch wird erläutert, wie Sie auf dem Kern Netzwerk aufbauen, indem Sie Anweisungen zur Bereitstellung von Technikern von Elektro-und Elektronik Technikern \(IEEE\) 802.1 x\-authentifizierten IEEE 802,11-drahtlos Zugriff mithilfe von Protected Extensible Authentication Protocol \ – Microsoft Challenge Handshake Authentication Protocol Version 2 \(PAP\-MS\-CHAP v2\)bereitstellen.

Die Authentifizierungsmethode "Peer-\-MS\-CHAP v2" erfordert, dass die Authentifizierung von Servern, auf denen der Netzwerk Richtlinien Server ausgeführt wird, \(NPS\) drahtlose Clients mit einem Server Zertifikat bereitstellen, um die NPS-Identität an den Client zu übermitteln. die Benutzerauthentifizierung wird jedoch nicht mithilfe eines Zertifikats durchgeführt.

Da der PEAP-\-MS\-CHAP v2 erfordert, dass Benutzer während des Authentifizierungs Vorgangs Kenn Wort basierte Anmelde Informationen anstelle eines Zertifikats angeben, ist die Bereitstellung in der Regel einfacher und kostengünstiger als EAP\-TLS oder PEAP\-TLS.

Bevor Sie dieses Handbuch verwenden, um drahtlosen Zugriff mit der Peer-\-MS\-CHAP v2-Authentifizierungsmethode bereitzustellen, müssen Sie die folgenden Schritte ausführen:

1. Befolgen Sie die Anweisungen im Handbuch zum Hauptnetzwerk, um Ihre zentrale Netzwerkinfrastruktur bereitzustellen, oder stellen Sie die in diesem Handbuch bereitgestellten Technologien bereits in Ihrem Netzwerk bereit.
2. Befolgen Sie die Anweisungen im Begleit Handbuch zum Hauptnetzwerk Bereitstellen von Server Zertifikaten für Kabel-und drahtlos Bereitstellungen mit 802.1 x, oder verfügen Sie bereits über die Technologien, die in diesem Handbuch in Ihrem Netzwerk bereitgestellt werden.

Anweisungen zum Bereitstellen des drahtlosen Zugriffs mit dem Peer-\-MS\-CHAP v2 finden Sie unter Bereitstellen von Kenn [Wort basiertem 802.1 x-authentifizierten drahtlosen Zugriff](wireless/a-deploy-8021X-wireless-access.md).

## <a name="core-network-companion-guide-deploy-branchcache-hosted-cache-mode"></a>Begleit Handbuch zum Hauptnetzwerk: Bereitstellen von BranchCache-Modus für gehostete Caches

In diesem Begleit Handbuch wird erläutert, wie Sie BranchCache im Modus "gehosteter Cache" in einer oder mehreren Zweigstellen bereitstellen.

BranchCache ist eine Technologie zur Optimierung der Bandbreite in einem WAN (Wide Area Network), die in einigen Editionen der Windows Server 2016-und Windows 10-Betriebssysteme sowie in früheren Versionen von Windows und Windows Server enthalten ist.

Bei der Bereitstellung von BranchCache im Modus für gehostete Caches wird der Inhaltscache in einer Filiale auf einem oder mehreren Servercomputern, so genannten gehosteten Cacheservern, gehostet. Gehostete Cache Server können Arbeits Auslastungen zusätzlich zum Hosten des Caches ausführen, sodass Sie den Server in der Zweigstelle für mehrere Zwecke verwenden können.

BranchCache-Modus für gehostete Caches erhöht die Effizienz des Caches, da Inhalte auch dann verfügbar sind, wenn der Client, der die Daten ursprünglich angefordert und zwischengespeichert hat, offline ist Da der gehostete Cacheserver immer verfügbar ist, kann mehr Inhalt zwischengespeichert werden, und dies führt zu größeren WAN-Bandbreiteneinsparungen und zur Verbesserung der BranchCache-Effizienz.

Wenn Sie den Modus "gehosteter Cache" bereitstellen, können alle Clients in einer Zweigniederlassung mit mehreren Subnetzen auf einen einzelnen Cache zugreifen, der auf dem gehosteten Cache Server gespeichert ist, auch wenn sich die Clients in unterschiedlichen Subnetzen befinden.

Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" finden Sie unter Bereitstellen von [BranchCache im Modus "gehosteter Cache](bc-hcm/1-Deploy-Bc-Hcm.md)".
