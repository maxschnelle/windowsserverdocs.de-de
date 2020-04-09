---
ms.assetid: b035e9f8-517f-432a-8dfb-40bfc215bee5
title: Bereitstellen der Unterstützung nach %%amp;quot;Zugriff verweigert%%amp;quot; (Schritte zur Veranschaulichung)
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: fc23e9d9dae9118bf6d489ed8697ce5bac44e7ba
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861263"
---
# <a name="deploy-access-denied-assistance-demonstration-steps"></a>Bereitstellen der Unterstützung nach %%amp;quot;Zugriff verweigert%%amp;quot; (Schritte zur Veranschaulichung)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird erläutert, wie Sie die Unterstützung nach "Zugriff verweigert" konfigurieren und überprüfen, ob diese ordnungsgemäß funktioniert.  
  
**In diesem Dokument**  
  
-   [Schritt 1: Konfigurieren der Unterstützung nach "Zugriff verweigert"](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_1)  
  
-   [Schritt 2: Konfigurieren der e-Mail-Benachrichtigungseinstellungen](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_2)  
  
-   [Schritt 3: überprüfen, ob die Unterstützung nach "Zugriff verweigert" richtig konfiguriert ist](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_3)  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit deren Hilfe einige beschriebene Verfahren automatisiert werden können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="step-1-configure-access-denied-assistance"></a><a name="BKMK_1"></a>Schritt 1: Konfigurieren der Unterstützung nach "Zugriff verweigert"  
Sie können die Unterstützung nach "Zugriff verweigert" in einer Domäne mithilfe von Gruppenrichtlinien konfigurieren. Sie haben aber auch die Möglichkeit, die Unterstützung über die Konsole des Ressourcen-Managers für Dateiserver einzeln auf jedem Dateiserver zu konfigurieren. Sie können auch die Meldung "Zugriff verweigert" für einen bestimmten freigegebenen Ordner auf einem Dateiserver ändern.  
  
Sie können die Unterstützung nach "Zugriff verweigert" für die Domäne mithilfe von Gruppenrichtlinien wie folgt konfigurieren:  
  
[Führen Sie diesen Schritt mithilfe von Windows PowerShell aus.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-configure-access-denied-assistance-by-using-group-policy"></a>So konfigurieren Sie die Unterstützung nach "Zugriff verweigert" mithilfe von Gruppenrichtlinien  
  
1.  Öffnen Sie die Gruppenrichtlinienverwaltung. Klicken Sie in Server-Manager auf **Extras** und dann auf **Gruppenrichtlinienverwaltung**.  
  
2.  Klicken Sie mit der rechten Maustaste auf die entsprechende Gruppenrichtlinie, und klicken Sie dann auf **Bearbeiten**.  
  
3.  Klicken Sie auf **Computerkonfiguration**. Klicken Sie auf **Richtlinien**, auf **Administrative Vorlagen**, auf **System** und dann auf **Unterstützung nach "Zugriff verweigert"** .  
  
4.  Klicken Sie mit der rechten Maustaste auf **Meldung für Zugriffsverweigerungsfehler anpassen**, und klicken Sie dann auf **Bearbeiten**.  
  
5.  Aktivieren Sie die Option **Aktiviert**.  
  
6.  Konfigurieren Sie die folgenden Optionen:  
  
    1.  Geben Sie im Feld **Benutzern, denen der Zugriff auf einen Ordner oder eine Datei verweigert wird, die folgende Meldung anzeigen** die Meldung ein, die Benutzern angezeigt werden soll, wenn ihnen der Zugriff auf eine Datei oder einen Ordner verweigert wird.  
  
        Sie können der Meldung Makros hinzufügen, durch die benutzerdefinierter Text eingefügt wird. Die Makros umfassen Folgendes:  
  
        -   **[Ursprünglicher Dateipfad]** : Der ursprüngliche Dateipfad, auf den der Benutzer zugegriffen hat  
  
        -   **[Ordner des ursprünglichen Dateipfads]** : Der übergeordnete Ordner mit dem ursprünglichen Dateipfad, auf den der Benutzer zugegriffen hat.  
  
        -   **[Administrator-E-Mail]** : Die Administrator-E-Mail-Empfängerliste  
  
        -   **[Datenbesitzer-E-Mail]** : Die Datenbesitzer-E-Mail-Empfängerliste  
  
    2.  Aktivieren Sie das Kontrollkästchen **Benutzern das Anfordern von Unterstützung ermöglichen** .  
  
    3.  Übernehmen Sie die restlichen Standardeinstellungen.  
  
![projektmappenanleitung für](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>entsprechende Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.  
  
```  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName AllowEmailRequests -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName GenerateLog -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName IncludeDeviceClaims -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName IncludeUserClaims -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName PutAdminOnTo -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName PutDataOwnerOnTo -Type DWORD -value 1  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName ErrorMessage -Type MultiString -value "Type the text that the user will see in the error message dialog box."  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\Software\Policies\Microsoft\Windows\ADR\AccessDenied" -ValueName Enabled -Type DWORD -value 1 
  
```  
  
Alternativ können Sie die Unterstützung nach "Zugriff verweigert" auch über die Konsole des Ressourcen-Managers für Dateiserver einzeln auf jedem Dateiserver konfigurieren.  
  
[Führen Sie diesen Schritt mithilfe von Windows PowerShell aus.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1a)  
  
#### <a name="to-configure-access-denied-assistance-by-using-file-server-resource-manager"></a>So konfigurieren Sie die Unterstützung nach "Zugriff verweigert" mit dem Ressourcen-Manager für Dateiserver  
  
1.  Öffnen Sie den Ressourcen-Manager für Dateiserver. Klicken Sie in Server-Manager auf **Extras** und dann auf **Ressourcen-Manager für Dateiserver**.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Ressourcen-Manager für Dateiserver (lokal)** , und klicken Sie dann auf **Optionen konfigurieren**.  
  
3.  Klicken Sie auf die Registerkarte **Unterstützung nach "Zugriff verweigert"** .  
  
4.  Aktivieren Sie das Kontrollkästchen **Unterstützung nach "Zugriff verweigert" aktivieren** .  
  
5.  Geben Sie im Feld **Benutzern, denen der Zugriff auf einen Ordner oder eine Datei verweigert wird, die folgende Meldung anzeigen** die Meldung ein, die Benutzern angezeigt werden soll, wenn ihnen der Zugriff auf eine Datei oder einen Ordner verweigert wird.  
  
    Sie können der Meldung Makros hinzufügen, durch die benutzerdefinierter Text eingefügt wird. Die Makros umfassen Folgendes:  
  
    -   **[Ursprünglicher Dateipfad]** : Der ursprüngliche Dateipfad, auf den der Benutzer zugegriffen hat  
  
    -   **[Ordner des ursprünglichen Dateipfads]** : Der übergeordnete Ordner mit dem ursprünglichen Dateipfad, auf den der Benutzer zugegriffen hat.  
  
    -   **[Administrator-E-Mail]** : Die Administrator-E-Mail-Empfängerliste  
  
    -   **[Datenbesitzer-E-Mail]** : Die Datenbesitzer-E-Mail-Empfängerliste  
  
6.  Klicken Sie auf **E-Mail-Anforderungen konfigurieren**, aktivieren Sie das Kontrollkästchen **Benutzern das Anfordern von Unterstützung ermöglichen**, und klicken Sie dann auf **OK**.  
  
7.  Klicken Sie auf **Vorschau** , wenn Sie sehen möchten, wie die Fehlermeldung dem Benutzer angezeigt wird.  
  
8.  Klicken Sie auf **OK**.  
  
![projektmappenanleitung für](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>entsprechende Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.
  
```  
Set-FSRMAdrSetting -Event "AccessDenied" -DisplayMessage "Type the text that the user will see in the error message dialog box." -Enabled:$true -AllowRequests:$true  
```  
  
Nachdem Sie die Unterstützung nach "Zugriff verweigert" konfiguriert haben, müssen Sie sie mithilfe von Gruppenrichtlinien für alle Dateitypen aktivieren.  
  
[Führen Sie diesen Schritt mithilfe von Windows PowerShell aus.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1c)  
  
#### <a name="to-configure-access-denied-assistance-for-all-file-types-by-using-group-policy"></a>So konfigurieren Sie die Unterstützung nach "Zugriff verweigert" mithilfe von Gruppenrichtlinien für alle Dateitypen  
  
1.  Öffnen Sie die Gruppenrichtlinienverwaltung. Klicken Sie in Server-Manager auf **Extras** und dann auf **Gruppenrichtlinienverwaltung**.  
  
2.  Klicken Sie mit der rechten Maustaste auf die entsprechende Gruppenrichtlinie, und klicken Sie dann auf **Bearbeiten**.  
  
3.  Klicken Sie auf **Computerkonfiguration**. Klicken Sie auf **Richtlinien**, auf **Administrative Vorlagen**, auf **System** und dann auf **Unterstützung nach "Zugriff verweigert"** .  
  
4.  Klicken Sie mit der rechten Maustaste auf **Unterstützung nach "Zugriff verweigert" für alle Dateitypen auf dem Client aktivieren**, und klicken Sie dann auf **Bearbeiten**.  
  
5.  Klicken Sie auf **Aktiviert**und dann auf **OK**.  
  
![projektmappenanleitung für](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>entsprechende Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können. 
  
```  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\SOFTWARE\Policies\Microsoft\Windows\Explore" -ValueName EnableShellExecuteFileStreamCheck -Type DWORD -value 1  
  
```  
  
Mithilfe der Konsole des Ressourcen-Managers für Dateiserver können Sie auch eine separate Meldung vom Typ "Zugriff verweigert" für jeden einzelnen freigegebenen Ordner auf einem Dateiserver angeben.  
  
[Führen Sie diesen Schritt mithilfe von Windows PowerShell aus.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1b)  
  
#### <a name="to-specify-a-separate-access-denied-message-for-a-shared-folder-by-using-file-server-resource-manager"></a>So geben Sie mit dem Ressourcen-Manager für Dateiserver eine separate Meldung vom Typ "Zugriff verweigert" für einen freigegebenen Ordner an  
  
1.  Öffnen Sie den Ressourcen-Manager für Dateiserver. Klicken Sie in Server-Manager auf **Extras** und dann auf **Ressourcen-Manager für Dateiserver**.  
  
2.  Erweitern Sie **Ressourcen-Manager für Dateiserver (lokal)** , und klicken Sie dann auf **Klassifizierungsverwaltung**.  
  
3.  Klicken Sie mit der rechten Maustaste auf **Klassifizierungseigenschaften**, und klicken Sie dann auf **Ordnerverwaltungseigenschaften festlegen**.  
  
4.  Klicken Sie im Dialogfeld **Eigenschaften** auf **Unterstützungsmeldung bei Zugriffsverweigerung**, und klicken Sie dann auf **Hinzufügen**.  
  
5.  Klicken Sie auf **Durchsuchen**, und wählen Sie dann den Ordner für die benutzerdefinierte Zugriffsverweigerungsmeldung aus.  
  
6.  Geben Sie im Feld **Wert** die Meldung ein, die Benutzern angezeigt werden soll, wenn ihnen der Zugriff auf eine Ressource in diesem Ordner verweigert wird.  
  
    Sie können der Meldung Makros hinzufügen, durch die benutzerdefinierter Text eingefügt wird. Die Makros umfassen Folgendes:  
  
    -   **[Ursprünglicher Dateipfad]** : Der ursprüngliche Dateipfad, auf den der Benutzer zugegriffen hat  
  
    -   **[Ordner des ursprünglichen Dateipfads]** : Der übergeordnete Ordner mit dem ursprünglichen Dateipfad, auf den der Benutzer zugegriffen hat.  
  
    -   **[Administrator-E-Mail]** : Die Administrator-E-Mail-Empfängerliste  
  
    -   **[Datenbesitzer-E-Mail]** : Die Datenbesitzer-E-Mail-Empfängerliste  
  
7.  Klicken Sie auf **OK** und dann auf **Schließen**.  
  
![projektmappenanleitung für](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>entsprechende Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können. 
  
```  
Set-FSRMMgmtProperty -Namespace "folder path" -Name "AccessDeniedMessage_MS" -Value "Type the text that the user will see in the error message dialog box."  
```  
  
## <a name="step-2-configure-the-email-notification-settings"></a><a name="BKMK_2"></a>Schritt 2: Konfigurieren der e-Mail-Benachrichtigungseinstellungen  
Sie müssen die E-Mail-Benachrichtigungseinstellungen auf jedem Dateiserver konfigurieren, von dem die Meldungen für die Unterstützung nach "Zugriff verweigert" gesendet werden.  
  
[Führen Sie diesen Schritt mithilfe von Windows PowerShell aus.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
1.  Öffnen Sie den Ressourcen-Manager für Dateiserver. Klicken Sie in Server-Manager auf **Extras** und dann auf **Ressourcen-Manager für Dateiserver**.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Ressourcen-Manager für Dateiserver (lokal)** , und klicken Sie dann auf **Optionen konfigurieren**.  
  
3.  Klicken Sie auf die Registerkarte **E-Mail-Benachrichtigungen**.  
  
4.  Konfigurieren Sie die folgenden Einstellungen:  
  
    -   Geben Sie im Feld **SMTP-Servername oder IP-Adresse** den Namen oder die IP-Adresse des SMTP-Servers Ihrer Organisation ein.  
  
    -   Geben Sie in den Feldern **Standard Administrator Empfänger** und **Standard-e-Mail-Adresse** die e-Mail-Adresse des Dateiserver Administrators ein.  
  
5.  Klicken Sie auf **Test-E-Mail senden**, um sicherzustellen, dass die E-Mail-Benachrichtigungen richtig konfiguriert wurden.  
  
6.  Klicken Sie auf **OK**.  
  
![projektmappenanleitung für](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>entsprechende Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.
  
```  
set-FSRMSetting -SMTPServer "server1" -AdminEmailAddress "fileadmin@contoso.com" -FromEmailAddress "fileadmin@contoso.com"  
```  
  
## <a name="step-3-verify-that-access-denied-assistance-is-configured-correctly"></a><a name="BKMK_3"></a>Schritt 3: überprüfen, ob die Unterstützung nach "Zugriff verweigert" richtig konfiguriert ist  
Sie können überprüfen, ob die Unterstützung nach "Zugriff verweigert" ordnungsgemäß konfiguriert ist, indem Sie einen Benutzer mit Windows 8 versuchen, auf eine Freigabe oder eine Datei in dieser Freigabe zuzugreifen, auf die Sie keinen Zugriff haben. Wenn die Meldung "Zugriff verweigert" angezeigt wird, muss die Schaltfläche **Unterstützung anfordern** für den Benutzer verfügbar sein. Nach dem Klicken auf die Schaltfläche "Unterstützung anfordern" kann der Benutzer einen Grund für den Zugriff angeben und dann eine E-Mail an den Besitzer des Ordners oder an den Dateiserveradministrator senden. Der Besitzer des Ordners oder der Dateiserveradministrator kann für Sie überprüfen, ob die E-Mail angekommen ist und die entsprechenden Details enthält.  
  
> [!IMPORTANT]  
> Wenn Sie die Unterstützung nach "Zugriff verweigert" überprüfen möchten, indem Sie einen Benutzer mit Windows Server 2012 verwenden, müssen Sie die Desktop Darstellung installieren, bevor Sie eine Verbindung mit der Dateifreigabe herstellen.  
  
## <a name="see-also"></a><a name="BKMK_Links"></a>Siehe auch  
  
-   [Szenario: Unterstützung nach "Zugriff verweigert"](Scenario--Access-Denied-Assistance.md)  
  
-   [Planen der Unterstützung nach "Zugriff verweigert"](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)  
  
-   [Dynamisches Access Control: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  

