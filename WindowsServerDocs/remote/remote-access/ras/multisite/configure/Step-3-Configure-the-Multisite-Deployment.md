---
title: Schritt 3 Konfigurieren der Bereitstellung für mehrere Standorte
description: Dieses Thema ist Teil des Handbuchs bereitstellen mehrere RAS-Server in einer Bereitstellung für mehrere Standorte in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ea7ecd52-4c12-4a49-92fd-b8c08cec42a9
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9c746e95efeb5d2e4a5bb5183cd3642e50901158
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282613"
---
# <a name="step-3-configure-the-multisite-deployment"></a>Schritt 3 Konfigurieren der Bereitstellung für mehrere Standorte

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Nach dem Konfigurieren der Infrastruktur für mehrere Standorte gehen Sie folgendermaßen vor, um die Bereitstellung des Remotezugriffs für mehrere Standorte einzurichten.  
  
|Aufgabe|Beschreibung|  
|----|--------|  
|3.1. Konfigurieren von RAS-Server|Konfigurieren Sie zusätzliche RAS-Server, indem Sie das Einrichten von IP-Adressen, verknüpfen sie mit der Domäne und installieren die Rolle "Remotezugriff".|  
|3.2. Gewähren von Administratorzugriff|GRANT-Berechtigungen für die zusätzlichen RAS-Server an den DirectAccess-Administrator.|  
|3.3. Konfigurieren von IP-HTTPS für eine Bereitstellung für mehrere Standorte|Konfigurieren Sie die IP-HTTPS-Zertifikat, das in einer Bereitstellung für mehrere Standorte verwendet.|  
|3.4. Konfigurieren des Netzwerkadressenservers für eine Bereitstellung für mehrere Standorte|Konfigurieren Sie die Netzwerkadressenserver-Zertifikat in einer Bereitstellung für mehrere Standorte verwendet.|  
|3.5. Konfigurieren von DirectAccess-Clients für eine Bereitstellung für mehrere Standorte|Entfernen Sie Windows 7-Clientcomputer aus Windows 8-Sicherheitsgruppen.|  
|3.6. Aktivieren Sie die Bereitstellung für mehrere Standorte|Aktivieren Sie die Bereitstellung für mehrere Standorte auf dem ersten RAS-Server.|  
|3.7. Hinzufügen von Einstiegspunkten zur Bereitstellung für mehrere Standorte|Fügen Sie weitere Einstiegspunkte, die Bereitstellung für mehrere Standorte.|  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="BKMK_ConfigServer"></a>3.1. Konfigurieren von RAS-Server  

  
### <a name="to-install-the-remote-access-role"></a>So installieren Sie die Remotezugriffsrolle  
  
1.  Stellen Sie sicher, dass jeder RAS-Server konfiguriert ist, mit der richtigen Bereitstellungstopologie (Edge, hinter einem NAT-Gerät, einzelne Netzwerkschnittstelle), und die entsprechenden Routen.  
  
2.  Konfigurieren Sie die IP-Adressen auf jedem RAS-Server gemäß der Standorttopologie und Ihres Unternehmens-IP-Adressierungsschema.  
  
3.  Verknüpfen Sie jede RAS-Server mit Active Directory-Domäne ein.  
  
4.  In der Server-Manager-Konsole in der **Dashboard**, klicken Sie auf **Rollen und Features hinzufügen**.  
  
5.   Klicken Sie dreimal auf **Weiter** , um zur Anzeige für die Serverrollenauswahl zu gelangen.  
  
6.  Auf der **Serverrollen auswählen** die Option **RAS**, und klicken Sie dann auf **Weiter**.  
  
7.  Klicken Sie auf **Weiter** drei Mal.  
  
8.  Auf der **Rollendienste auswählen** die Option **DirectAccess und VPN (RAS)** , und klicken Sie dann auf **Features hinzufügen**.  
  
9.  Wählen Sie **Routing**Option **Web Application Proxy**, klicken Sie auf **Features hinzufügen**, und klicken Sie dann auf **Weiter**.  
  
10. Klicken Sie auf **Weiter**, und klicken Sie dann auf **Installieren**.  
  
11.  Überprüfen Sie im Dialogfeld **Installationsstatus**, ob die Installation erfolgreich war, und klicken Sie dann auf **Schließen**.  
  
  
![Windows PowerShell](../../../../media/Step-3-Configure-the-Multisite-Deployment/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***  

  
Schritte 1 bis 3 müssen manuell durchgeführt werden, und verwenden dieses Windows PowerShell-Cmdlet werden nicht erreicht.  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Install-WindowsFeature RemoteAccess -IncludeManagementTools  
```  
  
## <a name="BKMK_Admin"></a>3.2. Gewähren von Administratorzugriff  
  
#### <a name="to-grant-administrator-permissions"></a>Gewähren von Administratorberechtigungen  
  
1.  Auf dem RAS-Server in den zusätzlichen Einstiegspunkt: Auf der **starten** geben **Computerverwaltung**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie im linken Bereich auf **lokale Benutzer und Gruppen**.  
  
3.  Doppelklicken Sie auf **Gruppen**, und doppelklicken Sie dann auf **Administratoren**.  
  
4.  Auf der **Administratoreigenschaften** Dialogfeld klicken Sie auf **hinzufügen**, und klicken Sie auf die **Auswahl von Benutzern, Computern, Dienstkonten oder Gruppen** im Dialogfeld klicken Sie auf  **Speicherorte**.  
  
5.  Auf der **Speicherorte** Dialogfeld die **Speicherort** Struktur, klicken Sie auf das Verzeichnis, das Benutzerkonto, von der DirectAccess-Administrator, und klicken Sie dann auf **OK**.  
  
6.  In der **Geben Sie die zu verwendenden Objektnamen**, geben Sie den Benutzernamen, der der DirectAccess-Administrator, und klicken Sie dann auf **OK** zweimal.  
  
7.  Auf der **Administratoreigenschaften** Dialogfeld klicken Sie auf **OK**.  
  
8.  Schließen Sie das Fenster "Computerverwaltung".  
  
9. Wiederholen Sie dieses Verfahren auf alle RAS-Server, die Teil der Bereitstellung für mehrere Standorte werden.  
  
## <a name="BKMK_IPHTTPS"></a>3.3. Konfigurieren von IP-HTTPS für eine Bereitstellung für mehrere Standorte  
Auf jedem RAS-Server, der die Bereitstellung für mehrere Standorte hinzugefügt wird, muss ein SSL-Zertifikat zur Überprüfung der HTTPS-Verbindung mit dem IP-HTTPS-Webserver. Grundvoraussetzung zur Ausführung dieses Vorgangs ist die Mitgliedschaft in der lokalen Gruppe **Administratoren** oder eine gleichwertige Mitgliedschaft.  
  
#### <a name="to-obtain-an-ip-https-certificate"></a>Um ein IP-HTTPS-Zertifikat zu erhalten.  
  
1.  Auf jedem RAS-Server: Auf der **starten** geben **Mmc**, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie im Menü **Datei** auf **Snap-Ins hinzufügen bzw. entfernen**.  
  
3.  Klicken Sie auf **Zertifikate**, **Hinzufügen**, **Computerkonto** und **Weiter**. Wählen Sie **Lokaler Computer** aus, klicken Sie auf **Fertig stellen** und anschließend auf **OK**.  
  
4.  Öffnen Sie in der Konsolenstruktur des Zertifikat-Snap-Ins den Eintrag **Zertifikate (Lokaler Computer)\Persönlich\Zertifikate**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, zeigen Sie auf **Alle Aufgaben**, und klicken Sie dann auf **Neues Zertifikat anfordern**.  
  
6.  Klicken Sie zweimal auf **Weiter** .  
  
7.  Auf der **Zertifikate anfordern** Seite, klicken Sie auf dem Webserver-Zertifikatvorlage und klicken Sie dann auf **zusätzliche Informationen für diese zertifikatsregistrierung benötigt**.  
  
    Wenn der Webserver-Zertifikatvorlage nicht angezeigt wird, stellen Sie sicher, dass das Computerkonto des RAS-Server verfügt über Berechtigungen für die Webserver-Zertifikatvorlage registrieren. Weitere Informationen finden Sie unter [Konfigurieren von Berechtigungen für die Webserver-Zertifikatvorlage](https://technet.microsoft.com/library/ee649249(v=ws.10).aspx).  
  
8.  Auf der **Betreff** auf der Registerkarte die **Zertifikateigenschaften** Dialogfeld **Antragstellername**, für **Typ**Option **allgemeine Namen**.  
  
9. In **Wert**, geben Sie den vollqualifizierten Domänennamen (FQDN) des Internetnamens des RAS-Servers (beispielsweise "Europe.contoso.com"), und klicken Sie dann auf **hinzufügen**.  
  
10. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
11. Überprüfen Sie im Detailbereich des Zertifikat-Snap-Ins, dass ein neues Zertifikat mit dem vollqualifizierten Domänennamen unter **Serverauthentifizierung** mit der Option **Beabsichtigte Zwecke** registriert wurde.  
  
12. Klicken Sie mit der rechten Maustaste auf das Zertifikat, und klicken Sie anschließend auf **Eigenschaften**.  
  
13. Geben Sie unter **Anzeigename** die Zeichenfolge **IP-HTTPS-Zertifikat** ein, und klicken Sie dann auf **OK**.  
  
    > [!TIP]  
    > Die Schritte 12 und 13 sind optional, aber Sie vereinfachen Sie das Zertifikat für IP-HTTPS wählen Sie beim Konfigurieren des Remotezugriffs.  
  
14. Wiederholen Sie dieses Verfahren auf alle RAS-Server in Ihrer Bereitstellung.  
  
## <a name="BKMK_NLS"></a>3.4. Konfigurieren des Netzwerkadressenservers für eine Bereitstellung für mehrere Standorte  
Wenn Sie ausgewählt haben, richten Sie die Netzwerkadressenserver-Website auf dem RAS-Server, wenn Sie Ihren ersten Server einrichten, hat jede neue RAS-Server, dass Sie hinzufügen, muss mit einem Webserver-Zertifikat konfiguriert werden, die den gleichen Antragstellernamen, der für t ausgewählt wurde er network Location Server für den ersten Server. Jeder Server benötigt ein Zertifikat zum Authentifizieren der Verbindung mit dem Netzwerkadressenserver und -Clientcomputern im internen Netzwerk müssen in der Lage, den Namen der Website im DNS auflösen.  
  
#### <a name="to-install-a-certificate-for-network-location"></a>Zum Installieren eines Zertifikats für Netzwerkadressen  
  
1.  Gehen Sie auf dem Remotezugriffsserver wie folgt vor: Auf der **starten** geben **Mmc**, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Klicken Sie im Menü **Datei** auf **Snap-Ins hinzufügen bzw. entfernen**.  
  
3.  Klicken Sie auf **Zertifikate**, **Hinzufügen**, **Computerkonto** und **Weiter**. Wählen Sie **Lokaler Computer** aus, klicken Sie auf **Fertig stellen** und anschließend auf **OK**.  
  
4.  Öffnen Sie in der Konsolenstruktur des Zertifikat-Snap-Ins den Eintrag **Zertifikate (Lokaler Computer)\Persönlich\Zertifikate**.  
  
5.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, zeigen Sie auf **Alle Aufgaben**, und klicken Sie dann auf **Neues Zertifikat anfordern**.  
  
    > [!NOTE]  
    > Sie können auch das gleiche Zertifikat importieren, das für den Netzwerkadressenserver für den ersten RAS-Server verwendet wurde.  
  
6.  Klicken Sie zweimal auf **Weiter** .  
  
7.  Auf der **Zertifikate anfordern** Seite, klicken Sie auf dem Webserver-Zertifikatvorlage und klicken Sie dann auf **zusätzliche Informationen für diese zertifikatsregistrierung benötigt**.  
  
    Wenn der Webserver-Zertifikatvorlage nicht angezeigt wird, stellen Sie sicher, dass das Computerkonto des RAS-Server verfügt über Berechtigungen für die Webserver-Zertifikatvorlage registrieren. Weitere Informationen finden Sie unter [Konfigurieren von Berechtigungen für die Webserver-Zertifikatvorlage](https://technet.microsoft.com/library/ee649249(v=ws.10).aspx).  
  
8.  Auf der **Betreff** auf der Registerkarte die **Zertifikateigenschaften** Dialogfeld **Antragstellername**, für **Typ**Option **allgemeine Namen**.  
  
9. In **Wert**, geben Sie den vollqualifizierten Domänennamen (FQDN), die für die Netzwerkadressenserver-Zertifikat des ersten RAS-Servers (z. B. nls.corp.contoso.com) konfiguriert wurde, und klicken Sie dann auf **hinzufügen**.  
  
10. Klicken Sie auf **OK**, **Registrieren** und dann auf **Fertig stellen**.  
  
11. Überprüfen Sie im Detailbereich des Zertifikat-Snap-Ins, dass ein neues Zertifikat mit dem vollqualifizierten Domänennamen unter **Serverauthentifizierung** mit der Option **Beabsichtigte Zwecke** registriert wurde.  
  
12. Klicken Sie mit der rechten Maustaste auf das Zertifikat, und klicken Sie anschließend auf **Eigenschaften**.  
  
13. Geben Sie unter **Anzeigenamen** den Namen **Netzwerkadressenzertifikat** ein, und klicken Sie dann auf **OK**.  
  
    > [!TIP]  
    > Die Schritte 12 und 13 sind optional, aber es erleichtern Ihnen die Auswahl des Zertifikats für Netzwerkadressen beim Konfigurieren des Remotezugriffs.  
  
14. Wiederholen Sie dieses Verfahren auf alle RAS-Server in Ihrer Bereitstellung.  
  
### <a name="NLS"></a>Um den Netzwerkadressenserver zu DNS-Einträge erstellen  
  
1.  Auf dem DNS-Server: Auf der **starten** geben **dnsmgmt.msc**, und drücken Sie dann die EINGABETASTE.  
  
2.  Im linken Bereich die **DNS-Manager** -Konsole, öffnen Sie die forward-Lookupzone für das interne Netzwerk. Klicken Sie mit der rechten Maustaste auf die entsprechende Zone, und klicken Sie auf **neuer Host (A oder AAAA)** .  
  
3.  Auf der **neuen Host** Dialogfeld die **Name (wird übergeordneter Domänenname bei Nichtangabe)** Geben Sie den Namen, die für den Netzwerkadressenserver für den ersten RAS-Server verwendet wurde. In der **IP-Adresse** Feld, geben Sie die Intranetverbindung IPv4-Adresse des RAS-Servers, und klicken Sie dann auf **Host hinzufügen**. Klicken Sie im Dialogfeld **DNS** auf **OK**.  
  
4.  Auf der **neuen Host** Dialogfeld die **Name (wird übergeordneter Domänenname bei Nichtangabe)** Geben Sie den Namen, die für den Netzwerkadressenserver für den ersten RAS-Server verwendet wurde. In der **IP-Adresse** Feld, geben Sie die Intranetverbindung IPv6-Adresse des RAS-Servers, und klicken Sie dann auf **Host hinzufügen**. Klicken Sie im Dialogfeld **DNS** auf **OK**.  
  
5.  Wiederholen Sie Schritte 3 und 4 für alle RAS-Server in Ihrer Bereitstellung ein.  
  
6.  Klicken Sie auf **Fertig**.  
  
7.  Wiederholen Sie diesen Vorgang vor dem Hinzufügen von Servern als zusätzliche Einstiegspunkte in der Bereitstellung ein.  
  
## <a name="BKMK_Client"></a>3.5. Konfigurieren von DirectAccess-Clients für eine Bereitstellung für mehrere Standorte  
DirectAccess-Windows-Clientcomputer muss Mitglied der Sicherheitsgruppe, die ihrer DirectAccess-Zuordnung zu definieren. Bevor Sie für mehrere Standorte aktiviert ist, können diese Sicherheitsgruppe, die sowohl für Windows 8-Clients als auch für Windows 7-Clients enthalten, (sofern der entsprechende "Downlevel"-Modus ausgewählt wurde). Wenn mehrere Standorte aktiviert ist, werden vorhandene Client-Sicherheitsgruppe, in einzelnen Servermodus in Sicherheitsgruppe, die für Windows 8 nur konvertiert. Nach Funktionen für mehrere Standorte aktiviert ist, wird DirectAccess Windows 7-Clientcomputer müssen zu entsprechenden dedizierte Windows 7-Client-Sicherheitsgruppen (die bestimmte Einstiegspunkte zugeordnet sind) verschoben werden, oder sie sind nicht in der Lage, über DirectAccess eine Verbindung herstellen. Die Windows 7-Clients müssen zunächst aus den vorhandenen Sicherheitsgruppen entfernt werden, die jetzt Windows 8-Sicherheitsgruppen sind. Vorsicht:  Windows 7-Clientcomputer, die Elemente sowohl Windows 7 und Windows 8-clientsicherheitsgruppen verlieren Remotezugriffs- und Windows 7-Clients ohne SP1 installiert, verlieren auch Unternehmenskonnektivität. Aus diesem Grund müssen alle Clientcomputer mit Windows 7 aus Windows 8-Sicherheitsgruppen entfernt werden.  
  
#### <a name="remove--windows-7--clients-from-windows-8-security-groups"></a>Entfernen Sie Windows 7-Clients aus Windows 8-Sicherheitsgruppen  
  
1.  Klicken Sie auf dem primären Domänencontroller, auf **starten**, und klicken Sie dann auf **Active Directory-Benutzer und-Computer**.  
  
2.  Doppelklicken Sie auf die Sicherheitsgruppe, um Computer aus der Sicherheitsgruppe zu entfernen, und klicken Sie auf die **< Gruppenname > Eigenschaften** Dialogfeld klicken Sie auf die **Mitglieder** Registerkarte.  
  
3.  Wählen Sie die Windows 7-Clientcomputer, und klicken Sie auf **entfernen**.  
  
4.  Wiederholen Sie dieses Verfahren, um die Windows 7-Clientcomputer aus den Windows 8-Sicherheitsgruppen zu entfernen.  
  
> [!IMPORTANT]  
> Wenn Sie eine Konfiguration des Remotezugriffs für mehrere Standorte aktivieren verlieren alle Client-Computer (Windows 7 und Windows 8) Remoteverbindungen, bis sie die Verbindung mit dem Unternehmensnetzwerk direkt oder über VPN herstellen, um die Gruppenrichtlinien aktualisieren können. Dies gilt, wenn zum ersten Mal für mehrere Standorte zu aktivieren und deaktivieren Sie die für mehrere Standorte.  
  
## <a name="BKMK_Enable"></a>3.6. Aktivieren Sie die Bereitstellung für mehrere Standorte  
Um eine Bereitstellung für mehrere Standorte zu konfigurieren, aktivieren Sie die Funktionen für mehrere Standorte auf Ihre vorhandenen RAS-Server. Stellen Sie vor der Aktivierung in Ihrer Bereitstellung für mehrere Standorte, benötigen Sie die folgende Informationen ein:  
  
1.  Verteilen DirectAccess-Client-Verbindungen für alle Einstiegspunkte in Ihrer Bereitstellung, für globale Lastenausgleich und IP-Adressen, wenn Sie laden möchten.  
  
2.  Die Sicherheit Gruppen mit Windows 7-Clientcomputer für den ersten Einstiegspunkt in Ihrer Bereitstellung auf, wenn Sie Remote Access for Windows 7-Clientcomputern aktivieren möchten.  
  
3.  Gruppieren Sie Gruppenrichtlinienobjekt-Namen, wenn Sie mit nicht standardmäßigen Group Policy Objects, die auf Windows 7-Clientcomputern für den ersten Einstiegspunkt in Ihrer Bereitstellung angewendet werden, wenn Sie Unterstützung für Windows 7-Clientcomputer erforderlich sind.  
  
### <a name="EnabledMultisite"></a>Um eine Konfiguration für mehrere Standorte zu aktivieren.  
  
1.  Auf dem vorhandenen RAS-Server: Auf der **starten** geben **RAMgmtUI.exe**, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  In der Remotezugriffs-Verwaltungskonsole, klicken Sie auf **Konfiguration**, und klicken Sie dann in der **Aufgaben** Bereich klicken Sie auf **aktivieren mehrere Standorte**.  
  
3.  In der **Aktivieren der Bereitstellung für mehrere Standorte** Assistenten, auf die **Vorbemerkungen** auf **Weiter**.  
  
4.  Auf der **Bereitstellungsname** auf der Seite **Namen der Bereitstellung für mehrere Standorte**, geben Sie einen Namen für Ihre Bereitstellung. In **erster Einstiegspunkt Namen**, geben Sie einen Namen zu den ersten Einstiegspunkt zu ermitteln, die aktuellen RAS-Servers ist, und klicken Sie dann auf **Weiter**.  
  
5.  Auf der **Eintrag Punktauswahl** eine der folgenden:  
  
    -   Klicken Sie auf **Einstiegspunkte automatisch zuweisen, und ermöglichen Sie Clients manuell auswählen** Clientcomputer automatisch auf den am besten geeigneten Einstiegspunkt, weitergeleitet werden, gleichzeitig Client Computer einen Einstiegspunkt manuell auswählen können. Manuelle Eingabe Punktauswahl ist nur für Windows 8-Computern verfügbar. Klicken Sie auf **Weiter**.  
  
    -   Klicken Sie auf **Einstiegspunkte automatisch zuweisen** automatisch leiten die Clientcomputer auf den am besten geeigneten Einstiegspunkt, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **globalen Lastenausgleich** eine der folgenden:  
  
    -   Klicken Sie auf **Nein, verwenden Sie keine globalen Lastenausgleich** , wenn Sie nicht, verwenden Sie einen globalen Lastenausgleich möchten, und klicken Sie dann auf **Weiter**.  
  
        > [!NOTE]  
        > Bei Auswahl dieser Option Client-Computer automatisch verbinden, auf die nächsten Einstiegspunkt.  
  
    -   Klicken Sie auf **Ja, verwenden Sie die globalen Lastenausgleich** , wenn Sie laden möchten, verteilen Sie den Datenverkehr zwischen allen Einstiegspunkten Global. In **Geben Sie den globale Lastenausgleich-FQDN von allen Einstiegspunkten verwendet werden**, geben Sie den globale Lastenausgleich-FQDN, und klicken Sie in **Geben Sie die IP-Adresse für diesen Einstiegspunkt der globalen Lastenausgleich** , enthält die erste RAS-Server, geben Sie die IP-Adresse für diesen Einstiegspunkt der globalen Lastenausgleich, und klicken Sie dann auf **Weiter**.  
  
7.  Auf der **Clientunterstützung** eine der folgenden:  
  
    -   Um den Zugriff auf den Clientcomputern mit Windows 8 oder neueren Betriebssystemen zu beschränken, klicken Sie auf **Einschränken des Zugriffs auf Clientcomputern unter Windows 8 oder einem höheren Betriebssystem**, und klicken Sie dann auf **Weiter**.  
  
    -   Um Computer mit Windows 7 ausführen, um Zugriff auf diesen Einstiegspunkt zuzulassen, klicken Sie auf **können Client-Computern mit Windows 7 ausführen, um Zugriff auf diesen Einstiegspunkt**, und klicken Sie auf **hinzufügen**. Auf der **Gruppen auswählen** wählen Sie im Dialogfeld die Sicherheitsgruppe, die die Windows 7-Clientcomputer enthält, klicken Sie auf **OK**, und klicken Sie dann auf **Weiter**.  
  
8.  Auf der **Client-GPO-Einstellungen** Seite, die standardmäßige GPO für Windows 7-Clientcomputer für diesen Einstiegspunkt akzeptieren, geben Sie den Namen des Gruppenrichtlinienobjekts, das möchten Remotezugriff auf automatisch erstellen, oder klicken Sie auf **Durchsuchen** auf Suchen Sie das Gruppenrichtlinienobjekt für Windows 7-Clientcomputer, und klicken Sie dann auf **Weiter**.  
  
    > [!NOTE]  
    > -   Die **Client-GPO-Einstellungen** Seite wird angezeigt, wenn Sie den Einstiegspunkt für Windows 7-Client-Computern mit Zugriff auf den Einstiegspunkt kann nur konfigurieren.  
    > -   Sie können optional klicken **überprüfen GPOs** sicherzustellen, dass Sie die richtigen Berechtigungen für das ausgewählte Gruppenrichtlinienobjekt oder Gruppenrichtlinienobjekte für diesen Einstiegspunkt verfügen. Berechtigungen sind erforderlich, wenn das GPO ist nicht vorhanden und automatisch erstellt werden wird, erstellen und verknüpfen. Klicken Sie dann in der Fall, in denen die Gruppenrichtlinienobjekte manuell erstellt wurden, bearbeiten, Ändern der Sicherheit und Delete-Berechtigungen sind erforderlich.  
  
9. Auf der **Zusammenfassung** auf **Commit**.  
  
10. Auf der **Multisite-Bereitstellung aktivieren** Dialogfeld klicken Sie auf **schließen** und Aktivieren von Multisite-Bereitstellungs-Assistenten klicken Sie dann auf **schließen**.  
  
![Windows PowerShell](../../../../media/Step-3-Configure-the-Multisite-Deployment/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
Mit dem Namen "Edge1-de", um eine Bereitstellung für mehrere Standorte mit dem Namen "Contoso" auf den ersten Einstiegspunkt zu aktivieren. Die Bereitstellung ermöglicht es Clients, die den Einstiegspunkt manuell auswählen und einen globalen Lastenausgleich nicht verwendet.  
  
```  
Enable-DAMultiSite -Name 'Contoso' -EntryPointName 'Edge1-US' -ManualEntryPointSelectionAllowed 'Enabled'  
```  
  
Auf Computern Windows 7-Clientzugriff über den ersten Einstiegspunkt mithilfe der Sicherheitsgruppe DA_Clients_US und verwenden die GPO-DA_W7_Clients_GPO_US zu ermöglichen.  
  
```  
Add-DAClient -EntrypointName 'Edge1-US' -DownlevelSecurityGroupNameList @('corp.contoso.com\DA_Clients_US') -DownlevelGpoName @('corp.contoso.com\DA_W7_Clients_GPO_US)  
```  
  
## <a name="BKMK_EntryPoint"></a>3.7. Hinzufügen von Einstiegspunkten zur Bereitstellung für mehrere Standorte  
Nach der Aktivierung in Ihrer Bereitstellung für mehrere Standorte, können Sie die zusätzlichen Einstiegspunkte, die mit den Einstiegspunkt des Assistenten zum Hinzufügen von hinzufügen. Stellen Sie vor dem Hinzufügen von Einstiegspunkten, benötigen Sie die folgende Informationen ein:  
  
-   Global Load Balancer-IP-Adressen für jeden neuen Eintrag verweisen, wenn Sie globale Lastenausgleich verwenden.  
  
-   Die Sicherheitsgruppe, die mit Windows 7-Clientcomputer für jeden Einstiegspunkt, der hinzugefügt werden, wenn Sie Remote Access for Windows 7-Clientcomputern aktivieren möchten.  
  
-   Gruppieren Sie Gruppenrichtlinienobjekt-Namen, wenn Sie mit nicht standardmäßigen Group Policy Objects, die auf Windows 7-Clientcomputer für jeden Einstiegspunkt, der hinzugefügt wird, angewendet werden, wenn Sie Unterstützung für Windows 7-Clientcomputer erforderlich sind.  
  
-   In dem Fall, in denen IPv6 im Netzwerk der Organisation bereitgestellt wird, müssen Sie die IP-HTTPS-Präfix für den neuen Einstiegspunkt vorbereiten.  
  
### <a name="AddEP"></a>Hinzufügen von Einstiegspunkten Ihrer Bereitstellung für mehrere Standorte  
  
1.  Auf dem vorhandenen RAS-Server: Auf der **starten** geben **RAMgmtUI.exe**, und drücken Sie dann die EINGABETASTE. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  In der Remotezugriffs-Verwaltungskonsole, klicken Sie auf **Konfiguration**, und klicken Sie dann in der **Aufgaben** Bereich klicken Sie auf **fügen einen Einstiegspunkt**.  
  
3.  Hinzufügen einen Einstiegspunkt-Assistenten auf der **Punkt Eingabedetails** auf der Seite **RAS-Server**, geben Sie den vollqualifizierten Domänennamen (FQDN) des Servers hinzufügen. In **Name des Einstiegspunkts**, geben Sie den Namen des Einstiegspunkts ein, und klicken Sie dann auf **Weiter**.  
  
4.  Auf der **globale laden Netzwerklastenausgleich-Einstellungen** Seite Geben Sie die IP-Adresse des dieser Einstiegspunkt der globalen Lastenausgleich, und klicken Sie dann auf **Weiter**.  
  
    > [!NOTE]  
    > Die **globale laden Netzwerklastenausgleich-Einstellungen** Seite angezeigt wird, nur, wenn die Konfiguration für mehrere Standorte einen globalen Lastenausgleich verwendet.  
  
5.  Auf der **Netzwerktopologie** klicken Sie auf die Topologie mit der Netzwerktopologie der RAS-Server, die Sie hinzufügen möchten, und klicken Sie dann auf **Weiter**.  
  
6.  Auf der **Netzwerkname oder IP-Adresse** auf der Seite **Geben Sie den öffentlichen Namen oder IP-Adresse, die von Clients zum Verbinden mit dem RAS-Server verwendet**, geben Sie den öffentlichen Namen oder die IP-Adresse, die von Clients zum Herstellen einer Verbindung mit verwendet das RAS-Server. Der öffentliche Namen entspricht, mit dem Antragstellernamen des IP-HTTPS-Zertifikats. In der Fall, in denen Edge-Netzwerktopologie implementiert wurde, ist die IP-Adresse des externen Adapters des RAS-Servers. Klicken Sie auf **Weiter**.  
  
7.  Auf der **Netzwerkadapter** Seite, gehen Sie wie im folgenden:  
  
    -   Wenn Sie eine Topologie mit zwei Netzwerkadaptern, in bereitstellen **externen Adapter**, wählen Sie den Adapter, der mit dem externen Netzwerk verbunden ist. In **des internen Adapters**, wählen Sie den Adapter, der mit dem internen Netzwerk verbunden ist.  
  
    -   Wenn Sie eine Topologie mit einem Netzwerkadapter im Bereitstellen **Netzwerkadapter**, wählen Sie den Adapter, der mit dem internen Netzwerk verbunden ist.  
  
8.  Auf der **Netzwerkadapter** auf der Seite **wählen Sie das Zertifikat zum Authentifizieren von IP-HTTPS-Verbindungen**, klicken Sie auf **Durchsuchen** zu suchen, und wählen Sie die IP-HTTPS-Zertifikat. Klicken Sie auf **Weiter**.  
  
9. Wenn IPv6 im Unternehmensnetzwerk, konfiguriert ist, auf die **Präfixkonfiguration** auf der Seite **Clientcomputern zugewiesene IPv6-Präfix**, geben Sie ein IP-HTTPS-Präfix zum Zuweisen von IPv6-Adressen an DirectAccess-Client Computer, und klicken Sie auf **Weiter**.  
  
10. Auf der **Clientunterstützung** eine der folgenden:  
  
    -   Um den Zugriff auf den Clientcomputern mit Windows 8 oder neueren Betriebssystemen zu beschränken, klicken Sie auf **Einschränken des Zugriffs auf Clientcomputern unter Windows 8 oder einem höheren Betriebssystem**, und klicken Sie dann auf **Weiter**.  
  
    -   Um Computer mit Windows 7 ausführen, um Zugriff auf diesen Einstiegspunkt zuzulassen, klicken Sie auf **können Client-Computern mit Windows 7 ausführen, um Zugriff auf diesen Einstiegspunkt**, und klicken Sie auf **hinzufügen**. Auf der **Gruppen auswählen** Dialogfeld wählen die Sicherheitsgruppe, die die, das die Verbindung mit diesen Einstiegspunkt, klicken Sie auf Windows 7-Clientcomputer enthalten **OK**, und klicken Sie auf **Weiter**.  
  
11. Auf der **Client-GPO-Einstellungen** Seite, die standardmäßige GPO für Windows 7-Clientcomputer für diesen Einstiegspunkt akzeptieren, geben Sie den Namen des Gruppenrichtlinienobjekts, das Sie Remotezugriff erhalten automatisch erstellen, oder klicken Sie auf möchten **Durchsuchen** auf Suchen Sie das Gruppenrichtlinienobjekt für Windows 7-Clientcomputer, und klicken Sie auf **Weiter**.  
  
    > [!NOTE]  
    > -   Die **Client-GPO-Einstellungen** Seite wird angezeigt, wenn Sie den Einstiegspunkt für Windows 7-Client-Computern mit Zugriff auf den Einstiegspunkt kann nur konfigurieren.  
    > -   Sie können optional klicken **überprüfen GPOs** sicherzustellen, dass Sie die richtigen Berechtigungen für das ausgewählte Gruppenrichtlinienobjekt oder Gruppenrichtlinienobjekte für diesen Einstiegspunkt verfügen. Berechtigungen sind erforderlich, wenn das GPO ist nicht vorhanden und automatisch erstellt werden wird, erstellen und verknüpfen. Klicken Sie dann in der Fall, in denen die Gruppenrichtlinienobjekte manuell erstellt wurden, bearbeiten, Ändern der Sicherheit und Delete-Berechtigungen sind erforderlich.  
  
12. Auf der **Server-GPO-Einstellungen** Seite, akzeptieren Sie die Standard-GPO für diesen Server Remotezugriff auf, geben Sie den Namen des Gruppenrichtlinienobjekts, das Sie Remotezugriff erhalten automatisch erstellen, oder klicken Sie auf möchten **Durchsuchen** auf das Gruppenrichtlinienobjekt für Suchen Dieser Server ein, und klicken Sie dann auf **Weiter**.  
  
13. Auf der **Netzwerkadressenserver** auf **Durchsuchen** wählen Sie das Zertifikat für die Netzwerkadressenserver-Website auf dem RAS-Server ausgeführt, und klicken Sie dann auf **Weiter**.  
  
    > [!NOTE]  
    > Die **Netzwerkadressenserver** Seite angezeigt wird, nur, wenn die Netzwerkadressenserver-Website auf dem RAS-Server ausgeführt wird.  
  
14. Auf der **Zusammenfassung** Seite überprüfen Sie die Einstellungen für den Eintrag, und klicken Sie dann auf **Commit**.  
  
15. Auf der **Einstiegspunkt hinzufügen** Dialogfeld klicken Sie auf **schließen** , und klicken Sie dann auf dem Assistenten einen Eintrag hinzufügen, auf **schließen**.  
  
    > [!NOTE]  
    > Wenn der Einstiegspunkt, der hinzugefügt wurde in einer anderen Gesamtstruktur als der vorhandene Einstiegspunkte oder -Clientcomputern, es ist erforderlich, klicken Sie auf **Verwaltungsserver aktualisieren** in die **Aufgaben** Bereich zum Ermitteln der Domänencontroller und System Center Configuration Manager in der neuen Gesamtstruktur.  
  
16. Wiederholen Sie dieses Verfahren aus Schritt 2 für jeden Einstiegspunkt, der Sie Ihre Bereitstellung für mehrere Standorte hinzufügen möchten.  
  
![Windows PowerShell](../../../../media/Step-3-Configure-the-Multisite-Deployment/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
Mit dem Namen "Edge2 Europa", die Computer von edge2 aus der Domäne corp2 als zweite Einstiegspunkt hinzufügen. Die Konfiguration des Eintrags ist: ein Client-IPv6-Präfix "2001:db8:2:2000:: / 64", Herstellen einer Verbindung zum Adresse (die IP-HTTPS-Zertifikat auf dem Computer von edge2) "edge2.contoso.com', ein Server-GPO mit dem Namen" DirectAccess Server Settings - Edge2-Europa ", und die interne und externe Schnittstellen, die mit dem Namen Internet und Corpnet2:  
  
```  
Add-DAEntryPoint -RemoteAccessServer 'edge2.corp2.corp.contoso.com' -Name 'Edge2-Europe' -ClientIPv6Prefix '2001:db8:2:2000::/64' -ConnectToAddress 'Europe.contoso.com' -ServerGpoName 'corp2.corp.contoso.com\DirectAccess Server Settings - Edge2-Europe' -InternetInterface 'Internet' -InternalInterface 'Corpnet2'  
```  
  
Auf Computern Windows 7-Clientzugriff über den zweiten Eintrag Punkt über die Sicherheitsgruppe DA_Clients_Europe und verwenden die GPO-DA_W7_Clients_GPO_Europe zu ermöglichen.  
  
```  
Add-DAClient -EntrypointName 'Edge2-Europe' -DownlevelGpoName @('corp.contoso.com\ DA_W7_Clients_GPO_Europe') -DownlevelSecurityGroupNameList @('corp.contoso.com\DA_Clients_Europe')  
```  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Schritt 2: Konfigurieren der Infrastruktur für mehrere Standorte](Step-2-Configure-the-Multisite-Infrastructure.md)
