---
title: Bereitstellen eines DirectAccess-Servers mit dem Assistenten für erste Schritte
description: Dieses Thema ist Teil des Handbuchs Bereitstellen eines einzelnen DirectAccess-Servers mit dem Assistenten für die ersten Schritte für Windows Server 2016
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: eb0cf464-0668-40f8-8222-feb6bae6d3d5
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 141c8ad17bd1c58d2bbe729aeacc88f498c8c619
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86962872"
---
# <a name="deploy-a-single-directaccess-server-using-the-getting-started-wizard"></a>Bereitstellen eines DirectAccess-Servers mit dem Assistenten für erste Schritte

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Dieses Thema bietet eine Einführung in das DirectAccess-Szenario mit einem einzelnem DirectAccess-Server und ermöglicht Ihnen die Bereitstellung von DirectAccess über ein paar einfache Schritte.  
  
## <a name="before-you-begin-deploying-see-the-list-of-unsupported-configurations-known-issues-and-prerequisites"></a>Bevor Sie mit der Bereitstellung beginnen, sollten Sie sich die folgende Liste mit nicht unterstützten Konfigurationen, bekannten Problemen und Voraussetzungen ansehen:  
In den folgenden Themen finden Sie Informationen zu Voraussetzungen und anderen Informationen vor der Bereitstellung von DirectAccess.  
  
-   [DirectAccess: Nicht unterstützte Konfigurationen](../../../remote-access/directaccess/DirectAccess-Unsupported-Configurations.md)  
  
-   [Erforderliche Komponenten für die Bereitstellung von DirectAccess](../../../remote-access/directaccess/Prerequisites-for-Deploying-DirectAccess.md)  
  
## <a name="scenario-description"></a><a name="BKMK_OVER"></a>Beschreibung des Szenarios  
In diesem Szenario wird ein einzelner Computer mit Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 in einigen einfachen Schritten des Assistenten als DirectAccess-Server mit Standardeinstellungen konfiguriert, ohne dass Infrastruktur Einstellungen wie eine Zertifizierungsstelle oder Active Directory Sicherheitsgruppen konfiguriert werden müssen.  
  
> [!NOTE]  
> Informationen zum Konfigurieren einer erweiterten Bereitstellung mit benutzerdefinierten Einstellungen finden Sie unter [Deploy a Single DirectAccess Server with Advanced Settings](../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md).  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Zum Einrichten eines einfachen DirectAccess-Servers sind mehrere Planungs-und Bereitstellungs Schritte erforderlich.  
  
### <a name="prerequisites"></a>Voraussetzungen  
Bevor Sie mit der Bereitstellung dieses Szenarios beginnen, sollten Sie die Liste der wichtigen Anforderungen lesen:  
  
-   Windows-Firewall muss in allen Profilen aktiviert sein.  
  
-   Dieses Szenario wird nur unterstützt, wenn auf den Client Computern Windows 10, Windows 8.1 oder Windows 8 ausgeführt wird.  
  
-   ISATAP wird im Unternehmensnetzwerk nicht unterstützt. Wenn Sie ISATAP verwenden, sollten Sie es entfernen und das systemeigene IPv6 verwenden.  
  
-   Eine Public Key-Infrastruktur ist nicht erforderlich.  
  
-   Die Bereitstellung der zweistufigen Authentifizierung wird nicht unterstützt. Für die Authentifizierung sind Domänenanmeldeinformationen erforderlich.  
  
-   DirectAccess wird automatisch auf allen mobilen Computern in der aktuellen Domäne bereitgestellt.  
  
-   Datenverkehr zum Internet wird nicht über den DirectAccess-Tunnel übertragen. Die Konfiguration einer Tunnelerzwingung wird nicht unterstützt.  
  
-   Der DirectAccess-Server ist der Netzwerkadressenserver.  
  
-   Netzwerkzugriffsschutz (Network Access Protection, NAP) wird nicht unterstützt.  
  
-   Das Ändern von Richtlinien außerhalb der DirectAccess-Verwaltungskonsole oder von PowerShell-Cmdlets wird nicht unterstützt.  
  
-   Zum Bereitstellen von mehreren Standorten, jetzt oder in Zukunft, stellen Sie zunächst [einen einzelnen DirectAccess-Server mit erweiterten Einstellungen](../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)bereit.  
  
### <a name="planning-steps"></a>Planungsschritte  
Die Planung besteht aus zwei Phasen:  
  
1.  Planen der DirectAccess-Infrastruktur. Diese Phase beschreibt die erforderlichen Planungsschritte zum Einrichten der Netzwerkinfrastruktur vor der DirectAccess-Bereitstellung. Dazu gehört die Planung von Netzwerk- und Servertopologie und DirectAccess-Netzwerkadressenserver.  
  
2.  Planen der DirectAccess-Bereitstellung. Diese Phase beschreibt die erforderlichen Planungsschritte zur Vorbereitung der DirectAccess-Bereitstellung. Dazu gehört die Planung für DirectAccess-Clientcomputer, Server- und Clientauthentifizierungsanforderungen, VPN-Einstellungen, Infrastrukturserver sowie Verwaltungs- und Anwendungsserver.  
  
Ausführliche Planungsschritte finden Sie unter [Planen einer erweiterten DirectAccess-Bereitstellung](../../../remote-access/directaccess/single-server-advanced/Plan-an-Advanced-DirectAccess-Deployment.md).  
  
### <a name="deployment-steps"></a>Bereitstellungsschritte  
Die Bereitstellung besteht aus drei Phasen:  
  
1.  Konfigurieren der DirectAccess-Infrastruktur: Diese Phase umfasst das Konfigurieren von Netzwerk und Routing, das Konfigurieren der Firewalleinstellungen (falls erforderlich), das Konfigurieren von Zertifikaten, DNS-Servern, Active Directory und GPO-Einstellungen und den DirectAccess-Netzwerkadressen Server.  
  
2.  Konfigurieren der DirectAccess-Servereinstellungen. Die Phase beinhaltet Schritte zum Konfigurieren von DirectAccess-Clientcomputern, DirectAccess-Server, Infrastrukturservern sowie Verwaltungs- und Anwendungsservern.  
  
3.  Überprüfen der Bereitstellung. Diese Phase umfasst Schritte zum Überprüfen, ob die Bereitstellung nach Bedarf funktioniert.  
  
Informationen zu den Bereitstellungsschritten finden Sie unter [Install and Configure Basic DirectAccess](../../../remote-access/directaccess/single-server-wizard/Install-and-Configure-Basic-DirectAccess.md).  
  
## <a name="practical-applications"></a><a name="BKMK_APP"></a>Praktische Anwendung  
Die Bereitstellung eines einzelnen Remotezugriffsservers bietet Folgendes:  
  
-   Einfache Zugriffsberechtigung. Verwaltete Client Computer, auf denen Windows 10, Windows 8.1, Windows 8 oder Windows 7 ausgeführt wird, können als DirectAccess-Clients konfiguriert werden. Diese Clients können immer, wenn sie im Internet sind, über DirectAccess auf interne Netzwerkressourcen zugreifen, ohne sich über eine VPN-Verbindung einzuloggen. Clientcomputer, die keines dieser Betriebssysteme verwenden, können über herkömmliche VPN-Verbindungen eine Verbindung mit dem internen Netzwerk herstellen.  
  
-   Einfache Verwaltung. Die Remoteverwaltung von DirectAccess-Clientcomputern im Internet ist mithilfe von RAS-Administratoren über DirectAccess möglich, selbst wenn die Clientcomputer sich nicht im internen Unternehmensnetzwerk befinden. Clientcomputer, die nicht den Unternehmensanforderungen entsprechen, können automatisch über Verwaltungsserver gewartet werden. Sowohl DirectAccess als auch VPN werden über dieselbe Konsole und mit denselben Assistenten verwaltet. Außerdem können einer oder mehrere RAS-Server über eine einzelne Remotezugriffs-Verwaltungskonsole verwaltet werden.  
  
## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und Features  
Die folgende Tabelle enthält die für dieses Szenario erforderlichen Rollen und Features:  
  
|Rolle/Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|---------|-----------------|  
|Remotezugriffs-Rolle|Die Rolle wird über die Server-Manager-Konsole oder Windows PowerShell installiert bzw. deinstalliert. Diese Rolle umfasst DirectAccess (zuvor ein Feature unter Windows Server 2008 R2) sowie die Routing- und RAS-Dienste (zuvor ein Rollendienst unter der Serverrolle für Netzwerkrichtlinien- und Zugriffsdienste). Die Remotezugriffs-Rolle besteht aus zwei Komponenten:<p>1. DirectAccess-und RRAS-VPN (Routing and Remote Access Services). DirectAccess und VPN werden in der Remote Zugriffs-Verwaltungskonsole verwaltet.<br />2. RRAS-Routing. RRAS-Routing Features werden in der Legacy-Routing-und Remote Zugriffs Konsole verwaltet.<p>Die RAS-Serverrolle ist von den folgenden Serverrollen/-features abhängig:<p>-Internetinformationsdienste (IIS)-Webserver: dieses Feature ist erforderlich, um den Netzwerkadressen Server auf dem Remote Zugriffs Server und den Standardweb Test zu konfigurieren.<br />-Interne Windows-Datenbank. Wird zur lokalen Ressourcenerfassung auf dem Remotezugriffsserver verwendet.|  
|Feature %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot;|So installieren Sie dieses Feature:<p>-Sie wird standardmäßig auf einem RAS-Server installiert, wenn die Remote Zugriffs Rolle installiert ist, und unterstützt die Benutzeroberfläche der Remote Verwaltungskonsole und Windows PowerShell-Cmdlets.<br />-Es kann optional auf einem Server installiert werden, auf dem die Remote Zugriffs-Server Rolle nicht ausgeführt wird. In diesem Fall wird es für die Remoteverwaltung eines RAS-Computers verwendet, der DirectAccess und VPN ausführt.<p>Das Feature "Tools für die Remotezugriffsverwaltung" besteht aus den folgenden Komponenten:<p>-Remote Zugriffs-GUI<br />-Remote Zugriffs Modul für Windows PowerShell<p>Abhängigkeiten umfassen:<p>-Gruppenrichtlinien-Verwaltungskonsole<br />-RAS-Verbindungs-Manager-Verwaltungskit (CMAK)<br />-Windows PowerShell 3,0<br />-Tools und Infrastruktur für die grafische Verwaltung|  
  
## <a name="hardware-requirements"></a><a name="BKMK_HARD"></a>Hardwareanforderungen  
Für dieses Szenario müssen die folgenden Hardwareanforderungen erfüllt werden:  
  
-   Serveranforderungen:  
  
    -   Ein Computer, der die Hardwareanforderungen für Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 erfüllt.  
  
    -   Auf dem Server muss mindestens ein Netzwerkadapter installiert, aktiviert und mit dem internen Netzwerk verbunden sein. Werden zwei Adapter verwendet, sollte ein Adapter mit dem internen Unternehmensnetzwerk und der andere mit dem externen Netzwerk (Internet oder privates Netzwerk) verbunden sein.  
  
    -   Mindestens ein Domänencontroller. RAS-Server und DirectAccess-Clients müssen Domänenmitglieder sein.  
  
-   Clientanforderungen:  
  
    -   Auf einem Client Computer muss Windows 10, Windows 8.1 oder Windows 8 ausgeführt werden.  
  
        > [!IMPORTANT]  
        > Wenn auf einigen oder allen Client Computern Windows 7 ausgeführt wird, müssen Sie den erweiterten Setup-Assistenten verwenden. Der in diesem Dokument beschriebene Setup-Assistent für die ersten Schritte unterstützt keine Client Computer, auf denen Windows 7 ausgeführt wird. Anweisungen zur Verwendung von Windows 7-Clients mit DirectAccess finden Sie unter Bereitstellen [eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) .  
  
        > [!NOTE]  
        > Nur die folgenden Betriebssysteme können als DirectAccess-Clients verwendet werden: Windows 10 Enterprise, Windows 8.1 Enterprise, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 8 Enterprise, Windows Server 2008 R2, Windows 7 Enterprise und Windows 7 Ultimate.  
  
-   Anforderungen an Infrastruktur und Verwaltungsserver:  
  
    -   Falls ein VPN aktiviert und kein statischer IP-Adressenpool konfiguriert ist, müssen Sie einen DHCP-Server bereitstellen, um VPN-Clients automatisch IP-Adressen zuzuweisen.  
  
-   Es ist ein DNS-Server erforderlich, auf dem Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 SP2 oder Windows Server 2008 R2 ausgeführt wird.  
  
## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>Softwareanforderungen  
Für dieses Szenario gelten eine Reihe von Anforderungen:  
  
-   Serveranforderungen:  
  
    -   Der RAS-Server muss Domänenmitglied sein. Der Server kann an der Schwelle zum internen Netzwerks oder geschützt durch eine Edgefirewall oder ein anderes Gerät bereitgestellt werden.  
  
    -   Wird der RAS-Server durch eine Edgefirewall oder ein NAT-Gerät geschützt, muss das Gerät so konfiguriert sein, dass ein- und ausgehender Datenverkehr für den RAS-Server zugelassen wird.  
  
    -   Die Person, die den Remotezugriff auf dem Server einrichtet, muss lokale Administratorberechtigungen für den Server und Benutzerberechtigungen für die Domäne besitzen. Zusätzlich benötigt der Administrator Berechtigungen für die Gruppenrichtlinien, die bei der DirectAccess-Bereitstellung verwendet werden. Um die Features nutzen zu können, die die DirectAccess-Bereitstellung auf mobile Computer beschränken, ist die Berechtigung zum Erstellen von WMI-Filtern für den Domänencontroller erforderlich.  
  
-   RAS-Client-Anforderungen:  
  
    -   DirectAccess-Clients müssen Domänenmitglieder sein. Domänen, die Clients enthalten, können zur selben Gesamtstruktur gehören wie der Remotezugriffsserver oder eine bidirektionale Vertrauensstellung mit der Remotezugriffsserver-Gesamtstruktur innehaben.  
  
    -   Eine Active Directory-Sicherheitsgruppe wird benötigt, um die Computer aufzunehmen, die als DirectAccess-Clients konfiguriert werden. Wird beim Konfigurieren der DirectAccess-Clienteinstellungen keine Sicherheitsgruppe angegeben, wird das Client-Gruppenrichtlinienobjekt standardmäßig auf alle Laptopcomputer in der Sicherheitsgruppe %%amp;quot;Domänencomputer%%amp;quot; angewendet. Nur die folgenden Betriebssysteme können als DirectAccess-Clients verwendet werden: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows 8 Enterprise, Windows 7 Enterprise und Windows 7 Ultimate.  
  
## <a name="see-also"></a><a name="BKMK_LINKS"></a>Siehe auch  
Die folgende Tabelle enthält Links zu zusätzlichen Ressourcen.  
  
|Inhaltstyp|Referenzen|  
|--------|-------|  
|**RAS auf TechNet**|[RAS im TechCenter](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn756544(v=ws.11))|  
|**Tools und Einstellungen**|[PowerShell-Cmdlets für den Remotezugriff](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn756544(v=ws.11))|  
|**Communityressourcen**|[DirectAccess Wiki-Einträge](https://go.microsoft.com/fwlink/?LinkId=236871)|  
|**Verwandte Technologien**|[Funktionsweise von IPv6](/previous-versions/windows/it-pro/windows-server-2003/cc781672(v=ws.10))|  
  
