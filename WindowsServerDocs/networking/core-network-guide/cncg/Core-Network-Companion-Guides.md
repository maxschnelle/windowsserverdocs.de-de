---
title: Begleithandbücher zum Hauptnetzwerk
description: Dieses Thema enthält eine Übersicht über die Begleithandbücher, Windows Server 2016 Core Network Guide
manager: brianlic
ms.technology: networking
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: d57af0bd-9301-4f62-9888-f528cd10451d
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b757e1914ee263a041f39e9767d3cb8af38403dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816801"
---
# <a name="core-network-companion-guidance"></a>Core-Netzwerk-Begleithandbuch

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Windows Server 2016 während [Core Network Guide](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide) enthält Anweisungen zum Bereitstellen einer neuen Active Directory&reg; Gesamtstruktur mit einer neuen Stammdomäne und der unterstützenden Netzwerkinfrastruktur Begleithandbücher bieten Ihnen mit der Möglichkeit zum Netzwerk hinzufügen.

Mit den einzelnen Handbüchern können Sie nach dem Bereitstellen des Hauptnetzwerks jeweils ein bestimmtes Ziel erreichen. In einigen Fällen gibt es mehrere Begleithandbücher, mit deren Hilfe Sie sehr komplexe Ziele auf wohlüberlegte, kostengünstige und sinnvolle Weise erreichen können, sofern Sie die Handbücher zusammen und in der richtigen Reihenfolge anwenden.

Wenn Sie die Active Directory-Domäne und das Hauptnetzwerk ohne das Handbuch zum Hauptnetzwerk bereitgestellt haben, können Sie dennoch mithilfe der Begleithandbücher dem Netzwerk Features hinzuzufügen. Verwenden Sie das Handbuch zum Hauptnetzwerk einfach als Liste mit Voraussetzungen, und denken Sie daran, dass das Netzwerk zum Hinzufügen weiterer Features mit den Begleithandbüchern die im Handbuch zum Hauptnetzwerk genannten Voraussetzungen erfüllen muss.

## <a name="core-network-companion-guide-deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>Core Network Companion Guide: Bereitstellen von Serverzertifikaten für drahtgebundene und drahtlose 802.1X-Bereitstellungen 

Diesem Begleithandbuch wird erläutert, wie Sie auf dem Hauptnetzwerk durch Bereitstellen von Serverzertifikaten für Computer, auf dem Network Policy Server ausgeführt werden \(NPS\), RAS-Dienst \(RAS\), oder beides.

Serverzertifikate sind erforderlich, wenn Sie zertifikatbasierte Authentifizierungsmethoden mit Extensible Authentication-Protokoll bereitstellen \(EAP\) und Protected EAP \(PEAP\) zum Authentifizieren des Netzwerkzugriffs. Bereitstellung von Serverzertifikaten mit Active Directory Certificate Services \(AD CS\) für die zertifikatbasierte Authentifizierung von EAP und PEAP-Methoden bietet die folgenden Vorteile:

- Die Identität des NPS- oder RAS-Servers Binden an einen privaten Schlüssel
- Eine kosteneffiziente und sichere Methode für die automatische Registrierung von Zertifikaten auf NPS- und RAS-Mitgliedsservern der Domäne
- Eine effiziente Methode zum Verwalten von Zertifikaten und Zertifizierungsstellen
- Sicherheit durch zertifikatbasierte Authentifizierung
- Möglichkeit zum Erweitern der Verwendung von Zertifikaten für weitere Zwecke
  
Anweisungen zum Bereitstellen von Serverzertifikaten finden Sie [Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen](server-certs/Deploy-Server-Certificates-for-802.1X-Wired-and-Wireless-Deployments.md).  
## <a name="core-network-companion-guide-deploy-password-based-8021x-authenticated-wireless-access"></a>Core Network Companion Guide: Bereitstellung des kennwortbasierten authentifizierten 802.1X-Funkzugriffs

Diesem Begleithandbuch wird erläutert, wie Sie auf dem Hauptnetzwerk durch Bereitstellen von Anleitungen zum Bereitstellen von Institute of Electrical and Electronics Engineers \(IEEE\) 802.1 X\-authentifizierten IEEE 802.11-Drahtlosnetzwerke Zugriff auf die Verwendung von Protected Extensible Authentication Protocol\ – Microsoft Challenge Handshake Authentication Protocol Version 2 \(PEAP\-MS\-CHAP-v2\).

Der PEAP-Authentifizierungsmethode\-MS\-CHAP v2 erfordert diese Authentifizierung Servern mit der Netzwerkrichtlinienserver \(NPS\) präsentieren Sie drahtlose Clients mit einem Serverzertifikat, um die NPS-Identität nachzuweisen der Client, jedoch keine Benutzerauthentifizierung durchgeführt wird, mit einem Zertifikat - Geben Sie stattdessen Benutzer ihren Domänenbenutzernamen und Ihr Kennwort.

Da PEAP\-MS\-CHAP v2 ist erforderlich, dass Benutzer Bereitstellen von Kennwörtern basierende Anmeldeinformationen anstelle eines Zertifikats während der Authentifizierung ist in der Regel einfacher und kostengünstiger als EAP bereitstellen\-TLS oder PEAP \-TLS.

Bevor Sie dieses Handbuch zur Bereitstellung von drahtlosen Zugriff mit den PEAP verwenden\-MS\-CHAP-v2-Authentifizierungsmethode, müssen Sie Folgendes tun:

1. Befolgen Sie die Anweisungen in das Handbuch zum Hauptnetzwerk Core Netzwerkinfrastruktur bereitstellen, oder die Technologien haben bereits vorgestellt, in dieser Anleitung, die in Ihrem Netzwerk bereitgestellt.
2. Befolgen Sie die Anweisungen in die Core Network Companion Guide bereitstellen Serverzertifikate für 802.1 X verkabelte und drahtlose Bereitstellungen und die Technologien haben bereits vorgestellt, in dieser Anleitung, die in Ihrem Netzwerk bereitgestellt.

Anweisungen zur Bereitstellung von 802.1X-Drahtloszugriff mit PEAP\-MS\-CHAP-v2, finden Sie unter [Bereitstellung Kennwort-basierten Drahtloszugriff mit 802.1X-Authentifizierung](wireless/a-deploy-8021X-wireless-access.md).

## <a name="core-network-companion-guide-deploy-branchcache-hosted-cache-mode"></a>Core Network Companion Guide: Bereitstellen des BranchCache-Modus „Gehosteter Cache“

Diesem Begleithandbuch wird erläutert, wie Sie BranchCache im Modus "gehosteter Cache" in eine oder mehrere Zweigstellen bereitstellen.

BranchCache ist eine Technologie wide Area Network (WAN)-Bandbreite Optimierung, die in einigen Editionen der Betriebssysteme Windows Server 2016 und Windows 10 als auch in früheren Versionen von Windows und Windows Server enthalten ist.

Bei der Bereitstellung von BranchCache im Modus für gehostete Caches wird der Inhaltscache in einer Filiale auf einem oder mehreren Servercomputern, so genannten gehosteten Cacheservern, gehostet. Gehostete Cacheserver führe Workloads neben dem Hosten des Caches, der Sie den Server für mehrere Zwecke in der Zweigstelle verwenden kann.

Gehostete BranchCache-Cachemodus erhöht die Effizienz, da Inhalte verfügbar sind, selbst wenn der Client, der ursprünglich angefordert und zwischengespeichert, und die Daten offline ist. Da der gehostete Cacheserver immer verfügbar ist, kann mehr Inhalt zwischengespeichert werden, und dies führt zu größeren WAN-Bandbreiteneinsparungen und zur Verbesserung der BranchCache-Effizienz.

Wenn Sie den Modus "gehosteter Cache" bereitstellen, können alle Clients in einer Filiale mit mehreren Subnetzen einen einzigen Cache zugreifen, der auf dem gehosteten Cacheserver gespeichert wird, auch wenn die Clients in unterschiedlichen Subnetzen befinden.

Anweisungen dazu, wie Sie BranchCache im Modus "gehosteter Cache" bereitstellen, finden Sie unter [Bereitstellen von BranchCache Hosted Cache Mode](bc-hcm/1-Deploy-Bc-Hcm.md).
