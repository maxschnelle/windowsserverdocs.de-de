---
title: Schritte nach der Bereitstellung für den Netzwerkcontroller
description: Dieses Thema enthält Anweisungen für nicht-Kerberos-Bereitstellungen von Netzwerkcontroller in Windows Server 2016 Datacenter Zertifikat.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: eea0aca9-8d89-48fb-8068-fca40c90d34b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f7d6bbd50537e24f392eabde7d103c91a4f07c90
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871081"
---
# <a name="post-deployment-steps-for-network-controller"></a>Schritte nach der Bereitstellung für den Netzwerkcontroller

Bei der Installation von Netzwerkcontroller können Sie Kerberos oder nicht-Kerberos-Bereitstellungen.

Für nicht\-Kerberos-Bereitstellungen müssen Sie Zertifikate konfigurieren.

## <a name="configure-certificates-for-non-kerberos-deployments"></a>Konfigurieren von Zertifikaten für nicht-Kerberos-Bereitstellungen

Wenn die Computer oder virtuelle Computer \(VMs\) für Netzwerkcontroller und den Management-Client nicht Domäne\-verknüpft ist, müssen Sie Zertifikat konfigurieren\--basierte Authentifizierung dazu die folgenden die Schritte.

- Erstellen Sie ein Zertifikat auf dem Netzwerkcontroller für die Computerauthentifizierung. Antragstellername des Zertifikats muss der DNS-Name des Netzwerkcontroller-Computer oder virtuellen Computer identisch sein.

- Erstellen Sie ein Zertifikat auf dem Management-Client. Dieses Zertifikat muss durch den Netzwerkcontroller vertrauenswürdig sein.
  
- Registrieren Sie ein Zertifikat auf dem Netzwerkcontroller-Computer oder virtuellen Computer. Das Zertifikat muss die folgenden Anforderungen erfüllen.
  
    -  Sowohl den Zertifizierungszweck der Serverauthentifizierung als auch den Zertifizierungszweck der Clientauthentifizierung im Enhanced Key Usage konfiguriert sein \(EKU\) oder Anwendungsrichtlinien-Erweiterungen. Die Objekt-ID für die Serverauthentifizierung ist 1.3.6.1.5.5.7.3.1. Die Objekt-ID für die Clientauthentifizierung ist 1.3.6.1.5.5.7.3.2.
  
    - Antragstellername des Zertifikats sollte aufgelöst:
  
        - Die IP-Adresse des Netzwerkcontroller-Computer oder der VM, wenn die Bereitstellung des Netzwerkcontrollers auf einem einzelnen Computer oder virtuellen Computer.

        - Die REST-IP-Adresse an, wenn die Bereitstellung des Netzwerkcontrollers auf mehreren Computern, mehreren virtuellen Computern oder beides.
  
    - Dieses Zertifikat muss von allen REST-Clients vertrauenswürdig sein. Das Zertifikat muss auch vertrauenswürdig sein, indem Sie den Multiplexer (Software Load Balancing, SLB) (MUX) und die southbound-Host-Computer, die vom Netzwerkcontroller verwaltet werden.
  
    - Das Zertifikat von einer Zertifizierungsstelle (CA) registriert werden oder ein selbstsigniertes Zertifikat handeln. Selbstsignierte Zertifikate werden für produktionsbereitstellungen nicht empfohlen, aber zulässig für Test Lab-Umgebungen sind.
  
    - Das gleiche Zertifikat muss auf allen Knoten für den Netzwerkcontroller bereitgestellt werden. Nach dem Erstellen des Zertifikats auf einem Knoten können Sie das Exportieren des Zertifikats (mit dem privaten Schlüssel) und importieren sie auf den anderen Knoten.

Weitere Informationen finden Sie unter [Network Controller](Network-Controller.md).
