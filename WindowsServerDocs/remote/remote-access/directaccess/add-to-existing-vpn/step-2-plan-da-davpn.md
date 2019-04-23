---
title: Schritt 2 planen die DirectAccess-Bereitstellung
description: Dieses Thema ist Teil des Handbuchs Add DirectAccess zu einer vorhandenen Remotezugriffsbereitstellung (VPN)-Bereitstellung für WindowsServer 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 72b5b2af-6925-41e0-a3f9-b8809ed711d1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7b4e0e8647fa2011eae73efa8bcbd696c422f12c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859681"
---
# <a name="step-2-plan-the-directaccess-deployment"></a>Schritt 2 planen die DirectAccess-Bereitstellung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Nach der Planung der Remotezugriffinfrastruktur besteht der nächste Schritt zur Aktivierung von DirectAccess darin, die Einstellungen zum Aktivieren des DirectAccess-Assistenten zu planen.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|Planen der Clientbereitstellung|Planen Sie die Methode zum Verbinden der Clientcomputer mithilfe von DirectAccess. Legen Sie fest, welche verwalteten Computer als DirectAccess-Clients konfiguriert werden sollen.|  
|Planen der Remotezugriffsserverbereitstellung|Planen Sie die Bereitstellung des Remotezugriffsservers.|  
  
## <a name="bkmk_2_1_client"></a>Planen der Clientbereitstellung  
Bei der Planung Ihrer Clientbereitstellung müssen zwei Entscheidungen getroffen werden:  
  
-   Soll DirectAcess für alle oder nur für mobile Computer verfügbar sein?  
  
    Bei der Konfiguration der DirectAccess-Clients im Assistenten zum Aktivieren von DirectAccess können Sie auswählen, dass nur mobile Computer in den angegebenen Sicherheitsgruppen eine Verbindung über DirectAccess aufbauen können. Wenn Sie nur den Zugriff für mobile Computer zulassen, konfiguriert der Remotezugriff automatisch einen WMI-Filter, um sicherzustellen, dass das Gruppenrichtlinienobjekt des DirectAccess-Clients nur auf mobile Computer in den angegebenen Sicherheitsgruppen angewendet wird. Der Remotezugriffsadministrator benötigt Berechtigungen zum Erstellen oder Bearbeiten der WMI-Filter für die Gruppenrichtlinie, um diese Einstellung zu aktivieren.  
  
-   In welchen Sicherheitsgruppen sollen die DirectAccess-Clientcomputer enthalten sein?  
  
    Die DirectAccess-Einstellungen befinden sich in dem Gruppenrichtlinienobjekt des DirectAccess-Clients. Das Gruppenrichtlinienobjekt wird auf Computer angewendet, die in den Sicherheitsgruppen enthalten sind, die Sie in dem Assistenten zum Aktivieren von DirectAccess angegeben haben. Sie können angeben, dass Sicherheitsgruppen in einer beliebigen unterstützten Domäne enthalten sein sollen. Bevor Sie den Remotezugriff konfigurieren, sollten die Sicherheitsgruppen erstellt werden. Nach Abschluss der Remotezugriffbereitstellung können Sie Computer zur Sicherheitsgruppe hinzufügen, wenn Sie jedoch Clientcomputer hinzufügen, die sich in einer anderen Domäne befinden wie die Sicherheitsgruppe, dann wird das Client-Gruppenrichtlinienobjekt nicht auf diese Clients angewendet. Wenn Sie beispielsweise SG1 in Domäne A für DirectAccess-Clients erstellen und später Clients von Domäne B zu dieser Gruppe hinzufügen, wird das Client-Gruppenrichtlinienobjekt nicht auf Clients von Domäne B angewendet. Sie können dieses Problem vermeiden, indem Sie eine neue Client-Sicherheitsgruppe für jede Domäne erstellen, die die Clientcomputer enthält. Alternativ dazu können Sie auch das Add-DAClient-Cmdlet mit dem Namen des neuen Gruppenrichtlinienobjekts für die neue Domäne ausführen, wenn Sie keine neue Sicherheitsgruppe erstellen möchten.  
  
## <a name="bkmk_2_2_server"></a>Planen der Bereitstellung von RAS-server  
Beim Planen der Bereitstellung Ihres Remotezugriffsservers müssen Sie mehrere Entscheidungen treffen:  
  
-   **Netzwerktopologie**-sind zwei Topologien verfügbar, wenn einen RAS-Server bereitstellen:  
  
    -   **Zwei Adapter**– mit zwei Netzwerkadaptern, RAS konfiguriert werden können, ein Netzwerkadapter direkt mit dem Internet verbunden und der andere mit dem internen Netzwerk verbunden ist. Alternativ kann der Server hinter einem Edgegerät installiert werden, wie z. B. einer Firewall oder einem Router. In dieser Konfiguration ist ein Netzwerkadapter mit dem Umkreisnetzwerk und der andere mit dem internen Netzwerk verbunden.  
  
    -   **Einzelner Netzwerkadapter**– In dieser Konfiguration die RAS-Server hinter einem edgegerät wie z. B. eine Firewall oder einem Router installiert ist. Der Netzwerkadapter ist mit dem internen Netzwerk verbunden.  
  
-   **Der Netzwerkadapter**– das Aktivieren von DirectAccess-Assistenten erkennt automatisch die Netzwerkadapter auf dem RAS-Server, basierend auf den vom VPN verwendeten Schnittstellen konfiguriert. Vergewissern Sie sich, dass die richtigen Adapter ausgewählt sind.  
  
-   **ConnectTo-Adresse**-Clientcomputer verwenden die ConnectTo-Adresse, um eine Verbindung mit dem RAS-Server herzustellen. Die von Ihnen gewählte Adresse muss mit dem Antragstellernamen des IP-HTTPS-Zertifikats übereinstimmen, das Sie für die IP-HTTPS-Verbindung bereitstellen. Außerdem muss sie im öffentlichen DNS verfügbar sein. Weitere Informationen finden Sie unter dem Thema Planen von Websitezertifikaten für IP-HTTPS.  
  
-   **IP-HTTPS-Zertifikat**– Wenn SSTP-VPN konfiguriert ist, wird der Aktivieren von DirectAccess-Assistenten übernimmt das von SSTP für IP-HTTPS verwendete Zertifikat. Wenn SSTP-VPN nicht konfiguriert ist, versucht der Assistent zu ermitteln, ob ein Zertifikate für IP-HTTPS konfiguriert wurde. Falls das nicht der Fall ist, stellt der Assistent automatisch selbstsignierte Zertifikate für IP-HTTPS bereit. Außerdem aktiviert er automatisch die Kerberos-Authentifizierung. Außerdem aktiviert der Assistent NAT64 und DNS64 für die Protokollübersetzung in der auf IPv4 beschränkten Umgebung.  
  
-   **IPv6-Präfixe**– Wenn der Assistent erkennt, dass IPv6 auf den Netzwerkadaptern bereitgestellt wurde, erstellt es automatisch IPv6-Präfixe für das interne Netzwerk, ein IPv6-Präfix zum Zuweisen für die DirectAccess-Clientcomputer und ein IPv6-Präfix zum Zuweisen von VPN Client-Computer. Wenn die automatisch generierten Präfixe nicht mit Ihrer systemeigenen IPv6- oder ISATAP-Infrastruktur übereinstimmen, müssen Sie sie manuell ändern. 1.1 Planen der Netzwerk- und Servertopologie und-Einstellungen finden Sie in.  
  
-   **Windows 7-Clients**-standardmäßig Windows 7-Clientcomputer keine Verbindung mit Herstellen einer Remote Access in Windows Server 2012-Bereitstellung. Wenn Sie Windows 7-Clientcomputer in Ihrer Organisation, die Remotezugriff für interne Ressourcen benötigen verfügen, können Sie eine Verbindung hergestellt werden. Clientcomputer, die auf interne Ressourcen zugreifen sollen, müssen Mitglied einer Sicherheitsgruppe sein, die Sie im Assistenten zum Aktivieren von DirectAccess angeben.  
  
    > [!NOTE]
    > Sodass Windows 7-Clientcomputer über DirectAccess eine Verbindung herstellen, müssen Sie Computerzertifikatauthentifizierung verwenden.
  
-   **Authentifizierung**-Assistenten für das Aktivieren von DirectAccess verwendet Active Directory zum Authentifizieren der Anmeldeinformationen des Benutzers. Weitere Informationen zum Bereitstellen einer zweistufigen Authentifizierung finden Sie unter [Bereitstellen des Remotezugriffs mit OTP-Authentifizierung](../../ras/otp/Deploy-RA-OTP.md).  
  

  


