---
title: Schritt 2 Planen der grundlegenden DirectAccess-Bereitstellung
description: Dieses Thema ist Teil des Handbuchs Bereitstellen eines einzelnen DirectAccess-Servers mit dem Assistenten für die ersten Schritte für Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7ddcb162-dd92-406c-acab-d3de7239c644
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3009b6002d9d4cd116795c46305ff02fda02ef63
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388491"
---
# <a name="step-2-plan-the-basic-directaccess-deployment"></a>Schritt 2 Planen der grundlegenden DirectAccess-Bereitstellung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Nach dem Planen der DirectAccess-Infrastruktur ist der nächste Schritt der Bereitstellung von DirectAccess auf einem einzelnen Server mit grundlegenden Einstellungen das Planen der Einstellungen für den Assistenten für die ersten Schritte.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|Planen der Clientbereitstellung|Standardmäßig stellt der Assistent für die ersten Schritte DirectAccess für alle Laptops und Notebook Computer in der Domäne bereit, indem er einen WMI-Filter auf das Gruppenrichtlinien Objekt für die Client Einstellungen anwendet.|  
|Planen der DirectAccess-Server Bereitstellung|Planen Sie die Bereitstellung des DirectAccess-Servers.|  
  
## <a name="bkmk_2_1_client"></a>Planen der Client Bereitstellung  
Bei der Planung Ihrer Clientbereitstellung müssen zwei Entscheidungen getroffen werden:  
  
1.  Soll DirectAcess für alle oder nur für mobile Computer verfügbar sein?  
  
    Wenn Sie DirectAccess-Clients im Assistenten für die ersten Schritte konfigurieren, können Sie festlegen, dass nur Mobile Computer in den angegebenen Sicherheitsgruppen mithilfe von DirectAccess eine Verbindung herstellen können. Wenn Sie den Zugriff auf mobile Computer einschränken, konfiguriert DirectAccess automatisch einen WMI-Filter, um sicherzustellen, dass das DirectAccess-Client-GPO nur auf mobile Computer in den angegebenen Sicherheitsgruppen angewendet wird. Der DirectAccess-Administrator benötigt Berechtigungen zum Erstellen oder Ändern von WMI-Filtern für Gruppenrichtlinien, um diese Einstellung zu aktivieren.  
  
2.  In welchen Sicherheitsgruppen sollen die DirectAccess-Clientcomputer enthalten sein?  
  
    Die DirectAccess-Einstellungen befinden sich in dem Gruppenrichtlinienobjekt des DirectAccess-Clients. Das Gruppenrichtlinien Objekt wird auf Computer angewendet, die Teil der Sicherheitsgruppen sind, die Sie im Assistenten für die ersten Schritte angeben. Sie können angeben, dass Sicherheitsgruppen in einer beliebigen unterstützten Domäne enthalten sein sollen. Bevor Sie DirectAccess konfigurieren, sollten die Sicherheitsgruppen erstellt werden. Nachdem Sie die DirectAccess-Bereitstellung abgeschlossen haben, können Sie der Sicherheitsgruppe Computer hinzufügen. Beachten Sie jedoch, dass das Client-Gruppenrichtlinien Objekt nicht auf diese Clients angewendet wird, wenn Sie die Client Computer, die sich in einer anderen Domäne befinden, der Sicherheitsgruppe hinzufügen. Wenn Sie beispielsweise SG1 in Domäne A für DirectAccess-Clients erstellen und später Clients von Domäne B zu dieser Gruppe hinzufügen, wird das Client-Gruppenrichtlinienobjekt nicht auf Clients von Domäne B angewendet. Sie können dieses Problem vermeiden, indem Sie eine neue Client-Sicherheitsgruppe für jede Domäne erstellen, die die Clientcomputer enthält. Alternativ dazu können Sie auch das Add-DAClient-Cmdlet mit dem Namen des neuen Gruppenrichtlinienobjekts für die neue Domäne ausführen, wenn Sie keine neue Sicherheitsgruppe erstellen möchten.  
  
## <a name="bkmk_2_2_server"></a>Planen der DirectAccess-Server Bereitstellung  
Bei der Planung der Bereitstellung des DirectAccess-Servers müssen Sie eine Reihe von Entscheidungen treffen:  
  
-   **Netzwerktopologie** : bei der Bereitstellung eines DirectAccess-Servers sind zwei Topologien verfügbar:  
  
    -   **Zwei Adapter** : mit zwei Netzwerkadaptern kann DirectAccess mit einem direkt mit dem Internet verbundenen Netzwerkadapter konfiguriert werden, während der andere mit dem internen Netzwerk verbunden ist. Alternativ kann der Server hinter einem Edgegerät installiert werden, wie z. B. einer Firewall oder einem Router. In dieser Konfiguration ist ein Netzwerkadapter mit dem Umkreisnetzwerk und der andere mit dem internen Netzwerk verbunden.  
  
    -   **Einzelner Netzwerkadapter** : in dieser Konfiguration wird der DirectAccess-Server hinter einem Edgegerät wie z. b. einer Firewall oder einem Router installiert. Der Netzwerkadapter ist mit dem internen Netzwerk verbunden.  
  
-   **Netzwerkadapter** : der DirectAccess-Assistent erkennt automatisch die auf dem DirectAccess-Server konfigurierten Netzwerkadapter. Sie können sicherstellen, dass die richtigen Adapter auf der Seite **überprüfen** ausgewählt sind.  
  
-   **IP-HTTPS-Zertifikat** : da in dieser Bereitstellung keine PKI erforderlich ist, stellt der Assistent automatisch selbst signierte Zertifikate für IP-HTTPS und den Netzwerkadressen Server (wenn keine Zertifikate vorhanden sind) bereit und aktiviert Kerberos automatisch. Proxy. Der Assistent aktiviert auch NAT64 und DNS64 für die Protokoll Übersetzung in der reinen IPv4-Umgebung. Nachdem der Assistent die Konfiguration erfolgreich angewendet hat, klicken Sie auf **Schließen**.  
  
-   **Windows 7-Clients** : Sie können die Unterstützung für Windows 7-Clients nicht über den Assistenten für die ersten Schritte aktivieren. Dies kann über den erweiterten Setup-Assistenten aktiviert werden. Weitere Informationen finden Sie unter Bereitstellen [eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md).  
  
-   **VPN-Konfiguration** : entscheiden Sie vor dem Konfigurieren von DirectAccess, ob Sie VPN-Zugriff auf Remote Clients bereitstellen möchten. Sie sollten VPN-Zugriff bereitstellen, wenn Sie in Ihrer Organisation über Client Computer verfügen, die keine DirectAccess-Konnektivität unterstützen (weil Sie entweder nicht verwaltet sind oder ein Betriebssystem ausführen, für das DirectAccess nicht unterstützt wird). Der Assistent für die ersten Schritte konfiguriert die VPN-IP-Adresszuweisung mithilfe von DHCP und konfiguriert VPN-Clients für die Authentifizierung mit Active Directory.  
  
-   **Erzwingen von Tunneln** : Wenn Sie die Tunnel Erzwingung verwenden oder in Zukunft hinzufügen möchten, sollten Sie die Bereitstellung [eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) verwenden, um eine Konfiguration mit zwei Tunneln bereitzustellen. Aufgrund von Sicherheitsüberlegungen wird die Tunnel Erzwingung in einer einzelnen Tunnel Konfiguration nicht unterstützt.  
  
## <a name="BKMK_Links"></a>Vorheriger Schritt  
  
-   [Schritt 1: Planen der grundlegenden DirectAccess-Infrastruktur](da-basic-plan-s1-infrastructure.md)  
  


