---
title: Schritt 2 Konfigurieren der erweiterten DirectAccess-Server
description: Dieses Thema ist Teil des Handbuchs Bereitstellen eines einzelnen DirectAccess-Servers mit erweiterten Einstellungen für Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35afec8e-39a4-463b-839a-3c300ab01174
ms.author: pashort
author: shortpatti
ms.openlocfilehash: adcd13bda942b756a122e9642da795dd9c847bad
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446963"
---
# <a name="step-2-configure-advanced-directaccess-servers"></a>Schritt 2 Konfigurieren der erweiterten DirectAccess-Server

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema wird die Konfiguration der Client- und Servereinstellungen erläutert, die für eine erweiterte Remotezugriffsbereitstellung erforderlich sind, die einen einzelnen Remotezugriffsserver in einer gemischten IPv4- und IPv6-Umgebung verwendet. Bevor Sie die Schritte zur Bereitstellung beginnen, stellen Sie sicher, dass Sie die Planungsschritte, die im Abschnitt abgeschlossen haben [Planen einer erweiterten DirectAccess-Bereitstellung](Plan-an-Advanced-DirectAccess-Deployment.md).  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|2.1. Installieren der Remotezugriffsrolle|Installieren Sie die Remotezugriffsrolle.|  
|2.2. Konfigurieren des Bereitstellungstypen|Konfigurieren Sie den Bereitstellungstypen als DirectAccess und VPN, nur DirectAccess, oder nur VPN|  
|[Planen einer erweiterten DirectAccess-Bereitstellung](Plan-an-Advanced-DirectAccess-Deployment.md)|Konfigurieren Sie den Remotezugriffsserver mit den Sicherheitsgruppen, die die DirectAccess-Clients enthalten.|  
|2.4. Konfigurieren des Remotezugriffsservers|Konfigurieren Sie die Einstellungen des Remotezugriffsservers.|  
|2.5. Konfigurieren des Infrastrukturservers|Konfigurieren Sie die Infrastrukturserver, die in der Organisation eingesetzt werden.|  
|2.6. Konfigurieren von Anwendungsservern|Konfigurieren Sie die Anwendungsserver so, dass für die Anmeldung eine Authentifizierung und Verschlüsselung vorausgesetzt wird.|  
|2.7. Zusammenfassung der Konfiguration und alternative Gruppenrichtlinienobjekte|Zeigen Sie die Zusammenfassung der Remotezugriffskonfiguration an und ändern Sie bei Bedarf die Gruppenrichtlinienobjekte.|  
|2.8. Konfiguration des Remotezugriffsservers mithilfe von Windows PowerShell|Konfigurieren Sie den Remotezugriff mithilfe von Windows PowerShell.|  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="BKMK_Role"></a>2.1. Installieren der Remotezugriffsrolle  
Um den Remotezugriff bereitzustellen, müssen Sie die Remotezugriffsrolle auf einem Server in Ihrer Organisation installieren, der als Remotezugriffsserver fungiert.  
  
#### <a name="to-install-the-remote-access-role"></a>So installieren Sie die Remotezugriffsrolle  
  
1.  Klicken Sie auf dem RAS-Server in der Server-Manager-Konsole in der **Dashboard**, klicken Sie auf **Rollen und Features hinzufügen**.  
  
2.  Klicken Sie dreimal auf **Weiter**, um zum Bildschirm **Serverrollen auswählen** zu gelangen.  
  
3.  Wählen Sie im Dialogfeld **Serverrollen auswählen** die Rolle **Remotezugriff** aus, klicken Sie bei Aufforderung auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.  
  
4.  Klicken Sie fünfmal auf **Weiter**.  
  
5.  Klicken Sie auf der Seite **Installationsauswahl bestätigen** auf **Installieren**.  
  
6.  Überprüfen Sie im Dialogfeld **Installationsstatus**, ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.  
  
![Fortschritt Installationserfolg](../../../media/Step-2-Configuring-DirectAccess-Servers/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Install-WindowsFeature RemoteAccess -IncludeManagementTools  
```  
  
## <a name="BKMK_Deploy"></a>2.2. Konfigurieren des Bereitstellungstypen  
Der Remotezugriff kann mithilfe der Remotezugriffs-Verwaltungskonsole auf drei verschiedene Arten bereitgestellt werden:  
  
-   DirectAccess und VPN  
  
-   Nur DirectAccess  
  
-   Nur VPN  
  
In dieser Anleitung wird in den Beispielverfahren eine Nur-DirectAccess-Bereitstellung verwendet.  
  
#### <a name="to-configure-the-deployment-type"></a>So konfigurieren Sie den Bereitstellungstypen  
  
1.  Öffnen Sie auf einem Remotezugriffsserver die Remotezugriffs-Verwaltungskonsole: Auf der **starten** geben**RAMgmtUI.exe**, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole im mittleren Bereich auf **Remotezugriffs-Setup-Assistenten ausführen**.  
  
3.  Klicken Sie im Dialogfeld **Remotezugriff konfigurieren** die entsprechende Bereitstellungsoption an (DirectAccess und VPN, nur DirectAccess oder nur VPN.  
  
## <a name="BKMK_Clients"></a>2.3. Konfigurieren von DirectAccess-Clients  
Damit ein Clientcomputer zur Verwendung von DirectAccess bereitgestellt werden kann, muss er zur ausgewählten Sicherheitsgruppe gehören. Nachdem DirectAccess konfiguriert wurde, werden Clientcomputer in der Sicherheitsgruppe bereitgestellt, damit sie das DirectAccess-Gruppenrichtlinienobjekt empfangen. Sie können auch das Bereitstellungsszenario konfigurieren, darüber können Sie DirectAccess für den Clientzugriff und die Remoteverwaltung oder nur für die Remoteverwaltung konfigurieren.  
  
#### <a name="to-configure-directaccess-clients"></a>So konfigurieren Sie DirectAccess-Clients  
  
1.  Klicken Sie im mittleren Bereich der Remotezugriffs-Verwaltungskonsole unter **Schritt 1 Remoteclients** auf **Konfigurieren**.  
  
2.  Klicken Sie im DirectAccess-Client-Setup-Assistenten auf der Seite **Bereitstellungsszenario** auf das Bereitstellungsszenario, das Sie in Ihrer Organisation verwenden möchten (**Gesamtes DirectAccess** oder **Nur Remoteverwaltung**) und klicken Sie dann auf **Weiter**.  
  
3.  Klicken Sie auf der Seite **Gruppen auswählen** auf **Hinzufügen**.  
  
4.  Wählen Sie im Dialogfeld **Gruppen auswählen** die Sicherheitsgruppen aus, die Ihre DirectAccess-Clientcomputer enthalten.  
  
    > [!NOTE]  
    > Wenn sich die Sicherheitsgruppe in einer anderen Struktur als der Remotezugriffsserver befindet, klicken Sie im Bereich **Aufgaben**auf **Verwaltungsserver aktualisieren**, nachdem Sie den Remotezugriffs-Setup-Assistenten beendet haben, um die Domänencontroller und System Center Configuration Manager-Server n der neuen Struktur zu finden.  
  
5.  Aktivieren Sie das Kontrollkästchen **DirectAccess ausschließlich für mobile Computer aktivieren**, damit bei Bedarf nur mobile Computer auf das interne Netzwerk zugreifen.  
  
6.  Aktivieren Sie das Kontrollkästchen **Tunnelerzwingung verwenden**, um den gesamten Client-Datenverkehr (an das interne Netzwerk und das Internet) bei Bedarf über den Remotezugriffsserver zu leiten.  
  
7.  Klicken Sie auf **Weiter**.  
  
8.  Vorgehensweise auf der Seite **Netzwerkkonnektivitäts-Assistent**:  
  
    -   Fügen Sie in der Tabelle Ressourcen hinzu, die zum Ermitteln der Konnektivität zum internen Netzwerk verwendet wird. Wenn keine weiteren Ressourcen konfiguriert werden, wird automatisch ein Standardwebtest erstellt.  
  
        > [!CAUTION]  
        > Wenn Sie die Webtestspeicherorte zum Ermitteln der Konnektivität zum Unternehmensnetzwerk konfigurieren, müssen Sie sich vergewissern, dass mindestens ein HTTP-basierter Test konfiguriert ist. Es reicht nicht aus, nur einen **ping**-Test zu konfigurieren. Diese Vorgehensweise kann zu einer ungenauen Ermittlung des Verbindungsstatus führen. Das liegt daran begründet, dass **ping** aus IPsec ausgeschlossen wird, folglich sorgt er nicht dafür, dass die IPsec-Tunnel ordnungsgemäß eingerichtet werden.  
  
    -   Fügen Sie eine Helpdesk-E-Mail-Adresse hinzu, damit Benutzer Informationen absenden können, wenn bei ihnen Verbindungsprobleme auftreten.  
  
    -   Geben Sie einen Anzeigenamen für die DirectAccess-Verbindung ein. Dieser Name wird in der Netzwerkliste angezeigt, wenn der Benutzer auf das Netzwerksymbol im Infobereich klickt.  
  
    -   Aktivieren Sie bei Bedarf das Kontrollkästchen **DirectAccess-Clients ermöglichen, die lokale Namensauflösung zu verwenden**.  
  
        > [!NOTE]  
        > Wenn die lokale Namensauflösung aktiviert ist, können Benutzer, bei denen den Netzwerkkonnektivitäts-Assistent ausgeführt wird, auswählen, Namen mithilfe von DNS-Servern aufzulösen, die auf dem DirectAccess-Clientcomputer konfiguriert sind.  
  
9. Klicken Sie auf **Fertig stellen**.  
  
## <a name="BKMK_Server"></a>2.4. Konfigurieren des Remotezugriffsservers  
Um den Remotezugriff bereitzustellen, müssen Sie den Remotezugriffsserver mit korrekten Netzwerkadaptern, einer öffentlichen URL für den Remotezugriffsserver, zu dem Clientcomputer eine Verbindung aufbauen können (die ConnectTo-Adresse), einem IP-HTTPS-Zertifikat mit einem Antragsteller, der mit der ConnectTo-Adresse übereinstimmt, IPv6-Einstellungen und Clientcomputer-Authentifizierung konfigurieren.  
  
#### <a name="to-configure-the-remote-access-server"></a>So konfigurieren Sie den Remotezugriffsserver  
  
1.  Klicken Sie im mittleren Bereich der Remotezugriffs-Verwaltungskonsole unter **Schritt 2 RAS-Server** auf **Konfigurieren**.  
  
2.  Klicken Sie im Setup-Assistenten für den Remotezugriffsserver auf der Seite **Netzwerktopologie** auf die Bereitstellungstopologie, die in Ihrer Organisation verwendet wird. Geben Sie unter **Geben Sie den öffentlichen Namen oder die öffentliche IPv4-Adresse an** den öffentlichen Namen für die Bereitstellung ein (dieser Name stimmt mit dem Antragstellernamen des IP-HTTPS-Zertifikats überein, z. B. edge1.contoso.com), und klicken Sie dann auf **Weiter**.  
  
3.  Auf der Seite **Netzwerkadapter** erkennt der Assistent automatisch die Netzwerkadapter für die Netzwerke in Ihrer Bereitstellung. Falls der Assistent nicht die korrekten Netzwerkadapter erkennt, wählen Sie die korrekten Adapter manuell aus. Der Assistent erkennt außerdem automatisch das IP-HTTPS-Zertifikat, das auf dem öffentlichen Namen für die Bereitstellung basiert und im vorherigen Schritt des Assistenten festgelegt wurde. Wenn der Assistent das korrekte IP-HTTPS-Zertifikat nicht erkennt, klicken Sie auf **Durchsuchen**, um das korrekte Zertifikat manuell auszuwählen und klicken Sie dann auf **Weiter**.  
  
4.  Auf der Seite **Präfixkonfiguration** wird nur bei IPv6-Bereitstellung im internen Netzwerk angezeigt) erkennt der Assistent automatisch die IPv6-Einstellungen, die im internen Netzwerk eingesetzt werden. Wenn für Ihre Bereitstellung zusätzliche Präfixe erforderlich sind, konfigurieren Sie die IPv6-Präfixe für das interne Netzwerk, ein IPv6-Präfix zum Zuweisen für DirectAccess-Clientcomputer und ein IPv6-Präfix zum Zuweisen für VPN-Clientcomputer.  
  
    > [!NOTE]  
    > Sie können mehrere interne IPv6-Präfixe angeben, indem Sie eine durch Semikolon getrennte Liste verwenden, z. B. 2001:db8:1::/48;2001:db8:2::/48.  
  
5.  Vorgehensweise auf der Seite **Authentifizierung**:  
  
    -   Klicken Sie unter **Benutzerauthentifizierung** auf **Active Directory-Anmeldeinformationen**. Um eine Bereitstellung mit der zweistufigen Authentifizierung zu konfigurieren, klicken Sie auf **Zweistufige Authentifizierung**. Weitere Informationen finden Sie unter [Bereitstellen des Remotezugriffs mit OTP-Authentifizierung](https://technet.microsoft.com/library/hh831379.aspx).  
  
    -   In Bereitstellungen für mehrere Standorte oder die zweistufige Authentifizierung müssen Sie die Computerzertifikatauthentifizierung verwenden. Aktivieren Sie das Kontrollkästchen **Computerzertifikate verwenden**, um die Computerzertifikatauthentifizierung zu verwenden und das IPsec-Stammzertifikat auszuwählen.  
  
    -   Um Windows 7-Clientcomputer über DirectAccess eine Verbindung zu aktivieren, wählen die **Aktivieren von Windows 7-Clientcomputer Verbindungen über DirectAccess zulassen** Kontrollkästchen.  
  
        > [!NOTE]  
        > Für diesen Bereitstellungstypen müssen Sie ebenfalls die Computerzertifikatauthentifizierung verwenden.  
  
6.  Klicken Sie auf **Fertig stellen**.  
  
## <a name="BKMK_Infra"></a>2.5. Konfigurieren des Infrastrukturservers  
Um die Infrastrukturserver in einer Remotezugriffsbereitstellung zu konfigurieren, müssen Sie den Netzwerkadressenserver, die DNS-Einstellungen (einschließlich DNS-Suffixsuchliste) und die Verwaltungsserver konfigurieren, die nicht automatisch vom Remotezugriff erkannt werden.  
  
#### <a name="to-configure-the-infrastructure-servers"></a>So konfigurieren Sie die Infrastrukturserver  
  
1.  Klicken Sie im mittleren Bereich der Remotezugriffs-Verwaltungskonsole unter **Schritt 3 Infrastrukturserver** auf **Konfigurieren**.  
  
2.  Klicken Sie im Assistenten zum Einrichten des Infrastrukturservers auf der Seite **Netzwerkadressenserver** auf die Option, die dem Speicherort des Netzwerkadressenservers in Ihrer Bereitstellung entspricht. Wenn der Netzwerkadressenserver auf einem Remotewebserver installiert ist, geben Sie die URL ein und klicken Sie dann auf **Überprüfen**, bevor Sie fortfahren. Wenn der Netzwerkadressenserver nicht auf einem Remotewebserver installiert ist, klicken Sie auf **Durchsuchen**, um das entsprechende Zertifikat zu suchen und klicken Sie dann auf **Weiter**.  
  
3.  Geben Sie auf der Seite **DNS** in der Tabelle alle zusätzlichen Namenssuffixe ein, die als NRPT-Ausnahmen (Name Resolution Policy Table, Richtlinientabelle für die Namensauflösung) angewendet werden. Wählen Sie die entsprechende Option für die lokale Namensauflösung, und klicken Sie dann auf **Weiter**.  
  
4.  Auf der Seite **DNS-Suffixsuchliste** erkennt der Remotezugriffsserver die Domänensuffixe in der Bereitstellung automatisch. Verwenden Sie die Schaltflächen **Hinzufügen** und **Entfernen**, um Domänensuffixe aus der Liste der zu verwendenden Domänensuffixe zu entfernen oder ihr hinzuzufügen. Um ein neues Domänensuffix unter **Neues Suffix** hinzuzufügen, müssen Sie dass Suffix eingeben und anschließend auf **Hinzufügen** klicken. Klicken Sie auf **Weiter**.  
  
5.  Fügen Sie auf der Seite **Verwaltung** die Verwaltungsserver hinzu, die nicht automatisch erkannt wurden und klicken Sie dann auf **Weiter**. Der Remotezugriff fügt die Domänencontroller und System Center Configuration Manager-Server automatisch hinzu.  
  
    > [!NOTE]  
    > Obwohl der Server automatisch hinzugefügt werden, nicht in der Liste angezeigt. Nachdem Sie die Konfiguration erstmalig anwenden, werden die System Center Configuration Manager-Server in der Liste angezeigt.  
  
6.  Klicken Sie auf **Fertig stellen**.  
  
## <a name="BKMK_App"></a>2.6. Konfigurieren von Anwendungsservern  
Bei einer Remotezugriffsbereitstellung ist das Konfigurieren von Anwendungsservern eine optionale Aufgabe. Mit dem Remotezugriff können Sie für ausgewählte Anwendungsserver eine Authentifizierung voraussetzen, die durch die Aufnahme in eine Sicherheitsgruppe der Anwendungsserver bestimmt wird. Standardmäßig wird der Datenverkehr an die Anwendungsserver, die eine Authentifizierung voraussetzen, ebenfalls verschlüsselt; sie können jedoch auswählen, den Datenverkehr an Anwendungsserver nicht zu verschlüsseln und nur die Authentifizierung verwenden.  
  
> [!NOTE]  
> Authentifizierung ohne Verschlüsselung wird nur auf Anwendungsservern, die unter Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 unterstützt.  
  
#### <a name="to-configure-application-servers"></a>So konfigurieren Sie die Anwendungsserver  
  
1.  Klicken Sie im mittleren Bereich der Remotezugriffs-Verwaltungskonsole unter **Schritt 4 Anwendungsserver** auf **Konfigurieren**.  
  
2.  Klicken Sie im DirectAccess-Anwendungsserver-Setup-Assistent auf **Authentifizierung auf ausgewählte Anwendungsserver erweitern**, um die Authentifizierung von ausgewählten Anwendungsservern vorauszusetzen. Klicken Sie auf **Hinzufügen**, um die Sicherheitsgruppe des Anwendungsservers auszuwählen.  
  
3.  Um den Zugriff nur auf Server in der Sicherheitsgruppe des Anwendungsservers zu beschränken, müssen Sie das Kontrollkästchen **Zugriff nur für Server in den Sicherheitsgruppen zulassen** aktivieren.  
  
4.  Wählen Sie zum Verwenden der Authentifizierung ohne Verschlüsselung der **Datenverkehr nicht verschlüsseln. Nur Authentifizierung verwenden** Kontrollkästchen.  
  
5.  Klicken Sie auf **Fertig stellen**.  
  
## <a name="BKMK_GPO"></a>2.7. Zusammenfassung der Konfiguration und alternative Gruppenrichtlinienobjekte  
Wenn die Konfiguration des Remotezugriffs abgeschlossen ist, wird das Dialogfeld **Überprüfung des Remotezugriffs** angezeigt. Sie können alle zuvor ausgewählten Einstellungen überprüfen, dazu gehören:  
  
1.  **GPO-Einstellungen**: Hier werden der Gruppenrichtlinienname des DirectAccess-Servers und der Client-Gruppenrichtlinienobjektname aufgelistet. Außerdem können Sie auf die Verknüpfung **Ändern** neben der Überschrift **GPO-Einstellungen** klicken, um die GPO-Einstellungen zu ändern.  
  
2.  **Remoteclients**: Hier wird die DirectAccess-Clientkonfiguration angezeigt, einschließlich der Sicherheitsgruppe, des Status der Tunnelerzwingung, der Verbindungsprüfer und des DirectAccess-Verbindungsnamens.  
  
3.  **Remotezugriffsserver**: Hier wird die DirectAccess-Konfiguration angezeigt, einschließlich des öffentlichen Namens/Adresse, der Netzwerkadapterkonfiguration, der Zertifikatinformationen und der OTP-Informationen, falls konfiguriert.  
  
4.  **Infrastrukturserver**: Diese Liste enthält die Netzwerkadressenserver-URL, DNS-Suffixe, die von DirectAcccess-Clients verwendet werden sowie Verwaltungsserverinformationen.  
  
5.  **Anwendungsserver**: Hier wird zusätzlich zum Status der End-to-End-Authentifizierung bestimmter Anwendungsserver der DirectAccess-Remoteverwaltungsstatus angezeigt.  
  
## <a name="BKMK_PS"></a>2.8. Konfiguration des Remotezugriffsservers mithilfe von Windows PowerShell  
![Windows PowerShell](../../../media/Step-2-Configuring-DirectAccess-Servers/PowerShellLogoSmall.gif)**gleichwertige Windows PowerShell-Befehle**  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
So führen Sie eine vollständige Installation des Remotezugriffs nur für DirectAccess mit dem Stamm **corp.contoso.com** und folgenden Parametern durch: Server-Gruppenrichtlinienobjekt: **DirectAccess Server Settings**, Client-Gruppenrichtlinienobjekt: DirectAccess-Clienteinstellungen, interner Netzwerkadapter: **Corpnet**, externer Netzwerkadapter: **Internet**, ConnectTo-Adresse: **edge1.contoso.com**, und der Netzwerkadressenserver: **nls.corp.contoso.com**:  
  
```  
Install-RemoteAccess -Force -PassThru -ServerGpoName 'corp.contoso.com\DirectAccess Server Settings' -ClientGpoName 'corp.contoso.com\DirectAccess Client Settings' -DAInstallType 'FullInstall' -InternetInterface 'Internet' -InternalInterface 'Corpnet' -ConnectToAddress 'edge1.contoso.com' -NlsUrl 'https://nls.corp.contoso.com/'  
```  
  
So konfigurieren Sie den Remotezugriffsserver so, dass er die Computerzertifikatauthentifizierung verwendet, mit einem IPsec-Stammzertifikat, das von der Zertifizierungsstelle mit der Bezeichnung CORP-APP1-CA ausgestellt wird:  
  
```  
$certs = Get-ChildItem Cert:\LocalMachine\Root  
$IPsecRootCert = $certs | Where-Object {$_.Subject -Match "corp-APP1-CA"}  
Set-DAServer -IPsecRootCertificate $IPsecRootCert  
```  
  
So fügen Sie die Sicherheitsgruppe hinzu, die die DirectAccess-Clients mit der Bezeichnung **DirectAccessClients** enthält, und entfernen die Standard-Domänencomputer-Sicherheitsgruppe:  
  
```  
Add-DAClient -SecurityGroupNameList @('corp.contoso.com\DirectAccessClients')  
Remove-DAClient -SecurityGroupNameList @('corp.contoso.com\Domain Computers')  
```  
  
Zum Aktivieren des Remotezugriffs für alle Computer (nicht nur Notebooks und Laptops) und Remote-Zugriff für Windows 7-Clients zu aktivieren:  
  
```  
Set-DAClient -OnlyRemoteComputers 'Disabled' -Downlevel 'Enabled'  
```  
  
So konfigurieren Sie die DirectAccess-Clienterfahrung, einschließlich des Anzeigenamens der Verbindung und der Webtest-URL:  
  
```  
Set-DAClientExperienceConfiguration -FriendlyName 'Contoso DirectAccess Connection' -PreferLocalNamesAllowed $False -PolicyStore 'corp.contoso.com\DirectAccess Client Settings' -CorporateResources @('HTTP:https://directaccess-WebProbeHost.corp.contoso.com')  
```  
  
## <a name="BKMK_Links"></a>Vorherigen Schritt  
  
-   [Schritt 1: Konfigurieren der erweiterten DirectAccess-Infrastruktur](da-adv-configure-s1-infrastructure.md)  
  
## <a name="next-step"></a>Nächster Schritt  
  
-   [Schritt 3: Überprüfen der Bereitstellung](Step-3-Verify-the-Deployment.md)  
  


