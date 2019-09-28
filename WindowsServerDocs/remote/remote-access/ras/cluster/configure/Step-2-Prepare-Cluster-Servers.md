---
title: Schritt 2 Vorbereiten von Cluster Servern
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs in einem Cluster unter Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35d68abb-6914-42e0-91e8-803933cf785e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 87983076ee8a7d5546a5ac491ed4ca88153798f0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367407"
---
# <a name="step-2-prepare-cluster-servers"></a>Schritt 2 Vorbereiten von Cluster Servern

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Bevor Sie eine Cluster Bereitstellung konfigurieren können, bereiten Sie zusätzliche Server vor, die dem Cluster hinzugefügt werden sollen.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[2,1 Konfigurieren der Remote Zugriffs Infrastruktur](#BKMK_config)|Konfigurieren Sie auf jedem Server, den Sie dem Cluster hinzufügen möchten, die Server Topologie, die IP-Adressierung, das Routing und die Weiterleitung. Wenn Sie einen Cluster mit Lastenausgleich für virtuelle Computer konfigurieren, müssen Sie die virtuellen Computer so konfigurieren, dass Sie das Spoofing von Mac-Adressen verwenden.<br /><br />Fügen Sie außerdem jeden Server derselben Domäne hinzu, und verbinden Sie alle Server mit dem gleichen Subnetz.|  
|[2,2 Installieren der Remote Zugriffs Rolle](#BKMK_Install)|Installieren Sie auf jedem zusätzlichen Server, den Sie dem Cluster hinzufügen möchten, die Remote Zugriffs Rolle.|  
|[2,3 Installieren von NLB](#BKMK_NLB)|Installieren Sie auf dem bereitgestellten Remote Zugriffs Server und auf jedem zusätzlichen Server, den Sie dem Cluster hinzufügen möchten, das NLB-Feature. Beachten Sie, dass dieser Schritt bei der Verwendung eines externen Load Balancer nicht erforderlich ist.|  
  
## <a name="BKMK_config"></a>2,1 Konfigurieren der Remote Zugriffs Infrastruktur  
Zum Konfigurieren eines Remote Zugriffs Clusters müssen Sie die Server Topologie, die IP-Adressierung, das Routing und die Weiterleitung auf jedem Server konfigurieren, der Teil des Clusters sein wird.  
  
### <a name="to-configure-the-remote-access-infrastructure"></a>So konfigurieren Sie die Remote Zugriffs Infrastruktur  
  
1.  Konfigurieren Sie jeden der Server, die sich im Cluster befinden, mit derselben Topologie wie der erste RAS-Server.  
  
2.  Konfigurieren Sie jeden Server, der sich im Cluster befinden soll, mit entsprechender IP-Adressierung, Routing und Weiterleitung basierend auf der Konfiguration des ersten RAS-Servers. Beachten Sie, dass alle Server im Cluster mit demselben Subnetz verbunden sein müssen.  
  
3.  Verknüpfen Sie jeden Server, der sich im Cluster befinden soll, mit derselben Domäne wie der erste RAS-Server.  
  
## <a name="BKMK_Install"></a>2,2 Installieren der Remote Zugriffs Rolle  
Zum Konfigurieren eines Remote Zugriffs Clusters müssen Sie die Remote Zugriffs Rolle auf allen Servern installieren, die einen Teil des Clusters bilden.  
  
### <a name="to-install-the-remote-access-role-on-always-on-vpn-servers"></a>So installieren Sie die Remote Zugriffs Rolle auf Always on VPN-Servern  
  
1.  Klicken Sie auf dem DirectAccess-Server in der Server-Manager-Konsole im **Dashboard**auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie dreimal auf **Weiter** , um zur Anzeige für die Serverrollenauswahl zu gelangen.  
  
3.  Wählen Sie im Dialogfeld **Server Rollen auswählen** die Option **Remote Zugriff**aus, und klicken Sie dann auf **weiter**.  
  
4.  Klicken Sie drei Mal auf **weiter** .  
  
5.  Wählen Sie im Dialogfeld **Rollen Dienste auswählen** die Option **DirectAccess und VPN (RAS)** aus, und klicken Sie dann auf **Features hinzufügen**.  
  
6.  Wählen Sie **Routing**, **webanwendungsproxy**aus, klicken Sie auf **Features hinzufügen**und dann auf **weiter**.  
  
7. Klicken Sie auf **Weiter**, und klicken Sie dann auf **Installieren**.  
  
8.  Überprüfen Sie im Dialogfeld **Installationsstatus**, ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.  
  
9.  Wiederholen Sie diesen Vorgang auf allen Servern, für die Sie Cluster Mitglieder sein möchten.  
  
## <a name="BKMK_NLB"></a>2,3 Installieren von NLB  
Wenn Sie einen Remote Zugriffs Cluster konfigurieren möchten, müssen Sie die Funktion für den Netzwerk Lastenausgleich auf jedem Server installieren, der einen Teil des Clusters bilden soll.  
  
> [!NOTE]  
> Dieser Schritt ist nicht erforderlich, wenn ein externer Load Balancer verwendet wird.  
  
#### <a name="to-install-the-nlb-role"></a>So installieren Sie die NLB-Rolle  
  
1.  Klicken Sie auf dem DirectAccess-Server in der Server-Manager-Konsole im **Dashboard**auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie viermal auf **weiter** , um zum Bildschirm für die Server Funktionsauswahl zu gelangen.  
  
3.  Klicken Sie im Dialogfeld **Features auswählen** auf **Netzwerk Lastenausgleich**, klicken Sie auf **Features hinzufügen**, klicken Sie auf **weiter**, und klicken Sie dann auf **Installieren**.  
  
4.  Überprüfen Sie im Dialogfeld **Installationsstatus**, ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.  
  
5.  Wiederholen Sie diesen Vorgang auf allen Servern, für die Sie Cluster Mitglieder sein möchten.  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Schritt 3: Konfigurieren eines Clusters mit Lastenausgleich @ no__t-0  
  


