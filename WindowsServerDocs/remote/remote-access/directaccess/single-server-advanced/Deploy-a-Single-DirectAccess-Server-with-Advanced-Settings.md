---
title: Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen
description: Dieses Thema ist Teil des Handbuchs Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen für Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b211a9ca-1208-4e1f-a0fe-26a610936c30
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f17e1c9dd1a4e2d064a4e5980904c524dc62fb72
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283611"
---
# <a name="deploy-a-single-directaccess-server-with-advanced-settings"></a>Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema enthält eine Einführung in das DirectAccess-Szenario, das mit einem einzelnen DirectAccess-Server und ermöglicht Ihnen das Bereitstellen von DirectAccess mit erweiterten Einstellungen an.  
  
## <a name="before-you-begin-deploying-see-the-list-of-unsupported-configurations-known-issues-and-prerequisites"></a>Bevor Sie mit der Bereitstellung beginnen, sollten Sie sich die folgende Liste mit nicht unterstützten Konfigurationen, bekannten Problemen und Voraussetzungen ansehen:  
In den folgenden Themen können Sie die Voraussetzungen und andere Informationen überprüfen, bevor Sie DirectAccess bereitstellen.  
  
-   [DirectAccess: Nicht unterstützte Konfigurationen](../../../remote-access/directaccess/DirectAccess-Unsupported-Configurations.md)  
  
-   [Erforderliche Komponenten für die Bereitstellung von DirectAccess](../../../remote-access/directaccess/Prerequisites-for-Deploying-DirectAccess.md)  
  
## <a name="BKMK_OVER"></a>Beschreibung des Szenarios  
In diesem Szenario wird ein einzelner Computer mit Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 können als DirectAccess-Server mit erweiterten Einstellungen konfiguriert.  
  
> [!NOTE]  
> Wenn Sie nur eine grundlegende Bereitstellung mit einfachen Standardeinstellungen konfigurieren möchten, finden Sie unter [Deploy a Single DirectAccess Server Using the Getting Started Wizard](../../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)weitere Informationen. In dem einfachen Szenario wird DirectAccess über einen Assistenten mit Standardeinstellungen eingerichtet, ohne dass die Notwendigkeit zur Konfiguration von Infrastruktureinstellungen wie einer Zertifizierungsstelle oder Active Directory-Sicherheitsgruppen besteht.  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Um einen einzelnen DirectAccess-Server mit erweiterten Einstellungen einzurichten, müssen Sie einige Planungs- und Bereitstellungsschritte durchführen.  
  
### <a name="prerequisites"></a>Vorraussetzungen  
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
  
Informationen zu den Bereitstellungsschritten finden Sie unter [Install and Configure Advanced DirectAccess](../../../remote-access/directaccess/single-server-advanced/Install-and-Configure-Advanced-DirectAccess.md).  
  
## <a name="BKMK_APP"></a>Praktische Anwendungen  
Die Bereitstellung eines einzelnen DirectAccess-Servers bietet Folgendes:  
  
-   **Erleichterte Bedienung**. Verwaltete Clientcomputer, die unter Windows 10, Windows 8.1, Windows 8 und Windows 7 können als DirectAccess-Clientcomputer konfiguriert werden. Diese Clients können immer, wenn sie im Internet sind, über DirectAccess auf interne Netzwerkressourcen zugreifen, ohne sich über eine VPN-Verbindung einzuloggen. Clientcomputer, die keines dieser Betriebssysteme verwenden, können per VPN eine Verbindung zum internen Netzwerk herstellen.  
  
-   **Erleichterte Verwaltung**. Die Remoteverwaltung von DirectAccess-Clientcomputern im Internet ist mithilfe von RAS-Administratoren über DirectAccess möglich, selbst wenn die Clientcomputer sich nicht im internen Unternehmensnetzwerk befinden. Clientcomputer, die nicht den Unternehmensanforderungen entsprechen, können automatisch über Verwaltungsserver gewartet werden. Sowohl DirectAccess als auch VPN werden über dieselbe Konsole und mit denselben Assistenten verwaltet. Außerdem können einer oder mehrere DirectAccess-Server über eine einzelne Remotezugriffs-Verwaltungskonsole verwaltet werden.  
  
## <a name="BKMK_NEW"></a>Für dieses Szenario erforderlichen Rollen und features  
Die folgende Tabelle enthält die für dieses Szenario erforderlichen Rollen und Features:  
  
|Rolle/Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|---------|-----------------|  
|Remotezugriffs-Rolle|Die Rolle wird über die Server-Manager-Konsole oder Windows PowerShell installiert bzw. deinstalliert. Diese Rolle umfasst DirectAccess sowie die Routing- und RAS-Dienste. Die Remotezugriffs-Rolle besteht aus zwei Komponenten:<br/><br/>1.  DirectAccess und RRAS-VPN. DirectAccess und VPN werden gemeinsam in der Remotezugriffs-Verwaltungskonsole verwaltet.<br/>2.  RRAS-Routing. RRAS-Routingfeatures werden in der älteren Routing- und RAS-Konsole verwaltet.<br /><br />Die RAS-Serverrolle ist von den folgenden Serverrollen/-features abhängig:<br/><br/> -IIS (Internetinformationsdienste) Webserver - ist dieses Feature erforderlich, um den Netzwerkadressenserver auf dem DirectAccess-Server und den standardwebtest zu konfigurieren.<br/> -Interne Windows-Datenbank. Zur lokalen Kontoführung auf dem DirectAccess-Server verwendet.|  
|Feature %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot;|So installieren Sie dieses Feature:<br /><br />– Es wird standardmäßig auf einem DirectAccess-Server installiert, wenn die Rolle "Remotezugriff" installiert ist, und die Benutzeroberfläche der Remote-Management-Verwaltungskonsole und Windows PowerShell-Cmdlets unterstützt.<br />– sie können optional auf einem Server nicht mit der DirectAccess-Server-Rolle installiert werden. In diesem Fall wird es für die Remoteverwaltung eines RAS-Computers verwendet, der DirectAccess und VPN ausführt.<br /><br />Das Feature "Tools für die Remotezugriffsverwaltung" besteht aus den folgenden Komponenten:<br /><br />-Remote Access grafische Benutzeroberfläche (GUI)<br />-RAS-Modul für Windows PowerShell<br /><br />Abhängigkeiten umfassen:<br /><br />-Gruppenrichtlinien-Verwaltungskonsole<br />-RAS-Verbindungs-Manager-Verwaltungskit (CMAK)<br />-Windows PowerShell 3.0<br />-Grafische Verwaltungstools und Infrastruktur|  
  
## <a name="BKMK_HARD"></a>Hardwareanforderungen  
Für dieses Szenario müssen die folgenden Hardwareanforderungen erfüllt werden:  
  
-   Serveranforderungen:  
  
    -   Ein Computer, der die hardwareanforderungen für Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 erfüllt.  
  
    -   Auf dem Server muss mindestens ein Netzwerkadapter installiert, aktiviert und mit dem internen Netzwerk verbunden sein. Werden zwei Adapter verwendet, sollte ein Adapter mit dem internen Unternehmensnetzwerk und der andere mit dem externen Netzwerk (Internet oder privates Netzwerk) verbunden sein.  
  
    -   Falls Teredo als IPv4- bis IPv6-Übergangsprotokoll benötigt wird, benötigt der externe Adapter des Servers zwei aufeinanderfolgenden öffentliche IPv4-Adressen. Wenn nur eine IP-Adresse verfügbar ist, kann nur IP-HTTPS als Übergangsprotokoll verwendet werden.  
  
    -   Mindestens ein Domänencontroller. DirectAccess-Server und DirectAccess-Clients müssen Domänenmitglieder sein.  
  
    -   Eine Zertifizierungsstelle ist erforderlich, wenn Sie keine selbstsignierten Zertifikate für IP-HTTPS oder den Netzwerkadressenserver verwenden möchten, oder wenn Sie Clientzertifikate zur Client-IPsec-Authentifizierung verwenden möchten. Alternativ können Sie die Zertifikate von einer öffentlichen Zertifizierungsstelle anfordern.  
  
    -   Befindet sich der Netzwerkadressenserver nicht auf dem DirectAccess-Server, ist ein separater Webserver für die Ausführung erforderlich.  
  
-   Clientanforderungen:  
  
    -   Ein Client-Computer muss Windows 10, Windows 8 oder Windows 7 ausgeführt werden.  
  
        > [!NOTE]  
        > Die folgenden Betriebssysteme können als DirectAccess-Clients verwendet werden: Windows 10, Windows Server 2012 R2, WindowsServer 2012, Windows 8 Enterprise, Windows 7 Enterprise oder Windows 7 Ultimate.  
  
-   Anforderungen an Infrastruktur und Verwaltungsserver:  
  
    -   Während der Remoteverwaltung von DirectAccess-Clientcomputern initiieren die Clients die Kommunikation mit Verwaltungsservern, z. B. Domänencontrollern, System Center-Konfigurationsservern und Inhaltsregistrierungsstellen (HRA)-Servern, für Dienste, darunter Windows- und Antivirus-Updates sowie Network Access Protection (NAP)-Clientkompatibilität. Die erforderlichen Server sollten bereitgestellt werden, bevor mit der Bereitstellung des Remotezugriffs begonnen wird.  
  
    -   Falls der Remotezugriff Client-NAP-Kompatibilität erfordert, sollten die NPS- und HRS-Server bereitgestellt werden, bevor mit der Bereitstellung des Remotezugriffs begonnen wird.  
  
    -   Falls ein VPN aktiviert ist, ist ein DHCP-Server erforderlich, um die IP-Adressen automatisch den VPN-Clients zuzuweisen, sofern kein statischen IP-Adresspool genutzt wird.  
  
## <a name="BKMK_SOFT"></a>Softwareanforderungen  
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
        > Wenn Sie Teredo in der DirectAccess-Bereitstellung aktiviert haben, und Sie Zugriff auf Windows 7-Clients ermöglichen möchten, stellen Sie sicher, dass die Clients auf Windows 7 mit SP1 aktualisiert werden. Clients mit Windows 7 RTM werden nicht über Teredo herstellen können. Diese Clients können jedoch weiterhin eine Verbindung zum Unternehmensnetzwerk über IP-HTTPS herstellen.  
  
## <a name="BKMK_LINKS"></a>Siehe auch  
Die folgende Tabelle enthält Links zu zusätzlichen Ressourcen.  
  
|Inhaltstyp|Verweise|  
|--------|-------|  
|**Bereitstellung**|[DirectAccess-Bereitstellungspfade in WindowsServer](../../../remote-access/directaccess/DirectAccess-Deployment-Paths-in-Windows-Server.md)<br /><br />[Bereitstellen eines DirectAccess-Servers mit dem Assistenten für erste Schritte](../../../remote-access/directaccess/single-server-wizard/Deploy-a-Single-DirectAccess-Server-Using-the-Getting-Started-Wizard.md)|  
|**Tools und Einstellungen**|[PowerShell-Cmdlets für Remoteserver](https://technet.microsoft.com/library/hh918399.aspx)|  
|**Communityressourcen**|[Orientierungshandbuch für DirectAccess](https://social.technet.microsoft.com/wiki/contents/articles/23210.directaccess-survival-guide.aspx)<br /><br />[DirectAccess Wiki-Einträge](https://go.microsoft.com/fwlink/?LinkId=236871)|  
|**Verwandte Technologien**|[Funktionsweise von IPv6](https://technet.microsoft.com/library/cc781672(v=WS.10).aspx)|  
  


