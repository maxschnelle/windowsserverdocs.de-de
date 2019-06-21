---
title: Bereitstellen eines DirectAccess-Servers mit dem Assistenten für erste Schritte
description: Dieses Thema ist Teil des Handbuchs Bereitstellen eines einzelnen DirectAccess-Servers mithilfe der erste Schritte-Assistenten für Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eb0cf464-0668-40f8-8222-feb6bae6d3d5
ms.author: pashort
author: shortpatti
ms.openlocfilehash: deb220ad5ee83e2849f962c588d6150892d990d6
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281792"
---
# <a name="deploy-a-single-directaccess-server-using-the-getting-started-wizard"></a>Bereitstellen eines DirectAccess-Servers mit dem Assistenten für erste Schritte

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema bietet eine Einführung in das DirectAccess-Szenario mit einem einzelnem DirectAccess-Server und ermöglicht Ihnen die Bereitstellung von DirectAccess über ein paar einfache Schritte.  
  
## <a name="before-you-begin-deploying-see-the-list-of-unsupported-configurations-known-issues-and-prerequisites"></a>Bevor Sie mit der Bereitstellung beginnen, sollten Sie sich die folgende Liste mit nicht unterstützten Konfigurationen, bekannten Problemen und Voraussetzungen ansehen:  
In den folgenden Themen können Sie die Voraussetzungen und andere Informationen überprüfen, bevor Sie DirectAccess bereitstellen.  
  
-   [DirectAccess: Nicht unterstützte Konfigurationen](../../../remote-access/directaccess/DirectAccess-Unsupported-Configurations.md)  
  
-   [Erforderliche Komponenten für die Bereitstellung von DirectAccess](../../../remote-access/directaccess/Prerequisites-for-Deploying-DirectAccess.md)  
  
## <a name="BKMK_OVER"></a>Beschreibung des Szenarios  
In diesem Szenario wird ist ein einzelner Computer mit Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 als DirectAccess-Server in wenigen einfachen Schritten des Assistenten, ohne dass die Notwendigkeit zur Konfiguration von infrastruktureinstellungen solche mit Standardeinstellungen konfiguriert als einer Zertifizierungsstelle (CA) oder Active Directory-Sicherheitsgruppen.  
  
> [!NOTE]  
> Informationen zum Konfigurieren einer erweiterten Bereitstellung mit benutzerdefinierten Einstellungen finden Sie unter [Deploy a Single DirectAccess Server with Advanced Settings](../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md).  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Zum Einrichten eines einfachen DirectAccess-Servers sind mehrere planungs- und Bereitstellungsschritte erforderlich.  
  
### <a name="prerequisites"></a>Vorraussetzungen  
Bevor Sie mit der Bereitstellung dieses Szenarios beginnen, sollten Sie die Liste der wichtigen Anforderungen lesen:  
  
-   Windows-Firewall muss in allen Profilen aktiviert sein.  
  
-   Dieses Szenario wird nur unterstützt, wenn die Clientcomputer Windows 10, Windows 8.1 oder Windows 8 ausgeführt werden.  
  
-   ISATAP wird im Unternehmensnetzwerk nicht unterstützt. Wenn Sie ISATAP verwenden, sollten Sie es entfernen und das systemeigene IPv6 verwenden.  
  
-   Eine Public Key-Infrastruktur ist nicht erforderlich.  
  
-   Die Bereitstellung der zweistufigen Authentifizierung wird nicht unterstützt. Für die Authentifizierung sind Domänenanmeldeinformationen erforderlich.  
  
-   DirectAccess wird automatisch auf allen mobilen Computern in der aktuellen Domäne bereitgestellt.  
  
-   Datenverkehr zum Internet wird nicht über den DirectAccess-Tunnel übertragen. Die Konfiguration einer Tunnelerzwingung wird nicht unterstützt.  
  
-   Der DirectAccess-Server ist der Netzwerkadressenserver.  
  
-   Netzwerkzugriffsschutz (Network Access Protection, NAP) wird nicht unterstützt.  
  
-   Das Ändern von Richtlinien außerhalb der DirectAccess-Verwaltungskonsole oder von PowerShell-Cmdlets wird nicht unterstützt.  
  
-   Für mehrere Standorte, jetzt oder in Zukunft zuerst bereitstellen [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md).  
  
### <a name="planning-steps"></a>Planungsschritte  
Die Planung besteht aus zwei Phasen:  
  
1.  Planen der DirectAccess-Infrastruktur. Diese Phase beschreibt die erforderlichen Planungsschritte zum Einrichten der Netzwerkinfrastruktur vor der DirectAccess-Bereitstellung. Dazu gehört die Planung von Netzwerk- und Servertopologie und DirectAccess-Netzwerkadressenserver.  
  
2.  Planen der DirectAccess-Bereitstellung. Diese Phase beschreibt die erforderlichen Planungsschritte zur Vorbereitung der DirectAccess-Bereitstellung. Dazu gehört die Planung für DirectAccess-Clientcomputer, Server- und Clientauthentifizierungsanforderungen, VPN-Einstellungen, Infrastrukturserver sowie Verwaltungs- und Anwendungsserver.  
  
Detaillierten Planungsschritte finden Sie unter [Planen einer erweiterten DirectAccess-Bereitstellung](../../../remote-access/directaccess/single-server-advanced/Plan-an-Advanced-DirectAccess-Deployment.md).  
  
### <a name="deployment-steps"></a>Bereitstellungsschritte  
Die Bereitstellung besteht aus drei Phasen:  
  
1.  Konfigurieren der DirectAccess-Infrastruktur: Diese Phase beinhaltet, Konfigurieren von Netzwerk und routing, das Konfigurieren der Firewalleinstellungen, ggf. Konfigurieren der Zertifikate, DNS-Server, Active Directory- und Gruppenrichtlinienobjekt-Einstellungen und die Netzwerkadresse für DirectAccess Server.  
  
2.  Konfigurieren der DirectAccess-servereinstellungen. Die Phase beinhaltet Schritte zum Konfigurieren von DirectAccess-Clientcomputern, DirectAccess-Server, Infrastrukturservern sowie Verwaltungs- und Anwendungsservern.  
  
3.  Überprüfen der Bereitstellung an. Diese Phase beinhaltet Schritte aus, um sicherzustellen, dass die Bereitstellung nach Bedarf funktioniert.  
  
Informationen zu den Bereitstellungsschritten finden Sie unter [Install and Configure Basic DirectAccess](../../../remote-access/directaccess/single-server-wizard/Install-and-Configure-Basic-DirectAccess.md).  
  
## <a name="BKMK_APP"></a>Praktische Anwendungen  
Die Bereitstellung eines einzelnen Remotezugriffsservers bietet Folgendes:  
  
-   Einfache Bedienung. Sie können verwaltete Clientcomputer, die unter Windows 10, Windows 8.1, Windows 8 oder Windows 7, als DirectAccess-Clients konfigurieren. Diese Clients können immer, wenn sie im Internet sind, über DirectAccess auf interne Netzwerkressourcen zugreifen, ohne sich über eine VPN-Verbindung einzuloggen. Clientcomputer, die keines dieser Betriebssysteme verwenden, können über herkömmliche VPN-Verbindungen eine Verbindung mit dem internen Netzwerk herstellen.  
  
-   Einfache Verwaltung. Die Remoteverwaltung von DirectAccess-Clientcomputern im Internet ist mithilfe von RAS-Administratoren über DirectAccess möglich, selbst wenn die Clientcomputer sich nicht im internen Unternehmensnetzwerk befinden. Clientcomputer, die nicht den Unternehmensanforderungen entsprechen, können automatisch über Verwaltungsserver gewartet werden. Sowohl DirectAccess als auch VPN werden über dieselbe Konsole und mit denselben Assistenten verwaltet. Außerdem können einer oder mehrere RAS-Server über eine einzelne Remotezugriffs-Verwaltungskonsole verwaltet werden.  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und features  
Die folgende Tabelle enthält die für dieses Szenario erforderlichen Rollen und Features:  
  
|Rolle/Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|---------|-----------------|  
|Remotezugriffs-Rolle|Die Rolle wird über die Server-Manager-Konsole oder Windows PowerShell installiert bzw. deinstalliert. Diese Rolle umfasst DirectAccess (zuvor ein Feature unter Windows Server 2008 R2) sowie die Routing- und RAS-Dienste (zuvor ein Rollendienst unter der Serverrolle für Netzwerkrichtlinien- und Zugriffsdienste). Die Remotezugriffs-Rolle besteht aus zwei Komponenten:<br /><br />1.  DirectAccess und Routing-und RAS-Dienste (RRAS) VPN. DirectAccess und VPN werden gemeinsam in der Remotezugriffs-Verwaltungskonsole verwaltet.<br />2.  RRAS-Routing. RRAS-Routingfeatures werden in der älteren Routing- und RAS-Konsole verwaltet.<br /><br />Die RAS-Serverrolle ist von den folgenden Serverrollen/-features abhängig:<br /><br />-IIS (Internetinformationsdienste) Webserver - ist dieses Feature erforderlich, um den Netzwerkadressenserver auf dem RAS-Server und den standardwebtest zu konfigurieren.<br />-Interne Windows-Datenbank. Wird zur lokalen Ressourcenerfassung auf dem Remotezugriffsserver verwendet.|  
|Feature %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot;|So installieren Sie dieses Feature:<br /><br />– Es wird standardmäßig auf einem RAS-Server installiert, wenn die Rolle "Remotezugriff" installiert ist, und die Benutzeroberfläche der Remote-Management-Verwaltungskonsole und Windows PowerShell-Cmdlets unterstützt.<br />– sie können optional auf einem Server nicht mit der RAS-Serverrolle installiert werden. In diesem Fall wird es für die Remoteverwaltung eines RAS-Computers verwendet, der DirectAccess und VPN ausführt.<br /><br />Das Feature "Tools für die Remotezugriffsverwaltung" besteht aus den folgenden Komponenten:<br /><br />-Remotezugriffs-GUI<br />-RAS-Modul für Windows PowerShell<br /><br />Abhängigkeiten umfassen:<br /><br />-Gruppenrichtlinien-Verwaltungskonsole<br />-RAS-Verbindungs-Manager-Verwaltungskit (CMAK)<br />-Windows PowerShell 3.0<br />-Grafische Verwaltungstools und Infrastruktur|  
  
## <a name="BKMK_HARD"></a>Hardwareanforderungen  
Für dieses Szenario müssen die folgenden Hardwareanforderungen erfüllt werden:  
  
-   Serveranforderungen:  
  
    -   Ein Computer, der die hardwareanforderungen für Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 erfüllt.  
  
    -   Auf dem Server muss mindestens ein Netzwerkadapter installiert, aktiviert und mit dem internen Netzwerk verbunden sein. Werden zwei Adapter verwendet, sollte ein Adapter mit dem internen Unternehmensnetzwerk und der andere mit dem externen Netzwerk (Internet oder privates Netzwerk) verbunden sein.  
  
    -   Mindestens ein Domänencontroller. RAS-Server und DirectAccess-Clients müssen Domänenmitglieder sein.  
  
-   Clientanforderungen:  
  
    -   Ein Client-Computer muss Windows 10, Windows 8.1 oder Windows 8 ausgeführt werden.  
  
        > [!IMPORTANT]  
        > Wenn einige oder alle Ihre Clientcomputer Windows 7 ausführen, müssen Sie die erweiterten Setup-Assistenten verwenden. Setup Assistent für erste Schritte in diesem Dokument beschriebenen unterstützt nicht die Client-Computern, auf denen Windows 7 ausgeführt werden. Finden Sie unter [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/../../../remote-access/directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md) Anweisungen zur Verwendung von Windows 7-Clients mit DirectAccess.  
  
        > [!NOTE]  
        > Es können nur die folgenden Betriebssysteme als DirectAccess-Clients verwendet werden: Windows 10 Enterprise, Windows 8.1 Enterprise, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows 8 Enterprise, Windows Server 2008 R2, Windows 7 Enterprise und Windows 7 Ultimate.  
  
-   Anforderungen an Infrastruktur und Verwaltungsserver:  
  
    -   Falls ein VPN aktiviert und kein statischer IP-Adressenpool konfiguriert ist, müssen Sie einen DHCP-Server bereitstellen, um VPN-Clients automatisch IP-Adressen zuzuweisen.  
  
-   Ein DNS-Server unter Windows Server 2016 ist Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 SP2 oder Windows Server 2008 R2 erforderlich.  
  
## <a name="BKMK_SOFT"></a>Softwareanforderungen  
Für dieses Szenario gelten eine Reihe von Anforderungen:  
  
-   Serveranforderungen:  
  
    -   Der Remotezugriffsserver muss Domänenmitglied sein. Der Server kann an der Schwelle zum internen Netzwerks oder geschützt durch eine Edgefirewall oder ein anderes Gerät bereitgestellt werden.  
  
    -   Wird der RAS-Server durch eine Edgefirewall oder ein NAT-Gerät geschützt, muss das Gerät so konfiguriert sein, dass ein- und ausgehender Datenverkehr für den RAS-Server zugelassen wird.  
  
    -   Die Person, die den Remotezugriff auf dem Server einrichtet, muss lokale Administratorberechtigungen für den Server und Benutzerberechtigungen für die Domäne besitzen. Zusätzlich benötigt der Administrator Berechtigungen für die Gruppenrichtlinien, die bei der DirectAccess-Bereitstellung verwendet werden. Um die Features nutzen zu können, die die DirectAccess-Bereitstellung auf mobile Computer beschränken, ist die Berechtigung zum Erstellen von WMI-Filtern für den Domänencontroller erforderlich.  
  
-   RAS-Client-Anforderungen:  
  
    -   DirectAccess-Clients müssen Domänenmitglieder sein. Domänen, die Clients enthalten, können zur selben Gesamtstruktur gehören wie der Remotezugriffsserver oder eine bidirektionale Vertrauensstellung mit der Remotezugriffsserver-Gesamtstruktur innehaben.  
  
    -   Eine Active Directory-Sicherheitsgruppe wird benötigt, um die Computer aufzunehmen, die als DirectAccess-Clients konfiguriert werden. Wird beim Konfigurieren der DirectAccess-Clienteinstellungen keine Sicherheitsgruppe angegeben, wird das Client-Gruppenrichtlinienobjekt standardmäßig auf alle Laptopcomputer in der Sicherheitsgruppe %%amp;quot;Domänencomputer%%amp;quot; angewendet. Es können nur die folgenden Betriebssysteme als DirectAccess-Clients verwendet werden:  WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2, Windows 8 Enterprise, Windows 7 Enterprise und Windows 7 Ultimate.  
  
## <a name="BKMK_LINKS"></a>Siehe auch  
Die folgende Tabelle enthält Links zu zusätzlichen Ressourcen.  
  
|Inhaltstyp|Verweise|  
|--------|-------|  
|**RAS auf TechNet**|[RAS im TechCenter](https://technet.microsoft.com/network/bb545655.aspx)|  
|**Tools und Einstellungen**|[PowerShell-Cmdlets für Remoteserver](https://technet.microsoft.com/library/hh918399.aspx)|  
|**Communityressourcen**|[DirectAccess Wiki-Einträge](https://go.microsoft.com/fwlink/?LinkId=236871)|  
|**Verwandte Technologien**|[Funktionsweise von IPv6](https://technet.microsoft.com/library/cc781672(v=WS.10).aspx)|  
  


