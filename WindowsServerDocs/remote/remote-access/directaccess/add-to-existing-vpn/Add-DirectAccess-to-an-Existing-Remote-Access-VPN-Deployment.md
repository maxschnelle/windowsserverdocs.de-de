---
title: Hinzufügen von DirectAccess zu einer vorhandenen Remotezugriffsbereitstellung (VPN)
description: Dieses Thema ist Teil des Handbuchs Hinzufügen von DirectAccess zu einer vorhandenen Remote Zugriffs Bereitstellung (VPN) für Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5db01f7-1ae0-46f2-9be7-8d9e121446b2
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 1ad1b823cf48a2c322c7ccab1799c76993b1e9bf
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314812"
---
# <a name="add-directaccess-to-an-existing-remote-access-vpn-deployment"></a>Hinzufügen von DirectAccess zu einer vorhandenen Remotezugriffsbereitstellung (VPN)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016
  
## <a name="scenario-description"></a><a name="BKMK_OVER"></a>Szenariobeschreibung  
In diesem Szenario wird ein einzelner Computer mit Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 als DirectAccess-Server mit den empfohlenen Einstellungen konfiguriert, nachdem Sie das VPN bereits installiert und konfiguriert haben. Wenn Sie DirectAccess mit Unternehmens Features wie einem Cluster mit Lastenausgleich, der Bereitstellung für mehrere Standorte oder zweistufiger Client Authentifizierung konfigurieren möchten, schließen Sie das in diesem Thema beschriebene Szenario zum Einrichten eines einzelnen Servers ab, und richten Sie dann das Enterprise-Szenario ein, wie unter Bereitstellen des [Remote Zugriffs in einem Unternehmen](../../ras/Deploy-Remote-Access-in-an-Enterprise.md)beschrieben.  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Zum Einrichten eines einzelnen Remotezugriffsservers sind mehrere Planungs- und Bereitstellungsschritte erforderlich.  
  
### <a name="planning-steps"></a>Planungsschritte  
Die Planung besteht aus zwei Phasen:  
  
1.  **Planen der Infrastruktur für den Remote Zugriff**  
  
    In dieser Phase beschreiben Sie die erforderliche Planung zum Einrichten der Netzwerkinfrastruktur, bevor Sie mit der Remotezugriffbereitstellung beginnen. Sie umfasst das Planen der Netzwerk- und Servertopologie, Zertifikate, des Domain Name System (DNS), der Active Directory, die Konfiguration der Gruppenrichtlinienobjekte und des DirectAccess-Netzwerkadressenservers.  
  
2.  **Planen der Bereitstellung des Remote Zugriffs**  
  
    In dieser Phase beschreiben Sie die erforderlichen Planungsschritte zur Vorbereitung der Remotezugriffbereitstellung. Dazu gehört die Planung der Clientcomputer für den Remotezugriff, Server- und Clientauthentifizierungsanforderungen und Infrastrukturserver.  
  
### <a name="deployment-steps"></a>Bereitstellungsschritte  
Die Bereitstellung besteht aus drei Phasen:  
  
1.  **Konfigurieren der Remote Zugriffs Infrastruktur**  
  
    In dieser Phase konfigurieren Sie das Netzwerk und Routing, die Firewalleinstellungen (falls erforderlich), die Zertifikate, DNS-Server, Active Directory- und Gruppenrichtlinienobjekt-Einstellungen und den DirectAccess-Netzwerkadressenserver.  
  
2.  **Konfigurieren der Einstellungen für den Remote Zugriffs Server**  
  
    In dieser Phase konfigurieren Sie die Remotezugriffsclientcomputer, den Remotezugriffsserver und die Infrastrukturserver.  
  
3.  **Überprüfen der Bereitstellung**  
  
    In dieser Phase überprüfen Sie die Bereitstellung auf die ordnungsgemäße Bereitstellung.  
  
## <a name="practical-applications"></a><a name="BKMK_APP"></a>Praktische Anwendungen  
Die Bereitstellung eines einzelnen Remotezugriffsservers bietet Folgendes:  
  
-   **Einfache Zugriffsrechte**  
  
    Verwaltete Client Computer unter Windows 8 und Windows 7 können als DirectAccess-Client Computer konfiguriert werden. Diese Clients können, wenn sie sich im Internet befinden, über DirectAccess auf interne Netzwerkressourcen zugreifen, ohne sich über eine VPN-Verbindung anmelden zu müssen. Clientcomputer, die keines dieser Betriebssysteme verwenden, können per VPN eine Verbindung zum internen Netzwerk herstellen. Sowohl DirectAccess als auch VPN werden über dieselbe Konsole und mit denselben Assistenten verwaltet.  
  
-   **Einfache Verwaltung**  
  
    Die Remoteverwaltung von DirectAccess-Clientcomputern im Internet ist mithilfe von Remotezugriff-Administratoren über DirectAccess möglich, selbst wenn sich die Clientcomputer nicht im internen Unternehmensnetzwerk befinden. Clientcomputer, die nicht den Unternehmensanforderungen entsprechen, können automatisch über Verwaltungsserver gewartet werden.  
  
## <a name="roles-and-features-required-for-this-scenario"></a><a name="BKMK_NEW"></a>Für dieses Szenario erforderliche Rollen und Features  
Die folgende Tabelle enthält die für dieses Szenario erforderlichen Rollen und Features:  
  
|Rolle/Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|---------|-----------------|  
|Remotezugriffs-Rolle|Die Rolle wird über die Server-Manager-Konsole oder Windows PowerShell installiert bzw. deinstalliert. Diese Rolle umfasst DirectAccess (zuvor ein Feature unter Windows Server 2008 R2) sowie die Routing- und RAS-Dienste (zuvor ein Rollendienst unter der Serverrolle für Netzwerkrichtlinien- und Zugriffsdienste). Die Remotezugriffs-Rolle besteht aus zwei Komponenten:<br /><br />1. DirectAccess-und RRAS-VPN (Routing and Remote Access Services): wird in der Remote Zugriffs-Verwaltungskonsole verwaltet.<br />2. RRAS-Routing: wird in der Routing-und RAS-Konsole verwaltet.<br /><br />Die Remotezugriffs-Serverrolle ist von den folgenden Serverfeatures abhängig:<br /><br />-Internetinformationsdienste (IIS)-Webserver: erforderlich, um den Netzwerkadressen Server auf dem Remote Zugriffs Server und den Standardweb Test zu konfigurieren.<br />-Interne Windows-Datenbank: wird für die lokale Kontoführung auf dem Remote Zugriffs Server verwendet.|  
|Feature %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot;|So installieren Sie dieses Feature:<br /><br />-Standardmäßig auf einem RAS-Server, wenn die Remote Zugriffs Rolle installiert ist. Unterstützt die Benutzeroberfläche der Remote-Verwaltungskonsole und die Windows PowerShell-Cmdlets.<br />: Optional auf einem Server installiert, auf dem die Remote Zugriffs-Server Rolle nicht ausgeführt wird. In diesem Fall wird es für die Remoteverwaltung eines RAS-Computers verwendet, der DirectAccess und VPN ausführt.<br /><br />Das Feature "Tools für die Remotezugriffsverwaltung" besteht aus den folgenden Komponenten:<br /><br />-Remote Zugriffs-GUI<br />-Remote Zugriffs Modul für Windows PowerShell<br /><br />Abhängigkeiten umfassen:<br /><br />-Gruppenrichtlinien-Verwaltungskonsole<br />-RAS-Verbindungs-Manager-Verwaltungskit (CMAK)<br />-Windows PowerShell 3,0<br />-Tools und Infrastruktur für die grafische Verwaltung|  
  
## <a name="hardware-requirements"></a><a name="BKMK_HARD"></a>Hardwareanforderungen  
Für dieses Szenario müssen die folgenden Hardwareanforderungen erfüllt werden:  
  
**Server Anforderungen**  
  
-   Ein Computer, der die Hardwareanforderungen für Windows Server 2012 erfüllt.  
  
-   Auf dem Server muss mindestens ein Netzwerkadapter installiert, aktiviert und mit dem internen Netzwerk verbunden sein. Werden zwei Adapter verwendet, sollte ein Adapter mit dem internen Unternehmensnetzwerk und der andere mit dem externen Netzwerk (Internet) verbunden sein.  
  
-   Falls Teredo als IPv4- bis IPv6-Übergangsprotokoll benötigt wird, benötigt der externe Adapter des Servers zwei aufeinanderfolgenden öffentliche IPv4-Adressen. Der Assistent zum Aktivieren von DirectAccess aktiviert nicht Teredo, selbst wenn zwei aufeinanderfolgende IP-Adressen vorhanden sind. Wenn nur eine IP-Adresse verfügbar ist, kann nur IP-HTTPS als Übergangsprotokoll verwendet werden.  
  
-   Mindestens ein Domänencontroller. RAS-Server und DirectAccess-Clients müssen Domänenmitglieder sein.  
  
-   Der Assistent zum Aktivieren von DirectAccess benötigt Zertifikate für IP-HTTPS und den Netzwerkadressenserver. Wenn das SSTP-VPN bereits ein Zertifikat verwendet, wird es für IP-HTTPS erneut verwendet. Wenn das SSTP-VPN nicht konfiguriert ist, können Sie ein Zertifikat für IP-HTTPS konfigurieren oder ein automatisch erstelltes selbstsigniertes Zertifikat verwenden. Für den Netzwerkadressenserver können Sie ein Zertifikat konfigurieren oder ein automatisch erstelltes selbstsigniertes Zertifikat verwenden.  
  
**Client Anforderungen**  
  
-   Auf einem Client Computer muss Windows 8 oder Windows 7 ausgeführt werden.  
  
    > [!NOTE]  
    > Nur die folgenden Betriebssysteme können als DirectAccess-Clients verwendet werden: Windows Server 2012, Windows Server 2008 R2, Windows 8 Enterprise, Windows 7 Enterprise und Windows 7 Ultimate.  
  
**Anforderungen an Infrastruktur und Management Server**  
  
-   Während der Remoteverwaltung von DirectAccess-Clientcomputern initiieren die Clients die Kommunikation mit Verwaltungsservern, z. B. Domänencontrollern, System Center-Konfigurationsservern und Inhaltsregistrierungsstellen (HRA)-Servern, für Dienste, darunter Windows- und Antivirus-Updates sowie Network Access Protection (NAP)-Clientkompatibilität. Die erforderlichen Server sollten bereitgestellt werden, bevor mit der Bereitstellung des Remotezugriffs begonnen wird.  
  
-   Falls der Remotezugriff Client-NAP-Kompatibilität erfordert, sollten die NPS-Server und der HRA bereitgestellt werden, bevor mit der Bereitstellung des Remotezugriffs begonnen wird.  
  
-   Es ist ein DNS-Server erforderlich, auf dem Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 mit SP2 ausgeführt wird.  
  
## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>Software Anforderungen  
Für dieses Szenario müssen die folgenden Softwareanforderungen erfüllt werden:  
  
**Server Anforderungen**  
  
-   Der Remotezugriffsserver muss Domänenmitglied sein. Der Server kann an der Schwelle zum internen Netzwerks oder geschützt durch eine Edgefirewall oder ein anderes Gerät bereitgestellt werden.  
  
-   Wird der RAS-Server durch eine Edgefirewall oder ein NAT-Gerät geschützt, muss das Gerät so konfiguriert sein, dass ein- und ausgehender Datenverkehr für den RAS-Server zugelassen wird.  
  
-   Die Person, die den Remotezugriff auf dem Server einrichtet, muss lokale Administratorberechtigungen für den Server und Benutzerberechtigungen für die Domäne besitzen. Zusätzlich benötigt der Administrator Berechtigungen für die Gruppenrichtlinien, die bei der DirectAccess-Bereitstellung verwendet werden. Um die Features nutzen zu können, die die DirectAccess-Bereitstellung auf mobile Computer beschränken, ist die Berechtigung zum Erstellen von WMI-Filtern für den Domänencontroller erforderlich.  
  
**Remote Zugriffs-Client Anforderungen**  
  
-   DirectAccess-Clients müssen Domänenmitglieder sein. Domänen, die Clients beinhalten, können zur selben Gesamtstruktur gehören wie der RAS-Server, oder sie können eine bidirektionale Vertrauensstellung mit dem RAS-Server und der Domäne innehaben.  
  
-   Eine Active Directory-Sicherheitsgruppe wird benötigt, um die Computer aufzunehmen, die als DirectAccess-Clients konfiguriert werden. Wird beim Konfigurieren der DirectAccess-Clienteinstellungen keine Sicherheitsgruppe angegeben, wird das Client-Gruppenrichtlinienobjekt standardmäßig auf alle Laptopcomputer (die DirectAccess-fähig sind) in der Sicherheitsgruppe "Domänencomputer" angewendet. Nur die folgenden Betriebssysteme können als DirectAccess-Clients verwendet werden: Windows Server 2012, Windows Server 2008 R2, Windows 8 Enterprise, Windows 7 Enterprise und Windows 7 Ultimate.  
  
    > [!NOTE]  
    > Es wird empfohlen, für jede Domäne eine Sicherheitsgruppe zu erstellen, die Computer enthält, die als DirectAccess-Clients konfiguriert werden.  
  

  

