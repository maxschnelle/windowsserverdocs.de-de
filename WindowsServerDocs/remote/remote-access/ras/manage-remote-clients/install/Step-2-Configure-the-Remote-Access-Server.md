---
title: Schritt 2 Konfigurieren des Remote Zugriffs Servers
description: Dieses Thema ist Teil des Handbuchs zur Remote Verwaltung von DirectAccess-Clients in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0257b98-5633-4264-9df6-b6ffae80592c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0c112898217eb05ad2fd9b387f401ce129b47e54
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822693"
---
# <a name="step-2-configure-the-remote-access-server"></a>Schritt 2 Konfigurieren des Remote Zugriffs Servers

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema wird beschrieben, wie Sie die Client-und Servereinstellungen konfigurieren, die für die Remote Verwaltung von DirectAccess-Clients erforderlich sind. Stellen Sie vor Beginn der Bereitstellungs Schritte sicher, dass Sie die in [Schritt 2 Planen der Remote Zugriffs Bereitstellung](../plan/Step-2-Plan-the-Remote-Access-Deployment.md)beschriebenen Planungsschritte abgeschlossen haben.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|Installieren der Remotezugriffsrolle|Installieren Sie die Remotezugriffsrolle.|  
|Konfigurieren des Bereitstellungstypen|Konfigurieren Sie den Bereitstellungstypen als DirectAccess und VPN, nur DirectAccess, oder nur VPN|  
|Konfigurieren von DirectAccess-Clients|Konfigurieren Sie den Remotezugriffsserver mit den Sicherheitsgruppen, die die DirectAccess-Clients enthalten.|  
|Konfigurieren des RAS-Servers|Konfigurieren Sie die Einstellungen des Remote Zugriffs Servers.|  
|Konfigurieren des Infrastrukturservers|Konfigurieren Sie die Infrastrukturserver, die in der Organisation eingesetzt werden.|  
|Konfigurieren von Anwendungsservern|Konfigurieren Sie die Anwendungsserver so, dass Authentifizierung und Verschlüsselung erforderlich sind.|  
|Zusammenfassung der Konfiguration und alternative Gruppenrichtlinienobjekte|Zeigen Sie die Zusammenfassung der Remotezugriffskonfiguration an und ändern Sie bei Bedarf die Gruppenrichtlinienobjekte.|  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="BKMK_Role"></a>Installieren der Remote Zugriffs Rolle  
Sie müssen die Remote Zugriffs Rolle auf einem Server in Ihrer Organisation installieren, der als Remote Zugriffs Server fungiert.  
  
#### <a name="to-install-the-remote-access-role"></a>So installieren Sie die Remotezugriffsrolle  
  
### <a name="to-install-the-remote-access-role-on-directaccess-servers"></a>So installieren Sie die Remote Zugriffs Rolle auf DirectAccess-Servern  
  
1.  Klicken Sie auf dem DirectAccess-Server in der Server-Manager-Konsole im **Dashboard**auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie dreimal auf **Weiter** , um zur Anzeige für die Serverrollenauswahl zu gelangen.  
  
3.  Wählen Sie im Dialogfeld **Server Rollen auswählen** die Option **Remote Zugriff**aus, und klicken Sie dann auf **weiter**.  
  
4.  Klicken Sie drei Mal auf **weiter** .  
  
5.  Wählen Sie im Dialogfeld **Rollen Dienste auswählen** die Option **DirectAccess und VPN (RAS)** aus, und klicken Sie dann auf **Features hinzufügen**.  
  
6.  Wählen Sie **Routing**, **webanwendungsproxy**aus, klicken Sie auf **Features hinzufügen**und dann auf **weiter**.  
  
7. Klicken Sie auf **Weiter**, und klicken Sie dann auf **Installieren**.  
  
8.  Überprüfen Sie im Dialogfeld **Installationsstatus** , ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.  
  
![der entsprechenden Windows PowerShell-](../../../../media/Step-2-Configure-the-Remote-Access-Server/PowerShellLogoSmall.gif)***<em>Befehle in Windows PowerShell</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Install-WindowsFeature RemoteAccess -IncludeManagementTools  
```  
  
## <a name="BKMK_Deploy"></a>Konfigurieren des Bereitstellungs Typs  
Es gibt drei Optionen, die Sie zum Bereitstellen des Remote Zugriffs über die Remote Zugriffs-Verwaltungskonsole verwenden können:  
  
-   DirectAccess und VPN  
  
-   Nur DirectAccess  
  
-   Nur VPN  
  
> [!NOTE]  
> In diesem Handbuch wird die einzige Methode für die Bereitstellung von DirectAccess in den Beispiel Prozeduren verwendet.  
  
#### <a name="to-configure-the-deployment-type"></a>So konfigurieren Sie den Bereitstellungstypen  
  
1.  Öffnen Sie auf dem Remote Zugriffs Server die Remote Zugriffs-Verwaltungskonsole: Geben Sie auf dem **Start** Bildschirm ein, geben Sie **Remote Zugriffs-Verwaltungskonsole**ein, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole im mittleren Bereich auf **Remotezugriffs-Setup-Assistenten ausführen**.  
  
3.  Wählen Sie im Dialogfeld **Remote Zugriff konfigurieren** die Option DirectAccess und VPN, nur DirectAccess oder nur VPN aus.  
  
## <a name="BKMK_Clients"></a>Konfigurieren von DirectAccess-Clients  
Damit ein Clientcomputer zur Verwendung von DirectAccess bereitgestellt werden kann, muss er zur ausgewählten Sicherheitsgruppe gehören. Nachdem DirectAccess konfiguriert wurde, werden Client Computer in der Sicherheitsgruppe bereitgestellt, um die DirectAccess-Gruppenrichtlinie Objekte (GPOs) für die Remote Verwaltung zu empfangen.  
  
#### <a name="to-configure-directaccess-clients"></a>So konfigurieren Sie DirectAccess-Clients  
  
1.  Klicken Sie im mittleren Bereich der Remotezugriffs-Verwaltungskonsole unter **Schritt 1 Remoteclients** auf **Konfigurieren**.  
  
2.  Klicken Sie im DirectAccess-Client-Setup-Assistenten auf der Seite **Bereitstellungs Szenario** auf **DirectAccess nur für die Remote Verwaltung**bereitstellen, und klicken Sie dann auf **weiter**.  
  
3.  Klicken Sie auf der Seite **Gruppen auswählen** auf **Hinzufügen**.  
  
4.  Wählen Sie im Dialogfeld **Gruppen auswählen** die Sicherheitsgruppen aus, die die DirectAccess-Client Computer enthalten, und klicken Sie dann auf **weiter**.  
  
5.  Vorgehensweise auf der Seite **Netzwerkkonnektivitäts-Assistent**:  
  
    -   Fügen Sie in der Tabelle die Ressourcen hinzu, die verwendet werden, um die Konnektivität zum internen Netzwerk zu ermitteln. Wenn keine weiteren Ressourcen konfiguriert werden, wird automatisch ein Standardwebtest erstellt. Stellen Sie beim Konfigurieren der webtestorte zum Ermitteln der Konnektivität mit dem Unternehmensnetzwerk sicher, dass mindestens ein HTTP-basierter Test konfiguriert ist. Das Konfigurieren eines Ping-Tests ist nicht ausreichend, und es kann zu einer ungenauen Ermittlung des Verbindungsstatus führen. Dies liegt daran, dass Ping von IPsec ausgenommen wird. Daher stellt Ping nicht sicher, dass die IPSec-Tunnel ordnungsgemäß eingerichtet werden.  
  
    -   Fügen Sie eine Helpdesk-E-Mail-Adresse hinzu, damit Benutzer Informationen absenden können, wenn bei ihnen Verbindungsprobleme auftreten.  
  
    -   Geben Sie einen Anzeigenamen für die DirectAccess-Verbindung ein.  
  
    -   Aktivieren Sie bei Bedarf das Kontrollkästchen **DirectAccess-Clients ermöglichen, die lokale Namensauflösung zu verwenden**.  
  
        > [!NOTE]  
        > Wenn die lokale Namensauflösung aktiviert ist, können Benutzer, die die NCA ausführen, Namen mithilfe von DNS-Servern auflösen, die auf dem DirectAccess-Client Computer konfiguriert sind.  
  
6.  Klicken Sie auf **Fertig stellen**.  
  
## <a name="BKMK_Server"></a>Konfigurieren des Remote Zugriffs Servers  
Zum Bereitstellen des Remote Zugriffs müssen Sie den Server, der als RAS-Server fungiert, mit den folgenden Einstellungen konfigurieren:  
  
1.  Korrigieren von Netzwerkadaptern  
  
2.  Eine öffentliche URL für den Remote Zugriffs Server, mit dem Client Computer eine Verbindung herstellen können (die ConnectTo-Adresse)  
  
3.  Ein IP-HTTPS-Zertifikat mit einem Betreff, der mit der ConnectTo-Adresse übereinstimmt.  
  
4.  IPv6-Einstellungen  
  
5.  Client Computer Authentifizierung  
  
#### <a name="to-configure-the-remote-access-server"></a>So konfigurieren Sie den RAS-Server  
  
1.  Klicken Sie im mittleren Bereich der Remotezugriffs-Verwaltungskonsole unter **Schritt 2 RAS-Server** auf **Konfigurieren**.  
  
2.  Klicken Sie im Setup-Assistenten für den Remotezugriffsserver auf der Seite **Netzwerktopologie** auf die Bereitstellungstopologie, die in Ihrer Organisation verwendet wird. Geben Sie unter **Geben Sie den öffentlichen Namen oder die öffentliche IPv4-Adresse an** den öffentlichen Namen für die Bereitstellung ein (dieser Name stimmt mit dem Antragstellernamen des IP-HTTPS-Zertifikats überein, z. B. edge1.contoso.com), und klicken Sie dann auf **Weiter**.  
  
3.  Auf der Seite **Netzwerkadapter** erkennt der Assistent automatisch Folgendes:  
  
    -   Netzwerkadapter für die Netzwerke in der Bereitstellung. Falls der Assistent nicht die korrekten Netzwerkadapter erkennt, wählen Sie die korrekten Adapter manuell aus.  
  
    -   IP-HTTPS-Zertifikat. Dies basiert auf dem öffentlichen Namen für die Bereitstellung, die Sie im vorherigen Schritt des Assistenten festgelegt haben. Wenn der Assistent das korrekte IP-HTTPS-Zertifikat nicht erkennt, klicken Sie auf **Durchsuchen** , um das richtige Zertifikat manuell auszuwählen.  
  
4.  Klicken Sie auf **Weiter**.  
  
5.  Auf der Seite **Präfix Konfiguration** (Diese Seite ist nur sichtbar, wenn IPv6 im internen Netzwerk erkannt wird) werden vom Assistenten automatisch die IPv6-Einstellungen erkannt, die im internen Netzwerk verwendet werden. Wenn für Ihre Bereitstellung zusätzliche Präfixe erforderlich sind, konfigurieren Sie die IPv6-Präfixe für das interne Netzwerk, ein IPv6-Präfix zum Zuweisen für DirectAccess-Clientcomputer und ein IPv6-Präfix zum Zuweisen für VPN-Clientcomputer.  
  
6.  Vorgehensweise auf der Seite **Authentifizierung**:  
  
    -   In Bereitstellungen für mehrere Standorte oder die zweistufige Authentifizierung müssen Sie die Computerzertifikatauthentifizierung verwenden. Aktivieren Sie das Kontrollkästchen **Computer Zertifikate verwenden** , um die Computer Zertifikat Authentifizierung zu verwenden, und wählen Sie das IPSec-Stamm Zertifikat aus.  
  
    -   Damit Client Computer mit Windows 7 über DirectAccess eine Verbindung herstellen können, aktivieren Sie das Kontrollkästchen **Aktivieren von Windows 7-Client Computern zum Herstellen einer Verbindung über DirectAccess** . Für diesen Bereitstellungstypen müssen Sie ebenfalls die Computerzertifikatauthentifizierung verwenden.  
  
7.  Klicken Sie auf **Fertig stellen**.  
  
## <a name="BKMK_Infra"></a>Konfigurieren der Infrastruktur Server  
Um die Infrastruktur Server in einer Remote Zugriffs Bereitstellung zu konfigurieren, müssen Sie Folgendes konfigurieren:  
  
-   Netzwerkadressenserver  
  
-   DNS-Einstellungen, einschließlich der Suchliste für DNS-Suffixe  
  
-   Alle Verwaltungs Server, die nicht automatisch vom Remote Zugriff erkannt werden  
  
#### <a name="to-configure-the-infrastructure-servers"></a>So konfigurieren Sie die Infrastrukturserver  
  
1.  Klicken Sie im mittleren Bereich der Remotezugriffs-Verwaltungskonsole unter **Schritt 3 Infrastrukturserver** auf **Konfigurieren**.  
  
2.  Klicken Sie im Assistenten zum Einrichten des Infrastrukturservers auf der Seite **Netzwerkadressenserver** auf die Option, die dem Speicherort des Netzwerkadressenservers in Ihrer Bereitstellung entspricht.  
  
    -   Wenn sich der Netzwerkadressen Server auf einem Remoteweb Server befindet, geben Sie die URL ein, **und klicken Sie** dann auf überprüfen, bevor Sie fortfahren.  
  
    -   Wenn der Netzwerkadressenserver nicht auf einem Remotewebserver installiert ist, klicken Sie auf **Durchsuchen**, um das entsprechende Zertifikat zu suchen und klicken Sie dann auf **Weiter**.  
  
3.  Geben Sie auf der Seite **DNS** in der Tabelle zusätzliche namens Suffixe ein, die als NRPT-Ausnahmen (Name Resolution Policy Table) angewendet werden. Wählen Sie die entsprechende Option für die lokale Namensauflösung, und klicken Sie dann auf **Weiter**.  
  
4.  Auf der Seite **DNS-Suffixsuchliste** erkennt der Remote Zugriffs Server automatisch Domänen Suffixe in der Bereitstellung. Verwenden Sie die Schaltflächen **Hinzufügen** und **Entfernen** , um die Liste der Domänen Suffixe zu erstellen, die Sie verwenden möchten. Um ein neues Domänensuffix unter **Neues Suffix** hinzuzufügen, müssen Sie dass Suffix eingeben und anschließend auf **Hinzufügen** klicken. Klicken Sie auf **Weiter**.  
  
5.  Fügen Sie auf der Seite **Verwaltung** Verwaltungs Server hinzu, die nicht automatisch erkannt werden, und klicken Sie dann auf **weiter**. Der Remote Zugriff fügt automatisch Domänen Controller und Configuration Manager Server hinzu.  
  
6.  Klicken Sie auf **Fertig stellen**.  
  
## <a name="BKMK_App"></a>Anwendungsserver konfigurieren  
Bei einer vollständigen Remote Zugriffs Bereitstellung ist das Konfigurieren von Anwendungsservern eine optionale Aufgabe. In diesem Szenario für die Remote Verwaltung von DirectAccess-Clients werden Anwendungsserver nicht verwendet, und dieser Schritt ist ausgegraut, um anzugeben, dass er nicht aktiv ist. Klicken Sie auf **Fertig** stellen, um die Konfiguration anzuwenden.  
  
## <a name="BKMK_GPO"></a>Konfigurations Zusammenfassung und Alternative GPOs  
Wenn die Konfiguration des Remotezugriffs abgeschlossen ist, wird das Dialogfeld **Überprüfung des Remotezugriffs** angezeigt. Sie können alle zuvor ausgewählten Einstellungen überprüfen, dazu gehören:  
  
-   **GPO-Einstellungen**  
  
    Der Name des Gruppenrichtlinien Objekts für den DirectAccess-Server und der Name des Gruppenrichtlinien Objekts sind aufgeführt. Sie können auf den Link **ändern** neben der Überschrift **GPO-Einstellungen** klicken, um die GPO-Einstellungen zu ändern.  
  
-   **Remote Clients**  
  
    Die DirectAccess-Client Konfiguration wird angezeigt, einschließlich der Sicherheitsgruppe, der Verbindungs Prüfer und des DirectAccess-Verbindungs namens.  
  
-   **RAS-Server**  
  
    Die DirectAccess-Konfiguration wird angezeigt, einschließlich des öffentlichen Namens und der Adresse, der Netzwerkadapter Konfiguration und der Zertifikat Informationen.  
  
-   **Infrastruktur Server**  
  
    Diese Liste enthält die Netzwerkadressenserver-URL, DNS-Suffixe, die von DirectAcccess-Clients verwendet werden sowie Verwaltungsserverinformationen.  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Schritt 3: Überprüfen der Bereitstellung](Step-3-Verify-the-Deployment_2.md)  
  
  


