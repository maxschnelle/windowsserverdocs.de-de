---
title: Schritte nach der Bereitstellung für den Netzwerkcontroller
description: Dieses Thema enthält konfigurationsanweisungen für Nicht-Kerberos-Bereitstellungen von Netzwerkcontroller in Windows Server2016 Datacenter Zertifikat.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: eea0aca9-8d89-48fb-8068-fca40c90d34b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f7d6bbd50537e24f392eabde7d103c91a4f07c90
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="post-deployment-steps-for-network-controller"></a>Schritte nach der Bereitstellung für den Netzwerkcontroller

Bei der Installation von Netzwerkcontroller können Sie Kerberos oder Nicht-Kerberos Bereitstellungen.

Für-Kerberos-Bereitstellungen müssen Sie Zertifikate konfigurieren.

## <a name="configure-certificates-for-non-kerberos-deployments"></a>Konfigurieren von Zertifikaten für Nicht-Kerberos-Bereitstellungen

Wenn die \(VMs\) oder virtuelle Computer für die Netzwerk-Controller und der Management-Client nicht Domäne\ eingebunden sind, müssen Sie Certificate\-basierte Authentifizierung konfigurieren, durch die folgenden Schrittedurchführen.

- Erstellen Sie ein Zertifikat auf dem Netzwerk-Controller für Authentifizierung. Antragstellername des Zertifikats muss dem DNS-Namen des Computers Netzwerkcontroller oder virtuellen Computer identisch sein.

- Erstellen Sie ein Zertifikat auf dem Client Management. Dieses Zertifikat muss vom Netzwerkcontroller vertrauenswürdig sein.
  
- Registrieren Sie ein Zertifikat auf dem Netzwerkcontroller-Computer oder virtuellen Computer. Das Zertifikat muss die folgenden Anforderungen erfüllen.
  
    -  Erweiterte Schlüsselverwendung \(EKU\) oder Anwendungsrichtlinien Erweiterungen müssen Serverauthentifizierung und Clientauthentifizierung konfiguriert werden. Die Objekt-ID für die Serverauthentifizierung ist 1.3.6.1.5.5.7.3.1. Die Objekt-ID für die Clientauthentifizierung ist 1.3.6.1.5.5.7.3.2.
  
    - Der Name des Zertifikatantragstellers sollten zu beheben:
  
        - Die IP-Adresse des Computers Netzwerkcontroller oder VM, wenn auf einem einzelnen Computer oder virtuellen Netzwerkcontroller bereitgestellt wird.

        - Der REST IP-Adresse, wenn auf mehreren Computern, mehrerer virtueller Maschinen oder beides Netzwerkcontroller bereitgestellt wird.
  
    - Dieses Zertifikat muss von allen REST-Clients vertrauenswürdig sein. Das Zertifikat muss auch von der Software Load Balancing (SLB) zur Vereinheitlichung (MUX) und die southbound-Host-Computer, die von Netzwerkcontroller verwaltet werden, vertrauenswürdig sein.
  
    - Das Zertifikat von einer Zertifizierungsstelle (Certification Authority, CA) registriert werden, oder ein selbstsigniertes Zertifikat handeln. Selbstsignierte Zertifikate werden nicht für den Praxiseinsatz empfohlen, aber für Testumgebungen geeignet sind.
  
    - Das gleiche Zertifikat muss auf allen Knoten Netzwerkcontroller bereitgestellt werden. Nach dem Erstellen des Zertifikats auf einem Knoten, können Sie Exportieren des Zertifikats (mit privaten Schlüssel) und importieren Sie es auf den anderen Knoten.

Weitere Informationen finden Sie unter [Netzwerkcontroller](Network-Controller.md).
