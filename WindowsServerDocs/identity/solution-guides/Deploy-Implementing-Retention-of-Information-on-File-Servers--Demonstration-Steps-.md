---
ms.assetid: ee008835-7d3b-4977-adcb-7084c40e5918
title: Deploy Implementing Retention of Information on File Servers (Demonstration Steps)
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 987d1af004955d7be75066de7a859272e656ffbc
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952801"
---
# <a name="deploy-implementing-retention-of-information-on-file-servers-demonstration-steps"></a>Deploy Implementing Retention of Information on File Servers (Demonstration Steps)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mithilfe der Dateiklassifizierungsinfrastruktur und dem Ressourcen-Manager für Dateiserver können Sie die Aufbewahrungsdauer für Ordner festlegen und Dateien eine rechtliche Aufbewahrungspflicht zuweisen.

**Inhalt dieses Dokuments**

-   [Voraussetzungen](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Prereqs)

-   [Schritt 1: Erstellen von Ressourceneigenschaftsdefinitionen](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step1)

-   [Schritt 2: Konfigurieren von Benachrichtigungen](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md#BKMK_Step2)

-   [„Schritt 3: Erstellen einer Dateiverwaltungsaufgabe](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_Step3)

-   [Schritt 4: Manuelles Klassifizieren einer Datei](Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-.md#BKMK_Step4)

> [!NOTE]
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [Verwenden von Cmdlets](https://go.microsoft.com/fwlink/p/?linkid=230693).

## <a name="prerequisites"></a>Voraussetzungen
Für die Schritte in diesem Thema wird angenommen, dass Sie einen SMTP-Server für Dateiablaufbenachrichtigungen konfiguriert haben.

## <a name="step-1-create-resource-property-definitions"></a><a name="BKMK_Step1"></a>Schritt 1: Erstellen von Ressourceneigenschaftsdefinitionen
In diesem Schritt werden die Ressourceneigenschaften für Aufbewahrungsdauer und Erkennbarkeit aktiviert, sodass diese Ressourceneigenschaften von der Dateiklassifizierungsinfrastruktur zum Kennzeichnen von Dateien verwendet werden können, die in einem freigegebenen Netzwerkordner gescannt werden.

[Führen Sie diesen Schritt mit Windows PowerShell aus.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep1)

#### <a name="to-create-resource-property-definitions"></a>So erstellen Sie Ressourceneigenschaftsdefinitionen

1.  Melden Sie sich auf dem Domänencontroller beim Server als Mitglied der Sicherheitsgruppe "Domänen-Admins" an.

2.  Öffnen Sie das Active Directory-Verwaltungscenter. Klicken Sie im Server-Manager auf **Extras** und dann auf **Active Directory-Verwaltungscenter**.

3.  Erweitern Sie **Dynamische Zugriffssteuerung**, und klicken Sie dann auf **Ressourceneigenschaften**.

4.  Klicken Sie mit der rechten Maustaste auf **Aufbewahrungsdauer**, und klicken Sie dann auf **Aktivieren**.

5.  Klicken Sie mit der rechten Maustaste auf **Erkennbarkeit**, und klicken Sie dann auf **Aktivieren**.

![projektmappenhandbücher](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>äquivalente Windows PowerShell-Befehle</em>***

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```
Set-ADResourceProperty -Enabled:$true -Identity:'CN=RetentionPeriod_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'
Set-ADResourceProperty -Enabled:$true -Identity:'CN=Discoverability_MS,CN=Resource Properties,CN=Claims Configuration,CN=Services,CN=Configuration,DC=contoso,DC=com'
```

## <a name="step-2-configure-notifications"></a><a name="BKMK_Step2"></a>Schritt 2: Konfigurieren von Benachrichtigungen
In diesem Schritt wird die Konsole für den Ressourcen-Manager für Dateiserver zum Konfigurieren des SMTP-Servers, der Standard-E-Mail-Adresse des Administrators und der Standard-E-Mail-Adresse verwendet, mit der die Berichte gesendet werden.

[Führen Sie diesen Schritt mit Windows PowerShell aus.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep2)

#### <a name="to-configure-notifications"></a>So konfigurieren Sie Benachrichtigungen

1.  Melden Sie sich als Mitglied der Sicherheitsgruppe "Administratoren" beim Dateiserver an.

2.  Geben Sie an der PowerShell-Eingabeaufforderung **Update-FsrmClassificationPropertyDefinition** ein, und drücken Sie dann die EINGABETASTE. Dadurch werden die Eigenschaftsdefinitionen, die auf dem Domänencontroller erstellt wurden, mit dem Dateiserver synchronisiert.

3.  Öffnen Sie den Ressourcen-Manager für Dateiserver. Klicken Sie in Server-Manager auf **Extras** und dann auf **Ressourcen-Manager für Dateiserver**.

4.  Klicken Sie mit der rechten Maustaste auf **Ressourcen-Manager für Dateiserver (lokal)**, und klicken Sie dann auf **Optionen konfigurieren**.

5.  Führen Sie auf der Registerkarte **E-Mail-Benachrichtigungen** Folgendes aus:

    -   Geben Sie im Feld **SMTP-Servername oder IP-Adresse** den Namen des SMTP-Servers in Ihrem Netzwerk ein.

    -   Geben Sie in das Feld **Standardadministratorempfänger** die E-Mail-Adresse des Administrators ein, der die Benachrichtigung erhalten soll.

    -   Geben Sie im Feld **Standard-e-Mail-Adresse** die e-Mail-Adresse ein, die zum Senden der Benachrichtigungen verwendet werden soll.

6.  Klicken Sie auf **OK**.

![projektmappenhandbücher](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>äquivalente Windows PowerShell-Befehle</em>***

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```
Set-FsrmSetting -SmtpServer IP address of SMTP server -FromEmailAddress "FromEmailAddress" -AdminEmailAddress "AdministratorEmailAddress"
```

## <a name="step-3-create-a-file-management-task"></a><a name="BKMK_Step3"></a>„Schritt 3: Erstellen einer Dateiverwaltungsaufgabe
In diesem Schritt wird die Konsole für den Ressourcen-Manager für Dateiserver zum Erstellen einer Dateiverwaltungsaufgabe verwendet, die am letzten Tag im Monat ausgeführt wird und alle Dateien mit den folgenden Kriterien als abgelaufen kennzeichnet:

-   Die Datei ist nicht mit zugewiesener rechtlicher Aufbewahrungspflicht klassifiziert.

-   Die Datei ist mit langfristiger Aufbewahrungsdauer klassifiziert.

-   Die Datei wurde in den letzten 10 Jahren nicht geändert.

[Führen Sie diesen Schritt mit Windows PowerShell aus.](assetId:///4a96cdaf-0081-4824-aab8-f0d51be501ac#BKMK_PSstep3)

#### <a name="to-create-a-file-management-task"></a>So erstellen Sie eine Dateiverwaltungsaufgabe

1.  Melden Sie sich als Mitglied der Sicherheitsgruppe "Administratoren" beim Dateiserver an.

2.  Öffnen Sie den Ressourcen-Manager für Dateiserver. Klicken Sie in Server-Manager auf **Extras** und dann auf **Ressourcen-Manager für Dateiserver**.

3.  Klicken Sie mit der rechten Maustaste auf **Dateiverwaltungsaufgaben**, und klicken Sie anschließend auf **Dateiverwaltungsaufgabe erstellen**.

4.  Geben Sie auf der Registerkarte **Allgemein** im Feld **Aufgabenname** einen Namen für die Dateiverwaltungsaufgabe ein, z. B. "Aufbewahrungsaufgabe".

5.  Klicken Sie auf der Registerkarte **Bereich** auf **Hinzufügen**, und wählen Sie die Ordner aus, die in dieser Regel einbezogen werden sollen, wie beispielsweise „D:\Finance Documents“.

6.  Klicken Sie auf der Registerkarte **Aktion** im Feld **Typ** auf **Dateiablauf**. Geben Sie in das Feld **Ablaufverzeichnis** einen Pfad zu einem Ordner auf dem lokalen Dateiserver ein, in den die abgelaufenen Dateien verschoben werden. Dieser Ordner sollte über eine Zugriffssteuerungsliste verfügen, die nur Dateiserveradministratoren den Zugriff erteilt.

7.  Klicken Sie auf der Registerkarte **Benachrichtigung** auf **Hinzufügen**.

    -   Aktivieren Sie das Kontrollkästchen **E-Mail an folgende Administratoren senden**.

    -   Aktivieren Sie das Kontrollkästchen **E-Mail an Benutzer senden, deren Dateien betroffen sind**, und klicken Sie dann auf **OK**.

8.  Klicken Sie auf der Registerkarte **Bedingung** auf **Hinzufügen**, und fügen Sie dann die folgenden Eigenschaften hinzu:

    -   Klicken Sie in der Liste **Eigenschaft** auf **Erkennbarkeit**. Klicken Sie in der Liste **Operator** auf **Ungleich**. Klicken Sie in der Liste **Wert** auf **Halten**.

    -   Klicken Sie in der Liste **Eigenschaft** auf **Aufbewahrungsdauer**. Klicken Sie in der Liste **Operator** auf **Gleich**. Klicken Sie in der Liste **Wert** auf **Langfristig**.

9. Aktivieren Sie auf der Registerkarte **Bedingung** das Kontrollkästchen **Tage seit der letzten Dateiänderung**, und legen Sie dann den Wert auf **3650** fest.

10. Klicken Sie auf der Registerkarte **Zeitplan** auf die Option **Monatlich**, und aktivieren Sie dann das Kontrollkästchen **Letzter**.

11. Klicken Sie auf **OK**.

![projektmappenhandbücher](media/Deploy-Implementing-Retention-of-Information-on-File-Servers--Demonstration-Steps-/PowerShellLogoSmall.gif)***<em>äquivalente Windows PowerShell-Befehle</em>***

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

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

## <a name="step-4-classify-a-file-manually"></a><a name="BKMK_Step4"></a>Schritt 4: Manuelles Klassifizieren einer Datei
In diesem Schritt wird eine Datei mit zugewiesener rechtlicher Aufbewahrungspflicht klassifiziert. Der übergeordnete Ordner dieser Datei wird mit einer langfristigen Aufbewahrungsdauer klassifiziert.

#### <a name="to-manually-classify-a-file"></a>So klassifizieren Sie eine Datei manuell

1.  Melden Sie sich als Mitglied der Sicherheitsgruppe "Administratoren" beim Dateiserver an.

2.  Navigieren Sie zu dem Ordner, der im Rahmen der Dateiverwaltungsaufgabe in Schritt 3 erstellt wurde.

3.  Klicken Sie mit der rechten Maustaste auf den Ordner, und klicken Sie anschließend auf **Eigenschaften**.

4.  Klicken Sie auf der Registerkarte **Klassifizierung** auf **Aufbewahrungsdauer**, klicken Sie auf **Langfristig**, und klicken Sie dann auf **OK**.

5.  Klicken Sie mit der rechten Maustaste auf eine Datei in diesem Ordner, und klicken Sie dann auf **Eigenschaften**.

6.  Klicken Sie auf der Registerkarte **Klassifizierung** auf **Erkennbarkeit**. Klicken Sie auf **Halten**, dann auf **Anwenden** und anschließend auf **OK**.

7.  Führen Sie auf dem Dateiserver die Dateiverwaltungsaufgabe mithilfe der Konsole für den Ressourcen-Manager für Dateiserver aus. Nachdem die Dateiverwaltungsaufgabe abgeschlossen ist, prüfen Sie den Ordner und stellen Sie sicher, dass die Datei nicht in das Ablaufverzeichnis verschoben wurde.

8.  Klicken Sie mit der rechten Maustaste auf dieselbe Datei in diesem Ordner, und klicken Sie dann auf **Eigenschaften**.

9. Klicken Sie auf der Registerkarte **Klassifizierung** auf **Erkennbarkeit**. Klicken Sie auf **Nicht zutreffend**, dann auf **Anwenden** und anschließend auf **OK**.

10. Führen Sie auf dem Dateiserver die Dateiverwaltungsaufgabe mithilfe der Konsole für den Ressourcen-Manager für Dateiserver erneut aus. Nachdem die Dateiverwaltungsaufgabe abgeschlossen ist, prüfen Sie den Ordner und stellen Sie sicher, dass diese Datei in das Ablaufverzeichnis verschoben wurde.

## <a name="see-also"></a><a name="BKMK_Links"></a>Siehe auch

-   [Szenario: Implementieren der Aufbewahrung von Informationen auf Dateiservern](Scenario--Implement-Retention-of-Information-on-File-Servers.md)

-   [Planen der Aufbewahrung von Informationen auf Dateiservern](assetId:///edf13190-7077-455a-ac01-f534064a9e0c)

-   [Dynamische Zugriffsteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)


