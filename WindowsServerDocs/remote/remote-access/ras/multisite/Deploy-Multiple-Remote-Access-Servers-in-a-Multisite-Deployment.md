---
title: Bereitstellen Sie mehrere RAS-Server in einer Bereitstellung mit mehreren Standorten
description: Dieses Thema ist Teil des Handbuchs Bereitstellen mehrerer Remote Zugriffs Server in einer Bereitstellung mit mehreren Standorten in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac2f6015-50a5-4909-8f67-8565f9d332a2
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 4b9da54822c1b7610bbd7a095beeb305eb243bb1
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314033"
---
# <a name="deploy-multiple-remote-access-servers-in-a-multisite-deployment"></a>Bereitstellen Sie mehrere RAS-Server in einer Bereitstellung mit mehreren Standorten

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

 Windows Server 2016 und Windows Server 2012 kombinieren DirectAccess-und RAS-VPN (RAS-Dienst) zu einer einzigen Remote Zugriffs Rolle. Der Remotezugriff kann in einer Reihe von Unternehmensszenarios bereitgestellt werden. Diese Übersicht bietet eine Einführung in das Unternehmens Szenario für die Bereitstellung von Remote Zugriffs Servern in einer Konfiguration mit mehreren Standorten.  
  
## <a name="scenario-description"></a><a name="BKMK_OVER"></a>Szenariobeschreibung  
In einer Bereitstellung mit mehreren Standorten werden zwei oder mehr RAS-Server oder Server Cluster als verschiedene Einstiegspunkte an einem einzigen Standort oder an verteilten geografischen Orten bereitgestellt und konfiguriert. Durch die Bereitstellung mehrerer Einstiegspunkte an einem einzigen Standort können Server Redundanz oder RAS-Server mit vorhandener Netzwerkarchitektur bereitgestellt werden. Durch die Bereitstellung nach geografischem Standort wird die effiziente Nutzung von Ressourcen sichergestellt, da Remote Client Computer mithilfe eines am nächsten liegenden Einstiegs Punkts eine Verbindung mit internen Netzwerkressourcen herstellen können. Der Datenverkehr in einer Bereitstellung mit mehreren Standorten kann mit einem externen globalen Load Balancer verteilt und ausgeglichen werden.  
  
Bei einer Bereitstellung mit mehreren Standorten werden Client Computer unter Windows 10, Windows 8 oder Windows 7 unterstützt. Auf Client Computern, auf denen Windows 10 oder Windows 8 ausgeführt wird, wird automatisch ein Einstiegspunkt identifiziert, oder der Benutzer kann einen Einstiegspunkt manuell auswählen. Die automatische Zuweisung erfolgt in der folgenden Prioritäts Reihenfolge:  
  
1.  Verwenden Sie einen vom Benutzer manuell ausgewählten Einstiegspunkt.  
  
2.  Verwenden Sie einen Einstiegspunkt, der von einem externen globalen Load Balancer identifiziert wird, wenn ein solcher bereitgestellt wird.  
  
3.  Verwenden Sie den nächstgelegenen Einstiegspunkt, der vom Client Computer mithilfe eines automatischen Test Mechanismus identifiziert wird.  
  
Die Unterstützung für Clients, auf denen Windows 7 ausgeführt wird, muss für jeden Einstiegspunkt manuell aktiviert werden, und die Auswahl eines Einstiegs Punkts durch diese Clients wird nicht unterstützt.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Bevor Sie mit der Bereitstellung dieses Szenarios beginnen, sollten Sie die Liste der wichtigen Anforderungen lesen:  
  
-   Die Bereitstellung [eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) muss vor einer Bereitstellung mit mehreren Standorten bereitgestellt werden.  
  
-   Windows 7-Clients stellen immer eine Verbindung mit einem bestimmten Standort her. Sie sind nicht in der Lage, eine Verbindung mit dem nächstgelegenen Standort basierend auf dem Standort des Clients herzustellen (im Gegensatz zu Windows 10-, 8-oder 8,1-Clients).  
  
-   Das Ändern von Richtlinien außerhalb der DirectAccess-Verwaltungskonsole oder von PowerShell-Cmdlets wird nicht unterstützt.  
  
-   Eine Public Key-Infrastruktur muss bereitgestellt werden.  
  
    Weitere Informationen finden Sie unter: [Testumgebungsanleitung – Minimodul: Basis-PKI für Windows Server 2012](https://social.technet.microsoft.com/wiki/contents/articles/7862.test-lab-guide-mini-module-basic-pki-for-windows-server-2012.aspx)  
  
-   Das Unternehmensnetzwerk muss IPv6-fähig sein. Wenn Sie ISATAP verwenden, sollten Sie es entfernen und das systemeigene IPv6 verwenden.  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Das Szenario für die Bereitstellung für mehrere Standorte umfasst eine Reihe von Schritten:  
  
1. Stellen Sie [einen einzelnen DirectAccess-Server mit erweiterten Einstellungen](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)bereit. Vor dem Einrichten einer Bereitstellung für mehrere Standorte muss ein einzelner Remote Zugriffs Server mit erweiterten Einstellungen bereitgestellt werden.  
  
2. [Planen Sie eine Bereitstellung für mehrere Standorte](plan/Plan-a-Multisite-Deployment.md). Zum Erstellen einer Bereitstellung für mehrere Standorte auf einem einzelnen Server sind eine Reihe zusätzlicher Planungsschritte erforderlich, einschließlich der Konformität mit den Voraussetzungen für mehrere Standorte und der Planung für Active Directory Sicherheitsgruppen, Gruppenrichtlinie Objekte (GPOs), DNS und Client Einstellungen.  
  
3. [Konfigurieren Sie eine Bereitstellung für mehrere Standorte](configure/Configure-a-Multisite-Deployment.md). Dies umfasst eine Reihe von Konfigurationsschritten, einschließlich der Vorbereitung der Active Directory-Infrastruktur, der Konfiguration des vorhandenen Remote Zugriffs Servers und der Addition mehrerer RAS-Server als Einstiegspunkte für die Bereitstellung für mehrere Standorte.  
  
4. Problembehandlung bei [einer Bereitstellung mit mehreren Stand](troubleshoot/Troubleshoot-a-Multisite-Deployment.md)Orten. In diesem Abschnitt zur Problembehandlung werden einige der häufigsten Fehler beschrieben, die beim Bereitstellen des Remote Zugriffs in einer Bereitstellung mit mehreren Standorten auftreten können.
  
## <a name="practical-applications"></a><a name="BKMK_APP"></a>Praktische Anwendungen  
Eine Bereitstellung mit mehreren Standorten bietet Folgendes:  
  
-   Verbesserte Leistung: bei einer Bereitstellung mit mehreren Standorten können Client Computer mithilfe des Remote Zugriffs auf interne Ressourcen zugreifen, indem Sie den nächstgelegenen und am besten geeigneten Einstiegspunkt verwenden. Der Client greift effizient auf interne Ressourcen zu, und die Geschwindigkeit von Client Internet Anforderungen, die über DirectAccess weitergeleitet werden, wurde verbessert. Der Datenverkehr über Einstiegspunkte kann mithilfe eines externen globalen Load Balancers ausgeglichen werden.  
  
-   Erleichterte Verwaltung: mit mehreren Standorten können Administratoren die Bereitstellung des Remote Zugriffs an eine Active Directory Standorte-Bereitstellung ausrichten und so eine vereinfachte Architektur bereitstellen. Freigegebene Einstellungen können problemlos auf Einstiegspunkt Server oder Cluster festgelegt werden. Remote Zugriffs Einstellungen können von einem beliebigen Server in der Bereitstellung oder Remote mithilfe von Remoteserver-Verwaltungstools (RSAT) verwaltet werden. Außerdem kann die gesamte Bereitstellung für mehrere Standorte über eine einzelne Remote Zugriffs-Verwaltungskonsole überwacht werden.  
  
## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und Features  
In der folgenden Tabelle sind die in diesem Szenario verwendeten Rollen und Features aufgeführt.  
  
|Rolle/Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|---------|-----------------|  
|Remotezugriffs-Rolle|Diese Rolle wird mithilfe der Server-Manager-Konsole installiert und deinstalliert. Sie umfasst DirectAccess (zuvor ein Feature unter Windows Server 2008 R2) sowie die Routing- und RAS-Dienste (RRAS, zuvor ein Rollendienst unter der Serverrolle für Netzwerkrichtlinien- und Zugriffsdienste). Die Remotezugriffs-Rolle besteht aus zwei Komponenten:<br /><br />-DirectAccess und RRAS (Routing and Remote Access Services) VPN-DirectAccess und VPN werden in der Remote Zugriffs-Verwaltungskonsole verwaltet.<br />-RRAS-Routing: RRAS-Routing Features werden in der Legacy-Routing-und Remote Zugriffs Konsole verwaltet.<br /><br />Es bestehen folgende Abhängigkeiten:<br /><br />-Internetinformationsdienste (IIS)-Webserver: dieses Feature ist erforderlich, um den Netzwerkadressen Server und den Standard Webtest zu konfigurieren.<br />-Interne Windows-Datenbank: wird für die lokale Kontoführung auf dem Remote Zugriffs Server verwendet.|  
|Feature %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot;|So installieren Sie dieses Feature:<br /><br />-Sie wird standardmäßig auf einem RAS-Server installiert, wenn die Remote Zugriffs Rolle installiert ist, und unterstützt die Benutzeroberfläche der Remote Verwaltungskonsole.<br />-Es kann optional auf einem Server installiert werden, auf dem die Remote Zugriffs-Server Rolle nicht ausgeführt wird. In diesem Fall wird es für die Remoteverwaltung eines RAS-Computers verwendet, der DirectAccess und VPN ausführt.<br /><br />Das Feature "Tools für die Remotezugriffsverwaltung" besteht aus den folgenden Komponenten:<br /><br />-Remote Zugriffs-GUI und Befehlszeilen Tools<br />-Remote Zugriffs Modul für Windows PowerShell<br /><br />Abhängigkeiten umfassen:<br /><br />-Gruppenrichtlinien-Verwaltungskonsole<br />-RAS-Verbindungs-Manager-Verwaltungskit (CMAK)<br />-Windows PowerShell 3,0<br />-Tools und Infrastruktur für die grafische Verwaltung|  
  
## <a name="hardware-requirements"></a><a name="BKMK_HARD"></a>Hardwareanforderungen  
Für dieses Szenario müssen die folgenden Hardwareanforderungen erfüllt werden:  
  
-   Mindestens zwei RAS-Computer, die in einer Bereitstellung mit mehreren Standorten gesammelt werden sollen.   
  
-   Um das Szenario zu testen, ist mindestens ein Computer erforderlich, auf dem Windows 8 ausgeführt wird und der als DirectAccess-Client konfiguriert ist. Um das Szenario für Clients mit Windows 7 zu testen, ist mindestens ein Computer erforderlich, auf dem Windows 7 ausgeführt wird.  
  
-   Für den Lastenausgleich des Datenverkehrs auf Einstiegspunkt Server ist ein externer globaler Load Balancer eines Drittanbieters erforderlich.  
  
## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>Software Anforderungen  
Für dieses Szenario müssen die folgenden Softwareanforderungen erfüllt werden:  
  
-   Softwareanforderungen für die Bereitstellung auf einem Einzelserver.  
  
-   Zusätzlich zu den Softwareanforderungen für einen einzelnen Server gibt es eine Reihe von Anforderungen für mehrere Standorte:  
  
    -   IPSec-Authentifizierungsanforderungen: bei einer Bereitstellung für mehrere Standorte muss DirectAccess mithilfe der IPSec-Computer Zertifikat Authentifizierung bereitgestellt werden. Die Option zum Ausführen der IPSec-Authentifizierung mithilfe des RAS-Servers als Kerberos-Proxy wird nicht unterstützt. Zum Bereitstellen der IPSec-Zertifikate ist eine interne Zertifizierungsstelle erforderlich.  
  
    -   Anforderungen an die IP-HTTPS-und Netzwerkadressen Server: die für IP-HTTPS und den Netzwerkadressen Server erforderlichen Zertifikate müssen von einer Zertifizierungsstelle ausgestellt werden. Die Option zum Verwenden von Zertifikaten, die vom Remote Zugriffs Server automatisch ausgestellt und selbst signiert werden, wird nicht unterstützt. Zertifikate können von einer internen Zertifizierungsstelle oder von einer externen Zertifizierungsstelle eines Drittanbieters ausgestellt werden.  
  
    -   Active Directory Anforderungen: mindestens ein Active Directory Standort ist erforderlich. Der Remote Zugriffs Server sollte sich am-Standort befinden. Für schnellere Update Zeiten wird empfohlen, dass jeder Standort über einen beschreibbaren Domänen Controller verfügt, obwohl dies nicht zwingend erforderlich ist.  
  
    -   Sicherheitsgruppen Anforderungen: Anforderungen lauten wie folgt:  
  
        -   Für alle Windows 8-Client Computer von allen Domänen ist eine einzelne Sicherheitsgruppe erforderlich. Es wird empfohlen, für jede Domäne eine eindeutige Sicherheitsgruppe dieser Clients zu erstellen.  
  
        -   Für jeden Einstiegspunkt, der zur Unterstützung von Windows 7-Clients konfiguriert ist, ist eine eindeutige Sicherheitsgruppe mit Windows 7-Computern erforderlich. Es wird empfohlen, für jeden Einstiegspunkt in jeder Domäne eine eindeutige Sicherheitsgruppe zu haben.  
  
        -   Computer dürfen immer nur einer Sicherheitsgruppe zugeordnet werden, die DirectAccess-Clients enthält. Wenn Clients in mehreren Gruppen enthalten sind, funktioniert die Namensauflösung für Clientanforderungen nicht wie erwartet.  
  
    -   GPO-Anforderungen: GPOs können manuell erstellt werden, bevor der Remote Zugriff konfiguriert wird, oder Sie werden automatisch während der Remote Zugriffs Bereitstellung erstellt. Die Anforderungen lauten wie folgt:  
  
        -   Ein eindeutiges Client-GPO ist für jede Domäne erforderlich.  
  
        -   Ein Server-GPO ist für jeden Einstiegspunkt in der Domäne erforderlich, in der sich der Einstiegspunkt befindet. Wenn sich also mehrere Einstiegspunkte in derselben Domäne befinden, werden mehrere Server-Gruppenrichtlinien Objekte (eines für jeden Einstiegspunkt) in der Domäne angezeigt.  
  
        -   Für jede Domäne ist ein eindeutiges Windows 7-Client-Gruppenrichtlinien Objekt für jeden Einstiegspunkt erforderlich, der für die Windows 7-Client Unterstützung aktiviert ist.  
  
## <a name="known-issues"></a><a name="KnownIssues"></a>Bekannte Probleme  
Im folgenden finden Sie bekannte Probleme beim Konfigurieren eines Szenarios mit mehreren Standorten:  
  
-   **Mehrere Einstiegspunkte im gleichen IPv4-Subnetz**. Wenn Sie mehrere Einstiegspunkte im gleichen IPv4-Subnetz hinzufügen, wird eine IP-Adress Konflikt Meldung angezeigt, und die DNS64-Adresse für den Einstiegspunkt wird nicht erwartungsgemäß konfiguriert. Dieses Problem tritt auf, wenn IPv6 nicht auf den internen Schnittstellen der Server im Unternehmensnetzwerk bereitgestellt wurde. Um dieses Problem zu vermeiden, führen Sie den folgenden Windows PowerShell-Befehl auf allen aktuellen und zukünftigen RAS-Servern aus:  
  
    ```  
    Set-NetIPInterface -InterfaceAlias <InternalInterfaceName> -AddressFamily IPv6 -DadTransmits 0  
    ```  
  
-   Wenn die für DirectAccess-Clients für die Verbindung mit dem RAS-Server angegebene öffentliche Adresse ein Suffix enthält, das in NRPT enthalten ist, funktioniert DirectAccess möglicherweise nicht wie erwartet. Stellen Sie sicher, dass die NRPT eine Ausnahme für den öffentlichen Namen aufweist. Bei einer Bereitstellung mit mehreren Standorten sollten Ausnahmen für die öffentlichen Namen aller Einstiegspunkte hinzugefügt werden. Beachten Sie, dass diese Ausnahmen automatisch hinzugefügt werden, wenn die Tunnel Erzwingung aktiviert ist. Sie werden entfernt, wenn die Tunnel Erzwingung deaktiviert ist.  
  
-   Wenn Sie das Windows PowerShell-Cmdlet **Deaktivieren-damultisite**verwenden, haben die Parameter "WhatIf" und "Confirm" keine Auswirkung, und die Funktion "Multisite" wird deaktiviert, und die Gruppenrichtlinien Objekte von Windows 7 werden entfernt.  
  
-   Wenn Windows 7-Clients, die DCA in einer Bereitstellung mit mehreren Standorten verwenden, auf Windows 8 aktualisiert werden, funktioniert der netzwerkkonnektivitätsassistent nicht. Dieses Problem kann im Vorfeld des Client Upgrades behoben werden, indem die Windows 7-Gruppenrichtlinien Objekte mithilfe der folgenden Windows PowerShell-Cmdlets geändert werden:  
  
    ```  
    Set-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant" -ValueName "TemporaryValue" -Type Dword -Value 1  
    Remove-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant"  
    ```  
  
    Wenn der Client bereits aktualisiert wurde, verschieben Sie den Client Computer in die Sicherheitsgruppe Windows 8.  
  
-   Wenn Sie Domänen Controller Einstellungen mithilfe des Windows PowerShell-Cmdlets **Set-daentrypointdc**ändern und der angegebene Computername-Parameter ein RAS-Server an einem anderen Einstiegspunkt als der der Bereitstellung mit mehreren Standorten hinzugefügt wird, wird eine Warnung mit dem Hinweis angezeigt, dass der angegebene Server erst nach der nächsten Richtlinien Aktualisierung aktualisiert wird. Die tatsächlichen Server, die nicht aktualisiert wurden, können mit dem **Konfigurations Status** im **Dashboard** der **Remote Zugriffs-Verwaltungskonsole**angezeigt werden. Dadurch entstehen keine funktionalen Probleme. Sie können jedoch **gpupdate/force** auf den Servern ausführen, die nicht aktualisiert wurden, damit der Konfigurations Status sofort aktualisiert wird.  
  
-   Wenn Multisite in einem reinen IPv4-Unternehmensnetzwerk bereitgestellt wird, wird durch Ändern des IPv6-Präfixes für das interne Netzwerk auch die DNS64-Adresse geändert, aber nicht die Adresse der Firewallregeln, die DNS-Abfragen an den DNS64-Dienst erlauben. Um dieses Problem zu beheben, führen Sie die folgenden Windows PowerShell-Befehle aus, nachdem Sie das interne IPv6-Präfix geändert haben:  
  
    ```  
    $dns64Address = (Get-DAClientDnsConfiguration).NrptEntry | ?{ $_.DirectAccessDnsServers -match ':3333::1' } | Select-Object -First 1 -ExpandProperty DirectAccessDnsServers  
  
    $serverGpoName = (Get-RemoteAccess).ServerGpoName  
  
    $serverGpoDc = (Get-DAEntryPointDC).DomainControllerName  
  
    $gpoSession = Open-NetGPO -PolicyStore $serverGpoName -DomainController $serverGpoDc  
  
    Get-NetFirewallRule -GPOSession $gpoSession | ? {$_.Name -in @('0FDEEC95-1EA6-4042-8BA6-6EF5336DE91A', '24FD98AA-178E-4B01-9220-D0DADA9C8503')} |  Set-NetFirewallRule -LocalAddress $dns64Address  
  
    Save-NetGPO -GPOSession $gpoSession  
    ```  
  
-   Wenn DirectAccess bereitgestellt wurde, als eine vorhandene ISATAP-Infrastruktur vorhanden war, wird beim Entfernen eines Einstiegs Punkts, bei dem es sich um einen ISATAP-Host handelt, die IPv6-Adresse des DNS64-Diensts aus den DNS-Serveradressen aller DNS-Suffixe in der NRPT entfernt.  
  
    Um dieses Problem zu beheben, entfernen Sie im Assistenten zum **Einrichten des Infrastruktur Servers** auf der Seite **DNS** die geänderten DNS-Suffixe, und fügen Sie Sie erneut mit den richtigen DNS-Serveradressen hinzu, indem Sie im Dialogfeld **DNS-Serveradressen** auf **erkennen** klicken.  
  


