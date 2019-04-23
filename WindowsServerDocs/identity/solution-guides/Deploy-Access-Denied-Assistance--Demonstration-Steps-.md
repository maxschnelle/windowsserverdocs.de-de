---
ms.assetid: b035e9f8-517f-432a-8dfb-40bfc215bee5
title: Bereitstellen der Unterstützung nach %%amp;quot;Zugriff verweigert%%amp;quot; (Schritte zur Veranschaulichung)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5201441ba884fe4658b917919e60c7d20530341b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835581"
---
# <a name="deploy-access-denied-assistance-demonstration-steps"></a>Bereitstellen der Unterstützung nach %%amp;quot;Zugriff verweigert%%amp;quot; (Schritte zur Veranschaulichung)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird erläutert, wie Sie die Unterstützung nach "Zugriff verweigert" konfigurieren und überprüfen, ob diese ordnungsgemäß funktioniert.  
  
**In diesem Dokument**  
  
-   [Schritt 1: Konfigurieren von Zugriff](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_1)  
  
-   [Schritt 2: Konfigurieren Sie die e-Mail-Benachrichtigungseinstellungen](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_2)  
  
-   [Schritt 3: Stellen Sie sicher, dass der Zugriff ordnungsgemäß konfiguriert ist](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_3)  
  
> [!NOTE]  
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="BKMK_1"></a>Schritt 1: Konfigurieren der Unterstützung nach "Zugriff verweigert"  
Sie können die Unterstützung nach "Zugriff verweigert" in einer Domäne mithilfe von Gruppenrichtlinien konfigurieren. Sie haben aber auch die Möglichkeit, die Unterstützung über die Konsole des Ressourcen-Managers für Dateiserver einzeln auf jedem Dateiserver zu konfigurieren. Sie können auch die Meldung "Zugriff verweigert" für einen bestimmten freigegebenen Ordner auf einem Dateiserver ändern.  
  
Sie können die Unterstützung nach "Zugriff verweigert" für die Domäne mithilfe von Gruppenrichtlinien wie folgt konfigurieren:  
  
[Führen Sie diesen Schritt mithilfe von Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-configure-access-denied-assistance-by-using-group-policy"></a>So konfigurieren Sie die Unterstützung nach "Zugriff verweigert" mithilfe von Gruppenrichtlinien  
  
1.  Öffnen Sie die Gruppenrichtlinienverwaltung. Klicken Sie in Server-Manager auf **Extras** und dann auf **Gruppenrichtlinienverwaltung**.  
  
2.  Klicken Sie mit der rechten Maustaste auf die entsprechende Gruppenrichtlinie, und klicken Sie dann auf **Bearbeiten**.  
  
3.  Klicken Sie auf **Computerkonfiguration**. Klicken Sie auf **Richtlinien**, auf **Administrative Vorlagen**, auf **System** und dann auf **Unterstützung nach "Zugriff verweigert"**.  
  
4.  Klicken Sie mit der rechten Maustaste auf **Meldung für Zugriffsverweigerungsfehler anpassen**, und klicken Sie dann auf **Bearbeiten**.  
  
5.  Aktivieren Sie die Option **Aktiviert**.  
  
6.  Konfigurieren Sie folgende Optionen:  
  
    1.  Geben Sie im Feld **Benutzern, denen der Zugriff auf einen Ordner oder eine Datei verweigert wird, die folgende Meldung anzeigen** die Meldung ein, die Benutzern angezeigt werden soll, wenn ihnen der Zugriff auf eine Datei oder einen Ordner verweigert wird.  
  
        Sie können der Meldung Makros hinzufügen, durch die benutzerdefinierter Text eingefügt wird. Die Makros umfassen Folgendes:  
  
        -   **[Ursprünglicher Dateipfad]** : Der ursprüngliche Dateipfad, auf den der Benutzer zugegriffen hat  
  
        -   **[Ordner des ursprünglichen Dateipfads]** : Der übergeordnete Ordner mit dem ursprünglichen Dateipfad, auf den der Benutzer zugegriffen hat.  
  
        -   **[Administrator-E-Mail]** : Die Administrator-E-Mail-Empfängerliste  
  
        -   **[Datenbesitzer-E-Mail]** : Die Datenbesitzer-E-Mail-Empfängerliste  
  
    2.  Aktivieren Sie das Kontrollkästchen **Benutzern das Anfordern von Unterstützung ermöglichen** .  
  
    3.  Übernehmen Sie die restlichen Standardeinstellungen.  
  
![Lösungshandbücher](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
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
  
[Führen Sie diesen Schritt mithilfe von Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1a)  
  
#### <a name="to-configure-access-denied-assistance-by-using-file-server-resource-manager"></a>So konfigurieren Sie die Unterstützung nach "Zugriff verweigert" mit dem Ressourcen-Manager für Dateiserver  
  
1.  Öffnen Sie den Ressourcen-Manager für Dateiserver. Klicken Sie in Server-Manager auf **Extras** und dann auf **Ressourcen-Manager für Dateiserver**.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Ressourcen-Manager für Dateiserver (lokal)**, und klicken Sie dann auf **Optionen konfigurieren**.  
  
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
  
![Lösungshandbücher](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.
  
```  
Set-FSRMAdrSetting -Event "AccessDenied" -DisplayMessage "Type the text that the user will see in the error message dialog box." -Enabled:$true -AllowRequests:$true  
```  
  
Nachdem Sie die Unterstützung nach "Zugriff verweigert" konfiguriert haben, müssen Sie sie mithilfe von Gruppenrichtlinien für alle Dateitypen aktivieren.  
  
[Führen Sie diesen Schritt mithilfe von Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1c)  
  
#### <a name="to-configure-access-denied-assistance-for-all-file-types-by-using-group-policy"></a>So konfigurieren Sie die Unterstützung nach "Zugriff verweigert" mithilfe von Gruppenrichtlinien für alle Dateitypen  
  
1.  Öffnen Sie die Gruppenrichtlinienverwaltung. Klicken Sie in Server-Manager auf **Extras** und dann auf **Gruppenrichtlinienverwaltung**.  
  
2.  Klicken Sie mit der rechten Maustaste auf die entsprechende Gruppenrichtlinie, und klicken Sie dann auf **Bearbeiten**.  
  
3.  Klicken Sie auf **Computerkonfiguration**. Klicken Sie auf **Richtlinien**, auf **Administrative Vorlagen**, auf **System** und dann auf **Unterstützung nach "Zugriff verweigert"**.  
  
4.  Klicken Sie mit der rechten Maustaste auf **Unterstützung nach "Zugriff verweigert" für alle Dateitypen auf dem Client aktivieren**, und klicken Sie dann auf **Bearbeiten**.  
  
5.  Klicken Sie auf **Aktiviert**und dann auf **OK**.  
  
![Lösungshandbücher](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind. 
  
```  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\SOFTWARE\Policies\Microsoft\Windows\Explore" -ValueName EnableShellExecuteFileStreamCheck -Type DWORD -value 1  
  
```  
  
Mithilfe der Konsole des Ressourcen-Managers für Dateiserver können Sie auch eine separate Meldung vom Typ "Zugriff verweigert" für jeden einzelnen freigegebenen Ordner auf einem Dateiserver angeben.  
  
[Führen Sie diesen Schritt mithilfe von Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1b)  
  
#### <a name="to-specify-a-separate-access-denied-message-for-a-shared-folder-by-using-file-server-resource-manager"></a>So geben Sie mit dem Ressourcen-Manager für Dateiserver eine separate Meldung vom Typ "Zugriff verweigert" für einen freigegebenen Ordner an  
  
1.  Öffnen Sie den Ressourcen-Manager für Dateiserver. Klicken Sie in Server-Manager auf **Extras** und dann auf **Ressourcen-Manager für Dateiserver**.  
  
2.  Erweitern Sie **Ressourcen-Manager für Dateiserver (lokal)**, und klicken Sie dann auf **Klassifizierungsverwaltung**.  
  
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
  
![Lösungshandbücher](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind. 
  
```  
Set-FSRMMgmtProperty -Namespace "folder path" -Name "AccessDeniedMessage_MS" -Value "Type the text that the user will see in the error message dialog box."  
```  
  
## <a name="BKMK_2"></a>Schritt 2: Konfigurieren der E-Mail-Benachrichtigungseinstellungen  
Sie müssen die E-Mail-Benachrichtigungseinstellungen auf jedem Dateiserver konfigurieren, von dem die Meldungen für die Unterstützung nach "Zugriff verweigert" gesendet werden.  
  
[Führen Sie diesen Schritt mithilfe von Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
1.  Öffnen Sie den Ressourcen-Manager für Dateiserver. Klicken Sie in Server-Manager auf **Extras** und dann auf **Ressourcen-Manager für Dateiserver**.  
  
2.  Klicken Sie mit der rechten Maustaste auf **Ressourcen-Manager für Dateiserver (lokal)**, und klicken Sie dann auf **Optionen konfigurieren**.  
  
3.  Klicken Sie auf die Registerkarte **E-Mail-Benachrichtigungen**.  
  
4.  Konfigurieren Sie die folgenden Einstellungen:  
  
    -   Geben Sie im Feld **SMTP-Servername oder IP-Adresse** den Namen oder die IP-Adresse des SMTP-Servers Ihrer Organisation ein.  
  
    -   In der **Standardadministratorempfänger** und **standardmäßig 'aus-e Mailadresse** geben die e-Mail-Adresse den dateiserveradministrator.  
  
5.  Klicken Sie auf **Test-E-Mail senden**, um sicherzustellen, dass die E-Mail-Benachrichtigungen richtig konfiguriert wurden.  
  
6.  Klicken Sie auf **OK**.  
  
![Lösungshandbücher](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.
  
```  
set-FSRMSetting -SMTPServer "server1" -AdminEmailAddress "fileadmin@contoso.com" -FromEmailAddress "fileadmin@contoso.com"  
```  
  
## <a name="BKMK_3"></a>Schritt 3: Überprüfen der ordnungsgemäßen Konfiguration der Unterstützung nach "Zugriff verweigert"  
Sie können überprüfen, ob die Zugriff verweigert-Unterstützung durch einen Benutzer mit Windows 8 wiederholen Sie den Zugriff auf eine Freigabe oder eine Datei im, die gemeinsam nutzen, dass sie den Zugriff auf keine läuft ordnungsgemäß konfiguriert ist. Wenn die Meldung "Zugriff verweigert" angezeigt wird, muss die Schaltfläche **Unterstützung anfordern** für den Benutzer verfügbar sein. Nach dem Klicken auf die Schaltfläche "Unterstützung anfordern" kann der Benutzer einen Grund für den Zugriff angeben und dann eine E-Mail an den Besitzer des Ordners oder an den Dateiserveradministrator senden. Der Besitzer des Ordners oder der Dateiserveradministrator kann für Sie überprüfen, ob die E-Mail angekommen ist und die entsprechenden Details enthält.  
  
> [!IMPORTANT]  
> Wenn Sie möchten Zugriff zu überprüfen, indem Sie einen Benutzer mit Windows Server 2012 ausgeführt wird, müssen Sie die Desktopdarstellung installieren, vor dem Herstellen einer Verbindung mit der Dateifreigabe.  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Szenario: Zugriff](Scenario--Access-Denied-Assistance.md)  
  
-   [Planen der Unterstützung nach den Zugriff verweigert](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)  
  
-   [Dynamische Zugriffssteuerung: Übersicht über das Szenario](Dynamic-Access-Control--Scenario-Overview.md)  
  

