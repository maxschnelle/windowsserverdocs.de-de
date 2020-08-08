---
title: Bereitstellen von Remotezugriff in einem Cluster
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs in einem Cluster unter Windows Server 2016.
manager: dougkim
ms.topic: article
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c1d0a9490a2b2ef6efbd15f39ec95f1b482efd5e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944170"
---
# <a name="deploy-remote-access-in-a-cluster"></a>Bereitstellen von Remotezugriff in einem Cluster

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Windows Server 2016 und Windows Server 2012 kombinieren DirectAccess-und RAS-Dienst- \( RAS- \) VPN zu einer einzigen Remote Zugriffs Rolle. Sie können den Remote Zugriff in einer Reihe von Unternehmens Szenarios bereitstellen. Diese Übersicht bietet eine Einführung in das Unternehmens Szenario für die Bereitstellung mehrerer RAS-Server in einem Cluster Lastenausgleich mit Windows-Netzwerk Lastenausgleich (Network Load Balancing \( , NLB) \) oder mit einem externen Lasten Ausgleichs Modul ( \( \) z. b. F5 Big \- IP).

## <a name="scenario-description"></a><a name="BKMK_OVER"></a>Beschreibung des Szenarios
Eine Cluster Bereitstellung sammelt mehrere RAS-Server in einer einzelnen Einheit, die dann als einzelner Kontaktpunkt für Remote Client Computer fungiert, die über DirectAccess oder VPN eine Verbindung mit dem internen Unternehmensnetzwerk mithilfe der externen virtuellen IP- \( VIP- \) Adresse des Remote Zugriffs Clusters herstellen.  Der Lastenausgleich für den Datenverkehr zum Cluster erfolgt mithilfe von Windows NLB oder mit einem externen Lasten Ausgleichs Modul, \( wie z. b. F5 Big \- IP \) .

## <a name="prerequisites"></a>Voraussetzungen
Bevor Sie mit der Bereitstellung dieses Szenarios beginnen, sollten Sie die Liste der wichtigen Anforderungen lesen:

-   Standardlastenausgleich über Windows NLB.

-   Externer Lastenausgleich wird unterstützt.

-   Der Unicast-Modus ist der standardmäßige und empfohlene Modus für den NLB.

-   Das Ändern von Richtlinien außerhalb der DirectAccess-Verwaltungskonsole oder von PowerShell-Cmdlets wird nicht unterstützt.

-   Wenn NLB oder ein externer Lastenausgleich verwendet wird, kann das IPHTTPS-Präfix nicht in einen anderen Wert als 59 geändert werden \/ .

-   Die Lastenausgleichsknoten müssen sich im gleichen IPv4-Subnetz befinden.

-   Wenn bei ELB-bereit Stellungen Manage out erforderlich ist, können DirectAccess-Clients nicht &nbsp; Teredo verwenden. Nur IPHTTPS können für die End- \- to-End-Kommunikation verwendet werden \- .

-   Stellen Sie sicher, dass alle bekannten NLB- \/ ELB-Hotfixes installiert sind.

-   ISATAP wird im Unternehmensnetzwerk nicht unterstützt. Wenn Sie ISATAP verwenden, sollten Sie es entfernen und das systemeigene IPv6 verwenden.

## <a name="in-this-scenario"></a>Inhalt dieses Szenarios
Das Clusterbereitstellungsszenario umfasst eine Reihe von Schritten:

1.  Stellen Sie [einen Always on-VPN-Server mit erweiterten Optionen](../../vpn/always-on-vpn/deploy/always-on-vpn-adv-options.md)bereit. Bevor eine Cluster Bereitstellung eingerichtet wird, muss ein einzelner Remote Zugriffs Server mit erweiterten Einstellungen bereitgestellt werden.

2.  [Planen Sie die Bereitstellung eines Remote Zugriffs Clusters](plan/Plan-a-Remote-Access-Cluster-Deployment.md). Um einen Cluster aus einer einzelnen Server Bereitstellung zu erstellen, sind einige zusätzliche Schritte erforderlich, einschließlich der Vorbereitung von Zertifikaten für die Cluster Bereitstellung.

3.  [Konfigurieren Sie einen Remote Zugriffs Cluster](configure/Configure-a-Remote-Access-Cluster.md). Dies umfasst eine Reihe von Konfigurationsschritten, einschließlich der Vorbereitung des einzelnen Servers für Windows NLB oder des externen Load Balancers, der Vorbereitung zusätzlicher Server für den Cluster Beitritt und dem Aktivieren des Lasten Ausgleichs.

## <a name="practical-applications"></a><a name="BKMK_APP"></a>Praktische Anwendung
Der Zusammenschluss mehrerer Server zu einem Servercluster bietet Folgendes:

-   Skalierbarkeit: Ein einzelner RAS-Server bietet ein eingeschränktes Maß an Server Zuverlässigkeit und skalierbarer Leistung. Durch die Gruppierung der Ressourcen von zwei oder mehr Servern zu einem einzigen Cluster können Sie die verfügbare Kapazität für die Benutzer und den Durchsatz erhöhen.

-   Hochverfügbarkeit. Ein Cluster bietet Hochverfügbarkeit für Always \- on-Zugriff. Wenn ein Server im Cluster ausfällt, können Remotebenutzer weiterhin über einen anderen Server im Cluster auf das Unternehmensnetzwerk zugreifen. Alle Server im Cluster verfügen über denselben Satz an virtuellen IP- \( Adressen für virtuelle IP- \) Adressen, während gleichzeitig eine eindeutige, dedizierte IP-Adresse für jeden Server beibehalten wird.

-   Einfache \- \- Verwaltung. Ein Cluster ermöglicht die Verwaltung mehrerer Server als einzelne Entität. Gemeinsam genutzte Einstellungen können problemlos clusterserverübergreifend festgelegt werden. Remote Zugriffs Einstellungen können von einem beliebigen Server im Cluster oder Remote mithilfe von Remoteserver-Verwaltungstools RSAT verwaltet werden \( \) . Darüber hinaus kann der ganze Cluster über eine einzelne Remotezugriffs-Verwaltungskonsole überwacht werden.

## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und Features
Die folgende Tabelle enthält die für dieses Szenario erforderlichen Rollen und Features:

|Rollen \/ Funktion|Auf welche Weise dieses Szenario unterstützt wird|
|---------|-----------------|
|Remotezugriffs-Rolle|Diese Rolle wird mithilfe der Server-Manager-Konsole installiert und deinstalliert. Sie umfasst DirectAccess, das zuvor ein Feature in Windows Server 2008 R2 war, sowie RRAS für Routing-und RAS-Dienste \( \) , die zuvor ein Rollen Dienst unter der Server Rolle Netzwerk Richtlinien-und Zugriffs Dienste \( npas war \) . Die Remotezugriffs-Rolle besteht aus zwei Komponenten:<p>-Always on VPN-und Routing-und RAS-Dienste \( RRAS \) -VPN-DirectAccess und VPN werden in der Remote Zugriffs-Verwaltungskonsole verwaltet.<br />-RRAS-Routing: RRAS-Routing Features werden in der Legacy-Routing-und Remote Zugriffs Konsole verwaltet.<p>Es bestehen folgende Abhängigkeiten:<p>-Internetinformationsdienste \( IIS \) -Webserver: dieses Feature ist erforderlich, um den Netzwerkadressen Server und den Standardweb Test zu konfigurieren.<br />-Interne Windows-Datenbank: wird für die lokale Kontoführung auf dem Remote Zugriffs Server verwendet.|
|Feature %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot;|So installieren Sie dieses Feature:<p>-Sie wird standardmäßig auf einem RAS-Server installiert, wenn die Remote Zugriffs Rolle installiert ist, und unterstützt die Benutzeroberfläche der Remote Verwaltungskonsole.<br />-Es kann optional auf einem Server installiert werden, auf dem die Remote Zugriffs-Server Rolle nicht ausgeführt wird. In diesem Fall wird es für die Remoteverwaltung eines RAS-Computers verwendet, der DirectAccess und VPN ausführt.<p>Das Feature "Tools für die Remotezugriffsverwaltung" besteht aus den folgenden Komponenten:<p>-Remote Zugriffs-GUI und Befehlszeilen Tools<br />-Remote Zugriffs Modul für Windows PowerShell<p>Abhängigkeiten umfassen:<p>-Gruppenrichtlinien-Verwaltungskonsole<br />-RAS-Verbindungs-Manager Administration Kit \( CMAK\)<br />-Windows PowerShell 3,0<br />-Tools und Infrastruktur für die grafische Verwaltung|
|Netzwerklastenausgleich|Dieses Feature ermöglicht den Lastenausgleich in einem Cluster mithilfe des Windows-Netzwerklastenausgleichs.|

## <a name="hardware-requirements"></a><a name="BKMK_HARD"></a>Hardwareanforderungen
Für dieses Szenario müssen die folgenden Hardwareanforderungen erfüllt werden:

-   Mindestens zwei Computer, die die Hardwareanforderungen für Windows Server 2012 erfüllen.

-   Für das externe Load Balancer Szenario ist dedizierte Hardware erforderlich, \( d. h. F5 BigIP \) .

-   Um das Szenario zu testen, müssen Sie mindestens einen Computer mit Windows 10 als Always on VPN-Client konfiguriert haben.

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>Softwareanforderungen
Für dieses Szenario gelten eine Reihe von Anforderungen:

-   Softwareanforderungen für die Bereitstellung auf einem Einzelserver. Weitere Informationen finden Sie [unter Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md). Ein einzelner Remote Zugriff).

-   Zusätzlich zu den Softwareanforderungen für einen einzelnen Server gibt es eine Reihe von Cluster \- spezifischen Anforderungen:

    -   Auf jedem Cluster Server muss der IP-HTTPS-Zertifikat Antragsteller \- Name der ConnectTo-Adresse entsprechen. Eine Cluster Bereitstellung unterstützt eine Mischung aus Platzhalter-und nicht-Platzhalter \- Zertifikaten auf Cluster Servern.

    -   Wenn der Netzwerkadressenserver auf dem Remotezugriffsserver installiert ist, muss das Netzwerkadressenserver-Zertifikat auf jedem Clusterserver den gleichen Antragstellernamen aufweisen. Darüber hinaus darf der Name des Netzwerkadressenserver-Zertifikats nicht mit dem Namen eines beliebigen Servers in der DirectAccess-Bereitstellung identisch sein.

    -   IP- \- https-und Netzwerkadressen Server-Zertifikate müssen mit derselben Methode ausgestellt werden, mit der das Zertifikat für den einzelnen Server ausgestellt wurde. Wenn der einzelne Server beispielsweise eine öffentliche Zertifizierungsstellen-Zertifizierungsstelle verwendet, \( \) müssen alle Server im Cluster über ein Zertifikat verfügen, das von einer öffentlichen Zertifizierungsstelle ausgestellt wurde. Wenn der einzelne Server ein selbst \- signiertes Zertifikat für IP HTTPS verwendet, \- müssen alle Server im Cluster entsprechend vorgehen.

    -   Das IPv6-Präfix, das DirectAccess-Clientcomputern in Serverclustern zugewiesen wird, muss 59 Bit umfassen. Wenn VPN aktiviert ist, muss das VPN-Präfix ebenfalls 59 Bit umfassen.

## <a name="known-issues"></a><a name="KnownIssues"></a>Bekannte Probleme
Im Folgenden finden Sie bekannte Probleme beim Konfigurieren eines Clusterszenarios:

-   Nach dem Konfigurieren von DirectAccess in einer reinen IPv4 \- -Bereitstellung mit einem einzelnen Netzwerkadapter und nach dem Standard DNS64 \( die IPv6-Adresse, die ": 3333::" enthält \) , wird automatisch auf dem Netzwerkadapter konfiguriert. bei dem Versuch, \- den Lastenausgleich über die Remote Zugriffs-Verwaltungskonsole zu aktivieren, wird der Benutzer dazu aufgefordert, eine IPv6-DIP-Adresse anzugeben. Wenn eine IPv6-DIP-Adresse angegeben wird, tritt nach dem Klicken auf **Commit ausführen** ein Konfigurationsfehler mit folgender Fehlermeldung auf: Der Parameter ist falsch.

    So lösen Sie das Problem:

    1.  Laden Sie die Sicherung herunter, und stellen Sie Skripts aus [Back up and Restore Remote Access Configuration](https://gallery.technet.microsoft.com/Back-up-and-Restore-Remote-e157e6a6)wieder her.

    2.  Sichern Sie die Remote Zugriffs-Gruppenrichtlinien Objekte mithilfe der heruntergeladenen Skript Sicherung \-RemoteAccess.ps1

    3.  Versuchen Sie, den Lastenausgleich bis zu dem Schritt zu aktivieren, bei dem ein Fehler auftritt. Erweitern Sie im Dialogfeld Lastenausgleich aktivieren den Bereich Details, \- Klicken Sie mit der rechten Maustaste in den Detailbereich, und klicken Sie dann auf **Skript kopieren**.

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

    8.  Wenn das Cmdlet fehlschlägt, während es \( nicht aufgrund falscher Eingabewerte ausgeführt wird \) , führen Sie den Befehl RestoreRemoteAccess.ps1 aus, \- und befolgen Sie die Anweisungen, um sicherzustellen, dass die Integrität der ursprünglichen Konfiguration gewahrt bleibt.

    9. Nun können Sie die Remotezugriffs-Verwaltungskonsole wieder öffnen.
