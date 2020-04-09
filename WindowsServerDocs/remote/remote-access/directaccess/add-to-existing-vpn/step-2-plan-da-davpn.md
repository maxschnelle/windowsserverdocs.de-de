---
title: Schritt 2 Planen der DirectAccess-Bereitstellung
description: Dieses Thema ist Teil des Handbuchs Hinzufügen von DirectAccess zu einer vorhandenen Remote Zugriffs Bereitstellung (VPN) für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 72b5b2af-6925-41e0-a3f9-b8809ed711d1
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 98fb738f3535845a2117f2f6547856b9081bd7d4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859543"
---
# <a name="step-2-plan-the-directaccess-deployment"></a>Schritt 2 Planen der DirectAccess-Bereitstellung

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Nach der Planung der Remotezugriffinfrastruktur besteht der nächste Schritt zur Aktivierung von DirectAccess darin, die Einstellungen zum Aktivieren des DirectAccess-Assistenten zu planen.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|Planen der Clientbereitstellung|Planen Sie die Methode zum Verbinden der Clientcomputer mithilfe von DirectAccess. Legen Sie fest, welche verwalteten Computer als DirectAccess-Clients konfiguriert werden sollen.|  
|Planen der Remotezugriffsserverbereitstellung|Planen Sie die Bereitstellung des Remotezugriffsservers.|  
  
## <a name="planning-for-client-deployment"></a><a name="bkmk_2_1_client"></a>Planen der Client Bereitstellung  
Bei der Planung Ihrer Clientbereitstellung müssen zwei Entscheidungen getroffen werden:  
  
-   Soll DirectAcess für alle oder nur für mobile Computer verfügbar sein?  
  
    Bei der Konfiguration der DirectAccess-Clients im Assistenten zum Aktivieren von DirectAccess können Sie auswählen, dass nur mobile Computer in den angegebenen Sicherheitsgruppen eine Verbindung über DirectAccess aufbauen können. Wenn Sie nur den Zugriff für mobile Computer zulassen, konfiguriert der Remotezugriff automatisch einen WMI-Filter, um sicherzustellen, dass das Gruppenrichtlinienobjekt des DirectAccess-Clients nur auf mobile Computer in den angegebenen Sicherheitsgruppen angewendet wird. Der Remotezugriffsadministrator benötigt Berechtigungen zum Erstellen oder Bearbeiten der WMI-Filter für die Gruppenrichtlinie, um diese Einstellung zu aktivieren.  
  
-   In welchen Sicherheitsgruppen sollen die DirectAccess-Clientcomputer enthalten sein?  
  
    Die DirectAccess-Einstellungen befinden sich in dem Gruppenrichtlinienobjekt des DirectAccess-Clients. Das Gruppenrichtlinienobjekt wird auf Computer angewendet, die in den Sicherheitsgruppen enthalten sind, die Sie in dem Assistenten zum Aktivieren von DirectAccess angegeben haben. Sie können angeben, dass Sicherheitsgruppen in einer beliebigen unterstützten Domäne enthalten sein sollen. Bevor Sie den Remotezugriff konfigurieren, sollten die Sicherheitsgruppen erstellt werden. Nach Abschluss der Remotezugriffbereitstellung können Sie Computer zur Sicherheitsgruppe hinzufügen, wenn Sie jedoch Clientcomputer hinzufügen, die sich in einer anderen Domäne befinden wie die Sicherheitsgruppe, dann wird das Client-Gruppenrichtlinienobjekt nicht auf diese Clients angewendet. Wenn Sie beispielsweise SG1 in Domäne A für DirectAccess-Clients erstellen und später Clients von Domäne B zu dieser Gruppe hinzufügen, wird das Client-Gruppenrichtlinienobjekt nicht auf Clients von Domäne B angewendet. Sie können dieses Problem vermeiden, indem Sie eine neue Client-Sicherheitsgruppe für jede Domäne erstellen, die die Clientcomputer enthält. Alternativ dazu können Sie auch das Add-DAClient-Cmdlet mit dem Namen des neuen Gruppenrichtlinienobjekts für die neue Domäne ausführen, wenn Sie keine neue Sicherheitsgruppe erstellen möchten.  
  
## <a name="planning-for-remote-access-server-deployment"></a><a name="bkmk_2_2_server"></a>Planen der Bereitstellung des Remote Zugriffs Servers  
Beim Planen der Bereitstellung Ihres Remotezugriffsservers müssen Sie mehrere Entscheidungen treffen:  
  
-   **Netzwerktopologie**: bei der Bereitstellung eines Remote Zugriffs Servers sind zwei Topologien verfügbar:  
  
    -   **Zwei Adapter**: mit zwei Netzwerkadaptern kann der Remote Zugriff mit einem direkt mit dem Internet verbundenen Netzwerkadapter konfiguriert werden, während der andere mit dem internen Netzwerk verbunden ist. Alternativ kann der Server hinter einem Edgegerät installiert werden, wie z. B. einer Firewall oder einem Router. In dieser Konfiguration ist ein Netzwerkadapter mit dem Umkreisnetzwerk und der andere mit dem internen Netzwerk verbunden.  
  
    -   **Einzelner Netzwerkadapter**: in dieser Konfiguration wird der RAS-Server hinter einem Edgegerät wie z. b. einer Firewall oder einem Router installiert. Der Netzwerkadapter ist mit dem internen Netzwerk verbunden.  
  
-   **Netzwerkadapter**: der Assistent zum Aktivieren von DirectAccess erkennt automatisch die Netzwerkadapter, die auf dem RAS-Server konfiguriert sind, basierend auf den Schnittstellen, die von VPN verwendet werden. Vergewissern Sie sich, dass die richtigen Adapter ausgewählt sind.  
  
-   **ConnectTo-Adresse**: Client Computer verwenden die ConnectTo-Adresse, um eine Verbindung mit dem Remote Zugriffs Server herzustellen. Die von Ihnen gewählte Adresse muss mit dem Antragstellernamen des IP-HTTPS-Zertifikats übereinstimmen, das Sie für die IP-HTTPS-Verbindung bereitstellen. Außerdem muss sie im öffentlichen DNS verfügbar sein. Weitere Informationen finden Sie unter dem Thema Planen von Websitezertifikaten für IP-HTTPS.  
  
-   **IP-HTTPS-Zertifikat**: Wenn das SSTP-VPN konfiguriert ist, übernimmt der Assistent zum Aktivieren von DirectAccess das Zertifikat, das von SSTP für IP-HTTPS verwendet wird. Wenn SSTP-VPN nicht konfiguriert ist, versucht der Assistent zu ermitteln, ob ein Zertifikate für IP-HTTPS konfiguriert wurde. Falls das nicht der Fall ist, stellt der Assistent automatisch selbstsignierte Zertifikate für IP-HTTPS bereit. Außerdem aktiviert er automatisch die Kerberos-Authentifizierung. Außerdem aktiviert der Assistent NAT64 und DNS64 für die Protokollübersetzung in der auf IPv4 beschränkten Umgebung.  
  
-   **IPv6-Präfixe**: Wenn der Assistent erkennt, dass IPv6 auf den Netzwerkadaptern bereitgestellt wurde, erstellt er automatisch IPv6-Präfixe für das interne Netzwerk, ein IPv6-Präfix, das DirectAccess-Client Computern zugewiesen werden soll, und ein IPv6-Präfix, das VPN-Client Computern zugewiesen werden soll. Wenn die automatisch generierten Präfixe nicht mit Ihrer systemeigenen IPv6- oder ISATAP-Infrastruktur übereinstimmen, müssen Sie sie manuell ändern. Weitere Informationen finden Sie unter 1.1 Planen der Netzwerk- und Servertopologie und -einstellungen.  
  
-   **Windows 7-Clients**: Windows 7-Client Computer können standardmäßig keine Verbindung mit einer Windows Server 2012-Remote Zugriffs Bereitstellung herstellen. Wenn Sie in Ihrer Organisation über Windows 7-Client Computer verfügen, die Remote Zugriff auf interne Ressourcen benötigen, können Sie eine Verbindung herstellen. Clientcomputer, die auf interne Ressourcen zugreifen sollen, müssen Mitglied einer Sicherheitsgruppe sein, die Sie im Assistenten zum Aktivieren von DirectAccess angeben.  
  
    > [!NOTE]
    > Damit Windows 7-Client Computer mithilfe von DirectAccess eine Verbindung herstellen können, müssen Sie die Computer Zertifikat Authentifizierung verwenden.
  
-   **Authentifizierung**: der Assistent zum Aktivieren von DirectAccess verwendet Active Directory, um die Anmelde Informationen des Benutzers zu authentifizieren. Weitere Informationen zum Bereitstellen einer zweistufigen Authentifizierung finden Sie unter [Bereitstellen des Remotezugriffs mit OTP-Authentifizierung](../../ras/otp/Deploy-RA-OTP.md).  
  

  


