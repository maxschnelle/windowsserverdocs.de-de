---
title: Verwalten des Remotezugriffs
description: Dieses Thema enthält Informationen zum Verwalten des Remote Zugriffs in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 1459819a-b1b6-4800-8770-4a85d02c7a2b
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 19798c5fb29d3b8aea68b29e5a42775970eeca46
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857449"
---
# <a name="manage-remote-access"></a>Verwalten des Remotezugriffs

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Im Bereitstellungsszenario "DirectAccess-Clientremoteverwaltung" wird DirectAccess verwendet, um Clients über das Internet zu verwalten. In diesem Abschnitt wird das Szenario samt Phasen, Rollen, Features und Links zu weiteren Ressourcen beschrieben.  
  
Windows Server 2016 und Windows Server 2012 kombinieren DirectAccess-und RRAS-VPN (Routing and Remote Access Service, Routing-und RAS-Dienst) zu einer einzigen Remote Zugriffs Rolle.   
  
> [!NOTE]  
> Über dieses Thema hinaus sind die folgenden Themen zur Verwaltung des Remotezugriffs verfügbar.  
>   
> -   [Verwenden der Remotezugriffsüberwachung und Ressourcenerfassung](monitoring-and-accounting/Use-Remote-Access-Monitoring-and-Accounting.md)  
> -   [Remoteverwaltung von DirectAccess-Clients](manage-remote-clients/Manage-DirectAccess-Clients-Remotely.md)  
  
## <a name="scenario-description"></a><a name="BKMK_OVER"></a>Szenariobeschreibung  
DirectAccess-Clientcomputer sind unabhängig davon, ob der Benutzer sich am Computer angemeldet hat, mit dem Intranet verbunden. Sie können als Intranetressourcen verwaltet werden und mithilfe von Gruppenrichtlinienänderungen, Betriebssystemupdates, Updates von Antischadsoftware und anderen organisatorischen Änderungen aktualisiert werden.  
  
In einigen Fällen müssen Intranetserver oder -computer Verbindungen mit DirectAccess-Clients initiieren. So können beispielsweise Mitarbeiter der Helpdeskabteilung über den Remotedesktop eine Verbindung mit DirectAccess-Remoteclients herstellen und Probleme beheben. Bei diesem Szenario wird die bestehende Remotezugriffslösung zwecks Benutzerkonnektivität beibehalten, während DirectAccess für die Remoteverwaltung verwendet wird.  
  
DirectAccess bietet eine Konfiguration, die die Remote Verwaltung von DirectAccess-Clients unterstützt. Dies erfolgt mithilfe einer Option im Bereitstellungs-Assistenten, die die Erstellung von Richtlinien auf solche Richtlinien beschränkt, die für die Remoteverwaltung von Clientcomputer benötigt werden.  
  
> [!NOTE]  
> Bei dieser Bereitstellung sind Konfigurationsoptionen auf Benutzerebene, beispielsweise Tunnelerzwingung, Integration in den Netzwerkzugriffsschutz (Network Access Protection, NAP) und zweistufige Authentifizierung, nicht verfügbar.  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Das Szenario der DirectAccess-Bereitstellung für die Remoteverwaltung von Clients umfasst für die Planung und Konfiguration die folgenden Schritte:  
  
### <a name="plan-the-deployment"></a>Planen der Bereitstellung  
Für die Planung dieses Szenarios müssen nur wenige Computer- und Netzwerkanforderungen erfüllt werden. Dazu gehören:  
  
-   **Netzwerk- und Servertopologie**: Mit DirectAccess können Sie den Remotezugriffsserver am Rand des Intranets oder hinter einem NAT-Gerät (Network Address Translation, Netzwerkadressenübersetzung) oder einer Firewall platzieren.  
  
-   **DirectAccess-Netzwerkadressenserver**: Der Netzwerkadressenserver wird von DirectAccess-Clients verwendet, um festzustellen, ob sie sich im internen Netzwerk befinden. Der Netzwerkadressenserver kann auf dem DirectAccess-Server oder auf einem anderen Server installiert werden.  
  
-   **DirectAccess-Clients**: Legen Sie fest, welche verwalteten Computer als DirectAccess-Clients konfiguriert werden sollen.  
  
### <a name="configure-the-deployment"></a>Konfigurieren des Bereitstellung  
Das Konfigurieren der Bereitstellung besteht aus einer Reihe von Schritten. Dazu gehören:  
  
1.  **Konfigurieren der Infrastruktur**: Konfigurieren Sie DNS-Einstellungen, fügen Sie den Server und die Clientcomputer bei Bedarf einer Domäne hinzu, und konfigurieren Sie Active Directory-Sicherheitsgruppen.  
  
    Bei diesem Bereitstellungsszenario werden Gruppenrichtlinienobjekte automatisch vom Remotezugriff erstellt. Erweiterte Optionen für das Gruppenrichtlinien Objekt finden Sie unter Bereitstellen des [erweiterten Remote Zugriffs](assetId:///3475e527-541f-4a34-b940-18d481ac59f6).  
  
2.  **Konfigurieren der RAS-Server- und Netzwerkeinstellungen**: Konfigurieren Sie Netzwerkadapter, IP-Adressen und Routing.  
  
3.  **Konfigurieren von Zertifikat Einstellungen**: in diesem Bereitstellungs Szenario erstellt der Assistent für die ersten Schritte selbst signierte Zertifikate, sodass die erweiterte Zertifikat Infrastruktur nicht konfiguriert werden muss.  
  
4.  **Konfigurieren des Netzwerkadressenservers**:  Bei diesem Szenario ist der Netzwerkadressenserver auf dem Remotezugriffsserver installiert.  
  
5.  **Planen der DirectAccess-Verwaltungsserver**: Administratoren können DirectAccess-Clientcomputer, die sich außerhalb des Unternehmensnetzwerks befinden, remote über das Internet verwalten. Verwaltungsserver sind Computer, die für die Verwaltung von Remoteclients verwendet werden (beispielsweise Updateserver).  
  
6.  **Konfigurieren des Remotezugriffsservers**: Installieren Sie die Rolle "Remotezugriff", und führen Sie den DirectAccess-Assistenten für erste Schritte aus, um DirectAccess zu konfigurieren.  
  
7.  **Überprüfen der Bereitstellung**: Testen Sie einen Client, um sicherzustellen, dass er mithilfe von DirectAccess eine Verbindung mit dem internen Netzwerk und dem Internet herstellen kann.  
  
## <a name="practical-applications"></a><a name="BKMK_APP"></a>Praktische Anwendungen  
Die Bereitstellung eines einzelnen Remotezugriffsservers für die Verwaltung von DirectAccess-Clients bietet Folgendes:  
  
-   **Einfache Zugriffs**Möglichkeiten: verwaltete Client Computer, auf denen Windows 8 oder Windows 7 ausgeführt wird, können als DirectAccess-Client Computer konfiguriert werden. Diese Clients können bei aktiver Verbindung mit dem Internet über DirectAccess auf interne Netzwerkressourcen zugreifen, ohne sich über eine VPN-Verbindung anmelden zu müssen. Clientcomputer, die keines dieser Betriebssysteme verwenden, können per VPN eine Verbindung mit dem internen Netzwerk herstellen. Sowohl DirectAccess als auch VPN werden über dieselbe Konsole und mit denselben Assistenten verwaltet.  
  
-   **Erleichterte Verwaltung**: Die Remoteverwaltung von DirectAccess-Clientcomputern im Internet ist mithilfe von Remotezugriffsadministratoren über DirectAccess möglich, selbst wenn sich die Clientcomputer nicht im internen Unternehmensnetzwerk befinden. Clientcomputer, die nicht den Unternehmensanforderungen entsprechen, können automatisch über Verwaltungsserver gewartet werden. Einer oder mehrere RAS-Server können über eine einzelne Remotezugriff-Verwaltungskonsole verwaltet werden.  
  
## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und Features  
Die folgende Tabelle enthält die für dieses Szenario erforderlichen Rollen und Features:  
  
|Rolle oder Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|----------|-----------------|  
|*Remote Zugriffs Rolle*|Die Rolle wird über die Server-Manager-Konsole oder Windows PowerShell installiert bzw. deinstalliert. Diese Rolle umfasst DirectAccess (zuvor ein Feature unter Windows Server 2008 R2) sowie die Routing- und RAS-Dienste (zuvor ein Rollendienst unter der Serverrolle für Netzwerkrichtlinien- und Zugriffsdienste). Die Remotezugriffs-Rolle besteht aus zwei Komponenten:<p>1. DirectAccess-und RRAS-VPN (Routing and Remote Access Services): DirectAccess und VPN werden in der Remote Zugriffs-Verwaltungskonsole verwaltet.<br />2. RRAS: Features werden in der Routing-und RAS-Konsole verwaltet.<p>Die Serverrolle "Remotezugriff" ist von den folgenden Features abhängig:<p>-Webserver (IIS): ist erforderlich, um den Netzwerkadressen Server und den Standardweb Test zu konfigurieren.<br />-Interne Windows-Datenbank: wird für die lokale Kontoführung auf dem Remote Zugriffs Server verwendet.|  
|Feature %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot;|So installieren Sie dieses Feature:<p>-Standardmäßig auf einem RAS-Server, wenn die Remote Zugriffs Rolle installiert ist und die Benutzeroberfläche der Remote Verwaltungskonsole unterstützt.<br />-Als Option auf einem Server, auf dem die Remote Zugriffs-Server Rolle nicht ausgeführt wird. In diesem Fall wird es für die Remoteverwaltung eines RAS-Servers verwendet.<p>Dieses Feature umfasst Folgendes:<p>-Remote Zugriffs-GUI und Befehlszeilen Tools<br />-Remote Zugriffs Modul für Windows PowerShell<p>Abhängigkeiten umfassen:<p>-Gruppenrichtlinien-Verwaltungskonsole<br />-RAS-Verbindungs-Manager-Verwaltungskit (CMAK)<br />-Windows PowerShell 3,0<br />-Tools und Infrastruktur für die grafische Verwaltung|  
  
## <a name="hardware-requirements"></a><a name="BKMK_HARD"></a>Hardwareanforderungen  
Für dieses Szenario müssen die folgenden Hardwareanforderungen erfüllt werden:  
  
### <a name="server-requirements"></a>Serveranforderungen  
  
-   Ein Computer, der die Hardwareanforderungen für Windows Server 2016 erfüllt. Weitere Informationen finden Sie unter [System Anforderungen](https://technet.microsoft.com/windows-server-docs/get-started/system-requirements-and-installation)für Windows Server 2016.  
  
-   Auf dem Server muss mindestens ein Netzwerkadapter installiert und aktiviert sein. Es darf nur ein Adapter an das interne Unternehmensnetzwerk und einer an das externe Netzwerk (Internet) angeschlossen sein.  
  
-   Falls Teredo als IPv6- bis IPv4-Übergangsprotokoll benötigt wird, benötigt der externe Adapter des Servers zwei aufeinanderfolgenden öffentliche IPv4-Adressen. Wenn nur eine Netzwerkkarte verfügbar ist, kann nur IP-HTTPS als Übergangsprotokoll verwendet werden.  
  
-   Mindestens ein Domänencontroller. Der RAS-Server und die DirectAccess-Clients müssen Domänenmitglieder sein.  
  
-   Eine Zertifizierungsstelle ist auf dem Server erforderlich, wenn Sie keine selbstsignierten Zertifikate für IP-HTTPS oder den Netzwerkadressenserver verwenden möchten, oder wenn Sie Clientzertifikate zur IPsec-Clientauthentifizierung verwenden möchten.  
  
### <a name="client-requirements"></a>Clientanforderungen  
  
-   Auf einem Client Computer muss Windows 10, Windows 8 oder Windows 7 ausgeführt werden.  
  
### <a name="infrastructure-and-management-server-requirements"></a>Anforderungen an Infrastruktur und Verwaltungsserver  
  
-   Während der Remoteverwaltung von DirectAccess-Clientcomputern initiieren die Clients die Kommunikation mit Verwaltungsservern, z. B. Domänencontrollern, System Center-Konfigurationsservern und Servern für Inhaltsregistrierungsstellen (Health Registration Authority, HRA). Diese Server bieten Dienste für Windows- und Antivirenupdates und NAP-Clientkompatibilität (Network Access Protection, Netzwerkzugriffsschutz). Die erforderlichen Server müssen bereitgestellt sein, bevor mit der Bereitstellung des Remotezugriffs begonnen wird.  
  
-   Es ist ein DNS-Server erforderlich, auf dem Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 mit SP2 ausgeführt wird.  
  
## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>Software Anforderungen  
Für dieses Szenario müssen die folgenden Softwareanforderungen erfüllt werden:  
  
### <a name="server-requirements"></a>Serveranforderungen  
  
-   Der Remotezugriffsserver muss Domänenmitglied sein. Der Server kann an der Schwelle zum internen Netzwerks oder geschützt durch eine Edgefirewall oder ein anderes Gerät bereitgestellt werden.  
  
-   Wird der RAS-Server durch eine Edgefirewall oder ein NAT-Gerät geschützt, muss das Gerät so konfiguriert sein, dass ein- und ausgehender Datenverkehr für den RAS-Server zugelassen wird.  
  
-   Administratoren, die einen Remotezugriffsserver bereitstellen, müssen lokale Administratorberechtigungen für den Server und Domänenbenutzerberechtigungen für die Domäne haben. Zusätzlich benötigt der Administrator Berechtigungen für die Gruppenrichtlinien, die bei der DirectAccess-Bereitstellung verwendet werden. Um die Features nutzen zu können, die die DirectAccess-Bereitstellung auf mobile Computer beschränken, ist die Berechtigung, WMI-Filter zu erstellen (Domänenadministratoren) für den Domänencontroller erforderlich.  
  
-   Befindet sich der Netzwerkadressenserver nicht auf dem RAS-Server, ist ein separater Server für die Ausführung erforderlich.  
  
### <a name="remote-access-client-requirements"></a>Remotezugriffs-Client-Anforderungen  
  
-   DirectAccess-Clients müssen Domänenmitglieder sein. Domänen, die Clients beinhalten, können zur selben Gesamtstruktur gehören wie der RAS-Server, oder sie können eine bidirektionale Vertrauensstellung mit dem RAS-Server und der Domäne innehaben.  
  
-   Eine Active Directory-Sicherheitsgruppe wird benötigt, um die Computer aufzunehmen, die als DirectAccess-Clients konfiguriert werden. Computer dürfen immer nur einer Sicherheitsgruppe zugeordnet werden, die DirectAccess-Clients enthält. Wenn Clients in mehreren Gruppen enthalten sind, funktioniert die Namensauflösung für Clientanforderungen nicht wie erwartet.  
  

