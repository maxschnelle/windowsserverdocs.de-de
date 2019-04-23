---
title: Schritt 2 planen die grundlegenden DirectAccess-Bereitstellung
description: Dieses Thema ist Teil des Handbuchs Bereitstellen eines einzelnen DirectAccess-Servers mithilfe der erste Schritte-Assistenten für Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7ddcb162-dd92-406c-acab-d3de7239c644
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8c21b7fa62246170caeb07cb5865c1ff311e0f09
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848751"
---
# <a name="step-2-plan-the-basic-directaccess-deployment"></a>Schritt 2 planen die grundlegenden DirectAccess-Bereitstellung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Der nächste Schritt bei der Bereitstellung von DirectAccess auf einem einzelnen Server mit grundlegenden Einstellungen werden nach der Planung der DirectAccess-Infrastruktur, Planen Sie die Einstellungen für den Assistenten für erste Schritte.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|Planen der Clientbereitstellung|Standardmäßig stellt der Assistent für erste Schritte DirectAccess an alle Laptops und Notebookcomputer in der Domäne durch Anwenden eines WMI-Filters auf das Client-Gruppenrichtlinienobjekt-Einstellungen|  
|Planen der Directacess-serverbereitstellung|Planen Sie die Bereitstellung des DirectAccess-Servers.|  
  
## <a name="bkmk_2_1_client"></a>Planen der Clientbereitstellung  
Bei der Planung Ihrer Clientbereitstellung müssen zwei Entscheidungen getroffen werden:  
  
1.  Soll DirectAcess für alle oder nur für mobile Computer verfügbar sein?  
  
    Wenn Sie im Assistent für erste Schritte DirectAccess-Clients konfigurieren, können Sie auswählen, um nur mobile Computer in den angegebenen Sicherheitsgruppen eine Verbindung über DirectAccess herstellen können. Wenn Sie den Zugriff auf mobile Computer beschränken, konfiguriert der DirectAccess automatisch einen WMI-Filter, um sicherzustellen, dass den DirectAccess-Client, die Gruppenrichtlinienobjekt nur auf mobile Computer in den angegebenen Sicherheitsgruppen angewendet wird. Der DirectAccess-Administrator benötigt Berechtigungen zum Erstellen oder ändern die Gruppenrichtlinie WMI-Filter, um diese Einstellung zu aktivieren.  
  
2.  In welchen Sicherheitsgruppen sollen die DirectAccess-Clientcomputer enthalten sein?  
  
    Die DirectAccess-Einstellungen befinden sich in dem Gruppenrichtlinienobjekt des DirectAccess-Clients. Das Gruppenrichtlinienobjekt wird auf Computer angewendet, die in den Sicherheitsgruppen enthalten sind, die Sie im Assistenten für erste Schritte angeben. Sie können angeben, dass Sicherheitsgruppen in einer beliebigen unterstützten Domäne enthalten sein sollen. Bevor Sie DirectAccess konfigurieren, sollten die Sicherheitsgruppen erstellt werden. Sie können Computer nach Abschluss der DirectAccess-Bereitstellung zur Sicherheitsgruppe hinzufügen, aber beachten Sie, dass wenn Sie Clientcomputer, die in einer anderen Domäne als der Sicherheitsgruppe befinden hinzufügen, das Client-Gruppenrichtlinienobjekt nicht für diese Clients angewendet werden. Wenn Sie beispielsweise SG1 in Domäne A für DirectAccess-Clients erstellen und später Clients von Domäne B zu dieser Gruppe hinzufügen, wird das Client-Gruppenrichtlinienobjekt nicht auf Clients von Domäne B angewendet. Sie können dieses Problem vermeiden, indem Sie eine neue Client-Sicherheitsgruppe für jede Domäne erstellen, die die Clientcomputer enthält. Alternativ dazu können Sie auch das Add-DAClient-Cmdlet mit dem Namen des neuen Gruppenrichtlinienobjekts für die neue Domäne ausführen, wenn Sie keine neue Sicherheitsgruppe erstellen möchten.  
  
## <a name="bkmk_2_2_server"></a>Planen der Directacess-serverbereitstellung  
Es gibt eine Anzahl von Entscheidungen, die bei den DirectAccess-Server bereitstellen möchten:  
  
-   **Netzwerktopologie** -sind zwei Topologien verfügbar, wenn einen DirectAccess-Server bereitstellen:  
  
    -   **Zwei Adapter** – mit zwei Netzwerkadaptern kann DirectAccess kann mit ein Netzwerkadapter direkt mit dem Internet konfiguriert werden können, und der andere mit dem internen Netzwerk verbunden ist. Alternativ kann der Server hinter einem Edgegerät installiert werden, wie z. B. einer Firewall oder einem Router. In dieser Konfiguration ist ein Netzwerkadapter mit dem Umkreisnetzwerk und der andere mit dem internen Netzwerk verbunden.  
  
    -   **Einzelner Netzwerkadapter** -Server ist In dieser Konfiguration der DirectAccess-Client hinter einem edgegerät wie z. B. eine Firewall oder einem Router installiert. Der Netzwerkadapter ist mit dem internen Netzwerk verbunden.  
  
-   **Der Netzwerkadapter** – der DirectAccess-Assistenten erkennt automatisch die Netzwerkadapter auf dem DirectAccess-Server konfiguriert. Sie können sicherstellen, dass die richtigen Adapter ausgewählt sind, aus der **Review** Seite.  
  
-   **IP-HTTPS-Zertifikat** -da keine PKI, die in dieser Bereitstellung erforderlich ist, der Assistent automatisch selbstsignierte Zertifikate für IP-HTTPS und den Netzwerkadressenserver (wenn keine Zertifikate vorhanden sind) bereitgestellt und wird automatisch aktiviert, Kerberos-Proxy. Der Assistent ermöglicht auch NAT64 und DNS64 für die protokollübersetzung in der nur-IPv4-Umgebung. Nachdem der Assistent die Konfiguration erfolgreich angewendet hat, klicken Sie auf **Schließen**.  
  
-   **Windows 7-Clients** -Unterstützung für Windows 7-Clients aus dem Assistenten für erste Schritte kann nicht aktiviert. Dies kann aus der erweiterten Setup-Assistenten aktiviert werden. Weitere Informationen finden Sie unter [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md).  
  
-   **VPN-Konfiguration** – bevor Sie DirectAccess konfigurieren, zu entscheiden, ob Sie beabsichtigen, VPN-Zugriff auf remote-Clients bereitstellen. Sie sollten die VPN-Zugriff bereitstellen, wenn Sie über Clientcomputer in Ihrer Organisation verfügen, die DirectAccess-Konnektivität nicht unterstützen (entweder weil sie nicht verwaltet werden, oder führen Sie ein Betriebssystem für die DirectAccess wird nicht unterstützt). Assistent für erste Schritte wird die VPN-IP-Adresszuweisung, die mithilfe von DHCP konfiguriert und konfiguriert VPN-Clients mithilfe von Active Directory authentifiziert werden.  
  
-   **Force-Tunneling-** – Wenn Sie das Erzwingen von Tunneln verwenden möchten oder können sie in der Zukunft hinzufügen, verwenden Sie [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) eine zwei-Tunnel-Konfiguration bereitstellen. Aufgrund von sicherheitsüberlegungen wird die Tunnelerzwingung in einer einzigen Tunnelkonfiguration nicht unterstützt.  
  
## <a name="BKMK_Links"></a>Vorherigen Schritt  
  
-   [Schritt 1: Planen der grundlegenden DirectAccess-Infrastruktur](da-basic-plan-s1-infrastructure.md)  
  


