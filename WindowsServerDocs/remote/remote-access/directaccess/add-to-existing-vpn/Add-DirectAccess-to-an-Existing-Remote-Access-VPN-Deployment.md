---
title: Hinzufügen von DirectAccess zu einer vorhandenen Remotezugriffsbereitstellung (VPN)
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
ms.assetid: b5db01f7-1ae0-46f2-9be7-8d9e121446b2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1abb0c55cc07641e8a3108fceee4cd8f60446fd8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870321"
---
# <a name="add-directaccess-to-an-existing-remote-access-vpn-deployment"></a>Hinzufügen von DirectAccess zu einer vorhandenen Remotezugriffsbereitstellung (VPN)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016
  
## <a name="BKMK_OVER"></a>Beschreibung des Szenarios  
In diesem Szenario wird ein einzelner Computer mit Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 konfiguriert als DirectAccess-Server mit den empfohlenen Einstellungen nach dem Sie bereits installiert und konfiguriert VPN. Wenn Sie DirectAccess mit Unternehmensfeatures konfigurieren möchten, schließen Sie das Szenario, die in diesem Thema zum Einrichten von eines einzelnen Servers beschrieben, wie z. B. ein NLB-Cluster, Bereitstellung für mehrere Standorte oder zweistufiger Clientauthentifizierung, und richten Sie dann auf das Unternehmen Szenario wie in beschrieben [Bereitstellen des Remotezugriffs in einem Unternehmen](../../ras/Deploy-Remote-Access-in-an-Enterprise.md).  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Zum Einrichten eines einzelnen Remotezugriffsservers sind mehrere Planungs- und Bereitstellungsschritte erforderlich.  
  
### <a name="planning-steps"></a>Planungsschritte  
Die Planung besteht aus zwei Phasen:  
  
1.  **Planen der remotezugriffinfrastruktur**  
  
    In dieser Phase beschreiben Sie die erforderliche Planung zum Einrichten der Netzwerkinfrastruktur, bevor Sie mit der Remotezugriffbereitstellung beginnen. Sie umfasst das Planen der Netzwerk- und Servertopologie, Zertifikate, des Domain Name System (DNS), der Active Directory, die Konfiguration der Gruppenrichtlinienobjekte und des DirectAccess-Netzwerkadressenservers.  
  
2.  **Planen der Bereitstellung des Remotezugriffs**  
  
    In dieser Phase beschreiben Sie die erforderlichen Planungsschritte zur Vorbereitung der Remotezugriffbereitstellung. Dazu gehört die Planung der Clientcomputer für den Remotezugriff, Server- und Clientauthentifizierungsanforderungen und Infrastrukturserver.  
  
### <a name="deployment-steps"></a>Bereitstellungsschritte  
Die Bereitstellung besteht aus drei Phasen:  
  
1.  **Konfigurieren der remotezugriffinfrastruktur**  
  
    In dieser Phase konfigurieren Sie das Netzwerk und Routing, die Firewalleinstellungen (falls erforderlich), die Zertifikate, DNS-Server, Active Directory- und Gruppenrichtlinienobjekt-Einstellungen und den DirectAccess-Netzwerkadressenserver.  
  
2.  **Konfigurieren der Einstellungen des Remotezugriffsservers**  
  
    In dieser Phase konfigurieren Sie die Remotezugriffsclientcomputer, den Remotezugriffsserver und die Infrastrukturserver.  
  
3.  **Überprüfen der Bereitstellung**  
  
    In dieser Phase überprüfen Sie die Bereitstellung auf die ordnungsgemäße Bereitstellung.  
  
## <a name="BKMK_APP"></a>Praktische Anwendungen  
Die Bereitstellung eines einzelnen Remotezugriffsservers bietet Folgendes:  
  
-   **Erleichterte Bedienung**  
  
    Verwaltet die Client-Computern mit Windows 8 und Windows 7 als DirectAccess-Clientcomputer konfiguriert werden können. Diese Clients können, wenn sie sich im Internet befinden, über DirectAccess auf interne Netzwerkressourcen zugreifen, ohne sich über eine VPN-Verbindung anmelden zu müssen. Clientcomputer, die keines dieser Betriebssysteme verwenden, können per VPN eine Verbindung zum internen Netzwerk herstellen. Sowohl DirectAccess als auch VPN werden über dieselbe Konsole und mit denselben Assistenten verwaltet.  
  
-   **Erleichterte Verwaltung**  
  
    Die Remoteverwaltung von DirectAccess-Clientcomputern im Internet ist mithilfe von Remotezugriff-Administratoren über DirectAccess möglich, selbst wenn sich die Clientcomputer nicht im internen Unternehmensnetzwerk befinden. Clientcomputer, die nicht den Unternehmensanforderungen entsprechen, können automatisch über Verwaltungsserver gewartet werden.  
  
## <a name="BKMK_NEW"></a>Für dieses Szenario erforderlichen Rollen und features  
Die folgende Tabelle enthält die für dieses Szenario erforderlichen Rollen und Features:  
  
|Rolle/Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|---------|-----------------|  
|Remotezugriffs-Rolle|Die Rolle wird über die Server-Manager-Konsole oder Windows PowerShell installiert bzw. deinstalliert. Diese Rolle umfasst DirectAccess (zuvor ein Feature unter Windows Server 2008 R2) sowie die Routing- und RAS-Dienste (zuvor ein Rollendienst unter der Serverrolle für Netzwerkrichtlinien- und Zugriffsdienste). Die Remotezugriffs-Rolle besteht aus zwei Komponenten:<br /><br />1.  DirectAccess und Routing- und RAS-Dienste (RRAS) für VPN: Verwaltet in der Remotezugriffs-Verwaltungskonsole.<br />2.  RRAS-Routing: Verwaltet in der Routing- und RAS-Konsole.<br /><br />Die Remotezugriffs-Serverrolle ist von den folgenden Serverfeatures abhängig:<br /><br />-IIS (Internetinformationsdienste) Webserver: erforderlich, um den Netzwerkadressenserver auf dem RAS-Server und den standardwebtest zu konfigurieren.<br />-Interne Windows-Datenbank: Wird zur lokalen Ressourcenerfassung auf dem Remotezugriffsserver verwendet.|  
|Feature %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot;|So installieren Sie dieses Feature:<br /><br />-Standardmäßig auf eine RAS-Server, wenn die Rolle "Remotezugriff" installiert ist. Unterstützt die Benutzeroberfläche der Remote-Verwaltungskonsole und die Windows PowerShell-Cmdlets.<br />-Optionales installiert auf einem Server die Remotezugriffs-Serverrolle nicht ausführt. In diesem Fall wird es für die Remoteverwaltung eines RAS-Computers verwendet, der DirectAccess und VPN ausführt.<br /><br />Das Feature "Tools für die Remotezugriffsverwaltung" besteht aus den folgenden Komponenten:<br /><br />-Remotezugriffs-GUI<br />-RAS-Modul für Windows PowerShell<br /><br />Abhängigkeiten umfassen:<br /><br />-Gruppenrichtlinien-Verwaltungskonsole<br />-RAS-Verbindungs-Manager-Verwaltungskit (CMAK)<br />-Windows PowerShell 3.0<br />-Grafische Verwaltungstools und Infrastruktur|  
  
## <a name="BKMK_HARD"></a>Hardwareanforderungen  
Für dieses Szenario müssen die folgenden Hardwareanforderungen erfüllt werden:  
  
**Serveranforderungen**  
  
-   Ein Computer, der die hardwareanforderungen für Windows Server 2012 erfüllt.  
  
-   Auf dem Server muss mindestens ein Netzwerkadapter installiert, aktiviert und mit dem internen Netzwerk verbunden sein. Werden zwei Adapter verwendet, sollte ein Adapter mit dem internen Unternehmensnetzwerk und der andere mit dem externen Netzwerk (Internet) verbunden sein.  
  
-   Falls Teredo als IPv4- bis IPv6-Übergangsprotokoll benötigt wird, benötigt der externe Adapter des Servers zwei aufeinanderfolgenden öffentliche IPv4-Adressen. Der Assistent zum Aktivieren von DirectAccess aktiviert nicht Teredo, selbst wenn zwei aufeinanderfolgende IP-Adressen vorhanden sind. Wenn nur eine IP-Adresse verfügbar ist, kann nur IP-HTTPS als Übergangsprotokoll verwendet werden.  
  
-   Mindestens ein Domänencontroller. RAS-Server und DirectAccess-Clients müssen Domänenmitglieder sein.  
  
-   Der Assistent zum Aktivieren von DirectAccess benötigt Zertifikate für IP-HTTPS und den Netzwerkadressenserver. Wenn das SSTP-VPN bereits ein Zertifikat verwendet, wird es für IP-HTTPS erneut verwendet. Wenn das SSTP-VPN nicht konfiguriert ist, können Sie ein Zertifikat für IP-HTTPS konfigurieren oder ein automatisch erstelltes selbstsigniertes Zertifikat verwenden. Für den Netzwerkadressenserver können Sie ein Zertifikat konfigurieren oder ein automatisch erstelltes selbstsigniertes Zertifikat verwenden.  
  
**Clientanforderungen**  
  
-   Ein Client-Computer muss Windows 8 oder Windows 7 ausgeführt werden.  
  
    > [!NOTE]  
    > Es können nur die folgenden Betriebssysteme als DirectAccess-Clients verwendet werden: WindowsServer 2012, Windows Server 2008 R2, Windows 8 Enterprise, Windows 7 Enterprise und Windows 7 Ultimate.  
  
**Infrastruktur- und serveranforderungen**  
  
-   Während der Remoteverwaltung von DirectAccess-Clientcomputern initiieren die Clients die Kommunikation mit Verwaltungsservern, z. B. Domänencontrollern, System Center-Konfigurationsservern und Inhaltsregistrierungsstellen (HRA)-Servern, für Dienste, darunter Windows- und Antivirus-Updates sowie Network Access Protection (NAP)-Clientkompatibilität. Die erforderlichen Server sollten bereitgestellt werden, bevor mit der Bereitstellung des Remotezugriffs begonnen wird.  
  
-   Falls der Remotezugriff Client-NAP-Kompatibilität erfordert, sollten die NPS-Server und der HRA bereitgestellt werden, bevor mit der Bereitstellung des Remotezugriffs begonnen wird.  
  
-   Ein DNS-Server unter Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 mit SP2 ist erforderlich.  
  
## <a name="BKMK_SOFT"></a>Softwareanforderungen  
Für dieses Szenario müssen die folgenden Softwareanforderungen erfüllt werden:  
  
**Serveranforderungen**  
  
-   Der Remotezugriffsserver muss Domänenmitglied sein. Der Server kann an der Schwelle zum internen Netzwerks oder geschützt durch eine Edgefirewall oder ein anderes Gerät bereitgestellt werden.  
  
-   Wird der RAS-Server durch eine Edgefirewall oder ein NAT-Gerät geschützt, muss das Gerät so konfiguriert sein, dass ein- und ausgehender Datenverkehr für den RAS-Server zugelassen wird.  
  
-   Die Person, die den Remotezugriff auf dem Server einrichtet, muss lokale Administratorberechtigungen für den Server und Benutzerberechtigungen für die Domäne besitzen. Zusätzlich benötigt der Administrator Berechtigungen für die Gruppenrichtlinien, die bei der DirectAccess-Bereitstellung verwendet werden. Um die Features nutzen zu können, die die DirectAccess-Bereitstellung auf mobile Computer beschränken, ist die Berechtigung zum Erstellen von WMI-Filtern für den Domänencontroller erforderlich.  
  
**RAS-Client-Anforderungen**  
  
-   DirectAccess-Clients müssen Domänenmitglieder sein. Domänen, die Clients beinhalten, können zur selben Gesamtstruktur gehören wie der RAS-Server, oder sie können eine bidirektionale Vertrauensstellung mit dem RAS-Server und der Domäne innehaben.  
  
-   Eine Active Directory-Sicherheitsgruppe wird benötigt, um die Computer aufzunehmen, die als DirectAccess-Clients konfiguriert werden. Wird beim Konfigurieren der DirectAccess-Clienteinstellungen keine Sicherheitsgruppe angegeben, wird das Client-Gruppenrichtlinienobjekt standardmäßig auf alle Laptopcomputer (die DirectAccess-fähig sind) in der Sicherheitsgruppe "Domänencomputer" angewendet. Es können nur die folgenden Betriebssysteme als DirectAccess-Clients verwendet werden:  WindowsServer 2012, Windows Server 2008 R2, Windows 8 Enterprise, Windows 7 Enterprise und Windows 7 Ultimate.  
  
    > [!NOTE]  
    > Es wird empfohlen, für jede Domäne eine Sicherheitsgruppe zu erstellen, die Computer enthält, die als DirectAccess-Clients konfiguriert werden.  
  

  

