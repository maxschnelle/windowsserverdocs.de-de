---
title: Schritt 2-Plan, die erweiterte DirectAccess-Bereitstellungen
description: Dieses Thema ist Teil des Handbuchs Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen für Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3bba28d4-23e2-449f-8319-7d2190f68d56
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c946d5bbdf6e8660aaa9e47ced44aed91cfb71da
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283462"
---
# <a name="step-2-plan-advanced-directaccess-deployments"></a>Schritt 2-Plan, die erweiterte DirectAccess-Bereitstellungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Nach der Planung der DirectAccess-Infrastruktur besteht der nächste Schritt der Bereitstellung des erweiterten DirectAccess auf einem einzelnen Server mit IPv4 und IPv6 darin, die Einstellungen für den Remotezugriffs-Setup-Assistenten vorzunehmen.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[2.1 Planen der Clientbereitstellung](#21-plan-for-client-deployment)|Planen Sie die Methode zum Verbinden der Clientcomputer mithilfe von DirectAccess. Entscheiden Sie, welche verwalteten Computer als DirectAccess-Clients konfiguriert werden, und planen Sie die Bereitstellung von NCA (Network Connectivity Assistant) oder DCA (DirectAccess Connectivity Assistant) auf den Clientcomputern.|  
|[2.2 Planen der Directacess-serverbereitstellung](#22-plan-for-directaccess-server-deployment)|Planen Sie die Bereitstellung des DirectAccess-Servers.|  
|[2.3 Planen der Infrastrukturserver](#23-plan-infrastructure-servers)|Planen Sie die Infrastrukturserver für Ihre DirectAccess-Bereitstellung, dazu gehört der DirectAccess-Netzwerkadressenserver, die DNS-Server (Domain Name System) und die DirectAccess-Verwaltungsserver.|  
|[2.4 Planen der Anwendungsserver](#24-plan-application-servers)|Planen Sie die IPv4- und IPv6-Anwendungsserver, und ziehen Sie die optionale Möglichkeit in Betracht, eine obligatorische End-to-End-Authentifizierung zwischen DirectAccess-Clientcomputern und internen Anwendungsservern einzurichten.|  
|[2.5 Planen von DirectAccess und Drittanbieter-VPN-clients](#25-plan-directaccess-and-third-party-vpn-clients)|Bei der Bereitstellung von DirectAccess mit VPN-Clients von Drittanbietern kann es erforderlich sein, die folgenden Registrierungswerte festzulegen, um die nahtlose gleichzeitige Verwendung der beiden Remotezugriffslösungen zu aktivieren.|  
  
## <a name="21-plan-for-client-deployment"></a>2.1 Planen der Clientbereitstellung  
Bei der Planung Ihrer Clientbereitstellung müssen drei Entscheidungen getroffen werden:  
  
1.  Soll DirectAcess für alle oder nur für mobile Computer verfügbar sein?  
  
    Bei der Konfiguration der DirectAccess-Clients im DirectAccess-Client-Setup-Assistenten können Sie auswählen, dass nur mobile Computer in den angegebenen Sicherheitsgruppen eine Verbindung über DirectAccess aufbauen können. Wenn Sie nur den Zugriff für mobile Computer zulassen, konfiguriert der Remotezugriff automatisch einen WMI-Filter, um sicherzustellen, dass das Gruppenrichtlinienobjekt des DirectAccess-Clients nur auf mobile Computer in den angegebenen Sicherheitsgruppen angewendet wird. Der Remotezugriffsadministrator benötigt Sicherheitsberechtigungen zum Erstellen oder Bearbeiten, damit er WMI-Filter für das Gruppenrichtlinienobjekt erstellen oder bearbeiten kann, um diese Einstellung zu aktivieren.  
  
2.  In welchen Sicherheitsgruppen sollen die DirectAccess-Clientcomputer enthalten sein?  
  
    Die DirectAccess-Clienteinstellungen befinden sich in dem Gruppenrichtlinienobjekt des DirectAccess-Clients. Das Gruppenrichtlinienobjekt wird auf Computer angewendet, die in den Sicherheitsgruppen enthalten sind, die Sie in dem DirectAccess-Client-Setup-Assistenten angegeben haben. Sie können angeben, dass Sicherheitsgruppen in einer beliebigen unterstützten Domäne enthalten sein sollen. Weitere Informationen finden Sie im Abschnitt [1.7 Planen der Active Directory Domain Services](da-adv-plan-s1-infrastructure.md#17-plan-active-directory-domain-services).  
  
    Bevor Sie DirectAccess konfigurieren, sollten Sie die Sicherheitsgruppen erstellen. Nach Abschluss der DirectAccess-Bereitstellung können Sie Computer zur Sicherheitsgruppe hinzufügen, wenn Sie jedoch Clientcomputer hinzufügen, die sich in einer anderen Domäne befinden wie die Sicherheitsgruppe, dann wird das Client-Gruppenrichtlinienobjekt nicht auf diese Clients angewendet. Wenn Sie beispielsweise SG1 in Domäne A für DirectAccess-Clients erstellen und später Clients von Domäne B zu dieser Gruppe hinzufügen, wird das Client-Gruppenrichtlinienobjekt nicht auf Clients von Domäne B angewendet. Sie können dieses Problem vermeiden, indem Sie eine neue Client-Sicherheitsgruppe für jede Domäne erstellen, die die DirectAccess-Clientcomputer enthält. Alternativ dazu können Sie auch das Windwows PowerShell-Cmdlet **Add-DAClient** mit dem Namen des neuen Gruppenrichtlinienobjekts für die neue Domäne ausführen, wenn Sie keine neue Sicherheitsgruppe erstellen möchten.  
  
3.  Welche Einstellungen müssen für den Netzwerkkonnektivitäts-Assistenten konfiguriert werden?  
  
    Der Netzwerkkonnektivitäts-Assistent wird auf Clientcomputern ausgeführt, er stellt zusätzliche Informationen zur DirectAccess-Verbindung mit Endbenutzern bereit. Im DirectAccess-Client-Setup-Assistenten können Sie Folgendes konfigurieren:  
  
    -   **Verbindungsprüfer**  
  
        Ein Standardwebtest wird erstellt, den Clients verwenden, um die Verbindung zum internen Netzwerk zu prüfen. Der Standardname lautet:  
  
        https://directaccess-WebProbeHost.<domain_name>  
  
        Der Name sollte manuell im DNS registriert werden. Mithilfe anderer Webadressen über HTTP oder **ping** können Sie weitere Verbindungsprüfer erstellen. Für jeden Verbindungsprüfer muss ein DNS-Eintrag vorhanden sein.  
  
    -   **Eine Helpdesk-e-Mail-Adresse**  
  
        Wenn Endbenutzer Probleme mit der DirectAccess-Verbindung haben, können Sie eine E-Mail mit Diagnoseinformationen an den DirectAccess-Administrator senden, um das Problem zu beheben.  
  
    -   **Ein DirectAccess-Verbindungsnamens.**  
  
        Geben Sie einen DirectAccess-Verbindungsnamen an, damit Endbenutzer die DirectAccess-Verbindung auf ihren Computern leichter identifizieren können.  
  
    -   **Ermöglichen von DirectAccess-Clients, die lokale namensauflösung verwenden**  
  
        Clients benötigen eine Methode, um Namen lokal aufzulösen. Wenn Sie zulassen, dass DirectAccess-Clients die lokale Namensauflösung verwenden, können Endbenutzer zum Auflösen von Namen lokale DNS-Server verwenden. Wenn Endbenutzer die Verwendung lokaler DNS-Server zur Namensauflösung auswählen, sendet DirectAccess keine Anforderungen zum Auflösen einzelner Bezeichnungsnamen an den internen Unternehmens-DNS-Server. Stattdessen verwendet er die lokale Namensauflösung, indem er die Multicastnamenauflösung für lokale Verbindungen (Link-Local Multicast Name Resolution, LLMNR) und NetBIOS über TCP/IP-Protokolle verwendet.  
  
## <a name="22-plan-for-directaccess-server-deployment"></a>2.2 Planen der DirectAcess-Serverbereitstellung  
Berücksichtigen Sie folgende Entscheidungen bei der Bereitstellung Ihres DirectAccess-Servers:  
  
-   **Netzwerktopologie**  
  
    Bei der Bereitstellung eines DirectAccess-Servers sind mehrere Topologien verfügbar:  
  
    -   **Zwei Netzwerkadapter**. Mit zwei Netzwerkadaptern kann DirectAccess so konfiguriert werden, dass ein Netzwerkadapter direkt mit dem Internet und der andere mit dem internen Netzwerk verbunden ist. Alternativ kann der Server hinter einem Edgegerät installiert werden, wie z. B. einer Firewall oder einem Router. In dieser Konfiguration ist ein Netzwerkadapter direkt mit dem Umkreisnetzwerk und der andere mit dem internen Netzwerk verbunden.  
  
    -   **Ein Netzwerkadapter**. In dieser Konfiguration ist der Server hinter einem Edgegerät wie z. B. einer Firewall oder einem Router installiert. Der Netzwerkadapter ist mit dem internen Netzwerk verbunden.  
  
    Weitere Informationen zur Auswahl der Topologie für Ihre Bereitstellung finden Sie unter [1.1 Plan-Netzwerktopologie und-Einstellungen](da-adv-plan-s1-infrastructure.md#11-plan-network-topology-and-settings).  
  
-   **ConnectTo-Adresse**  
  
    Clientcomputer verwenden die ConnectTo-Adresse, um eine Verbindung zum DirectAccess-Server herzustellen. Die von Ihnen gewählte Adresse muss mit dem Antragstellernamen des IP-HTTPS-Zertifikats übereinstimmen, das Sie für die IP-HTTPS-Verbindung bereitstellen. Außerdem muss sie im öffentlichen DNS verfügbar sein.  
  
-   **Leistungsverlauf für Netzwerkadapter**  
  
    Der Setup-Assistent für den Remotezugriffsserver erkennt automatisch die Netzwerkadapter, die auf dem DirectAccess-Server konfiguriert sind. Vergewissern Sie sich, dass die richtigen Adapter ausgewählt sind.  
  
-   **IP-HTTPS-Zertifikat**  
  
    Der Setup-Assistent für den Remotezugriffsserver erkennt automatisch ein Zertifikat, das für die IP-HTTPS-Verbindung geeignet ist. Der Antragstellername von Ihnen gewählten Zertifikats muss mit der ConnectTo-Adresse übereinstimmen. Wenn Sie selbstsignierte Zertifikate verwenden, können Sie die Verwendung eines Zertifikats auswählen, das automatisch vom Remotezugriffsserver erstellt wird.  
  
-   **IPv6-Präfixe**  
  
    Wenn der Setup-Assistent für den Remotezugriffsserver erkennt, dass IPv6 auf den Netzwerkadaptern bereitgestellt wurde, füllt er automatisch IPv6-Präfixe für das interne Netzwerk auf. Ein IPv6-Präfix zum Zuweisen für die DirectAccess-Clientcomputer und ein IPv6-Präfix zum Zuweisen für die VPN-Clientcomputer. Wenn die automatisch generierten Präfixe nicht mit Ihrer systemeigenen IPv6-Infrastruktur übereinstimmen, müssen Sie sie manuell ändern. Weitere Informationen finden Sie unter [1.1 Plan-Netzwerktopologie und-Einstellungen](da-adv-plan-s1-infrastructure.md#11-plan-network-topology-and-settings).  
  
-   **Authentifizierung**  
  
    Entscheiden Sie, wie DirectAccess-Clients sich mit dem DirectAccess-Server authentifizieren sollen:  
  
    -   **Benutzerauthentifizierung**. Sie können für Benutzer die zweistufige oder die Authentifizierung mit Active Directory-Anmeldeinformationen aktivieren. Weitere Informationen zur zweistufigen Authentifizierung finden Sie unter [Bereitstellen des Remotezugriffs mit OTP-Authentifizierung](https://technet.microsoft.com/library/hh831379.aspx).  
  
    -   **Computerauthentifizierung**. Sie können die Computerauthentifizierung so konfigurieren, dass sie im Auftrag des Clients Zertifikate oder den DirectAccess-Server als Kerberos-Proxy verwendet. Weitere Informationen finden Sie unter [1.3 Plan zertifikatanforderungen](da-adv-plan-s1-infrastructure.md#13-plan-certificate-requirements).  
  
    -   **Windows 7-Clients**. Standardmäßig Verbindung keine Clientcomputer, auf denen Windows 7 ausführen, mit einer Windows Server 2012 R2 oder Windows Server 2012 DirectAccess-Bereitstellung. Wenn Sie Clients in Ihrer Organisation, die Windows 7 ausgeführt werden, und der Remotezugriff auf interne Ressourcen benötigen, können Sie eine Verbindung hergestellt. Clientcomputer, die auf interne Ressourcen zugreifen sollen, müssen Mitglied einer Sicherheitsgruppe sein, die Sie im DirectAccess-Client-Setup-Assistenten angeben.  
  
        > [!NOTE]  
        > Ermöglicht Clients, auf denen Windows 7 mithilfe von DirectAccess eine Verbindung herstellen muss, dass Sie die Computerzertifikatauthentifizierung verwenden.  
  
-   **VPN-Konfiguration**  
  
    Entscheiden Sie, ob ein VPN-Zugriff auf nicht DirectAccess-fähige Remoteclients bereitgestellt werden soll, bevor Sie DirectAccess konfigurieren. Sie sollten einen VPN-Zugriff bereitstellen, wenn Sie in Ihrer Organisation über Clientcomputer verfügen, die die DirectAccess-Konnektivität nicht unterstützen (da sie nicht verwaltet werden oder ein Betriebssystem einsetzen, bei dem DirectAccess nicht unterstützt wird). Mit dem Setup-Assistent für den Remotezugriffsserver können Sie konfigurieren, wie IP-Adressen zugewiesen werden (über DHCP oder einen Pool statischer Adressen) und wie VPN-Clients authentifiziert werden - mithilfe des Active Directory oder eines RADIUS-Servers (Remote Authentication Dial-Up Service).  
  
## <a name="23-plan-infrastructure-servers"></a>2.3 Planen der Infrastrukturserver  
Für DirectAccess sind drei Typen von Infrastrukturservern erforderlich:  
  
-   **DNS-Server**. Weitere Informationen finden Sie im Abschnitt [1.4 Planen von DNS-Anforderungen](da-adv-plan-s1-infrastructure.md#14-plan-dns-requirements).  
  
-   **Netzwerkadressenserver**. Weitere Informationen finden Sie unter [1.5 Planen des Netzwerkadressenservers](da-adv-plan-s1-infrastructure.md#15-plan-the-network-location-server).  
  
-   **Verwaltungsserver**. Weitere Informationen finden Sie unter [1.6 Planen von Verwaltungsservern](da-adv-plan-s1-infrastructure.md#16-plan-management-servers).  
  
## <a name="24-plan-application-servers"></a>2.4 Planen der Anwendungsserver  
Anwendungsserver sind Server im Unternehmensnetzwerk, die von Clientcomputern über eine DirectAccess-Verbindung zugänglich sind. Anwendungsserver werden identifiziert, indem Sie in einer Sicherheitsgruppe hinzugefügt werden. Das Gruppenrichtlinienobjekt des Anwendungsservers wird dann auf die Server in der Gruppe angewendet.  
  
> [!NOTE]  
> Das Hinzufügen von Anwendungsservern zu einer Sicherheitsgruppe ist nur erforderlich, wenn Sie eine End-to-End-Authentifizierung und -Verschlüsselung benötigen.  
  
Optional können Sie auch die End-to-End-Authentifizierung und -Verschlüsselung zwischen DirectAccess-Client und ausgewählten internen Anwendungsservern voraussetzen. Wenn Sie die End-to-End-Authentifizierung konfigurieren, verwenden DirectAccess-Clients eine IPsec-Transportrichtlinie. Bei der Verwendung dieser Richtlinie muss die Authentifizierung und der Schutz der IPsec-Sitzungen auf den angegebenen Anwendungsservern beendet werden. In diesem Fall leitet der Remotezugriffsserver die authentifizierten und geschützten IPsec-Sitzungen an die Anwendungsserver weiter.  
  
Standardmäßig wird bei der Erweiterung der Authentifizierung auf Anwendungsserver die Datennutzlast zwischen DirectAccess-Client und Anwendungsserver verschlüsselt. Sie können auch auswählen, den Datenverkehr nicht zu verschlüsseln und nur die Authentifizierung verwenden. Allerdings ist dies weniger sicher als die Verwendung von Authentifizierung und Verschlüsselung, und wird nur für Anwendungsserver, die Ausführung des Windows Server 2008 R2 oder Windows Server 2012-Betriebssystemen unterstützt.  
  
## <a name="25-plan-directaccess-and-third-party-vpn-clients"></a>2.5 Planen von DirectAccess und VPN-Clients von Drittanbietern  
Einige VPN-Clients von Drittanbietern erstellen im Ordner Netzwerkverbindungen keine Verbindungen. Dies kann dazu führen, dass DirectAccess keine Intranetkonnektivität erkennt, wenn die VPN-Verbindung hergestellt ist und eine Verbindung zum Intranet besteht. Diese Bedingung tritt auf, wenn VPN-Clients von Drittanbietern ihre Schnittstellen registrieren, indem sie diese als (NDIS) ENDPOINT-Typen (Network Device Interface Specification) definieren. Sie können die gleichzeitige Verwendung dieser VPN-Clienttypen aktivieren, indem Sie den folgenden Registrierungswert auf 1 festlegen.  
  
**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\NlaSvc\Parameters\ShowDomainEndpointInterfaces (REG_DWORD)**  
  
Einige VPN-Clients von Drittanbietern verwenden eine Konfiguration mit geteiltem Tunneln, sodass der VPN-Clientcomputer direkt auf das Internet zugreifen kann, ohne den Datenverkehr über die VPN-Verbindung an das Intranet senden zu müssen.  
  
Bei Konfigurationen mit geteiltem Tunneln wird die Standardgatewayeinstellung für den VPN-Client in der Regel als nicht konfiguriert oder als nur Nullen (0.0.0.0) belassen. Sie können dieses Verhalten prüfen, indem Sie eine erfolgreiche VPN-Verbindung zum Intranet herstellen und das Ipconfig.exe-Befehlszeilentool verwenden, um die entsprechende Konfiguration anzuzeigen.  
  
Wenn die VPN-Verbindung das Standardgateway als leer oder nur Nullen (0.0.0.0) anzeigt, ist Ihr  VPN-Client entsprechend konfiguriert. Standardmäßig erkennt der DirectAccess-Client geteilte Tunnelkonfigurationen nicht. Um DirectAccess-Clients für eine Erkennung dieser VPN-Clientkonfigurationstypen zu konfigurieren, müssen Sie den folgenden Registrierungswert auf 1 festlegen.  
  
**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\services\NlaSvc\Parameters\Internet\ EnableNoGatewayLocationDetection (REG_DWORD)**  
  
## <a name="previous-step"></a>Vorheriger Schritt  
  
-   [Schritt 1: Planen der DirectAccess-Infrastruktur](da-adv-plan-s1-infrastructure.md)  
  


