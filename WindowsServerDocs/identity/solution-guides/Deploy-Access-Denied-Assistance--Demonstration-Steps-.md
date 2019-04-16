---
ms.assetid: b035e9f8-517f-432a-8dfb-40bfc215bee5
title: Bereitstellen von "Zugriff verweigert" Assistance (Demonstration Steps)
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5201441ba884fe4658b917919e60c7d20530341b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-access-denied-assistance-demonstration-steps"></a>Bereitstellen von "Zugriff verweigert" Assistance (Demonstration Steps)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema erläutert das Konfigurieren der Unterstützung nach "Zugriff verweigert", und stellen Sie sicher, dass er ordnungsgemäß ausgeführt wird.  
  
**In diesem Dokument**  
  
-   [Schritt1: Konfigurieren der Unterstützung nach "Zugriff verweigert"](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_1)  
  
-   [Schritt2: Konfigurieren der E-Mail-Benachrichtigungseinstellungen](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_2)  
  
-   [Schritt3: Stellen Sie sicher, dass die Unterstützung nach "Zugriff verweigert" richtig konfiguriert ist](Deploy-Access-Denied-Assistance--Demonstration-Steps-.md#BKMK_3)  
  
> [!NOTE]  
> Dieses Thema enthält Beispiel für Windows PowerShell-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="BKMK_1"></a>Schritt1: Konfigurieren der Unterstützung nach "Zugriff verweigert"  
Sie können die Unterstützung nach "Zugriff verweigert" in einer Domäne mithilfe von Gruppenrichtlinien konfigurieren, oder Sie können Konfigurieren der Unterstützung einzeln auf jedem Dateiserver mithilfe der Ressourcen-Manager-Konsole. Sie können auch die Meldung "Zugriff verweigert" für einen bestimmten freigegebenen Ordner auf einem Dateiserver ändern.  
  
Sie können "Zugriff verweigert" Unterstützung für die Domäne mithilfe von Gruppenrichtlinien wie folgt konfigurieren:  
  
[Wiederholen Sie diesen Schrittmithilfe von Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-configure-access-denied-assistance-by-using-group-policy"></a>So konfigurieren Sie die Unterstützung nach "Zugriff verweigert" mithilfe von Gruppenrichtlinien  
  
1.  Öffnen Sie die Gruppenrichtlinien-Management. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **Gruppenrichtlinienverwaltung**.  
  
2.  Maustaste auf die entsprechende Gruppenrichtlinie, und klicken Sie dann auf **bearbeiten**.  
  
3.  Klicken Sie auf **Computerkonfiguration**, klicken Sie auf **Richtlinien**, klicken Sie auf **Administrative Vorlagen**, klicken Sie auf **System**, und klicken Sie dann auf **Denied Assistance**.  
  
4.  Mit der rechten Maustaste **anpassen Meldung für Zugriffsverweigerungsfehler**, und klicken Sie dann auf **bearbeiten**.  
  
5.  Wählen Sie die **aktiviert** Option.  
  
6.  Konfigurieren Sie die folgenden Optionen:  
  
    1.  In der **für Benutzer, die der Zugriff verweigert werden die folgende Meldung anzeigen** geben eine Meldung, dass Benutzer angezeigt werden, wenn sie den Zugriff auf eine Datei oder einen Ordner verweigert wird.  
  
        Sie können die Meldung Makros hinzufügen, die benutzerdefinierter Text eingefügt wird. Die Makros umfassen Folgendes:  
  
        -   **[Ursprünglicher Dateipfad] **Der ursprüngliche Dateipfad, die vom Benutzer auf die zugegriffen wurde.  
  
        -   **[Ordner der ursprünglichen Datei Pfad] **Der übergeordnete Ordner des ursprünglichen Dateipfads, die vom Benutzer auf die zugegriffen wurde.  
  
        -   **[Administrator E-Mail] **Die Administrator-E-Mail-Empfängerliste.  
  
        -   **[Daten Besitzer E-Mail] **Der Daten Besitzer E-Mail-Empfängerliste.  
  
    2.  Wählen Sie die **ermöglichen Benutzern das Anfordern von Unterstützung** Kontrollkästchen.  
  
    3.  Lassen Sie die restlichen Standardeinstellungen.  
  
![Lösungshandbücher](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
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
  
Alternativ können Sie Unterstützung nach "Zugriff verweigert" einzeln auf jedem Dateiserver konfigurieren mithilfe der Ressourcen-Manager-Konsole.  
  
[Wiederholen Sie diesen Schrittmithilfe von Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1a)  
  
#### <a name="to-configure-access-denied-assistance-by-using-file-server-resource-manager"></a>So konfigurieren Sie die Unterstützung nach "Zugriff verweigert" mithilfe des File Server Resource Manager  
  
1.  File Server Resource Manager zu öffnen. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **File Server Resource Manager**.  
  
2.  Mit der rechten Maustaste **File Server Resource Manager (lokal)**, und klicken Sie dann auf **Optionen konfigurieren**.  
  
3.  Klicken Sie auf die **Denied Assistance** Registerkarte.  
  
4.  Wählen Sie die **Aktivieren der Unterstützung nach "Zugriff verweigert"** Kontrollkästchen.  
  
5.  In der **für Benutzer, die Zugriff auf die Datei oder einen Ordner verweigert werden die folgende Meldung anzeigen** geben eine Meldung, dass Benutzer angezeigt werden, wenn sie den Zugriff auf eine Datei oder einen Ordner verweigert wird.  
  
    Sie können die Meldung Makros hinzufügen, die benutzerdefinierter Text eingefügt wird. Die Makros umfassen Folgendes:  
  
    -   **[Ursprünglicher Dateipfad] **Der ursprüngliche Dateipfad, die vom Benutzer auf die zugegriffen wurde.  
  
    -   **[Ordner der ursprünglichen Datei Pfad] **Der übergeordnete Ordner des ursprünglichen Dateipfads, die vom Benutzer auf die zugegriffen wurde.  
  
    -   **[Administrator E-Mail] **Die Administrator-E-Mail-Empfängerliste.  
  
    -   **[Daten Besitzer E-Mail] **Der Daten Besitzer E-Mail-Empfängerliste.  
  
6.  Klicken Sie auf **E-Mail-Anforderungen konfigurieren**, wählen die **ermöglichen Benutzern das Anfordern von Unterstützung**, und klicken Sie dann auf **OK**.  
  
7.  Klicken Sie auf **Preview** sollten Sie sehen, wie die Fehlermeldung für den Benutzer angezeigt wird.  
  
8.  Klicken Sie auf **OK**.  
  
![Lösungshandbücher](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.
  
```  
Set-FSRMAdrSetting -Event "AccessDenied" -DisplayMessage "Type the text that the user will see in the error message dialog box." -Enabled:$true -AllowRequests:$true  
```  
  
Nachdem Sie die Unterstützung nach "Zugriff verweigert" konfiguriert haben, müssen Sie es mithilfe von Gruppenrichtlinien für alle Dateitypen aktivieren.  
  
[Wiederholen Sie diesen Schrittmithilfe von Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1c)  
  
#### <a name="to-configure-access-denied-assistance-for-all-file-types-by-using-group-policy"></a>So konfigurieren Sie die Unterstützung nach "Zugriff verweigert" für alle Dateitypen mithilfe von Gruppenrichtlinien  
  
1.  Öffnen Sie die Gruppenrichtlinien-Management. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **Gruppenrichtlinienverwaltung**.  
  
2.  Maustaste auf die entsprechende Gruppenrichtlinie, und klicken Sie dann auf **bearbeiten**.  
  
3.  Klicken Sie auf **Computerkonfiguration**, klicken Sie auf **Richtlinien**, klicken Sie auf **Administrative Vorlagen**, klicken Sie auf **System**, und klicken Sie dann auf **Denied Assistance**.  
  
4.  Mit der rechten Maustaste **"Zugriff verweigert"-Unterstützung auf Clients aktivieren, für alle Dateitypen**, und klicken Sie dann auf **bearbeiten**.  
  
5.  Klicken Sie auf **aktiviert**, und klicken Sie dann auf **OK**.  
  
![Lösungshandbücher](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind. 
  
```  
Set-GPRegistryValue -Name "Name of GPO" -key "HKLM\SOFTWARE\Policies\Microsoft\Windows\Explore" -ValueName EnableShellExecuteFileStreamCheck -Type DWORD -value 1  
  
```  
  
Sie können auch eine separate Meldung der "Zugriff verweigert" für jeden freigegebenen Ordner auf einem Dateiserver angeben, mit der File Server Resource Manager-Konsole.  
  
[Wiederholen Sie diesen Schrittmithilfe von Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1b)  
  
#### <a name="to-specify-a-separate-access-denied-message-for-a-shared-folder-by-using-file-server-resource-manager"></a>So geben Sie eine separate Meldung der "Zugriff verweigert" für einen freigegebenen Ordner mit File Server Resource Manager  
  
1.  File Server Resource Manager zu öffnen. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **File Server Resource Manager**.  
  
2.  Erweitern Sie **File Server Resource Manager (lokal)**, und klicken Sie dann auf **Klassifizierungsverwaltung**.  
  
3.  Mit der rechten Maustaste **Klassifizierungseigenschaften**, und klicken Sie dann auf **Ordnerverwaltungseigenschaften festlegen**.  
  
4.  In der **Eigenschaft** auf **Unterstützungsmeldung**, und klicken Sie dann auf **hinzufügen**.  
  
5.  Klicken Sie auf **Durchsuchen**, und wählen Sie dann den Ordner, der die benutzerdefinierte Meldung "Zugriff verweigert".  
  
6.  In der **Wert** geben die Meldung, die für den Benutzer angezeigt werden soll, wenn sie eine Ressource in diesem Ordner zugreifen können.  
  
    Sie können die Meldung Makros hinzufügen, die benutzerdefinierter Text eingefügt wird. Die Makros umfassen Folgendes:  
  
    -   **[Ursprünglicher Dateipfad] **Der ursprüngliche Dateipfad, die vom Benutzer auf die zugegriffen wurde.  
  
    -   **[Ordner der ursprünglichen Datei Pfad] **Der übergeordnete Ordner des ursprünglichen Dateipfads, die vom Benutzer auf die zugegriffen wurde.  
  
    -   **[Administrator E-Mail] **Die Administrator-E-Mail-Empfängerliste.  
  
    -   **[Daten Besitzer E-Mail] **Der Daten Besitzer E-Mail-Empfängerliste.  
  
7.  Klicken Sie auf **OK**, und klicken Sie dann auf **schließen**.  
  
![Lösungshandbücher](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind. 
  
```  
Set-FSRMMgmtProperty -Namespace "folder path" -Name "AccessDeniedMessage_MS" -Value "Type the text that the user will see in the error message dialog box."  
```  
  
## <a name="BKMK_2"></a>Schritt2: Konfigurieren der E-Mail-Benachrichtigungseinstellungen  
Sie müssen die E-Mail-Benachrichtigungseinstellungen auf jedem Dateiserver konfigurieren, die die Unterstützung nach "Zugriff verweigert"-Nachrichten senden soll.  
  
[Wiederholen Sie diesen Schrittmithilfe von Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
1.  File Server Resource Manager zu öffnen. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **File Server Resource Manager**.  
  
2.  Mit der rechten Maustaste **File Server Resource Manager (lokal)**, und klicken Sie dann auf **Optionen konfigurieren**.  
  
3.  Klicken Sie auf die **E-Mail-Benachrichtigungen** Registerkarte.  
  
4.  Konfigurieren Sie die folgenden Einstellungen:  
  
    -   In der **SMTP-Servername oder IP-Adresse** geben den Namen der IP-Adresse des SMTP-Servers in Ihrer Organisation.  
  
    -   In der **Standardadministratorempfänger** und **Standard "Von" E-Mail-Adresse** Dialogfelder, geben Sie die E-Mail-Adresse des Dateiserver-Administrator.  
  
5.  Klicken Sie auf **Test E-Mail senden** um sicherzustellen, dass die E-Mail-Benachrichtigungen richtig konfiguriert sind.  
  
6.  Klicken Sie auf **OK**.  
  
![Lösungshandbücher](media/Deploy-Access-Denied-Assistance--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.
  
```  
set-FSRMSetting -SMTPServer "server1" -AdminEmailAddress "fileadmin@contoso.com" -FromEmailAddress "fileadmin@contoso.com"  
```  
  
## <a name="BKMK_3"></a>Schritt3: Stellen Sie sicher, dass die Unterstützung nach "Zugriff verweigert" richtig konfiguriert ist  
Sie können überprüfen, ob die Unterstützung nach "Zugriff verweigert" richtig konfiguriert ist, dass ein Benutzer, die Windows8, versuchen Sie, auf eine Freigabe oder eine Datei im, die gemeinsam nutzen, dass sie nicht den Zugriff auf ausgeführt wird. Wenn die Meldung "Zugriff verweigert" angezeigt wird, sollte der Benutzer finden Sie unter einem **Unterstützung anfordern** Schaltfläche. Der Benutzer kann nach dem Klicken auf die Schaltfläche "Unterstützung anfordern", geben Sie einen Grund für den Zugriff auf und klicken Sie dann eine E-Mail an den Besitzer des Ordners oder der dateiserveradministrator senden. Der Besitzer des Ordners oder der Dateiserver-Administrator können Sie überprüfen, ob die E-Mail angekommen ist und die entsprechenden Detail enthält.  
  
> [!IMPORTANT]  
> Wenn Sie möchten Unterstützung nach "Zugriff verweigert" überprüfen, indem Sie einen Benutzer, die Windows Server2012 ausgeführt wird, müssen Sie die Desktopdarstellung installieren, vor dem Herstellen einer Verbindung mit der Dateifreigabe.  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Szenario: Unterstützung nach "Zugriff verweigert"](Scenario--Access-Denied-Assistance.md)  
  
-   [Planen der Unterstützung nach "Zugriff verweigert"](assetId:///b169f0a4-8b97-4da8-ae4a-c8f1986d19e1)  
  
-   [Dynamische Zugriffssteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  

