---
title: Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen
description: Dieses Thema ist Teil des Handbuchs Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: b211a9ca-1208-4e1f-a0fe-26a610936c30
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 7f6a6724a2ab7bb6da48a11d31fb04461912e388
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859523"
---
# <a name="deploy-a-single-directaccess-server-with-advanced-settings"></a>Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dieses Thema bietet eine Einführung in das DirectAccess-Szenario, in dem ein einzelner DirectAccess-Server verwendet wird, und ermöglicht es Ihnen, DirectAccess mit erweiterten Einstellungen bereitzustellen.  
  
## <a name="before-you-begin-deploying-see-the-list-of-unsupported-configurations-known-issues-and-prerequisites"></a>Bevor Sie mit der Bereitstellung beginnen, sollten Sie sich die folgende Liste mit nicht unterstützten Konfigurationen, bekannten Problemen und Voraussetzungen ansehen:  
In den folgenden Themen finden Sie Informationen zu Voraussetzungen und anderen Informationen vor der Bereitstellung von DirectAccess.  
  
-   [DirectAccess: Nicht unterstützte Konfigurationen](../../../remote-access/directaccess/DirectAccess-Unsupported-Configurations.md)  
  
-   [Erforderliche Komponenten für die Bereitstellung von DirectAccess](../../../remote-access/directaccess/Prerequisites-for-Deploying-DirectAccess.md)  
  
## <a name="scenario-description"></a><a name="BKMK_OVER"></a>Szenariobeschreibung  
In diesem Szenario wird ein einzelner Computer, auf dem entweder Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird, als DirectAccess-Server mit erweiterten Einstellungen konfiguriert.  
  
> [!NOTE]  
> Wenn Sie nur eine grundlegende Bereitstellung mit einfachen Standardeinstellungen konfigurieren möchten, finden Sie unter [Deploy a Single DirectAccess Server Using the Getting Started Wizard](../../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)weitere Informationen. In dem einfachen Szenario wird DirectAccess über einen Assistenten mit Standardeinstellungen eingerichtet, ohne dass die Notwendigkeit zur Konfiguration von Infrastruktureinstellungen wie einer Zertifizierungsstelle oder Active Directory-Sicherheitsgruppen besteht.  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Um einen einzelnen DirectAccess-Server mit erweiterten Einstellungen einzurichten, müssen Sie einige Planungs- und Bereitstellungsschritte durchführen.  
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
Vor dem Beginn können Sie folgende Anforderungen überprüfen:  
  
-   Windows-Firewall muss in allen Profilen aktiviert sein.  
  
-   Der DirectAccess-Server ist der Netzwerkadressenserver.  
  
-   Sie möchten, dass alle Drahtloscomputer in der Domäne, in der der DirectAccess-Server installiert wird, DirectAccess-fähig sind. Wenn Sie DirectAccess bereitstellen, ist es automatisch auf allen mobilen Computern in der aktuellen Domäne aktiviert.  
  
> [!IMPORTANT]  
> Einige Technologien und Konfigurationen werden bei der Bereitstellung von DirectAccess nicht unterstützt.  
>   
> -   ISATAP (Intra-Site Automatic Tunnel Addressing Protocol) wird im Unternehmensnetzwerk nicht unterstützt. Wenn Sie ISATAP verwenden, müssen Sie es entfernen und das systemeigene IPv6 verwenden.  
  
### <a name="planning-steps"></a>Planungsschritte  
Die Planung besteht aus zwei Phasen:  
  
1.  **Planen der DirectAccess-Infrastruktur**. Diese Phase beschreibt die erforderlichen Planungsschritte zum Einrichten der Netzwerkinfrastruktur vor der DirectAccess-Bereitstellung. Sie umfasst das Planen der Netzwerk- und Servertopologie, der Zertifikate, des Domain Name System (DNS), der Active Directory-Konfiguration, der Konfiguration der Gruppenrichtlinienobjekte und des DirectAccess-Netzwerkadressenservers.  
  
2.  **Planen der DirectAccess-Bereitstellung**. Diese Phase beschreibt die erforderlichen Planungsschritte zur Vorbereitung der DirectAccess-Bereitstellung. Dazu gehört die Planung für DirectAccess-Clientcomputer, Server- und Clientauthentifizierungsanforderungen, VPN-Einstellungen, Infrastrukturserver sowie Verwaltungs- und Anwendungsserver.  
  
### <a name="deployment-steps"></a>Bereitstellungsschritte  
Die Bereitstellung besteht aus drei Phasen:  
  
1.  **Konfigurieren der DirectAccess-Infrastruktur**. Diese Phase beinhaltet das Konfigurieren von Netzwerk und Routing, das Konfigurieren der Firewalleinstellungen (falls erforderlich), das Konfigurieren von Zertifikaten, DNS-Servern, Active Directory- und Gruppenrichtlinienobjekt-Einstellungen und DirectAccess-Netzwerkadressenserver.  
  
2.  **Konfigurieren der DirectAccess-Servereinstellungen**. Die Phase beinhaltet Schritte zum Konfigurieren von DirectAccess-Clientcomputern, DirectAccess-Server, Infrastrukturservern sowie Verwaltungs- und Anwendungsservern.  
  
3.  **Überprüfen der Bereitstellung**. Diese Phase beinhaltet Schritte zur Überprüfung der DirectAccess-Bereitstellung.  
  
Ausführliche Informationen zu den Bereitstellungsschritten finden Sie unter [Installieren und Konfigurieren des erweiterten DirectAccess](../../../remote-access/directaccess/single-server-advanced/Install-and-Configure-Advanced-DirectAccess.md).  
  
## <a name="practical-applications"></a><a name="BKMK_APP"></a>Praktische Anwendungen  
Die Bereitstellung eines einzelnen DirectAccess-Servers bietet Folgendes:  
  
-   **Erleichterte Bedienung**. Verwaltete Client Computer, auf denen Windows 10, Windows 8.1, Windows 8 und Windows 7 ausgeführt wird, können als DirectAccess-Client Computer konfiguriert werden. Diese Clients können immer, wenn sie im Internet sind, über DirectAccess auf interne Netzwerkressourcen zugreifen, ohne sich über eine VPN-Verbindung einzuloggen. Clientcomputer, die keines dieser Betriebssysteme verwenden, können per VPN eine Verbindung zum internen Netzwerk herstellen.  
  
-   **Erleichterte Verwaltung**. Die Remoteverwaltung von DirectAccess-Clientcomputern im Internet ist mithilfe von RAS-Administratoren über DirectAccess möglich, selbst wenn die Clientcomputer sich nicht im internen Unternehmensnetzwerk befinden. Clientcomputer, die nicht den Unternehmensanforderungen entsprechen, können automatisch über Verwaltungsserver gewartet werden. Sowohl DirectAccess als auch VPN werden über dieselbe Konsole und mit denselben Assistenten verwaltet. Außerdem können einer oder mehrere DirectAccess-Server über eine einzelne Remotezugriffs-Verwaltungskonsole verwaltet werden.  
  
## <a name="roles-and-features-required-for-this-scenario"></a><a name="BKMK_NEW"></a>Für dieses Szenario erforderliche Rollen und Features  
Die folgende Tabelle enthält die für dieses Szenario erforderlichen Rollen und Features:  
  
|Rolle/Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|---------|-----------------|  
|Remotezugriffs-Rolle|Die Rolle wird über die Server-Manager-Konsole oder Windows PowerShell installiert bzw. deinstalliert. Diese Rolle umfasst DirectAccess sowie die Routing- und RAS-Dienste. Die Remotezugriffs-Rolle besteht aus zwei Komponenten:<br/><br/>1. DirectAccess und RRAS-VPN. DirectAccess und VPN werden in der Remote Zugriffs-Verwaltungskonsole verwaltet.<br/>2. RRAS-Routing. RRAS-Routing Features werden in der Legacy-Routing-und Remote Zugriffs Konsole verwaltet.<p>Die RAS-Serverrolle ist von den folgenden Serverrollen/-features abhängig:<br/><br/> -Internetinformationsdienste (IIS)-Webserver: dieses Feature ist erforderlich, um den Netzwerkadressen Server auf dem DirectAccess-Server und den Standard Webtest zu konfigurieren.<br/> -Interne Windows-Datenbank. Wird für die lokale Kontoführung auf dem DirectAccess-Server verwendet.|  
|Feature %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot;|So installieren Sie dieses Feature:<p>-Sie wird bei der Installation der Remote Zugriffs Rolle standardmäßig auf einem DirectAccess-Server installiert und unterstützt die Benutzeroberfläche der Remote Verwaltungskonsole und Windows PowerShell-Cmdlets.<br />-Es kann optional auf einem Server installiert werden, auf dem die DirectAccess-Server Rolle nicht ausgeführt wird. In diesem Fall wird es für die Remoteverwaltung eines RAS-Computers verwendet, der DirectAccess und VPN ausführt.<p>Das Feature "Tools für die Remotezugriffsverwaltung" besteht aus den folgenden Komponenten:<p>-Remote Zugriff grafische Benutzeroberfläche (GUI)<br />-Remote Zugriffs Modul für Windows PowerShell<p>Abhängigkeiten umfassen:<p>-Gruppenrichtlinien-Verwaltungskonsole<br />-RAS-Verbindungs-Manager-Verwaltungskit (CMAK)<br />-Windows PowerShell 3,0<br />-Tools und Infrastruktur für die grafische Verwaltung|  
  
## <a name="hardware-requirements"></a><a name="BKMK_HARD"></a>Hardwareanforderungen  
Für dieses Szenario müssen die folgenden Hardwareanforderungen erfüllt werden:  
  
-   Serveranforderungen:  
  
    -   Ein Computer, der die Hardwareanforderungen für Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 erfüllt.  
  
    -   Auf dem Server muss mindestens ein Netzwerkadapter installiert, aktiviert und mit dem internen Netzwerk verbunden sein. Werden zwei Adapter verwendet, sollte ein Adapter mit dem internen Unternehmensnetzwerk und der andere mit dem externen Netzwerk (Internet oder privates Netzwerk) verbunden sein.  
  
    -   Falls Teredo als IPv4- bis IPv6-Übergangsprotokoll benötigt wird, benötigt der externe Adapter des Servers zwei aufeinanderfolgenden öffentliche IPv4-Adressen. Wenn nur eine IP-Adresse verfügbar ist, kann nur IP-HTTPS als Übergangsprotokoll verwendet werden.  
  
    -   Mindestens ein Domänencontroller. DirectAccess-Server und DirectAccess-Clients müssen Domänenmitglieder sein.  
  
    -   Eine Zertifizierungsstelle ist erforderlich, wenn Sie keine selbstsignierten Zertifikate für IP-HTTPS oder den Netzwerkadressenserver verwenden möchten, oder wenn Sie Clientzertifikate zur Client-IPsec-Authentifizierung verwenden möchten. Alternativ können Sie die Zertifikate von einer öffentlichen Zertifizierungsstelle anfordern.  
  
    -   Befindet sich der Netzwerkadressenserver nicht auf dem DirectAccess-Server, ist ein separater Webserver für die Ausführung erforderlich.  
  
-   Clientanforderungen:  
  
    -   Auf einem Client Computer muss Windows 10, Windows 8 oder Windows 7 ausgeführt werden.  
  
        > [!NOTE]  
        > Die folgenden Betriebssysteme können als DirectAccess-Clients verwendet werden: Windows 10, Windows Server 2012 R2, Windows Server 2012, Windows 8 Enterprise, Windows 7 Enterprise oder Windows 7 Ultimate.  
  
-   Anforderungen an Infrastruktur und Verwaltungsserver:  
  
    -   Während der Remoteverwaltung von DirectAccess-Clientcomputern initiieren die Clients die Kommunikation mit Verwaltungsservern, z. B. Domänencontrollern, System Center-Konfigurationsservern und Inhaltsregistrierungsstellen (HRA)-Servern, für Dienste, darunter Windows- und Antivirus-Updates sowie Network Access Protection (NAP)-Clientkompatibilität. Die erforderlichen Server sollten bereitgestellt werden, bevor mit der Bereitstellung des Remotezugriffs begonnen wird.  
  
    -   Falls der Remotezugriff Client-NAP-Kompatibilität erfordert, sollten die NPS- und HRS-Server bereitgestellt werden, bevor mit der Bereitstellung des Remotezugriffs begonnen wird.  
  
    -   Falls ein VPN aktiviert ist, ist ein DHCP-Server erforderlich, um die IP-Adressen automatisch den VPN-Clients zuzuweisen, sofern kein statischen IP-Adresspool genutzt wird.  
  
## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>Software Anforderungen  
Für dieses Szenario gelten eine Reihe von Anforderungen:  
  
-   Serveranforderungen:  
  
    -   Der DirectAccess-Server muss Domänenmitglied sein. Der Server kann an der Schwelle zum internen Netzwerks oder geschützt durch eine Edgefirewall oder ein anderes Gerät bereitgestellt werden.  
  
    -   Wird der DirectAccess-Server durch eine Edgefirewall oder ein NAT-Gerät geschützt, muss das Gerät so konfiguriert sein, dass ein- und ausgehender Datenverkehr für den DirectAccess-Server zugelassen wird.  
  
    -   Die Person, die den Remotezugriff auf dem Server einrichtet, muss lokale Administratorberechtigungen für den Server und Benutzerberechtigungen für die Domäne besitzen. Zusätzlich benötigt der Administrator Berechtigungen für die Gruppenrichtlinien, die bei der DirectAccess-Bereitstellung verwendet werden. Um die Features nutzen zu können, die die DirectAccess-Bereitstellung auf mobile Computer beschränken, ist die Berechtigung zum Erstellen von WMI-Filtern für den Domänencontroller erforderlich.  
  
-   RAS-Client-Anforderungen:  
  
    -   DirectAccess-Clients müssen Domänenmitglieder sein. Domänen, die Clients beinhalten, können zur selben Gesamtstruktur gehören wie der DirectAccess-Server, oder sie können eine bidirektionale Vertrauensstellung mit der DirectAccess-Serverstruktur oder der Domäne innehaben.  
  
    -   Eine Active Directory-Sicherheitsgruppe wird benötigt, um die Computer aufzunehmen, die als DirectAccess-Clients konfiguriert werden. Wird beim Konfigurieren der DirectAccess-Clienteinstellungen keine Sicherheitsgruppe angegeben, wird das Client-Gruppenrichtlinienobjekt standardmäßig auf alle Laptopcomputer in der Sicherheitsgruppe %%amp;quot;Domänencomputer%%amp;quot; angewendet.  
  
        > [!NOTE]  
        > Es wird empfohlen, dass Sie eine Sicherheitsgruppe für jede Domäne erstellen, die DirectAccess-Clientcomputer enthält.  
  
        > [!IMPORTANT]  
        > Wenn Sie Teredo in der DirectAccess-Bereitstellung aktiviert haben und Zugriff auf Windows 7-Clients bereitstellen möchten, müssen Sie sicherstellen, dass die Clients auf Windows 7 mit SP1 aktualisiert werden. Clients, die Windows 7 RTM verwenden, können keine Verbindung über Teredo herstellen. Diese Clients können jedoch weiterhin eine Verbindung zum Unternehmensnetzwerk über IP-HTTPS herstellen.  
  
## <a name="see-also"></a><a name="BKMK_LINKS"></a>Siehe auch  
Die folgende Tabelle enthält Links zu zusätzlichen Ressourcen.  
  
|Art des Inhalts|Verweise|  
|--------|-------|  
|**Bereitstellung**|[DirectAccess-Bereitstellungs Pfade in Windows Server](../../../remote-access/directaccess/DirectAccess-Deployment-Paths-in-Windows-Server.md)<p>[Bereitstellen eines einzelnen DirectAccess-Servers mit dem Assistenten für die ersten Schritte](../../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)|  
|**Tools und Einstellungen**|[PowerShell-Cmdlets für den Remote Zugriff](https://technet.microsoft.com/library/hh918399.aspx)|  
|**Communityressourcen**|[Leitfaden zum DirectAccess-Lebensfaden](https://social.technet.microsoft.com/wiki/contents/articles/23210.directaccess-survival-guide.aspx)<p>[DirectAccess-wiki-Einträge](https://go.microsoft.com/fwlink/?LinkId=236871)|  
|**Verwandte Technologien**|[Funktionsweise von IPv6](https://technet.microsoft.com/library/cc781672(v=WS.10).aspx)|  
  


