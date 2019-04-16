---
ms.assetid: ee008835-7d3b-4977-adcb-7084c40e5918
title: Bereitstellen der Implementierung der Aufbewahrung von Informationen auf Dateiservern (Schrittezur Veranschaulichung)
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e0f79dd72190888340144bc5c109ee31fa301937
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-implementing-retention-of-information-on-file-servers-demonstration-steps"></a>Bereitstellen der Implementierung der Aufbewahrung von Informationen auf Dateiservern (Schrittezur Veranschaulichung)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Sie können Aufbewahrungsdauer für Ordner festlegen und Dateien auf gesetzliche Aufbewahrungspflicht mithilfe der Dateiklassifizierungsinfrastruktur und File Server Resource Manager bereitstellen.  
  
**In diesem Dokument**  
  
-   [Erforderliche Komponenten](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Prereqs)  
  
-   [Schritt1: Erstellen von ressourceneigenschaftsdefinitionen](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step1)  
  
-   [Schritt2: Konfigurieren von Benachrichtigungen](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md#BKMK_Step2)  
  
-   [Schritt3: Erstellen einer Dateiverwaltungsaufgabe](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step3)  
  
-   [Schritt4: Manuelles Klassifizieren einer Datei](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md#BKMK_Step4)  
  
> [!NOTE]  
> Dieses Thema enthält Beispiel für Windows PowerShell-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Die Schrittein diesem Thema wird davon ausgegangen, dass Sie einen SMTP-Server für dateiablaufbenachrichtigungen konfiguriert haben.  
  
## <a name="BKMK_Step1"></a>Schritt1: Erstellen von ressourceneigenschaftsdefinitionen  
In diesem Schrittkönnen wir die Ressourceneigenschaften für Aufbewahrungsdauer und Erkennbarkeit, sodass die Dateiklassifizierungsinfrastruktur diese Ressourceneigenschaften verwenden können, zum Kennzeichnen von Dateien, die in einem freigegebenen Netzwerkordner gescannt werden.  
  
[Wiederholen Sie diesen Schrittmithilfe von Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)  
  
#### <a name="to-create-resource-property-definitions"></a>Zum Erstellen Sie ressourceneigenschaftsdefinitionen  
  
1.  Melden Sie auf dem Domänencontroller sich an den Server als ein Mitglied der Sicherheitsgruppe "Domänen-Admins".  
  
2.  Active Directory-Verwaltungscenter zu öffnen. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **Active Directory-Verwaltungscenter**.  
  
3.  Erweitern Sie **dynamische Zugriffssteuerung**, und klicken Sie dann auf **Ressourceneigenschaften**.  
  
4.  Mit der rechten Maustaste **Aufbewahrungsdauer**, und klicken Sie dann auf **aktivieren**.  
  
5.  Mit der rechten Maustaste **Auffindbarkeit**, und klicken Sie dann auf **aktivieren**.  
  
![Lösungshandbücher](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Set-ADResourceProperty -Enabled:$true -Identity:'CN=RetentionPeriod_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'  
Set-ADResourceProperty -Enabled:$true -Identity:'CN=Discoverability_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'  
```  
  
## <a name="BKMK_Step2"></a>Schritt2: Konfigurieren von Benachrichtigungen  
In diesem Schrittverwenden wir die File Server Resource Manager-Konsole zum Konfigurieren der SMTP-Server, der standardmäßige Administrator E-Mail-Adresse und die standardmäßige E-Mail-Adresse, der die Berichte gesendet werden.  
  
[Wiederholen Sie diesen Schrittmithilfe von Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)  
  
#### <a name="to-configure-notifications"></a>Konfigurieren von Benachrichtigungen  
  
1.  Melden Sie sich mit dem Dateiserver als Mitglied der Sicherheitsgruppe "Administratoren".  
  
2.  Geben Sie in der Windows PowerShell-Eingabeaufforderung **Update-FsrmClassificationPropertyDefinition**, und drücken Sie dann die EINGABETASTE. Dadurch werden die Eigenschaftsdefinitionen synchronisiert, die auf dem Domänencontroller, auf dem Dateiserver erstellt werden.  
  
3.  File Server Resource Manager zu öffnen. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **File Server Resource Manager**.  
  
4.  Mit der rechten Maustaste **File Server Resource Manager (lokal)**, und klicken Sie dann auf **Optionen konfigurieren**.  
  
5.  Auf der **E-Mail-Benachrichtigungen** Registerkarte, konfigurieren Sie Folgendes:  
  
    -   In der **SMTP-Servername oder IP-Adresse** geben den Namen des SMTP-Servers im Netzwerk.  
  
    -   In der **Standardadministratorempfänger** geben die E-Mail-Adresse des Administrators, der die Benachrichtigung erhalten sollen.  
  
    -   In der **Standard-E-Mail-Adresse** Geben Sie die E-Mail-Adresse, die Senden von Benachrichtigungen verwendet werden soll.  
  
6.  Klicken Sie auf **OK**.  
  
![Lösungshandbücher](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
Set-FsrmSetting -SmtpServer IP address of SMTP server -FromEmailAddress "FromEmailAddress" -AdminEmailAddress "AdministratorEmailAddress"  
```  
  
## <a name="BKMK_Step3"></a>Schritt3: Erstellen einer Dateiverwaltungsaufgabe  
In diesem Schrittverwenden wir die File Server Resource Manager-Konsole eine Dateiverwaltungsaufgabe zu erstellen, die am letzten Tag des Monats ausgeführt wird, und laufen alle Dateien mit den folgenden Kriterien:  
  
-   Die Datei wird nicht als rechtlicher Aufbewahrungspflicht klassifiziert.  
  
-   Die Datei wird mit einer langfristigen Aufbewahrungsdauer klassifiziert.  
  
-   Die Datei wurde in den letzten 10Jahren nicht geändert wurde.  
  
[Wiederholen Sie diesen Schrittmithilfe von Windows PowerShell](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep3)  
  
#### <a name="to-create-a-file-management-task"></a>Um eine Dateiverwaltungsaufgabe zu erstellen.  
  
1.  Melden Sie sich mit dem Dateiserver als Mitglied der Sicherheitsgruppe "Administratoren".  
  
2.  File Server Resource Manager zu öffnen. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **File Server Resource Manager**.  
  
3.  Mit der rechten Maustaste **Dateiverwaltungsaufgaben**, und klicken Sie dann auf **Dateiverwaltungsaufgabe erstellen**.  
  
4.  Auf der **allgemeine** Registerkarte die **den Namen der Aufgabe** geben einen Namen für die Dateiverwaltungsaufgabe, z.B. Beibehaltungsdauer Aufgabe.  
  
5.  Auf der **Bereich** auf **hinzufügen**, und wählen Sie die Ordner, die in dieser Regel, z.B. "D:\Finance Documents" einbezogen werden sollen.  
  
6.  Auf der **Aktion** Registerkarte die **Typ** auf **Dateiablauf**. In der **Ablaufverzeichnis** Geben Sie einen Pfad zu einem Ordner auf dem lokalen Server, in denen die abgelaufenen Dateien verschoben werden. In diesem Ordner sollte eine Zugriffssteuerungsliste verfügen, die nur dateiserveradministratoren den Zugriff gewährt.  
  
7.  Auf der **Benachrichtigung** auf **hinzufügen**.  
  
    -   Wählen Sie die **E-Mail an folgenden Administratoren senden** Kontrollkästchen.  
  
    -   Wählen Sie die **eine E-Mail an Benutzer senden, deren Dateien betroffen sind**, und klicken Sie dann auf **OK**.  
  
8.  Auf der **Bedingung** auf **hinzufügen**, und fügen Sie die folgenden Eigenschaften:  
  
    -   In der **Eigenschaft** auf **Auffindbarkeit**. In der **Operator** auf **nicht gleich**. In der **Wert** auf **halten**.  
  
    -   In der **Eigenschaft** auf **Aufbewahrungsdauer**. In der **Operator** auf **gleich**. In der **Wert** auf **langfristigen**.  
  
9. Auf der **Bedingung** Registerkarte die **Tage seit der letzten dateiänderung**, und legen Sie den Wert auf **3650**.  
  
10. Auf der **Zeitplan** auf die **monatlichen** aus, und wählen Sie dann die **letzten** Kontrollkästchen.  
  
11. Klicken Sie auf **OK**.  
  
![Lösungshandbücher](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***  
  
Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
$fmjexpiration = New-FSRMFmjAction -Type 'Expiration' -ExpirationFolder folder  
$fmjNotificationAction = New-FsrmFmjNotificationAction -Type Email -MailTo "[FileOwner],[AdminEmail]"  
$fmjNotification = New-FsrmFMJNotification -Days 10 -Action @($fmjNotificationAction)  
$fmjCondition1 = New-FSRMFmjCondition -Property 'Discoverability_MS' -Condition 'NotEqual' -Value "Hold" 
$fmjCondition2 = New-FSRMFmjCondition -Property 'RetentionPeriod_MS' -Condition 'Equal' -Value "Long-term"  
$fmjCondition3 = New-FSRMFmjCondition -Property 'File.DateLastAccessed' -Condition 'Equal' -Value 3650  
$date = get-date  
$schedule = New-FsrmScheduledTask -Time $date -Monthly @(-1)    
$fmj1=New-FSRMFileManagementJob -Name "Retention Task" -Namespace @('D:\Finance Documents') -Action $fmjexpiration -Schedule $schedule -Notification @($fmjNotification) -Condition @( $fmjCondition1, $fmjCondition2, $fmjCondition3)  
```  
  
## <a name="BKMK_Step4"></a>Schritt4: Manuelles Klassifizieren einer Datei  
Manuelles klassifizieren wir in diesem Schrittwird eine Datei, um eine rechtliche Aufbewahrungspflicht zuweisen werden. Der übergeordnete Ordner dieser Datei wird mit einer langfristigen Aufbewahrungsdauer klassifiziert.  
  
#### <a name="to-manually-classify-a-file"></a>Zum manuellen Klassifizieren einer Datei  
  
1.  Melden Sie sich mit dem Dateiserver als Mitglied der Sicherheitsgruppe "Administratoren".  
  
2.  Navigieren Sie zu dem Ordner, der im Rahmen der Dateiverwaltungsaufgabe in Schritt3 erstellte konfiguriert wurde.  
  
3.  Maustaste auf den Ordner, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Auf der **Klassifizierung** auf **Aufbewahrungsdauer**, klicken Sie auf **langfristigen**, und klicken Sie dann auf **OK**.  
  
5.  Maustaste auf eine Datei in diesem Ordner, und klicken Sie dann auf **Eigenschaften**.  
  
6.  Auf der **Klassifizierung** auf **Auffindbarkeit**, klicken Sie auf **halten**, klicken Sie auf **übernehmen**, und klicken Sie dann auf **OK**.  
  
7.  Führen Sie auf dem Dateiserver die Dateiverwaltungsaufgabe mithilfe der Ressourcen-Manager-Konsole. Nachdem die Dateiverwaltungsaufgabe abgeschlossen ist, prüfen Sie den Ordner, und stellen Sie sicher, dass die Datei nicht in das Ablaufverzeichnis verschoben wurde.  
  
8.  Maustaste auf die gleiche Datei in diesem Ordner, und klicken Sie dann auf **Eigenschaften**.  
  
9. Auf der **Klassifizierung** auf **Auffindbarkeit**, klicken Sie auf **nicht zutreffend**, klicken Sie auf **übernehmen**, und klicken Sie dann auf **OK**.  
  
10. Auf dem Dateiserver die Dateiverwaltungsaufgabe erneut mithilfe der Ressourcen-Manager-Konsole ausführen. Nachdem die Dateiverwaltungsaufgabe abgeschlossen ist, prüfen Sie den Ordner, und stellen Sie sicher, dass die Datei in das Ablaufverzeichnis verschoben wurde.  
  
## <a name="BKMK_Links"></a>Siehe auch  
  
-   [Szenario: Implementieren der Aufbewahrung von Informationen auf Dateiservern](Scenario--Implement-Retention-of-Information-on-File-Servers.md)  
  
-   [Planen der Aufbewahrung von Informationen auf Dateiservern](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)  
  
-   [Dynamische Zugriffssteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  

