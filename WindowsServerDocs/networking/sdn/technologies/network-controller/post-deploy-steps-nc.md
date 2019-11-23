---
title: Schritte nach der Bereitstellung für den Netzwerkcontroller
description: Dieses Thema enthält Anweisungen zur Zertifikat Konfiguration für nicht-Kerberos-bereit Stellungen von Netzwerk Controllern in Windows Server 2016 Datacenter.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: eea0aca9-8d89-48fb-8068-fca40c90d34b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3f95d2884a808239c1d171eecbc983e26e799102
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355615"
---
# <a name="post-deployment-steps-for-network-controller"></a>Schritte nach der Bereitstellung für den Netzwerkcontroller

Wenn Sie den Netzwerk Controller installieren, können Sie Kerberos-oder nicht-Kerberos-bereit Stellungen auswählen.

Für nicht\-Kerberos-bereit Stellungen müssen Sie Zertifikate konfigurieren.

## <a name="configure-certificates-for-non-kerberos-deployments"></a>Konfigurieren von Zertifikaten für nicht-Kerberos-bereit Stellungen

Wenn die Computer oder virtuellen Computer \(virtuellen Computer\) für den Netzwerk Controller und der Verwaltungs Client nicht Mitglied einer Domäne\-sind, müssen Sie die Zertifikat\-basierte Authentifizierung konfigurieren, indem Sie die folgenden Schritte ausführen.

- Erstellen Sie ein Zertifikat auf dem Netzwerk Controller für die Computer Authentifizierung. Der Antragsteller Name des Zertifikats muss mit dem DNS-Namen des Netzwerk Controller Computers oder der VM identisch sein.

- Erstellen Sie ein Zertifikat auf dem Verwaltungs Client. Dieses Zertifikat muss vom Netzwerk Controller als vertrauenswürdig eingestuft werden.
  
- Registrieren Sie ein Zertifikat auf dem Netzwerk Controller Computer oder der VM. Das Zertifikat muss die folgenden Anforderungen erfüllen.
  
    -  Sowohl der Zweck der Server Authentifizierung als auch der Zweck der Client Authentifizierung müssen in der erweiterten Schlüssel Verwendung \(EKU-\) oder Anwendungsrichtlinien Erweiterungen konfiguriert werden. Der Objekt Bezeichner für die Server Authentifizierung ist 1.3.6.1.5.5.7.3.1. Der Objekt Bezeichner für die Client Authentifizierung ist 1.3.6.1.5.5.7.3.2.
  
    - Der Antragsteller Name des Zertifikats sollte in Folgendes aufgelöst werden:
  
        - Die IP-Adresse des Netzwerk Controller Computers oder der VM, wenn der Netzwerk Controller auf einem einzelnen Computer oder virtuellen Computer bereitgestellt wird.

        - Die Rest-IP-Adresse, wenn der Netzwerk Controller auf mehreren Computern, mehreren VMS oder beidem bereitgestellt wird.
  
    - Dieses Zertifikat muss von allen Rest-Clients als vertrauenswürdig eingestuft werden. Das Zertifikat muss auch vom Software Lastenausgleich (Software Load Balancing, SLB) Multiplexer (MUX) und den von einem Netzwerk Controller verwalteten, von einem Netzwerk Controller verwalteten Host Computern als vertrauenswürdig eingestuft werden.
  
    - Das Zertifikat kann von einer Zertifizierungsstelle (Certification Authority, ca) registriert werden oder ein selbst signiertes Zertifikat sein. Selbst signierte Zertifikate werden für Produktions Bereitstellungen nicht empfohlen, sind jedoch für Testumgebungen akzeptabel.
  
    - Das gleiche Zertifikat muss auf allen Netzwerk Controller Knoten bereitgestellt werden. Nachdem Sie das Zertifikat auf einem Knoten erstellt haben, können Sie das Zertifikat (mit dem privaten Schlüssel) exportieren und auf die anderen Knoten importieren.

Weitere Informationen finden Sie unter [Network Controller](Network-Controller.md).
