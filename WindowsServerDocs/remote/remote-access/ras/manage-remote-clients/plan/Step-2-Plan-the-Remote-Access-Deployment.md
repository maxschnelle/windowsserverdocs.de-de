---
title: Schritt 2 Planen der Bereitstellung des Remote Zugriffs
description: Dieses Thema ist Teil des Handbuchs zur Remote Verwaltung von DirectAccess-Clients in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: cc9f02b9-8ddd-4cae-b397-a832996144dd
ms.author: lizross
author: eross-msft
ms.openlocfilehash: befd517f8e00548524dc9bf9c328d63034c653be
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860573"
---
# <a name="step-2-plan-the-remote-access-deployment"></a>Schritt 2 Planen der Bereitstellung des Remote Zugriffs

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Nachdem Sie die Infrastruktur geplant haben, die Sie zum Einrichten des einzelnen RAS-Servers für die Remote Verwaltung von DirectAccess-Clients verwenden möchten, können Sie die Einstellungen planen, die vom Setup-Assistenten für den Remote Zugriff verwendet werden.  
  
> [!NOTE]  
> Bevor Sie mit diesen Aufgaben fortfahren, finden Sie weitere Informationen unter [Schritt 1: Planen der Infrastruktur für den Remote Zugriff](Step-1-Plan-the-Remote-Access-Infrastructure.md).  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|[Planen einer Strategie für die Client Bereitstellung](#plan-a-client-deployment-strategy)|Legen Sie fest, welche verwalteten Computer als DirectAccess-Clients konfiguriert werden sollen.|  
|[Planen einer Bereitstellungs Strategie für den Remote Zugriffs Server](#plan-a-remote-access-server-deployment-strategy)|Planen Sie die Bereitstellung des Remotezugriffsservers.|  
|[Planen der Konfigurationen der Infrastruktur Server](#plan-the-infrastructure-servers-configurations)|Planen Sie die Infrastruktur Server in der Remote Zugriffs Bereitstellung, einschließlich DirectAccess-Netzwerkadressen Server, DNS-Server und DirectAccess-Verwaltungs Server.|  
  
## <a name="plan-a-client-deployment-strategy"></a>Planen einer Strategie für die Client Bereitstellung  
Bei der Planung Ihrer Clientbereitstellung müssen drei Entscheidungen getroffen werden:  
  
1.  Ist DirectAccess nur für mobile Computer oder für alle Computer in einer angegebenen Sicherheitsgruppe verfügbar?  
  
    Wenn Sie DirectAccess-Clients im DirectAccess-Client-Setup-Assistenten konfigurieren, können Sie festlegen, dass nur Mobile Computer in angegebenen Sicherheitsgruppen mithilfe von DirectAccess eine Verbindung mit dem Server herstellen können. Wenn Sie nur den Zugriff für mobile Computer zulassen, konfiguriert der Remotezugriff automatisch einen WMI-Filter, um sicherzustellen, dass das Gruppenrichtlinienobjekt des DirectAccess-Clients nur auf mobile Computer in den angegebenen Sicherheitsgruppen angewendet wird. Der Remotezugriffsadministrator benötigt Berechtigungen zum Erstellen oder Bearbeiten der WMI-Filter für die Gruppenrichtlinie, um diese Einstellung zu aktivieren.  
  
2.  In welchen Sicherheitsgruppen sollen die DirectAccess-Clientcomputer enthalten sein?  
  
    DirectAccess-Einstellungen sind im DirectAccess-Client Gruppenrichtlinie-Objekt (GPO) enthalten. Das Gruppenrichtlinienobjekt wird auf Computer angewendet, die in den Sicherheitsgruppen enthalten sind, die Sie in dem DirectAccess-Client-Setup-Assistenten angegeben haben. Sie können Sicherheitsgruppen angeben, die in einer beliebigen unterstützten Domäne enthalten sind.
  
    Bevor Sie den Remote Zugriff konfigurieren, müssen Sie die Sicherheitsgruppen erstellen. Nachdem Sie die Remote Zugriffs Bereitstellung fertiggestellt haben, können Sie der Sicherheitsgruppe Computer hinzufügen. Wenn Sie jedoch Client Computer hinzufügen, die sich in einer anderen Domäne als der Sicherheitsgruppe befinden, wird das Client-Gruppenrichtlinien Objekt nicht auf diese Clients angewendet. Wenn Sie z. B. SG1 in Domäne A für DirectAccess-Clients erstellt haben und später Clients von Domäne b zu dieser Gruppe hinzufügen, wird das Client-Gruppenrichtlinien Objekt nicht auf Clients in Domäne b angewendet.  
  
    Um dieses Problem zu vermeiden, erstellen Sie eine neue Client Sicherheitsgruppe für jede Domäne, die Client Computer enthält. Wenn Sie keine neue Sicherheitsgruppe erstellen möchten, führen Sie alternativ das Windows PowerShell-Cmdlet **Add-daclient** mit dem Namen des neuen Gruppenrichtlinien Objekts für die neue Domäne aus.  
  
3.  Welche Einstellungen werden für den DirectAccess-netzwerkkonnektivitätsassistant konfiguriert?  
  
    Der DirectAccess-netzwerkkonnektivitätsassistent wird auf Client Computern ausgeführt und stellt zusätzliche Informationen über die DirectAccess-Verbindung mit Endbenutzern bereit. Im DirectAccess-Client-Setup-Assistenten können Sie Folgendes konfigurieren:  
  
    -   **Konnektivitätsverifier**  
  
        Ein Standardwebtest wird erstellt, den Clients verwenden, um die Verbindung zum internen Netzwerk zu prüfen. Der Standardname lautet `https://directaccess-WebProbeHost.<domain_name>`. Der Name sollte manuell im DNS registriert werden. Sie können andere konnektivitätsprobleer erstellen, die andere Webadressen über HTTP oder Ping verwenden. Für jeden Verbindungsprüfer muss ein DNS-Eintrag vorhanden sein.  
  
    -   **Helpdesk-e-Mail-Adresse**  
  
        Wenn bei Endbenutzern DirectAccess-Konnektivitätsprobleme auftreten, können Sie eine e-Mail mit Diagnoseinformationen an den Remote Zugriffs Administrator senden, die das Problem beheben können.  
  
    -   **DirectAccess-Verbindungs Name**  
  
        Sie können einen DirectAccess-Verbindungs Namen angeben, um Endbenutzern zu helfen, die DirectAccess-Verbindung auf Ihrem Computer zu identifizieren.  
  
    -   **DirectAccess-Clients die Verwendung der lokalen Namensauflösung gestatten**  
  
        Clients benötigen eine Möglichkeit zum lokalen Auflösen von Namen. Wenn Sie zulassen, dass DirectAccess-Clients die lokale Namensauflösung verwenden, können Endbenutzer zum Auflösen von Namen lokale DNS-Server verwenden. Wenn Endbenutzer lokale DNS-Server für die Namensauflösung verwenden möchten, sendet DirectAccess keine Auflösungsanforderungen für einzelne Bezeichnungs Namen an den internen DNS-Server des Unternehmens. Stattdessen wird die lokale Namensauflösung verwendet (mit der Link-Local-Multicast-Namensauflösung (LLMNR) und NetBIOS über TCP/IP-Protokollen).  
  
## <a name="plan-a-remote-access-server-deployment-strategy"></a>Planen einer Bereitstellungs Strategie für den Remote Zugriffs Server  
Bei der Planung der Bereitstellung des Remote Zugriffs Servers müssen folgende Entscheidungen getroffen werden:  
  
-   **Netzwerktopologie**  
  
    Beim Bereitstellen eines Remote Zugriffs Servers sind zwei Topologien verfügbar:  
  
    -   **Zwei Adapter**: mit zwei Netzwerkadaptern kann der Remote Zugriff mit einem Netzwerkadapter konfiguriert werden, der direkt mit dem Internet verbunden ist, und mit dem anderen, der mit dem internen Netzwerk verbunden ist. Alternativ dazu wird der Server hinter einem Edgegerät installiert, z. b. einer Firewall oder einem Router. In dieser Konfiguration ist ein Netzwerkadapter mit dem Umkreis Netzwerk und der andere mit dem internen Netzwerk verbunden.  
  
    -   **Einzelner Netzwerkadapter**: in dieser Konfiguration wird der RAS-Server hinter einem Edgegerät installiert, z. b. einer Firewall oder einem Router. Der Netzwerkadapter ist mit dem internen Netzwerk verbunden.  

-   **Leistungsverlauf für Netzwerkadapter**  
  
    Der Setup-Assistent für den Remote Zugriffs Server erkennt automatisch die Netzwerkadapter, die auf dem Remote Zugriffs Server konfiguriert sind. Vergewissern Sie sich, dass die richtigen Adapter ausgewählt sind.  
  
-   **IP-HTTPS-Zertifikat**  
  
    Der Setup-Assistent für den Remotezugriffsserver erkennt automatisch ein Zertifikat, das für die IP-HTTPS-Verbindung geeignet ist. Der Antragstellername von Ihnen gewählten Zertifikats muss mit der ConnectTo-Adresse übereinstimmen. Wenn Sie selbst signierte Zertifikate verwenden, können Sie ein Zertifikat verwenden, das automatisch vom Remote Zugriffs Server erstellt wird.  
  
-   **IPv6-Präfixe**  
  
    Wenn der Setup-Assistent für den Remotezugriffsserver erkennt, dass IPv6 auf den Netzwerkadaptern bereitgestellt wurde, füllt er automatisch IPv6-Präfixe für das interne Netzwerk auf. Ein IPv6-Präfix zum Zuweisen für die DirectAccess-Clientcomputer und ein IPv6-Präfix zum Zuweisen für die VPN-Clientcomputer. Wenn die automatisch generierten Präfixe nicht mit Ihrer systemeigenen IPv6- oder ISATAP-Infrastruktur übereinstimmen, müssen Sie sie manuell ändern.  
  
-   **Authentifizierung**  
  
    Sie können eine der folgenden Methoden zum Authentifizieren von DirectAccess-Clients auf dem RAS-Server auswählen:  
  
    -   **Benutzerauthentifizierung**: Sie können es Benutzern ermöglichen, sich mit Active Directory Anmelde Informationen oder mit zweistufiger Authentifizierung zu authentifizieren.  
  
    -   **Computer Authentifizierung**: Sie können die Computer Authentifizierung für die Verwendung von Zertifikaten konfigurieren. Oder der Remote Zugriffs Server kann als Proxy für die Kerberos-Authentifizierung fungieren, ohne dass Zertifikate erforderlich sind. 
  
    -   **Windows 7-Clients** Standardmäßig können Client Computer, auf denen Windows 7 ausgeführt wird, keine Verbindung mit einer Remote Zugriffs Bereitstellung unter Windows Server 2012 herstellen. Wenn Sie über Clients verfügen, auf denen Windows 7 in Ihrer Organisation ausgeführt wird und die den Remote Zugriff auf interne Ressourcen benötigen, können Sie Ihnen gestatten, eine Verbindung herzustellen. Clientcomputer, die auf interne Ressourcen zugreifen sollen, müssen Mitglied einer Sicherheitsgruppe sein, die Sie im DirectAccess-Client-Setup-Assistenten angeben.  
  
        > [!NOTE]  
        > Wenn Sie es Clients mit Windows 7 gestatten, eine Verbindung mithilfe von DirectAccess herzustellen, müssen Sie die Computer Zertifikat Authentifizierung verwenden.  
  
-   **VPN-Konfiguration**  
  
    Bevor Sie den Remote Zugriff konfigurieren, entscheiden Sie, ob Sie VPN-Zugriff auf Remote Clients bereitstellen möchten. Sie sollten VPN-Zugriff bereitstellen, wenn Sie in Ihrer Organisation über Client Computer verfügen, die keine DirectAccess-Konnektivität unterstützen (z. b. Wenn Sie nicht verwaltet werden oder wenn ein Betriebssystem ausgeführt wird, für das DirectAccess nicht unterstützt wird). Mithilfe des Setup-Assistenten für den Remote Zugriffs Server können Sie konfigurieren, wie IP-Adressen zugewiesen werden (mithilfe von DHCP oder aus einem statischen Adresspool) und wie VPN-Clients authentifiziert werden (mithilfe von Active Directory oder einem RADIUS-Server).  
  
## <a name="plan-the-infrastructure-servers-configurations"></a>Planen der Konfigurationen der Infrastruktur Server  
Der Remote Zugriff erfordert drei Arten von Infrastruktur Servern:  
  
-   **Netzwerkadressen Server**  
  
-   **DNS-Server** 
  
-   **Verwaltungs Server** 
  
## <a name="see-also"></a>Siehe auch  
  
-   [Schritt 1: Planen der Infrastruktur für den Remote Zugriff](Step-1-Plan-the-Remote-Access-Infrastructure.md)  
  


