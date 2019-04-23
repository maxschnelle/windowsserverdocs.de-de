---
title: Bereitstellen Sie mehrere RAS-Server in einer Bereitstellung mit mehreren Standorten
description: Dieses Thema ist Teil des Handbuchs bereitstellen mehrere RAS-Server in einer Bereitstellung für mehrere Standorte in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac2f6015-50a5-4909-8f67-8565f9d332a2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3091c770fb9b207d82deaa571970bfeb44d17ee3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875881"
---
# <a name="deploy-multiple-remote-access-servers-in-a-multisite-deployment"></a>Bereitstellen Sie mehrere RAS-Server in einer Bereitstellung mit mehreren Standorten

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

 Windows Server 2016 und Windows Server 2012 kombiniert DirectAccess- und Remote Access Service (RAS) VPN in einer einzigen remotezugriffsrolle. Der Remotezugriff kann in einer Reihe von Unternehmensszenarios bereitgestellt werden. Diese Übersicht bietet eine Einführung in das Unternehmensszenario für die Bereitstellung von RAS-Server in einer Konfiguration mit mehreren Standorten.  
  
## <a name="BKMK_OVER"></a>Beschreibung des Szenarios  
In einer Bereitstellung für mehrere Standorte sind zwei oder mehr RAS-Server oder Servercluster bereitgestellt und konfiguriert werden, als unterschiedliche Einstiegspunkte in einem zentralen Ort oder in unterschiedlichen geografischen Standorten befinden. Die Bereitstellung mehrere Einstiegspunkte in einem einzigen Ort ermöglicht, Serverredundanz oder für die Ausrichtung des RAS-Server mit vorhandenen Netzwerkarchitektur. Bereitstellung nach geografischem Standort effiziente Nutzung von Ressourcen wird sichergestellt, wie der Remoteclientcomputer auf interne Netzwerkressourcen, die ihnen am nächsten Einstiegspunkt über eine Verbindung herstellen können. Datenverkehr über eine Bereitstellung für mehrere Standorte verteilt und mit einem externen globalen Lastenausgleich verteilt.  
  
Eine Bereitstellung für mehrere Standorte unterstützt Clientcomputer unter Windows 10, Windows 8 oder Windows 7. Clientcomputer unter Windows 10 oder Windows 8 automatisch identifizieren ein Einstiegspunkts an, oder der Benutzer kann einen Einstiegspunkt manuell auswählen. Automatische Zuweisung erfolgt in der folgenden Reihenfolge ihrer Priorität:  
  
1.  Verwenden Sie einen Einstiegspunkt manuell vom Benutzer ausgewählt.  
  
2.  Verwenden Sie einen Einstiegspunkt, der von einem externen globalen Lastenausgleich identifiziert wird, wenn eine bereitgestellt wird.  
  
3.  Verwenden Sie den nächsten Einstiegspunkt identifiziert durch den Clientcomputer, die über einen Mechanismus für die automatische Überprüfung.  
  
Unterstützung für Clients unter Windows 7 muss manuell aktiviert werden, für jeden Einstiegspunkt und Auswahl eines Einstiegspunkts, die von diesen Clients wird nicht unterstützt.  
  
## <a name="prerequisites"></a>Vorraussetzungen  
Bevor Sie mit der Bereitstellung dieses Szenarios beginnen, sollten Sie die Liste der wichtigen Anforderungen lesen:  
  
-   [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) muss vor einer Bereitstellung für mehrere Standorte bereitgestellt werden.  
  
-   Windows 7-Clients werden immer mit einem bestimmten Standort verbunden. Sie werden kann nicht für die Verbindung mit dem nächsten Standort basierend auf dem Standort des Clients (im Gegensatz zu Windows 10, 8 oder 8.1-Clients).  
  
-   Das Ändern von Richtlinien außerhalb der DirectAccess-Verwaltungskonsole oder von PowerShell-Cmdlets wird nicht unterstützt.  
  
-   Eine Public Key-Infrastruktur muss bereitgestellt werden.  
  
    Weitere Informationen finden Sie unter: [Testen Sie Testumgebungsanleitung – Minimodul: Einfache PKI für WindowsServer 2012.](https://social.technet.microsoft.com/wiki/contents/articles/7862.test-lab-guide-mini-module-basic-pki-for-windows-server-2012.aspx)  
  
-   Im Unternehmensnetzwerk muss IPv6-fähig sein. Wenn Sie ISATAP verwenden, sollten Sie es entfernen und das systemeigene IPv6 verwenden.  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Das Szenario für die Bereitstellung für mehrere Standorte umfasst eine Reihe von Schritten:  
  
1. [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md). Ein einzelnes Remotezugriffsservers mit erweiterten Einstellungen muss vor dem Einrichten einer Bereitstellung für mehrere Standorte bereitgestellt werden.  
  
2. [Planen eine Bereitstellung für mehrere Standorte](plan/Plan-a-Multisite-Deployment.md). Um etliche zusätzliche Planung einer Bereitstellung für mehrere Standorte, von einem einzelnen Server zu erstellen sind erforderlich, einschließlich Kompatibilität multisite Voraussetzungen erfüllt sind, und Planen von Active Directory-Sicherheitsgruppen, die Gruppenrichtlinienobjekte (GPOs), DNS und Clienteinstellungen.  
  
3. [Konfigurieren eine Bereitstellung für mehrere Standorte](configure/Configure-a-Multisite-Deployment.md). Dies umfasst eine Reihe von Konfigurationsschritten, einschließlich der Vorbereitung des Active Directory-Infrastruktur, Konfiguration der vorhandenen RAS-Server sowie mehrere RAS-Server als Einstiegspunkte für die Bereitstellung für mehrere Standorte hinzufügen.  
  
4. [Problembehandlung bei einer Bereitstellung für mehrere Standorte](troubleshoot/Troubleshoot-a-Multisite-Deployment.md). In diesem Abschnitt zur Problembehandlung werden verschiedene die häufigsten Fehler, die auftreten können, bei der Bereitstellung von Remotezugriff in einer Bereitstellung für mehrere Standorte beschrieben.
  
## <a name="BKMK_APP"></a>Praktische Anwendungen  
Eine Bereitstellung für mehrere Standorte bietet Folgendes:  
  
-   Verbesserte Leistung – eine Bereitstellung für mehrere Standorte ermöglicht Clientcomputern, die Zugriff auf interne Ressourcen, die mithilfe von Remote-Zugriff zum Herstellen einer Verbindung mit der nächsten und am besten geeigneten Einstiegspunkt. Client Zugriff auf interne Ressourcen effizient, und die Geschwindigkeit des Clients, die Internet-Anforderungen über DirectAccess zulassen weitergeleitet wurde verbessert. Datenverkehr auf die Einstiegspunkte kann mit einem externen globalen Lastenausgleich abgewogen werden.  
  
-   Einfache-von-Management-Funktionen für mehrere Standorte kann Administratoren die Bereitstellung des Remotezugriffs auf Active Directory-Websites-Bereitstellung, wodurch eine einfachere Architektur ausrichten. Gemeinsam genutzte Einstellungen können problemlos über den Eintrag-Geräteverwaltungspunkt-Server oder Cluster festgelegt werden. Remotezugriffseinstellungen können von jedem Server in der Bereitstellung und – mithilfe der Remote Server Administration Tools (RSAT) verwaltet werden. Darüber hinaus kann die gesamte Bereitstellung über eine einzelne Remotezugriffs-Konsole überwacht werden.  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und features  
Die folgende Tabelle enthält die Rollen und Features, die in diesem Szenario verwendet.  
  
|Rolle/Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|---------|-----------------|  
|Remotezugriffs-Rolle|Diese Rolle wird mithilfe der Server-Manager-Konsole installiert und deinstalliert. Sie umfasst DirectAccess (zuvor ein Feature unter Windows Server 2008 R2) sowie die Routing- und RAS-Dienste (RRAS, zuvor ein Rollendienst unter der Serverrolle für Netzwerkrichtlinien- und Zugriffsdienste). Die Remotezugriffs-Rolle besteht aus zwei Komponenten:<br /><br />– DirectAccess und Routing- und RAS-Dienste (RRAS) VPN – DirectAccess und VPN werden gemeinsam in der Remotezugriffs-Verwaltungskonsole verwaltet.<br />-RRAS Routing – RRAS-Routingfeatures werden in der älteren Routing- und RAS-Konsole verwaltet.<br /><br />Es bestehen folgende Abhängigkeiten:<br /><br />-IIS (Internetinformationsdienste) Webserver - ist dieses Feature erforderlich, um den Netzwerkadressenserver und den standardwebtest zu konfigurieren.<br />-Windows interne Database-Used zur lokalen Kontoführung auf dem RAS-Server.|  
|Feature %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot;|So installieren Sie dieses Feature:<br /><br />– Es wird standardmäßig auf einem RAS-Server installiert, wenn die Rolle "Remotezugriff" installiert ist, und unterstützt die Benutzeroberfläche der RAS-Konsole.<br />– sie können optional auf einem Server nicht mit der RAS-Serverrolle installiert werden. In diesem Fall wird es für die Remoteverwaltung eines RAS-Computers verwendet, der DirectAccess und VPN ausführt.<br /><br />Das Feature "Tools für die Remotezugriffsverwaltung" besteht aus den folgenden Komponenten:<br /><br />-Remotezugriffs-GUI und Befehlszeilentools<br />-RAS-Modul für Windows PowerShell<br /><br />Abhängigkeiten umfassen:<br /><br />-Gruppenrichtlinien-Verwaltungskonsole<br />-RAS-Verbindungs-Manager-Verwaltungskit (CMAK)<br />-Windows PowerShell 3.0<br />-Grafische Verwaltungstools und Infrastruktur|  
  
## <a name="BKMK_HARD"></a>Hardwareanforderungen  
Für dieses Szenario müssen die folgenden Hardwareanforderungen erfüllt werden:  
  
-   Mindestens zwei Computer Remote Access in einer Bereitstellung für mehrere Standorte gesammelt werden.   
  
-   Um das Szenario testen zu können, muss auf mindestens einem Computer Windows 8 ausgeführt wird und als ein DirectAccess-Client konfiguriert werden. Zum Testen des Szenarios für Windows 7-Clients muss auf mindestens einem Computer, auf denen Windows 7 ausgeführt wird.  
  
-   Um einen Lastenausgleich für Datenverkehr über den Eintrag-Geräteverwaltungspunkt-Server zu laden, ist ein Drittanbieter-externen globalen Lastenausgleich erforderlich.  
  
## <a name="BKMK_SOFT"></a>Softwareanforderungen  
Für dieses Szenario müssen die folgenden Softwareanforderungen erfüllt werden:  
  
-   Softwareanforderungen für die Bereitstellung auf einem Einzelserver.  
  
-   Es gibt eine Reihe von multisite-bestimmte Anforderungen, zusätzlich zu den softwareanforderungen für einen einzelnen Server:  
  
    -   IPSec-Authentifizierung-Anforderungen In eine Bereitstellung für mehrere Standorte DirectAccess IPsec-Computerzertifikatauthentifizierung bereitgestellt werden muss. Die Option zum Ausführen von IPsec-Authentifizierung mithilfe von RAS-Servers als Kerberos-Proxy wird nicht unterstützt. Eine interne Zertifizierungsstelle ist erforderlich, um die IPsec-Zertifikate bereitzustellen.  
  
    -   IP-HTTPS und Netzwerk Anforderungen-Zertifikate für IP-HTTPS und den Netzwerkadressenserver erforderlich sind, müssen von einer Zertifizierungsstelle ausgestellt werden. Die Option zum Verwenden von Zertifikaten, die automatisch ausgestellt und selbstsigniert von RAS-Servers wird nicht unterstützt. Zertifikate können von einer internen Zertifizierungsstelle oder von einer Drittanbieter-externe Zertifizierungsstelle ausgestellt werden.  
  
    -   Active Directory-Anforderungen: mindestens eine Active Directory-Standort ist erforderlich. RAS-Server sollte auf der Website befinden. Für schnellere aktualisieren wird empfohlen, dass jeder Standort mit einen beschreibbaren Domänencontroller hat, obwohl dies nicht erforderlich ist.  
  
    -   Anforderungen-Anforderungen für die Sicherheitsgruppen lauten wie folgt aus:  
  
        -   Eine einzelne Sicherheitsgruppe ist für alle Windows 8-Clientcomputern aus allen Domänen erforderlich. Es wird empfohlen, um eine eindeutige Sicherheits-Gruppe von diesen Clients für jede Domäne zu erstellen.  
  
        -   Eine eindeutige Sicherheits-Gruppe, die mit Windows 7-Computer muss für jeden Einstiegspunkt für die Unterstützung von Windows 7-Clients konfiguriert. Es wird empfohlen, um eine eindeutige Sicherheits-Gruppe für jeden Einstiegspunkt in den einzelnen Domänen zu erhalten.  
  
        -   Computer dürfen immer nur einer Sicherheitsgruppe zugeordnet werden, die DirectAccess-Clients enthält. Wenn Clients in mehreren Gruppen enthalten sind, funktioniert die Namensauflösung für Clientanforderungen nicht wie erwartet.  
  
    -   GPO-Anforderungen-Gruppenrichtlinienobjekte können vor dem Konfigurieren des Remotezugriffs manuell erstellt oder während der Bereitstellung des Remotezugriffs automatisch erstellt werden. Es gelten folgende Anforderungen:  
  
        -   Eine eindeutige Client-Gruppenrichtlinienobjekt muss für jede Domäne.  
  
        -   Ein Server-Gruppenrichtlinienobjekt muss für jeden Einstiegspunkt, in der Domäne, in der sich der Einstiegspunkt befindet. Also wenn mehrere Einstiegspunkte in derselben Domäne befinden, stehen mehrere Server Gruppenrichtlinienobjekte (eine für jeden Einstiegspunkt) in der Domäne.  
  
        -   Eine eindeutige Client-Gruppenrichtlinienobjekt von Windows 7 ist erforderlich, für jeden Einstiegspunkt für Windows 7-Client-Unterstützung für jede Domäne aktiviert.  
  
## <a name="KnownIssues"></a>Bekannte Probleme  
Im folgenden werden bekannte Probleme beim einen Szenario mit mehreren Standorten konfigurieren:  
  
-   **Mehrere Einstiegspunkte im gleichen IPv4-Subnetz**. Das Hinzufügen mehrere Einstiegspunkte im gleichen IPv4-Subnetz führt zu einer IP-Adresse-konfliktmeldung, und die DNS64-Adresse für den Einstiegspunkt wird nicht wie erwartet konfiguriert werden. Dieses Problem tritt auf, wenn IPv6 nicht auf die internen Schnittstellen der Server im Unternehmensnetzwerk bereitgestellt wurde. Um dieses Problem, führen den folgenden Windows PowerShell-Befehl auf allen aktuellen und zukünftigen RAS-Servern zu vermeiden:  
  
    ```  
    Set-NetIPInterface -InterfaceAlias <InternalInterfaceName> -AddressFamily IPv6 -DadTransmits 0  
    ```  
  
-   Wenn die öffentliche Adresse, die für DirectAccess-Clients für die Verbindung zum RAS-Servers angegebenen ein Suffix enthalten, die in der NRPT verfügt, kann DirectAccess nicht erwartungsgemäß. Stellen Sie sicher, dass die NRPT eine Ausnahme für den öffentlichen Namen verfügt. Bei einer Bereitstellung mit mehreren Standorten sollten Ausnahmen für den öffentlichen Namen, der alle Einstiegspunkte hinzugefügt werden. Beachten Sie, dass bei des Erzwingens von Tunneln ist aktiviert. diese Ausnahmen werden automatisch hinzugefügt. Sie werden entfernt, wenn das Erzwingen von Tunneln deaktiviert ist.  
  
-   Wenn Sie das Windows PowerShell-Cmdlet verwenden **Disable-DAMultiSite**, WhatIf und Confirm-Parameter wirken sich nicht, und für mehrere Standorte wird deaktiviert, und Windows 7-Gruppenrichtlinienobjekte entfernt werden.  
  
-   Wenn DCA in einer Bereitstellung für mehrere Standorte mit Windows 7-Clients auf Windows 8 aktualisiert werden, funktioniert den Netzwerkkonnektivitäts-Assistent nicht. Dieses Problem kann vor der Clientaktualisierung behoben werden, indem Sie die Windows 7-GPOs mit den folgenden Windows PowerShell-Cmdlets ändern:  
  
    ```  
    Set-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant" -ValueName "TemporaryValue" -Type Dword -Value 1  
    Remove-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant"  
    ```  
  
    Wenn der Client bereits aktualisiert wurde, verschieben Sie den Clientcomputer, der Windows 8-Sicherheitsgruppe.  
  
-   Beim Ändern der Einstellungen des Domänencontrollers mit dem Windows PowerShell-Cmdlet **Set-DAEntryPointDC**, wenn der ComputerName-Parameter angegebenen RAS-Server im Einstiegspunkt als dem zuletzt hinzugefügt, die für mehrere Standorte Bereitstellung, eine Warnung wird angezeigt, dass der angegebene Server nicht erst nach der nächsten richtlinienaktualisierung aktualisiert wird. Die tatsächlichen Server, die nicht aktualisiert wurde können angezeigt werden, mithilfe der **Konfigurationsstatus** in die **DASHBOARD** von der **Remotezugriffs-Verwaltungskonsole**. Nicht dadurch, dass keine Funktionsprobleme, allerdings können Sie ausführen **Gpupdate/force** auf den Servern, die nicht aktualisiert wurde, damit der Konfigurationsstatus sofort aktualisiert wird.  
  
-   Wenn mehrere Standorte bereitgestellt wird, in einem nur-IPv4-Unternehmensnetzwerk, ändern die interne Netzwerk IPv6-Präfix auch Änderungen der DNS64-Adresse, aber die Firewallregeln, mit denen DNS-Abfragen an den Dienst DNS64-Adresse wird nicht aktualisiert. Um dieses Problem zu beheben, führen Sie die folgenden Windows PowerShell-Befehlen nach dem Ändern der internen Netzwerk IPv6-Präfix:  
  
    ```  
    $dns64Address = (Get-DAClientDnsConfiguration).NrptEntry | ?{ $_.DirectAccessDnsServers -match ':3333::1' } | Select-Object -First 1 -ExpandProperty DirectAccessDnsServers  
  
    $serverGpoName = (Get-RemoteAccess).ServerGpoName  
  
    $serverGpoDc = (Get-DAEntryPointDC).DomainControllerName  
  
    $gpoSession = Open-NetGPO -PolicyStore $serverGpoName -DomainController $serverGpoDc  
  
    Get-NetFirewallRule -GPOSession $gpoSession | ? {$_.Name -in @('0FDEEC95-1EA6-4042-8BA6-6EF5336DE91A', '24FD98AA-178E-4B01-9220-D0DADA9C8503')} |  Set-NetFirewallRule -LocalAddress $dns64Address  
  
    Save-NetGPO -GPOSession $gpoSession  
    ```  
  
-   Wenn DirectAccess bereitgestellt wurde, wenn eine ISATAP-Infrastruktur vorhanden ist, wenn einen Einstiegspunkt zu entfernen, der ein ISATAP-Host wurde werden die IPv6-Adresse des DNS64-Diensts aus der DNS-Serveradressen alle DNS-Suffixe in der NRPT entfernt.  
  
    Um dieses Problem zu beheben, in der **Einrichten des Infrastrukturservers** Assistenten, auf die **DNS** Seite, entfernen Sie die DNS-Suffixe, die geändert wurden und erneut hinzufügen mit den richtigen Adressen für DNS-Server, indem Sie auf die  **Erkennen** auf die **DNS-Serveradressen** Dialogfeld.  
  


