---
title: Schritt 3 Konfigurieren der Bereitstellung für mehrere Standorte
description: Dieses Thema ist Teil des Handbuchs Bereitstellen mehrerer Remote Zugriffs Server in einer Bereitstellung mit mehreren Standorten in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ea7ecd52-4c12-4a49-92fd-b8c08cec42a9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ccfde5d13b9b2b722498e824d497a9b790875e14
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404505"
---
# <a name="step-3-configure-the-multisite-deployment"></a>Schritt 3 Konfigurieren der Bereitstellung für mehrere Standorte

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Führen Sie nach dem Konfigurieren der Infrastruktur für mehrere Standorte die folgenden Schritte aus, um die Bereitstellung des Remote Zugriffs für mehrere Standorte einzurichten.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|3.1. Konfigurieren von Remote Zugriffs Servern|Konfigurieren Sie zusätzliche Remote Zugriffs Server, indem Sie IP-Adressen einrichten, Sie der Domäne hinzufügen und die Remote Zugriffs Rolle installieren.|  
|3.2. Gewähren des Administrator Zugriffs|Erteilen Sie dem DirectAccess-Administrator Berechtigungen für die zusätzlichen Remote Zugriffs Server.|  
|3.3. Konfigurieren von IP-HTTPS für eine Bereitstellung mit mehreren Standorten|Konfigurieren des IP-HTTPS-Zertifikats, das in einer Bereitstellung für mehrere Standorte verwendet wird.|  
|3.4. Konfigurieren des Netzwerkadressen Servers für eine Bereitstellung mit mehreren Standorten|Konfigurieren des Netzwerkadressen Server-Zertifikats, das bei einer Bereitstellung mit mehreren Standorten verwendet wird|  
|3.5. Konfigurieren von DirectAccess-Clients für eine Bereitstellung mit mehreren Standorten|Entfernen Sie Windows 7-Client Computer aus Windows 8-Sicherheitsgruppen.|  
|3.6. Aktivieren der Bereitstellung für mehrere Standorte|Aktivieren Sie die Bereitstellung für mehrere Standorte auf dem ersten Remote Zugriffs Server.|  
|3,7. Hinzufügen von Einstiegspunkten zur Bereitstellung für mehrere Standorte|Fügen Sie der Bereitstellung für mehrere Standorte zusätzliche Einstiegspunkte hinzu.|  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="BKMK_ConfigServer"></a>3,1. Konfigurieren von Remote Zugriffs Servern  

  
### <a name="to-install-the-remote-access-role"></a>So installieren Sie die Remotezugriffsrolle  
  
1.  Stellen Sie sicher, dass jeder RAS-Server mit der richtigen Bereitstellungs Topologie (Edge, hinter einer NAT, einer einzelnen Netzwerkschnittstelle) und entsprechenden Routen konfiguriert ist.  
  
2.  Konfigurieren Sie die IP-Adressen auf jedem RAS-Server entsprechend der Standort Topologie und dem IP-Adressierungs Schema Ihrer Organisation.  
  
3.  Verknüpfen Sie jeden RAS-Server mit einer Active Directory Domäne.  
  
4.  Klicken Sie in der Server-Manager-Konsole im **Dashboard**auf **Rollen und Features hinzufügen**.  
  
5.   Klicken Sie dreimal auf **Weiter** , um zur Anzeige für die Serverrollenauswahl zu gelangen.  
  
6.  Wählen Sie im Dialogfeld **Server Rollen auswählen** die Option **Remote Zugriff**aus, und klicken Sie dann auf **weiter**.  
  
7.  Klicken Sie drei Mal auf **weiter** .  
  
8.  Wählen Sie im Dialogfeld **Rollen Dienste auswählen** die Option **DirectAccess und VPN (RAS)** aus, und klicken Sie dann auf **Features hinzufügen**.  
  
9.  Wählen Sie **Routing**, **webanwendungsproxy**aus, klicken Sie auf **Features hinzufügen**und dann auf **weiter**.  
  
10. Klicken Sie auf **Weiter**, und klicken Sie dann auf **Installieren**.  
  
11.  Überprüfen Sie im Dialogfeld **Installationsstatus**, ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.  
  
  
](../../../../media/Step-3-Configure-the-Multisite-Deployment/PowerShellLogoSmall.gif)***<em>äquivalente Windows PowerShell-Befehle</em> mit @no__t 0shell***  

  
Die Schritte 1-3 müssen manuell ausgeführt werden und werden nicht mithilfe dieses Windows PowerShell-Cmdlets ausgeführt.  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Install-WindowsFeature RemoteAccess -IncludeManagementTools  
```  
  
## <a name="BKMK_Admin"></a>3,2. Gewähren des Administrator Zugriffs  
  
#### <a name="to-grant-administrator-permissions"></a>So erteilen Sie Administrator Berechtigungen  
  
1.  Auf dem Remote Zugriffs Server im zusätzlichen Einstiegspunkt: Geben Sie auf dem **Start** Bildschirm **Computer Verwaltung**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie im linken Bereich auf **lokale Benutzer und Gruppen**.  
  
3.  Doppelklicken Sie auf **Gruppen**, und doppelklicken Sie dann auf **Administratoren**.  
  
4.  Klicken Sie im Dialogfeld **Administrator Eigenschaften** auf **Hinzufügen**, und klicken Sie im Dialogfeld **Benutzer, Computer, Dienst Konten oder Gruppen auswählen** auf Speicher **Orte**.  
  
5.  Klicken Sie im Dialogfeld Speicher **Orte** in der Struktur **Speicherort** auf den Speicherort, der das Benutzerkonto des DirectAccess-Administrators enthält, und klicken Sie dann auf **OK**.  
  
6.  Geben Sie unter **Geben Sie die zu ausgewäfenden Objektnamen**ein den Benutzernamen des DirectAccess-Administrators ein, und klicken Sie dann zweimal auf **OK** .  
  
7.  Klicken Sie im Dialogfeld **Administrator Eigenschaften** auf **OK**.  
  
8.  Schließen Sie das Fenster Computer Verwaltung.  
  
9. Wiederholen Sie diesen Vorgang auf allen RAS-Servern, die Teil der Bereitstellung für mehrere Standorte sein werden.  
  
## <a name="BKMK_IPHTTPS"></a>3,3. Konfigurieren von IP-HTTPS für eine Bereitstellung mit mehreren Standorten  
Auf jedem Remote Zugriffs Server, der der Bereitstellung für mehrere Standorte hinzugefügt wird, ist ein SSL-Zertifikat erforderlich, um die HTTPS-Verbindung mit dem IP-HTTPS-Webserver zu überprüfen. Grundvoraussetzung zur Ausführung dieses Vorgangs ist die Mitgliedschaft in der lokalen Gruppe **Administratoren** oder eine gleichwertige Mitgliedschaft.  
  
#### <a name="to-obtain-an-ip-https-certificate"></a>So erhalten Sie ein IP-HTTPS-Zertifikat  
  
1.  Auf jedem Remote Zugriffs Server: Geben Sie auf dem **Start** Bildschirm **MMC**ein, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie im Menü **Datei** auf **Snap-Ins hinzufügen bzw. entfernen**.  
  
3.  Klicken Sie auf **Zertifikate**, **Hinzufügen**, **Computerkonto** und **Weiter**. Wählen Sie **Lokaler Computer** aus, klicken Sie auf **Fertig stellen** und anschließend auf **OK**.  
  
4.  Öffnen Sie in der Konsolenstruktur des Zertifikat-Snap-Ins den Eintrag **Zertifikate (Lokaler Computer)\Persönlich\Zertifikate**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, zeigen Sie auf **Alle Aufgaben**, und klicken Sie dann auf **Neues Zertifikat anfordern**.  
  
6.  Klicken Sie zweimal auf **Weiter** .  
  
7.  Klicken Sie auf der Seite **Zertifikate anfordern** auf die Vorlage Webserver Zertifikat, und klicken Sie dann auf **Weitere Informationen sind erforderlich, um sich für dieses Zertifikat zu registrieren**.  
  
    Wenn die Vorlage für das Webserver Zertifikat nicht angezeigt wird, stellen Sie sicher, dass das Remote Zugriffs Server-Computer Konto über die Berechtigung "registrieren" für die Webserver-Zertifikat Vorlage verfügt. Weitere Informationen finden Sie unter [Konfigurieren von Berechtigungen für die Webserver-Zertifikat Vorlage](https://technet.microsoft.com/library/ee649249(v=ws.10).aspx).  
  
8.  Wählen Sie im Dialogfeld **Zertifikat Eigenschaften** **auf der Register** Karte Antragsteller unter Antragsteller **Name**für **Typ**die Option allgemeiner **Name**aus.  
  
9. Geben Sie unter **Wert**den voll qualifizierten Domänen Namen (FQDN) des Internet namens des Remote Zugriffs Servers (z. b. Europe.contoso.com) ein, und klicken Sie dann auf **Hinzufügen**.  
  
10. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
11. Überprüfen Sie im Detailbereich des Zertifikat-Snap-Ins, dass ein neues Zertifikat mit dem vollqualifizierten Domänennamen unter **Serverauthentifizierung** mit der Option **Beabsichtigte Zwecke** registriert wurde.  
  
12. Klicken Sie mit der rechten Maustaste auf das Zertifikat, und klicken Sie anschließend auf **Eigenschaften**.  
  
13. Geben Sie unter **Anzeigename** die Zeichenfolge **IP-HTTPS-Zertifikat** ein, und klicken Sie dann auf **OK**.  
  
    > [!TIP]  
    > Die Schritte 12 und 13 sind optional, erleichtern Ihnen jedoch die Auswahl des Zertifikats für IP-HTTPS beim Konfigurieren des Remote Zugriffs.  
  
14. Wiederholen Sie diesen Vorgang auf allen RAS-Servern in Ihrer Bereitstellung.  
  
## <a name="BKMK_NLS"></a>3,4. Konfigurieren des Netzwerkadressen Servers für eine Bereitstellung mit mehreren Standorten  
Wenn Sie beim Einrichten des ersten Servers die Netzwerkadressen Server-Website auf dem RAS-Server eingerichtet haben, muss jeder neue RAS-Server, den Sie hinzufügen, mit einem Webserver Zertifikat konfiguriert werden, das den gleichen Antragsteller Namen hat, den Sie für t ausgewählt haben. Er ist der Netzwerkadressen Server für den ersten Server. Jeder Server benötigt ein Zertifikat, um die Verbindung mit dem Netzwerkadressen Server zu authentifizieren, und Client Computer im internen Netzwerk müssen in der Lage sein, den Namen der Website in DNS aufzulösen.  
  
#### <a name="to-install-a-certificate-for-network-location"></a>So installieren Sie ein Zertifikat für den Netzwerk Speicherort  
  
1.  Gehen Sie auf dem Remotezugriffsserver wie folgt vor: Geben Sie auf dem **Start** Bildschirm **MMC**ein, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie im Menü **Datei** auf **Snap-Ins hinzufügen bzw. entfernen**.  
  
3.  Klicken Sie auf **Zertifikate**, **Hinzufügen**, **Computerkonto** und **Weiter**. Wählen Sie **Lokaler Computer** aus, klicken Sie auf **Fertig stellen** und anschließend auf **OK**.  
  
4.  Öffnen Sie in der Konsolenstruktur des Zertifikat-Snap-Ins den Eintrag **Zertifikate (Lokaler Computer)\Persönlich\Zertifikate**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, zeigen Sie auf **Alle Aufgaben**, und klicken Sie dann auf **Neues Zertifikat anfordern**.  
  
    > [!NOTE]  
    > Sie können auch das Zertifikat importieren, das für den Netzwerkadressen Server für den ersten RAS-Server verwendet wurde.  
  
6.  Klicken Sie zweimal auf **Weiter** .  
  
7.  Klicken Sie auf der Seite **Zertifikate anfordern** auf die Vorlage Webserver Zertifikat, und klicken Sie dann auf **Weitere Informationen sind erforderlich, um sich für dieses Zertifikat zu registrieren**.  
  
    Wenn die Vorlage für das Webserver Zertifikat nicht angezeigt wird, stellen Sie sicher, dass das Remote Zugriffs Server-Computer Konto über die Berechtigung "registrieren" für die Webserver-Zertifikat Vorlage verfügt. Weitere Informationen finden Sie unter [Konfigurieren von Berechtigungen für die Webserver-Zertifikat Vorlage](https://technet.microsoft.com/library/ee649249(v=ws.10).aspx).  
  
8.  Wählen Sie im Dialogfeld **Zertifikat Eigenschaften** **auf der Register** Karte Antragsteller unter Antragsteller **Name**für **Typ**die Option allgemeiner **Name**aus.  
  
9. Geben Sie unter **Wert**den voll qualifizierten Domänen Namen (FQDN) ein, der für das Netzwerkadressen Server-Zertifikat des ersten Remote Zugriffs Servers (z. b. nls.Corp.contoso.com) konfiguriert wurde, und klicken Sie dann auf **Hinzufügen**.  
  
10. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
11. Überprüfen Sie im Detailbereich des Zertifikat-Snap-Ins, dass ein neues Zertifikat mit dem vollqualifizierten Domänennamen unter **Serverauthentifizierung** mit der Option **Beabsichtigte Zwecke** registriert wurde.  
  
12. Klicken Sie mit der rechten Maustaste auf das Zertifikat, und klicken Sie anschließend auf **Eigenschaften**.  
  
13. Geben Sie unter **Anzeigenamen** den Namen **Netzwerkadressenzertifikat** ein, und klicken Sie dann auf **OK**.  
  
    > [!TIP]  
    > Die Schritte 12 und 13 sind optional, erleichtern es Ihnen jedoch, das Zertifikat für den Netzwerk Speicherort beim Konfigurieren des Remote Zugriffs auszuwählen.  
  
14. Wiederholen Sie diesen Vorgang auf allen RAS-Servern in Ihrer Bereitstellung.  
  
### <a name="NLS"></a>So erstellen Sie DNS-Einträge für den Netzwerkadressen Server  
  
1.  Auf dem DNS-Server: Geben Sie auf der **Start** Seite **dnsmgmt. msc**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Öffnen Sie im linken Bereich der **DNS-Manager** -Konsole die Forward-Lookupzone für das interne Netzwerk. Klicken Sie mit der rechten Maustaste auf die relevante Zone, und klicken Sie auf **neuer Host (A oder AAAA)**  
  
3.  Geben Sie im Dialogfeld **neuer Host** in das Feld **Name (verwendet übergeordneter Domänen Name wenn leer)** den Namen ein, der für den Netzwerkadressen Server für den ersten RAS-Server verwendet wurde. Geben Sie im Feld **IP-Adresse** die IPv4-Adresse des Remote Zugriffs Servers ein, und klicken Sie dann auf **Host hinzufügen**. Klicken Sie im Dialogfeld **DNS** auf **OK**.  
  
4.  Geben Sie im Dialogfeld **neuer Host** in das Feld **Name (verwendet übergeordneter Domänen Name wenn leer)** den Namen ein, der für den Netzwerkadressen Server für den ersten RAS-Server verwendet wurde. Geben Sie im Feld **IP-Adresse** die IPv6-Adresse des Remote Zugriffs Servers ein, und klicken Sie dann auf **Host hinzufügen**. Klicken Sie im Dialogfeld **DNS** auf **OK**.  
  
5.  Wiederholen Sie die Schritte 3 und 4 für jeden RAS-Server in der Bereitstellung.  
  
6.  Klicken Sie auf **Fertig**.  
  
7.  Wiederholen Sie dieses Verfahren, bevor Sie Server als zusätzliche Einstiegspunkte in der Bereitstellung hinzufügen.  
  
## <a name="BKMK_Client"></a>3,5. Konfigurieren von DirectAccess-Clients für eine Bereitstellung mit mehreren Standorten  
DirectAccess-Windows-Client Computer müssen Mitglieder der Sicherheitsgruppe (n) sein, die ihre DirectAccess-Zuordnung definieren. Vor der Aktivierung mehrerer Standorte können diese Sicherheitsgruppen sowohl Windows 8-Clients als auch Windows 7-Clients enthalten (sofern der entsprechende Modus "Downlevel" ausgewählt wurde). Wenn die Funktion für mehrere Standorte aktiviert ist, werden vorhandene Client Sicherheitsgruppen im Einzel Server Modus nur für Windows 8 in die Sicherheitsgruppe (n) konvertiert. Nachdem Multisite aktiviert ist, müssen DirectAccess-Windows 7-Client Computer in die entsprechenden dedizierten Windows 7-Client Sicherheitsgruppen (die bestimmten Einstiegspunkten zugeordnet sind) verschoben werden, oder Sie können keine Verbindung über DirectAccess herstellen. Die Windows 7-Clients müssen zunächst aus den vorhandenen Sicherheitsgruppen entfernt werden, die jetzt Windows 8-Sicherheitsgruppen sind. Vorsicht:  Windows 7-Client Computer, die Mitglieder von Windows 7-und Windows 8-Client Sicherheitsgruppen sind, verlieren die Remote Konnektivität, und Windows 7-Clients ohne installiertes SP1 verlieren auch die Unternehmens Konnektivität. Daher müssen alle Windows 7-Client Computer aus Windows 8-Sicherheitsgruppen entfernt werden.  
  
#### <a name="remove--windows-7--clients-from-windows-8-security-groups"></a>Entfernen von Windows 7-Clients aus Windows 8-Sicherheitsgruppen  
  
1.  Klicken Sie auf dem primären Domänen Controller auf **Start**, und klicken Sie dann auf **Active Directory Benutzer und Computer**.  
  
2.  Wenn Sie Computer aus der Sicherheitsgruppe entfernen möchten, doppelklicken Sie auf die Sicherheitsgruppe, und klicken Sie im Dialogfeld **Eigenschaften von < Gruppenname >** auf die Registerkarte **Mitglieder** .  
  
3.  Wählen Sie den Windows 7-Client Computer aus, und klicken Sie auf **Entfernen**.  
  
4.  Wiederholen Sie dieses Verfahren, um die Windows 7-Client Computer aus den Windows 8-Sicherheitsgruppen zu entfernen.  
  
> [!IMPORTANT]  
> Wenn Sie eine Remote Zugriffs Konfiguration für mehrere Standorte aktivieren, verlieren alle Client Computer (Windows 7 und Windows 8) Remote Verbindungen, bis Sie direkt oder per VPN eine Verbindung mit dem Unternehmensnetzwerk herstellen können, um Ihre Gruppenrichtlinien zu aktualisieren. Dies trifft zu, wenn Sie die Funktionalität für mehrere Standorte zum ersten Mal aktivieren, und auch wenn Sie mehrere Websites deaktivieren.  
  
## <a name="BKMK_Enable"></a>3,6. Aktivieren der Bereitstellung für mehrere Standorte  
Um eine Bereitstellung für mehrere Standorte zu konfigurieren, aktivieren Sie die Funktion für mehrere Standorte auf dem vorhandenen Remote Zugriffs Server. Stellen Sie sicher, dass Sie über die folgenden Informationen verfügen, bevor Sie mehrere Standorte in der Bereitstellung aktivieren:  
  
1.  Globale Load Balancer-Einstellungen und IP-Adressen, wenn Sie einen Lastenausgleich für DirectAccess-Clientverbindungen über alle Einstiegspunkte in der Bereitstellung ausführen möchten.  
  
2.  Die Sicherheitsgruppen, die Windows 7-Client Computer für den ersten Einstiegspunkt in der Bereitstellung enthalten, wenn Sie den Remote Zugriff für Windows 7-Client Computer aktivieren möchten.  
  
3.  Gruppenrichtlinie Objektnamen, wenn Sie nicht standardmäßige Gruppenrichtlinie Objekte verwenden müssen, die auf Windows 7-Client Computern für den ersten Einstiegspunkt in der Bereitstellung angewendet werden, wenn Sie Unterstützung für Windows 7-Client Computer benötigen.  
  
### <a name="EnabledMultisite"></a>So aktivieren Sie eine Konfiguration für mehrere Standorte  
  
1.  Auf dem vorhandenen Remote Zugriffs Server: Geben Sie auf dem **Start** Bildschirm **ramgmtui. exe**ein, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remote Zugriffs-Verwaltungskonsole auf **Konfiguration**, und klicken Sie dann im Bereich **Tasks** auf **Multisite aktivieren**.  
  
3.  Klicken Sie im Assistenten zum **Aktivieren der Bereitstellung für mehrere Standorte** auf der Seite **Vorbemerkungen** auf **weiter**.  
  
4.  Geben Sie auf der Seite **Bereitstellungs Name** unter Name der Bereitstellung für **mehrere Standorte**einen Namen für die Bereitstellung ein. Geben Sie unter **Name des ersten Einstiegs Punkts**einen Namen ein, um den ersten Einstiegspunkt zu identifizieren, der der aktuelle RAS-Server ist, und klicken Sie dann auf **weiter**.  
  
5.  Führen Sie auf der Seite **Einstiegspunkt Auswahl** einen der folgenden Schritte aus:  
  
    -   Klicken Sie auf **Einstiegspunkte automatisch zuweisen, und lassen Sie Clients die Option manuell auswählen** , um Client Computer automatisch an den am besten geeigneten Einstiegspunkt weiterzuleiten, während gleichzeitig Client Computer einen Einstiegspunkt manuell auswählen können. Die Auswahl für den manuellen Einstiegspunkt ist nur für Windows 8-Computer verfügbar. Klicken Sie auf **Weiter**.  
  
    -   Klicken Sie auf **Einstiegspunkte automatisch zuweisen** , um Client Computer automatisch an den am besten geeigneten Einstiegspunkt weiterzuleiten, und klicken Sie dann auf **weiter**.  
  
6.  Führen Sie auf der Seite **Globaler Lastenausgleich** einen der folgenden Schritte aus:  
  
    -   Klicken Sie auf **Nein, verwenden Sie keinen globalen Lastenausgleich** , wenn Sie keinen globalen Lastenausgleich verwenden möchten, und klicken Sie dann auf **weiter**.  
  
        > [!NOTE]  
        > Wenn Sie diese Option auswählen, wird automatisch eine Verbindung mit dem nächstgelegenen Einstiegspunkt hergestellt.  
  
    -   Klicken Sie auf **Ja, globalen Lastenausgleich verwenden,** Wenn Sie den Datenverkehr Global zwischen allen Einstiegspunkten gleichmäßig verteilen möchten. Geben Sie unter Geben Sie den **globalen Lastenausgleich-FQDN ein, der von allen Einstiegspunkten verwendet werden soll**, den globalen Lastenausgleich-FQDN ein, und geben Sie in **Geben Sie die globale Lasten Ausgleichs-IP-Adresse für diesen Einstiegspunkt ein** , der den ersten RAS-Server enthält. Lasten Ausgleichs-IP-Adresse für diesen Einstiegspunkt, und klicken Sie dann auf **weiter**.  
  
7.  Führen Sie auf der Seite **Client Unterstützung** einen der folgenden Schritte aus:  
  
    -   Um den Zugriff auf Client Computer unter Windows 8 oder höher einzuschränken, klicken Sie auf **Zugriff auf Client Computer mit Windows 8 oder höher beschränken**, und klicken Sie dann auf **weiter**.  
  
    -   Damit Client Computer mit Windows 7 auf diesen Einstiegspunkt zugreifen können, klicken Sie auf **Client Computern, auf denen Windows 7 ausgeführt wird, auf diesen Einstiegspunkt zugreifen**, und klicken Sie auf **Hinzufügen**. Wählen Sie im Dialogfeld **Gruppen auswählen** die Sicherheitsgruppen aus, die die Windows 7-Client Computer enthalten, klicken Sie auf **OK**, und klicken Sie dann auf **weiter**.  
  
8.  Akzeptieren Sie auf der Seite Client-Gruppenrichtlinien Objekt- **Einstellungen** das Standard-Gruppenrichtlinien Objekt für Windows 7-Client Computer für diesen Einstiegspunkt, geben Sie den Namen des Gruppenrichtlinien Objekts ein, das automatisch erstellt werden soll, oder klicken Sie auf **Durchsuchen** , um das Gruppenrichtlinien Objekt für Windows 7-Client Computer zu suchen. und klicken Sie dann auf **weiter**.  
  
    > [!NOTE]  
    > -   Die Seite Einstellungen für das **Client** -Gruppenrichtlinien Objekt wird nur angezeigt, wenn Sie den Einstiegspunkt so konfigurieren, dass Windows 7-Client Computer auf den Einstiegspunkt zugreifen können.  
    > -   Optional können Sie auf **GPOs** überprüfen klicken, um sicherzustellen, dass Sie über die entsprechenden Berechtigungen für das ausgewählte Gruppenrichtlinien Objekt oder GPOs für diesen Einstiegspunkt verfügen. Wenn das GPO nicht vorhanden ist und automatisch erstellt wird, sind Create-und Link-Berechtigungen erforderlich. Wenn die Gruppenrichtlinien Objekte manuell erstellt wurden, sind die Berechtigungen bearbeiten, Sicherheit ändern und Löschen erforderlich.  
  
9. Klicken Sie auf der Seite **Zusammenfassung** auf **Commit**.  
  
10. Klicken Sie im Dialogfeld **Bereitstellung für mehrere Standorte** aktivieren auf **Schließen** , und klicken Sie dann im Assistenten zum Aktivieren der Bereitstellung für mehrere Standorte auf **Schließen**.  
  
](../../../../media/Step-3-Configure-the-Multisite-Deployment/PowerShellLogoSmall.gif)***<em>äquivalente Windows PowerShell-Befehle</em> mit @no__t 0shell***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
So aktivieren Sie eine Bereitstellung mit mehreren Standorten mit dem Namen "Configuration Manager" auf dem ersten Einstiegspunkt mit dem Namen "EDGE1-US". Mithilfe der Bereitstellung können Clients den Einstiegspunkt manuell auswählen und keinen globalen Lastenausgleich verwenden.  
  
```  
Enable-DAMultiSite -Name 'Contoso' -EntryPointName 'Edge1-US' -ManualEntryPointSelectionAllowed 'Enabled'  
```  
  
, Um Windows 7-Client Computern den Zugriff über den ersten Einstiegspunkt über die Sicherheitsgruppe DA_Clients_US und die Verwendung des Gruppenrichtlinien Objekts DA_W7_Clients_GPO_US zuzulassen.  
  
```  
Add-DAClient -EntrypointName 'Edge1-US' -DownlevelSecurityGroupNameList @('corp.contoso.com\DA_Clients_US') -DownlevelGpoName @('corp.contoso.com\DA_W7_Clients_GPO_US)  
```  
  
## <a name="BKMK_EntryPoint"></a>3,7. Hinzufügen von Einstiegspunkten zur Bereitstellung für mehrere Standorte  
Nachdem Sie mehrere Standorte in der Bereitstellung aktiviert haben, können Sie mithilfe des Assistenten zum Hinzufügen eines Einstiegs Punkts weitere Einstiegspunkte hinzufügen. Stellen Sie vor dem Hinzufügen von Einstiegspunkten sicher, dass Sie über die folgenden Informationen verfügen:  
  
-   Globale Load Balancer-IP-Adressen für jeden neuen Einstiegspunkt, wenn Sie einen globalen Lastenausgleich verwenden.  
  
-   Die Sicherheitsgruppen, die Windows 7-Client Computer für jeden Einstiegspunkt enthalten, der hinzugefügt wird, wenn Sie den Remote Zugriff für Windows 7-Client Computer aktivieren möchten.  
  
-   Gruppenrichtlinie Objektnamen, wenn Sie nicht standardmäßige Gruppenrichtlinie Objekte verwenden müssen, die für jeden hinzu zufügenden Einstiegspunkt auf Windows 7-Client Computern angewendet werden, wenn Sie Unterstützung für Windows 7-Client Computer benötigen.  
  
-   Wenn IPv6 im Netzwerk der Organisation bereitgestellt wird, müssen Sie das IP-HTTPS-Präfix für den neuen Einstiegspunkt vorbereiten.  
  
### <a name="AddEP"></a>So fügen Sie Ihrer Bereitstellung für mehrere Standorte Einstiegspunkte hinzu  
  
1.  Auf dem vorhandenen Remote Zugriffs Server: Geben Sie auf dem **Start** Bildschirm **ramgmtui. exe**ein, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie in der Remote Zugriffs-Verwaltungskonsole auf **Konfiguration**, und klicken Sie dann im Bereich **Tasks** auf **Einstiegspunkt hinzufügen**.  
  
3.  Geben Sie im Assistenten zum Hinzufügen von Einstiegspunkten auf der Seite **Einstiegspunkt Details** unter RAS- **Server**den voll qualifizierten Domänen Namen (FQDN) des hinzu zufügenden Servers ein. Geben Sie unter **Einstiegspunkt Name**den Namen des Einstiegs Punkts ein, und klicken Sie dann auf **weiter**.  
  
4.  Geben Sie auf der Seite **globale Einstellungen für den Lastenausgleich** die globale IP-Adresse für den Lastenausgleich dieses Einstiegs Punkts ein, und klicken Sie dann auf **weiter**.  
  
    > [!NOTE]  
    > Die Seite **globale Einstellungen für den Lastenausgleich** wird nur angezeigt, wenn die Konfiguration für mehrere Standorte einen globalen Load Balancer verwendet.  
  
5.  Klicken Sie auf der Seite **Netzwerktopologie** auf die Topologie, die der Netzwerktopologie des RAS-Servers entspricht, den Sie hinzufügen, und klicken Sie dann auf **weiter**.  
  
6.  Geben Sie auf der Seite **Netzwerkname oder IP-Adresse** in **Geben Sie den öffentlichen Namen oder die IP-Adresse ein, die von Clients zum Herstellen einer Verbindung mit dem RAS-Server verwendet**wird. Der öffentliche Name entspricht dem Antragsteller Namen des IP-HTTPS-Zertifikats. Bei der Implementierung der edgenetzwerktopologie ist die IP-Adresse die Adresse des externen Adapters des RAS-Servers. Klicken Sie auf **Weiter**.  
  
7.  Führen Sie auf der Seite **Netzwerkadapter** einen der folgenden Schritte aus:  
  
    -   Wenn Sie eine Topologie mit zwei Netzwerkadaptern bereitstellen, wählen Sie in **externer Adapter**den Adapter aus, der mit dem externen Netzwerk verbunden ist. Wählen Sie unter **interner Adapter**den Adapter aus, der mit dem internen Netzwerk verbunden ist.  
  
    -   Wenn Sie eine Topologie mit einem Netzwerkadapter bereitstellen, wählen Sie unter **Netzwerkadapter**den Adapter aus, der mit dem internen Netzwerk verbunden ist.  
  
8.  Klicken Sie auf der Seite **Netzwerkadapter** unter **Wählen Sie das Zertifikat zum Authentifizieren von IP-HTTPS-Verbindungen auswählen**auf **Durchsuchen** , um das IP-HTTPS-Zertifikat zu suchen und auszuwählen. Klicken Sie auf **Weiter**.  
  
9. Wenn IPv6 im Unternehmensnetzwerk konfiguriert ist, geben Sie auf der Seite **Präfix Konfiguration** unter **IPv6-Präfix, das Client Computern zugewiesen**ist ein IP-HTTPS-Präfix ein, um den DirectAccess-Client Computern IPv6-Adressen zuzuweisen, und klicken Sie auf **weiter**.  
  
10. Führen Sie auf der Seite **Client Unterstützung** einen der folgenden Schritte aus:  
  
    -   Um den Zugriff auf Client Computer unter Windows 8 oder höher einzuschränken, klicken Sie auf **Zugriff auf Client Computer mit Windows 8 oder höher beschränken**, und klicken Sie dann auf **weiter**.  
  
    -   Damit Client Computer mit Windows 7 auf diesen Einstiegspunkt zugreifen können, klicken Sie auf **Client Computern, auf denen Windows 7 ausgeführt wird, auf diesen Einstiegspunkt zugreifen**, und klicken Sie auf **Hinzufügen**. Wählen Sie im Dialogfeld **Gruppen auswählen** die Sicherheitsgruppen aus, die die Windows 7-Client Computer enthalten, von denen eine Verbindung mit diesem Einstiegspunkt hergestellt werden soll, klicken Sie auf **OK**, und klicken Sie **dann auf weiter**.  
  
11. Akzeptieren Sie auf der Seite **Client-GPO-Einstellungen** das Standard-Gruppenrichtlinien Objekt für Windows 7-Client Computer für diesen Einstiegspunkt, geben Sie den Namen des Gruppenrichtlinien Objekts ein, das Sie automatisch erstellen möchten, oder klicken Sie auf **Durchsuchen** , um das Gruppenrichtlinien Objekt für Windows 7-Client Computer zu suchen. , und klicken Sie auf **weiter**.  
  
    > [!NOTE]  
    > -   Die Seite Einstellungen für das **Client** -Gruppenrichtlinien Objekt wird nur angezeigt, wenn Sie den Einstiegspunkt so konfigurieren, dass Windows 7-Client Computer auf den Einstiegspunkt zugreifen können.  
    > -   Optional können Sie auf **GPOs** überprüfen klicken, um sicherzustellen, dass Sie über die entsprechenden Berechtigungen für das ausgewählte Gruppenrichtlinien Objekt oder GPOs für diesen Einstiegspunkt verfügen. Wenn das GPO nicht vorhanden ist und automatisch erstellt wird, sind Create-und Link-Berechtigungen erforderlich. Wenn die Gruppenrichtlinien Objekte manuell erstellt wurden, sind die Berechtigungen bearbeiten, Sicherheit ändern und Löschen erforderlich.  
  
12. Akzeptieren Sie auf der Seite **Server-GPO-Einstellungen** das Standard-Gruppenrichtlinien Objekt für diesen RAS-Server, geben Sie den Namen des GPO ein, das Sie automatisch erstellen möchten, oder klicken Sie auf **Durchsuchen** , um das Gruppenrichtlinien Objekt für diesen Server zu suchen, und klicken Sie dann auf **weiter**.  
  
13. Klicken Sie auf der Seite **Netzwerkadressen Server** auf **Durchsuchen** , um das Zertifikat für die Netzwerkadressen Server-Website auszuwählen, die auf dem Remote Zugriffs Server ausgeführt wird, und klicken Sie dann auf **weiter**.  
  
    > [!NOTE]  
    > Die Seite **Netzwerkadressen Server** wird nur angezeigt, wenn die Netzwerkadressen Server-Website auf dem Remote Zugriffs Server ausgeführt wird.  
  
14. Überprüfen Sie auf der Seite **Zusammenfassung** die Einstellungen für den Einstiegspunkt, und klicken Sie dann auf **Commit**.  
  
15. Klicken Sie im Dialogfeld **Einstiegspunkt hinzufügen** auf **Schließen** , und klicken Sie dann im Assistenten zum Hinzufügen von Einstiegspunkten auf **Schließen**.  
  
    > [!NOTE]  
    > Wenn sich der hinzugefügte Einstiegspunkt in einer anderen Gesamtstruktur als die vorhandenen Einstiegspunkte oder Client Computer befindet, müssen Sie im Bereich **Tasks** auf **Verwaltungs Server aktualisieren** klicken, um die Domänen Controller und System Center zu ermitteln. Configuration Manager in der neuen Gesamtstruktur.  
  
16. Wiederholen Sie dieses Verfahren aus Schritt 2 für jeden Einstiegspunkt, den Sie der Bereitstellung für mehrere Standorte hinzufügen möchten.  
  
](../../../../media/Step-3-Configure-the-Multisite-Deployment/PowerShellLogoSmall.gif)***<em>äquivalente Windows PowerShell-Befehle</em> mit @no__t 0shell***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
Um den Computer edge2 aus der corp2-Domäne als zweiten Einstiegspunkt mit dem Namen edge2-Europe hinzuzufügen. Die Einstiegspunkt Konfiguration lautet wie folgt: ein Client-IPv6-Präfix "2001: db8:2: 2000::/64", eine Connect to-Adresse (das IP-HTTPS-Zertifikat auf dem edge2-Computer) "edge2.contoso.com", ein Server-Gruppenrichtlinien Objekt mit dem Namen "DirectAccess-Servereinstellungen-edge2-Europa" und die internen und externe Schnittstellen mit dem Namen Internet und Corpnet2:  
  
```  
Add-DAEntryPoint -RemoteAccessServer 'edge2.corp2.corp.contoso.com' -Name 'Edge2-Europe' -ClientIPv6Prefix '2001:db8:2:2000::/64' -ConnectToAddress 'Europe.contoso.com' -ServerGpoName 'corp2.corp.contoso.com\DirectAccess Server Settings - Edge2-Europe' -InternetInterface 'Internet' -InternalInterface 'Corpnet2'  
```  
  
Um Windows 7-Client Computern den Zugriff auf den zweiten Einstiegspunkt über die Sicherheitsgruppe DA_Clients_Europe und die Verwendung des Gruppenrichtlinien Objekts DA_W7_Clients_GPO_Europe zuzulassen.  
  
```  
Add-DAClient -EntrypointName 'Edge2-Europe' -DownlevelGpoName @('corp.contoso.com\ DA_W7_Clients_GPO_Europe') -DownlevelSecurityGroupNameList @('corp.contoso.com\DA_Clients_Europe')  
```  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Schritt 2: Konfigurieren der Infrastruktur für mehrere Standorte @ no__t-0
