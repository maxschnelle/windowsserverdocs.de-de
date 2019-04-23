---
title: Bereitstellen des Remotezugriffs in einem Cluster
description: Dieses Thema ist Teil des Leitfadens Bereitstellen des Remotezugriffs in einem Cluster unter Windows Server 2016.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ab2b0731a5673e14fb130d539324701a336f30ac
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863631"
---
# <a name="deploy-remote-access-in-a-cluster"></a>Bereitstellen des Remotezugriffs in einem Cluster

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Windows Server 2016 und Windows Server 2012 kombiniert DirectAccess- und RAS-Dienst \(RAS\) VPN in einer einzigen remotezugriffsrolle. Sie können die RAS-Dienst in einer Reihe von Unternehmensszenarios bereitstellen. Diese Übersicht bietet eine Einführung in das Unternehmensszenario für die Bereitstellung mehrerer Remotezugriffsserver in einem Auslastungstestszenario Cluster mit Windows-Netzwerklastenausgleich verteilt \(NLB\) oder mit einem externen Lastenausgleich \(ELB \), z. B. F5 Big\-IP.  

## <a name="BKMK_OVER"></a>Beschreibung des Szenarios  
Eine Clusterbereitstellung schließt mehrere Remotezugriffsserver zu einer Einheit, die dann als eine zentrale Anlaufstelle für Remoteclientcomputer über DirectAccess oder VPN mit dem internen Unternehmensnetzwerk, die mit der externen virtuellen IP- fungiert\(VIP\) Adresse des RAS-Clusters.  Datenverkehr an den Cluster ein Lastenausgleich mit Windows NLB oder mit einem externen Lastenausgleich \(wie z. B. F5 Big\-IP\).  

## <a name="prerequisites"></a>Vorraussetzungen  
Bevor Sie mit der Bereitstellung dieses Szenarios beginnen, sollten Sie die Liste der wichtigen Anforderungen lesen:  

-   Standardlastenausgleich über Windows NLB.  

-   Externer Lastenausgleich wird unterstützt.  

-   Der Unicast-Modus ist der standardmäßige und empfohlene Modus für den NLB.  

-   Das Ändern von Richtlinien außerhalb der DirectAccess-Verwaltungskonsole oder von PowerShell-Cmdlets wird nicht unterstützt.  

-   Wenn NLB oder ein externer Lastenausgleich verwendet wird, das Präfix IPHTTPS kann nicht geändert werden, nichts außer \/59.  

-   Die Lastenausgleichsknoten müssen sich im gleichen IPv4-Subnetz befinden.  

-   ELB-Bereitstellungen Wenn verwalten erforderlich ist, und DirectAccess-Clients können keine&nbsp;Teredo. Nur IPHTTPS kann verwendet werden, für das Ende\-zu\-Kommunikation zu beenden.  

-   Stellen Sie sicher alle bekannten NLB\/ELB-Hotfixes installiert sind.  

-   ISATAP wird im Unternehmensnetzwerk nicht unterstützt. Wenn Sie ISATAP verwenden, sollten Sie es entfernen und das systemeigene IPv6 verwenden.  

## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Das Clusterbereitstellungsszenario umfasst eine Reihe von Schritten:  

1.  [Bereitstellen einer Always on-VPN-Server mit erweiterten Optionen](../../vpn/always-on-vpn/deploy/always-on-vpn-adv-options.md). Ein einzelnes Remotezugriffsservers mit erweiterten Einstellungen muss bereitgestellt werden, bevor eine Clusterbereitstellung eingerichtet wird.  

2.  [Planen eine Clusterbereitstellung mit Remotezugriff](plan/Plan-a-Remote-Access-Cluster-Deployment.md). Um eine Anzahl zusätzlicher einem Clusters von einer Einzelserver-Bereitstellung zu erstellen sind die Schritte, einschließlich der Vorbereitung von Zertifikaten für die Bereitstellung des Clusters erforderlich.  

3.  [Konfigurieren eines Clusters mit Remotezugriff](configure/Configure-a-Remote-Access-Cluster.md). Dies umfasst eine Reihe von Konfigurationsschritten, einschließlich der Vorbereitung des einzelnen Servers für Windows NLB oder externen Lastenausgleich, Vorbereitung weiterer Server den Cluster beitreten und Aktivieren des Lastenausgleichs.  

## <a name="BKMK_APP"></a>Praktische Anwendungen  
Der Zusammenschluss mehrerer Server zu einem Servercluster bietet Folgendes:  

-   Skalierbarkeit. Ein einzelnes Remotezugriffsservers bietet eine eingeschränkte serverzuverlässigkeit und die Skalierbarkeit der Leistung. Durch die Gruppierung der Ressourcen von zwei oder mehr Servern zu einem einzigen Cluster können Sie die verfügbare Kapazität für die Benutzer und den Durchsatz erhöhen.  

-   Hohe Verfügbarkeit. Ein Cluster bietet hohen Verfügbarkeit für immer\-Zugriff. Wenn ein Server im Cluster ausfällt, können Remotebenutzer weiterhin über einen anderen Server im Cluster auf das Unternehmensnetzwerk zugreifen. Alle Server im Cluster verfügen, den gleichen Satz von Cluster virtuelle IP-Adresse \(VIP\) Adressen, während gleichzeitig eine eindeutige, dedizierte IP-Adressen für jeden Server.  

-   Einfache\-von\-Management. Ein Cluster ermöglicht die Verwaltung mehrerer Server als einzelne Entität. Gemeinsam genutzte Einstellungen können problemlos clusterserverübergreifend festgelegt werden. Remotezugriffseinstellungen können von jedem der Server im Cluster oder Remote mithilfe der Remoteserver-Verwaltungstools verwaltet werden \(RSAT\). Darüber hinaus kann der ganze Cluster über eine einzelne Remotezugriffs-Verwaltungskonsole überwacht werden.  

## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und features  
Die folgende Tabelle enthält die für dieses Szenario erforderlichen Rollen und Features:  

|Rolle\/Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|---------|-----------------|  
|Remotezugriffs-Rolle|Diese Rolle wird mithilfe der Server-Manager-Konsole installiert und deinstalliert. Sie umfasst DirectAccess, die zuvor ein Feature in Windows Server 2008 R2 und Routing und RAS-Dienste \(RRAS\), zuvor ein Rollendienst unter der Netzwerkrichtlinie und Zugriffsdienste \(NPAS\) -Serverrolle. Die Remotezugriffs-Rolle besteht aus zwei Komponenten:<br /><br />– Always On-VPN- und Routing und RAS-Dienste \(RRAS\) VPN – DirectAccess und VPN werden gemeinsam in der Remotezugriffs-Verwaltungskonsole verwaltet.<br />-RRAS Routing – RRAS-Routingfeatures werden in der älteren Routing- und RAS-Konsole verwaltet.<br /><br />Es bestehen folgende Abhängigkeiten:<br /><br />– Internet Information Services \(IIS\) Webserver – dieses Feature ist erforderlich, um die Netzwerk-Speicherort Server und den standardwebtest zu konfigurieren.<br />-Windows interne Database-Used zur lokalen Kontoführung auf dem RAS-Server.|  
|Feature %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot;|So installieren Sie dieses Feature:<br /><br />– Es wird standardmäßig auf einem RAS-Server installiert, wenn die Rolle "Remotezugriff" installiert ist, und unterstützt die Benutzeroberfläche der RAS-Konsole.<br />– sie können optional auf einem Server nicht mit der RAS-Serverrolle installiert werden. In diesem Fall wird es für die Remoteverwaltung eines RAS-Computers verwendet, der DirectAccess und VPN ausführt.<br /><br />Das Feature "Tools für die Remotezugriffsverwaltung" besteht aus den folgenden Komponenten:<br /><br />-Remotezugriffs-GUI und Befehlszeilentools<br />-RAS-Modul für Windows PowerShell<br /><br />Abhängigkeiten umfassen:<br /><br />-Gruppenrichtlinien-Verwaltungskonsole<br />-RAS-Verbindungs-Manager-Verwaltungskit \(CMAK\)<br />-Windows PowerShell 3.0<br />-Grafische Verwaltungstools und Infrastruktur|  
|Netzwerklastenausgleich|Dieses Feature ermöglicht den Lastenausgleich in einem Cluster mithilfe des Windows-Netzwerklastenausgleichs.|  

## <a name="BKMK_HARD"></a>Hardwareanforderungen  
Für dieses Szenario müssen die folgenden Hardwareanforderungen erfüllt werden:  

-   Mindestens zwei Computer, die die hardwareanforderungen für Windows Server 2012 zu erfüllen.  

-   Für das Szenario für den externen Lastenausgleich ist dedizierte Hardware erforderlich \(d. h. F5 BigIP\).  

-   Um das Szenario testen zu können, benötigen Sie mindestens einen Computer mit Windows 10 als Always On-VPN-Client konfiguriert.   

## <a name="BKMK_SOFT"></a>Softwareanforderungen  
Für dieses Szenario gelten eine Reihe von Anforderungen:  

-   Softwareanforderungen für die Bereitstellung auf einem Einzelserver. Weitere Informationen finden Sie unter [Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md). Eine einzelne Remotezugriff).  

-   Zusätzlich zu den softwareanforderungen für einen einzelnen Server stehen eine Anzahl von Cluster\-besondere Anforderungen:  

    -   Auf jedem Clusterserver die IP-Adresse\-HTTPS-Zertifikat Antragstellername muss die ConnectTo-Adresse übereinstimmen. Eine Clusterbereitstellung unterstützt eine Mischung von Platzhalterzeichen und nicht\-Platzhalterzertifikate auf Clusterservern.  

    -   Wenn der Netzwerkadressenserver auf dem Remotezugriffsserver installiert ist, muss das Netzwerkadressenserver-Zertifikat auf jedem Clusterserver den gleichen Antragstellernamen aufweisen. Darüber hinaus darf der Name des Netzwerkadressenserver-Zertifikats nicht mit dem Namen eines beliebigen Servers in der DirectAccess-Bereitstellung identisch sein.  

    -   IP\-HTTPS und den Netzwerkadressenserver-Zertifikate müssen mit derselben Methode mit dem das Zertifikat für den einzelnen Server ausgestellt wurde ausgestellt werden. Wenn die einzelne Server mit eine öffentlichen Zertifizierungsstelle verwendet z. B. \(Zertifizierungsstelle\) alle Server im Cluster müssen ein von einer öffentlichen Zertifizierungsstelle ausgestelltes Zertifikat verfügen. Oder wenn die einzelne Server ein selbstsigniertes\-signiertes Zertifikat für IP-Adresse\-HTTPS und allen Servern im Cluster müssen entsprechend.  

    -   Das IPv6-Präfix, das DirectAccess-Clientcomputern in Serverclustern zugewiesen wird, muss 59 Bit umfassen. Wenn VPN aktiviert ist, muss das VPN-Präfix ebenfalls 59 Bit umfassen.  

## <a name="KnownIssues"></a>Bekannte Probleme  
Im Folgenden finden Sie bekannte Probleme beim Konfigurieren eines Clusterszenarios:  

-   Nach dem Konfigurieren von DirectAccess in einem IPv4-\-nur die Bereitstellung mit einem einzelnen Netzwerkadapter und nach dem Standard-DNS64 \(die IPv6-Adresse mit ": 3333::"\) automatisch auf den Netzwerkadapter konfiguriert ist Es wird versucht, den aktivieren\-Lastenausgleich über die Remotezugriffs-Verwaltungskonsole wird eine Eingabeaufforderung für den Benutzer auf ein IPv6-DIP-Adresse. Wenn eine IPv6-DIP-Adresse angegeben wird, tritt nach dem Klicken auf **Commit ausführen** ein Konfigurationsfehler mit folgender Fehlermeldung auf: Der Parameter ist falsch.  

    So beheben Sie dieses Problem  

    1.  Laden Sie die Sicherung herunter, und stellen Sie Skripts aus [Back up and Restore Remote Access Configuration](https://gallery.technet.microsoft.com/Back-up-and-Restore-Remote-e157e6a6)wieder her.  

    2.  Sichern Sie die Remotezugriffs-GPOs verwenden das heruntergeladene Skript Sicherung\-RemoteAccess.ps1  

    3.  Versuchen Sie, den Lastenausgleich bis zu dem Schritt zu aktivieren, bei dem ein Fehler auftritt. Erweitern Sie im Dialogfeld "Lastenausgleich aktivieren" im Detailbereich rechts\-klicken Sie im Detailbereich auf, und klicken Sie dann auf **Skript kopieren**.  

    4.  Öffnen Sie Editor, und fügen Sie den Inhalt der Zwischenablage ein. Zum Beispiel:  

        ```  
        Set-RemoteAccessLoadBalancer -InternetDedicatedIPAddress @('10.244.4.19 /255.255.255.0','fdc4:29bd:abde:3333::2/128') -InternetVirtualIPAddress @('fdc4:29bd:abde:3333::1/128', '10.244.4.21 /255.255.255.0') -ComputerName 'DA1.domain1.corp.contoso.com' -Verbose  
        ```  

    5.  Schließen Sie alle offenen Remotezugriffs-Dialogfelder und die Remotezugriffs-Verwaltungskonsole.  

    6.  Bearbeiten Sie den eingefügten Text, und entfernen Sie die IPv6-Adressen. Zum Beispiel:  

        ```  
        Set-RemoteAccessLoadBalancer -InternetDedicatedIPAddress @('10.244.4.19 /255.255.255.0') -InternetVirtualIPAddress @('10.244.4.21 /255.255.255.0') -ComputerName 'DA1.domain1.corp.contoso.com' -Verbose  
        ```  

    7.  Führen Sie den Befehl aus dem vorherigen Schritt in einem PowerShell-Fenster mit erhöhten Rechten aus.  

    8.  Wenn das Cmdlet ein Fehler auftritt, während der Ausführung \(nicht durch falsche Eingabewerte\), führen Sie den Befehl Restore\-RemoteAccess.ps1, und führen Sie Anweisungen, um sicherzustellen, dass die Integrität der ursprünglichen Konfiguration beibehalten wird .  

    9. Nun können Sie die Remotezugriffs-Verwaltungskonsole wieder öffnen.  
