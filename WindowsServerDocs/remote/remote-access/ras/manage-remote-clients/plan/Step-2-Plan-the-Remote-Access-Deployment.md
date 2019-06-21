---
title: Schritt 2 Planen der Bereitstellung des Remotezugriffs
description: Dieses Thema ist Teil des Leitfadens verwalten DirectAccess-Clients Remote in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc9f02b9-8ddd-4cae-b397-a832996144dd
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 78303bbdd29819389944348a279fb4a52f1570fb
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282794"
---
# <a name="step-2-plan-the-remote-access-deployment"></a>Schritt 2 Planen der Bereitstellung des Remotezugriffs

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Nachdem Sie die Planung der Infrastruktur, die Sie zum Einrichten Ihrer einzelnen Remotezugriffsservers für die Remoteverwaltung von DirectAccess-Clients verwenden möchten, können Sie die Einstellungen zu planen, die den Remotezugriffs-Setup-Assistenten verwenden.  
  
> [!NOTE]  
> Bevor Sie diese Aufgaben fortsetzen, lesen Sie [Schritt 1: Planen der Remotezugriffinfrastruktur](Step-1-Plan-the-Remote-Access-Infrastructure.md).  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[Planen einer Strategie für die Bereitstellung](#plan-a-client-deployment-strategy)|Legen Sie fest, welche verwalteten Computer als DirectAccess-Clients konfiguriert werden sollen.|  
|[Planen einer Strategie für RAS-Server-Bereitstellung](#plan-a-remote-access-server-deployment-strategy)|Planen Sie die Bereitstellung des Remotezugriffsservers.|  
|[Planen der Infrastrukturserver-Konfigurationen](#plan-the-infrastructure-servers-configurations)|Planen Sie die Infrastrukturserver in der Remotezugriffs-Bereitstellung, einschließlich der DirectAccess-Netzwerkadressenserver, DNS-Server und DirectAccess-Verwaltungsserver.|  
  
## <a name="plan-a-client-deployment-strategy"></a>Planen einer Strategie für die Bereitstellung  
Bei der Planung Ihrer Clientbereitstellung müssen drei Entscheidungen getroffen werden:  
  
1.  Wird DirectAccess für mobile Computer verfügbar ist, oder für alle Computer in einer bestimmten Sicherheitsgruppe sein?  
  
    Wenn Sie DirectAccess-Clients in der DirectAccess-Client-Setup-Assistenten konfigurieren, können Sie auswählen, um nur mobile Computer in angegebenen Sicherheitsgruppen eine Verbindung mit dem Server herstellen, mithilfe von DirectAccess zu ermöglichen. Wenn Sie nur den Zugriff für mobile Computer zulassen, konfiguriert der Remotezugriff automatisch einen WMI-Filter, um sicherzustellen, dass das Gruppenrichtlinienobjekt des DirectAccess-Clients nur auf mobile Computer in den angegebenen Sicherheitsgruppen angewendet wird. Der Remotezugriffsadministrator benötigt Berechtigungen zum Erstellen oder Bearbeiten der WMI-Filter für die Gruppenrichtlinie, um diese Einstellung zu aktivieren.  
  
2.  In welchen Sicherheitsgruppen sollen die DirectAccess-Clientcomputer enthalten sein?  
  
    DirectAccess-Einstellungen sind in der DirectAccess-Client (Group Policy Object, GPO) enthalten. Das Gruppenrichtlinienobjekt wird auf Computer angewendet, die in den Sicherheitsgruppen enthalten sind, die Sie in dem DirectAccess-Client-Setup-Assistenten angegeben haben. Sie können Sicherheitsgruppen angeben, die in einer beliebigen unterstützten Domäne enthalten sind.
  
    Bevor Sie den Remotezugriff konfigurieren, müssen Sie die Sicherheitsgruppen zu erstellen. Sie können die Computer zur Sicherheitsgruppe hinzufügen, nach der Durchführung der Bereitstellung des Remotezugriffs. Wenn Sie über Clientcomputer, die in einer anderen Domäne als der Sicherheitsgruppe befinden hinzufügen, wird jedoch das Client-Gruppenrichtlinienobjekt nicht auf diese Clients angewendet. Beispielsweise wird, wenn Sie in Domäne A für DirectAccess-Clients SG1, und Sie später Clients von Domäne B zu dieser Gruppe hinzufügen, das Client-Gruppenrichtlinienobjekt nicht auf Clients in Domäne b angewendet werden  
  
    Um dieses Problem zu vermeiden, erstellen Sie eine neue Client-Sicherheitsgruppe für jede Domäne, die Clientcomputer enthält. Wenn Sie nicht, um eine neue Sicherheitsgruppe zu erstellen möchten, aber auch das Ausführen der **Add-DAClient** Windows PowerShell-Cmdlet mit dem Namen des neuen Gruppenrichtlinienobjekts für die neue Domäne.  
  
3.  Welche Einstellungen konfigurieren Sie für die DirectAccess Netzwerkkonnektivitäts-Assistent?  
  
    Der DirectAccess Netzwerkkonnektivitäts-Assistent wird auf Clientcomputern ausgeführt und bietet zusätzliche Informationen über die DirectAccess-Verbindung für Endbenutzer bereitzustellen. Im DirectAccess-Client-Setup-Assistenten können Sie Folgendes konfigurieren:  
  
    -   **Verbindungsprüfer**  
  
        Ein Standardwebtest wird erstellt, den Clients verwenden, um die Verbindung zum internen Netzwerk zu prüfen. Der Standardname lautet `https://directaccess-WebProbeHost.<domain_name>`. Der Name sollte manuell im DNS registriert werden. Sie können weitere verbindungsprüfer erstellen, mit denen anderer Webadressen über HTTP oder PING. Für jeden Verbindungsprüfer muss ein DNS-Eintrag vorhanden sein.  
  
    -   **Help Desk-e-Mail-Adresse**  
  
        Wenn Endbenutzer die DirectAccess-Verbindungsprobleme auftreten, können sie eine e-Mail senden mit Diagnoseinformationen an den RAS-Administrator, die das Problem beheben können.  
  
    -   **DirectAccess-Verbindungsnamens**  
  
        Sie können einen DirectAccess-Verbindungsnamens können Endbenutzer die DirectAccess-Verbindung auf ihrem Computer zu identifizieren, angeben.  
  
    -   **Ermöglichen von DirectAccess-Clients, die lokale namensauflösung verwenden**  
  
        Clients benötigen eine Möglichkeit zum Auflösen von Namen lokal. Wenn Sie zulassen, dass DirectAccess-Clients die lokale Namensauflösung verwenden, können Endbenutzer zum Auflösen von Namen lokale DNS-Server verwenden. Wenn Benutzer entscheiden, die lokalen DNS-Server für die namensauflösung zu verwenden, sendet DirectAccess keine Anforderungen zum einteilige Namen auflösen an den internen Unternehmens-DNS-Server. Er verwendet lokale namensauflösung stattdessen (mithilfe der Gruppenrichtlinien-Verwaltungskonsole (Link-Local Multicast Name Resolution, LLMNR) und NetBios über TCP/IP-Protokolle).  
  
## <a name="plan-a-remote-access-server-deployment-strategy"></a>Planen einer Strategie für RAS-Server-Bereitstellung  
Entscheidungen, die Sie vornehmen, wenn Sie beabsichtigen, einen RAS-Server bereitstellen müssen zählen:  
  
-   **Netzwerktopologie**  
  
    Es sind zwei Topologien verfügbar, bei der Bereitstellung von RAS-Server:  
  
    -   **Zwei Adapter**: Mit zwei Netzwerkadaptern: Remotezugriff kann mit einem direkt mit dem Internet verbundenen Netzwerkadapter konfiguriert werden, und der andere mit dem internen Netzwerk verbunden. Oder Sie können auch der Server hinter einem edgegerät, z. B. eine Firewall oder einem Router installiert ist. In dieser Konfiguration eine Netzwerk-Adapter mit dem Umkreisnetzwerk verbunden ist, und der andere mit dem internen Netzwerk verbunden ist.  
  
    -   **Einzelner Netzwerkadapter**: In dieser Konfiguration der Remotezugriff wird der Server hinter einem edgegerät, z. B. eine Firewall oder einem Router installiert. Der Netzwerkadapter ist mit dem internen Netzwerk verbunden.  

-   **Leistungsverlauf für Netzwerkadapter**  
  
    Der RAS-Server-Setup-Assistenten erkennt automatisch die Netzwerkadapter, die auf dem RAS-Server konfiguriert sind. Vergewissern Sie sich, dass die richtigen Adapter ausgewählt sind.  
  
-   **IP-HTTPS-Zertifikat**  
  
    Der Setup-Assistent für den Remotezugriffsserver erkennt automatisch ein Zertifikat, das für die IP-HTTPS-Verbindung geeignet ist. Der Antragstellername von Ihnen gewählten Zertifikats muss mit der ConnectTo-Adresse übereinstimmen. Wenn Sie selbstsignierte Zertifikate verwenden, können Sie ein Zertifikat verwenden, die von RAS-Servers automatisch erstellt wird.  
  
-   **IPv6-Präfixe**  
  
    Wenn der Setup-Assistent für den Remotezugriffsserver erkennt, dass IPv6 auf den Netzwerkadaptern bereitgestellt wurde, füllt er automatisch IPv6-Präfixe für das interne Netzwerk auf. Ein IPv6-Präfix zum Zuweisen für die DirectAccess-Clientcomputer und ein IPv6-Präfix zum Zuweisen für die VPN-Clientcomputer. Wenn die automatisch generierten Präfixe nicht mit Ihrer systemeigenen IPv6- oder ISATAP-Infrastruktur übereinstimmen, müssen Sie sie manuell ändern.  
  
-   **Authentifizierung**  
  
    Sie können eine der folgenden Methoden für die Authentifizierung von DirectAccess-Clients auf dem RAS-Server auswählen:  
  
    -   **Benutzerauthentifizierung**: Sie können für Benutzer die zweistufige oder die Authentifizierung mit Active Directory-Anmeldeinformationen aktivieren.  
  
    -   **Computerauthentifizierung**: Sie können die Computerauthentifizierung zur Verwendung von Zertifikaten konfigurieren. Oder RAS-Server kann als Proxy für Kerberos-Authentifizierung ohne erforderliche Zertifikate. 
  
    -   **Windows 7-Clients** standardmäßig Clientcomputer mit Windows 7 können nicht Herstellen einer Verbindung mit einer remotezugriffsbereitstellung mit dem Windows Server 2012 ausgeführt wird. Wenn Sie Clients, auf denen Windows 7 in Ihrer Organisation, die Remotezugriff für interne Ressourcen benötigen verfügen, können Sie eine Verbindung hergestellt werden. Clientcomputer, die auf interne Ressourcen zugreifen sollen, müssen Mitglied einer Sicherheitsgruppe sein, die Sie im DirectAccess-Client-Setup-Assistenten angeben.  
  
        > [!NOTE]  
        > Ermöglicht Clients, auf denen Windows 7 mithilfe von DirectAccess eine Verbindung herstellen, müssen Sie Computerzertifikatauthentifizierung verwenden.  
  
-   **VPN-Konfiguration**  
  
    Bevor Sie den Remotezugriff konfigurieren, entscheiden Sie, ob Sie beabsichtigen, VPN-Zugriff auf remote-Clients bereitstellen. Sie sollten die VPN-Zugriff bereitstellen, wenn Sie über Clientcomputer in Ihrer Organisation verfügen, die DirectAccess-Konnektivität nicht unterstützen (z. B. sie nicht verwaltet werden, oder führen Sie ein Betriebssystem für die DirectAccess wird nicht unterstützt). Der RAS-Server-Setup-Assistenten können Sie konfigurieren, wie die IP-Adressen (mithilfe von DHCP oder aus einem statischen Adresspool) zugewiesen werden und wie VPN-Clients (mithilfe von Active Directory oder einen RADIUS-Server) authentifiziert werden.  
  
## <a name="plan-the-infrastructure-servers-configurations"></a>Planen der Infrastrukturserver-Konfigurationen  
Remotezugriff sind drei Typen von Infrastrukturservern erforderlich:  
  
-   **Netzwerkadressenserver**  
  
-   **DNS-Server** 
  
-   **Verwaltungsserver** 
  
## <a name="see-also"></a>Siehe auch  
  
-   [Schritt 1: Planen der Infrastruktur für den Remotezugriff](Step-1-Plan-the-Remote-Access-Infrastructure.md)  
  


