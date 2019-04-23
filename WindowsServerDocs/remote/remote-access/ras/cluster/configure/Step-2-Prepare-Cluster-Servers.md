---
title: Schritt 2 Vorbereiten von Clusterservern
description: Dieses Thema ist Teil des Leitfadens Bereitstellen des Remotezugriffs in einem Cluster unter Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35d68abb-6914-42e0-91e8-803933cf785e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ab08c4ced9431fe17a4876f6df471624f22a6c44
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836591"
---
# <a name="step-2-prepare-cluster-servers"></a>Schritt 2 Vorbereiten von Clusterservern

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Bevor Sie eine Bereitstellung des Clusters konfigurieren können, können Sie zusätzliche Server hinzufügen zum Cluster vorbereiten.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[2.1 Konfigurieren der remotezugriffinfrastruktur](#BKMK_config)|Konfigurieren Sie auf jedem Server, die Sie dem Cluster hinzufügen möchten die Server-Topologie, IP-Adressierung, routing und Weiterleitung. Wenn Sie eine Load-Clusters mit Lastenausgleich von virtuellen Computern konfigurieren, müssen Sie die virtuellen Computer als verwenden Sie das Spoofing von MAC-Adressen konfigurieren.<br /><br />Darüber hinaus verknüpfen Sie jeden Server mit der gleichen Domäne, und verbinden Sie alle Server, mit dem gleichen Subnetz.|  
|[2.2 Installieren der Rolle "Remotezugriff"](#BKMK_Install)|Installieren Sie für jeden zusätzlichen Server, die Sie dem Cluster hinzufügen möchten die Rolle "Remotezugriff"|  
|[2.3 Installieren von NLB](#BKMK_NLB)|Installieren Sie auf dem bereitgestellten RAS-Server und für jeden zusätzlichen Server, die Sie dem Cluster hinzufügen möchten die NLB-Funktion. Beachten Sie, dass dieser Schritt nicht erforderlich ist, wenn Sie einen externen Load Balancer verwenden.|  
  
## <a name="BKMK_config"></a>2.1 Konfigurieren der remotezugriffinfrastruktur  
Um eine Testumgebungsbereitstellung eines remotezugriffsclusters konfigurieren zu können, müssen Sie konfigurieren den Server-Topologie, IP-Adressierung, routing und Weiterleitung auf jedem Server, die Teil des Clusters bilden.  
  
### <a name="to-configure-the-remote-access-infrastructure"></a>Zum Konfigurieren der remotezugriffinfrastruktur  
  
1.  Konfigurieren Sie jeden Server, die im Cluster mit die gleiche Topologie als erste RAS-Servers.  
  
2.  Konfigurieren Sie jeden Server, die im Cluster mit den entsprechenden IP-Adressierung, routing und Weiterleitung auf Basis der Konfiguration des ersten RAS-Servers. Beachten Sie, dass alle Server im Cluster mit demselben Subnetz verbunden sein müssen.  
  
3.  Verknüpfen Sie jeden Server, die im Cluster auf der gleichen Domäne wie der erste RAS-Server.  
  
## <a name="BKMK_Install"></a>2.2 Installieren der Rolle "Remotezugriff"  
Um eine Testumgebungsbereitstellung eines remotezugriffsclusters konfigurieren zu können, müssen Sie die Rolle "Remotezugriff" auf jedem Server installieren, die einen Teil des Clusters bilden.  
  
### <a name="to-install-the-remote-access-role-on-always-on-vpn-servers"></a>So installieren die Rolle "Remotezugriff" auf Always On-VPN-Servern  
  
1.  Klicken Sie auf dem DirectAccess-Server in der Server-Manager-Konsole in der **Dashboard**, klicken Sie auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie dreimal auf **Weiter** , um zur Anzeige für die Serverrollenauswahl zu gelangen.  
  
3.  Auf der **Serverrollen auswählen** die Option **RAS**, und klicken Sie dann auf **Weiter**.  
  
4.  Klicken Sie auf **Weiter** drei Mal.  
  
5.  Auf der **Rollendienste auswählen** die Option **DirectAccess und VPN (RAS)** , und klicken Sie dann auf **Features hinzufügen**.  
  
6.  Wählen Sie **Routing**Option **Web Application Proxy**, klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.  
  
7. Klicken Sie auf **Weiter**, und klicken Sie dann auf **Installieren**.  
  
8.  Überprüfen Sie im Dialogfeld **Installationsstatus**, ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.  
  
9.  Wiederholen Sie dieses Verfahren auf allen Servern, die Clustermitglieder sein sollen.  
  
## <a name="BKMK_NLB"></a>2.3 Installieren von NLB  
Um eine Testumgebungsbereitstellung eines remotezugriffsclusters konfigurieren zu können, müssen Sie den Netzwerklastenausgleich-Funktion auf jedem Server installieren, die einen Teil des Clusters bilden.  
  
> [!NOTE]  
> Dieser Schritt ist nicht erforderlich, wenn ein externer Lastenausgleich verwendet wird.  
  
#### <a name="to-install-the-nlb-role"></a>So installieren Sie den NLB-Serverrolle  
  
1.  Klicken Sie auf dem DirectAccess-Server in der Server-Manager-Konsole in der **Dashboard**, klicken Sie auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie auf **Weiter** viermal, um Server Funktionsauswahl-Bildschirm zu erhalten.  
  
3.  Auf der **Funktionen auswählen** die Option **Netzwerklastenausgleich**, klicken Sie auf **Features hinzufügen**, klicken Sie auf **Weiter**, und klicken Sie dann auf **Installieren**.  
  
4.  Überprüfen Sie im Dialogfeld **Installationsstatus**, ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.  
  
5.  Wiederholen Sie dieses Verfahren auf allen Servern, die Clustermitglieder sein sollen.  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Schritt 3: Konfigurieren Sie einen Cluster mit Lastenausgleich](Step-3-Configure-a-Load-Balanced-Cluster.md)  
  


