---
ms.assetid: 074e63e9-976c-49da-8cba-9ae0b3325e34
title: "Einführung in Active Directory Administrative Center Enhancements (Level 100)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 7f52b22ec74ba12c383952e68b412f871a56474c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="introduction-to-active-directory-administrative-center-enhancements-level-100"></a>Einführung in Active Directory Administrative Center Enhancements (Level 100)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

ADAC in Windows Server 2012 enthält Verwaltungsfunktionen für Folgendes:

-   [Active Directory-Papierkorb](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#ad_recycle_bin_mgmt)

-   [Differenzierte Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#fine_grained_pswd_policy_mgmt)

-   [Windows PowerShell-Verlaufsanzeige](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#windows_powershell_history_viewer)

## <a name="ad_recycle_bin_mgmt"></a>Active Directory-Papierkorb
Versehentliches Löschen von Active Directory-Objekten ist häufig für Benutzer von Active Directory-Domänendienste (AD DS) und Active Directory Lightweight Directory Services (AD LDS). In früheren Versionen von Windows Server vor Windows Server 2008 R2 eine Wiederherstellung versehentlich gelöschte Objekte in Active Directory, aber Ansätze hatten die Nachteile.

In Windows Server 2008 können Sie das Windows Server-Sicherungsfeature und **Ntdsutil** autorisierende Wiederherstellung markieren Sie Objekte als autorisierend, um sicherzustellen, dass die wiederhergestellten Daten innerhalb der gesamten Domäne repliziert wurde. Der Nachteil autorisierenden Wiederherstellung wurde, dass es war in Directory Services-Wiederherstellungsmodus (DSRM) ausgeführt werden. Während des Verzeichnisdienst-Wiederherstellungsmodus musste der wiederherzustellende Domänencontroller offline bleiben. Es konnte daher nicht Clientanforderungen zu verarbeiten.

In Windows Server 2003 Active Directory und Windows Server 2008 AD DS konnte Sie gelöschte Active Directory-Objekte über Wiederbelebung wiederherstellen. Allerdings wiederbelebten Objekten Attribute (z. B. Gruppenmitgliedschaften von Benutzerkonten), die physisch entfernt wurden und nicht-Attribute, die gelöscht wurden, wurden nicht wiederhergestellt. Aus diesem Grund können Administratoren nicht auf die Wiederbelebung als ultimative Lösung versehentliches Löschen von Objekten verlassen. Weitere Informationen zur Wiederbelebung finden Sie unter [Wiederbeleben veralteter Active Directory-Objekte](https://go.microsoft.com/fwlink/?LinkID=125452).

Active Directory-Papierkorb ab Windows Server 2008 R2, basiert auf der vorhandenen Infrastruktur der Tombstone-Wiederbelebung und räumt beibehalten und Wiederherstellen von versehentlich gelöschte Active Directory-Objekte.

Wenn Sie die Active Directory-Papierkorb, alle verknüpften Werten aktivieren und nicht-Attribute der gelöschten Active Directory-Objekte werden beibehalten und die Objekte werden vollständig in der gleichen logischen Zustand, in dem sie unmittelbar vor dem Löschen waren, wiederhergestellt. Beispielsweise seinen wiederhergestellte Benutzerkonten automatisch alle Gruppenmitgliedschaften und entsprechenden Zugriffsrechte, die sie unmittelbar vor dem Löschen, innerhalb und zwischen den Domänen hatten. Active Directory-Papierkorb kann in AD DS- und AD LDS-Umgebungen. Eine ausführliche Beschreibung des Active Directory-Papierkorb, finden Sie unter [What's New in AD DS: Active Directory-Papierkorb](https://technet.microsoft.com/library/dd391916(WS.10).aspx).

**Was ist neu?** In Windows Server 2012 wurde das Active Directory-Papierkorb-Feature mit einer neuen grafischen Benutzeroberfläche für Benutzer verwalten und gelöschte Objekte wiederherzustellen, verbessert. Benutzer können jetzt visuell eine Liste der gelöschten Objekte suchen und an ihren ursprünglichen oder an neuen Speicherorten wiederhergestellt werden.

Wenn Sie Active Directory-Papierkorb in Windows Server 2012 aktivieren möchten, beachten Sie Folgendes:

-   Standardmäßig ist der Active Directory-Papierkorb deaktiviert. Um es zu aktivieren, müssen Sie zunächst die Funktionsebene der Gesamtstruktur Ihrer AD DS oder AD LDS-Umgebung für Windows Server 2008 R2 oder höher heraufstufen. Dies wiederum ist es erforderlich, dass alle Domänencontroller in der Gesamtstruktur oder alle Server, auf denen Instanzen von AD LDS-Konfigurationssätze gehostet werden unter Windows Server 2008 R2 oder höher.

-   Der Prozess der Active Directory-Papierkorb aktivieren ist nicht rückgängig gemacht werden. Nachdem Sie Active Directory-Papierkorb in Ihrer Umgebung aktiviert haben, können Sie es nicht deaktivieren.

-   Zum Verwalten des Papierkorbs über eine Benutzeroberfläche müssen Sie die Version des Active Directory-Verwaltungscenters in Windows Server 2012 installieren.

    > [!NOTE]
    > Sie können **Server-Manager** So installieren Sie Remoteserver-Verwaltungstools (RSAT) auf Windows Server 2012-Computern, um die richtige Version des Active Directory-Verwaltungscenters verwenden, um den Papierkorb über eine Benutzeroberfläche zu verwalten.
    > 
    > Sie können [Remoteserver-Verwaltungstools](https://go.microsoft.com/fwlink/?LinkID=238560) unter Windows&reg; 8 Computer auf die richtige Version des Active Directory-Verwaltungscenters verwenden Sie zum Verwalten des Papierkorbs über eine Benutzeroberfläche.

### <a name="active-directory-recycle-bin-step-by-step"></a>Active Directory-Papierkorb schrittweise
In den folgenden Schritten werden Sie ADAC verwenden, um die folgenden Aufgaben aus Active Directory-Papierkorb in Windows Server 2012 auszuführen:

-   [Schritt 1: Heraufstufen der Gesamtstrukturfunktionsebene](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_raise_ffl)

-   [Schritt 2: Papierkorb aktivieren](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_enable_recycle_bin)

-   [Schritt 3: Erstellen Sie Testbenutzern, Gruppe und Organisationseinheit](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_test_env)

-   [Schritt 4: Wiederherstellen gelöschter Objekte](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_restore_del_obj)

> [!NOTE]
> Mitgliedschaft in der Gruppe "Organisations-Admins" oder entsprechende Berechtigungen ist erforderlich, um die folgenden Schritte ausführen.

### <a name="bkmk_raise_ffl"></a>Schritt 1: Heraufstufen der Gesamtstrukturfunktionsebene
In diesem Schritt werden Sie die Gesamtstrukturfunktionsebene auf Heraufstufen. Sie müssen zuerst die Funktionsebene der für die Zielgesamtstruktur mindestens Windows Server 2008 R2 sein, bevor Sie die Active Directory-Papierkorb aktivieren.

##### <a name="to-raise-the-functional-level-on-the-target-forest"></a>Um die Funktionsebene für die Zielgesamtstruktur

1.  Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2.  Klicken Sie auf **verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne in der **Navigationsknoten hinzufügen** Dialogfeld, und klicken Sie dann auf **OK**.

3.  Klicken Sie auf die Zieldomäne im linken Navigationsbereich und in der **Aufgaben** Bereich, klicken Sie auf **Heraufstufen der Gesamtstrukturfunktionsebene**. Wählen Sie eine Gesamtstrukturfunktionsebene, die mindestens Windows Server 2008 R2 oder höher, und klicken Sie dann auf **OK**.

![Einführung in die AD-Admin center](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```
Set-ADForestMode -Identity contoso.com -ForestMode Windows2008R2Forest -Confirm:$false
```

Für die **-Identität** Argument, geben Sie den vollqualifizierten DNS-Namen.

### <a name="bkmk_enable_recycle_bin"></a>Schritt 2: Papierkorb aktivieren
In diesem Schritt aktivieren Sie den Papierkorb zum Wiederherstellen gelöschter Objekte in AD DS.

##### <a name="to-enable-active-directory-recycle-bin-in-adac-on-the-target-domain"></a>So aktivieren Sie Active Directory-Papierkorb in ADAC für die Zieldomäne

1.  Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2.  Klicken Sie auf **verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne in der **Navigationsknoten hinzufügen** Dialogfeld, und klicken Sie dann auf **OK**.

3.  In der **Aufgaben** Bereich, klicken Sie auf **Papierkorb aktivieren... ** in der **Aufgaben** Bereich, klicken Sie auf **OK** auf die Warnung, und klicken Sie dann auf **OK** um die ADAC-Meldung zu aktualisieren.

4.  Drücken Sie F5, um ADAC zu aktualisieren.

![Einführung in die AD-Admin center](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```
Enable-ADOptionalFeature -Identity 'CN=Recycle Bin Feature,CN=Optional Features,CN=Directory Service,CN=Windows NT,CN=Services,CN=Configuration,DC=contoso,DC=com' -Scope ForestOrConfigurationSet -Target 'contoso.com'
```

### <a name="bkmk_create_test_env"></a>Schritt 3: Erstellen Sie Testbenutzern, Gruppe und Organisationseinheit
In den folgenden Verfahren erstellen Sie zwei Testbenutzer. Sie werden dann eine Testgruppe erstellen und Ihr die Testbenutzer zuweisen. Außerdem erstellen Sie eine Organisationseinheit.

##### <a name="to-create-test-users"></a>Testbenutzer erstellen

1.  Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2.  Klicken Sie auf **verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne in der **Navigationsknoten hinzufügen** Dialogfeld, und klicken Sie dann auf **OK**.

3.  In der **Aufgaben** Bereich, klicken Sie auf **neu** , und klicken Sie dann auf **Benutzer**.

    ![Einführung in die AD-Admin center](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/ADDS_ADACNewUser.gif)

4.  Geben Sie die folgende Informationen unter **Konto** , und klicken Sie dann auf OK:

    -   Vollständiger Name: test1

    -   SamAccountName-Benutzeranmeldung: test1

    -   Kennwort:p@ssword1

    -   Bestätigen Sie Kennwort:p@ssword1

5.  Wiederholen Sie die vorherigen Schritte zum Erstellen eines zweiten Benutzers test2.

##### <a name="to-create-a-test-group-and-add-users-to-the-group"></a>Erstellen eine Testgruppe und fügen der Gruppe Benutzer hinzu

1.  Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2.  Klicken Sie auf **verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne in der **Navigationsknoten hinzufügen** Dialogfeld, und klicken Sie dann auf **OK**.

3.  In der **Aufgaben** Bereich, klicken Sie auf **neu** , und klicken Sie dann auf **Gruppe**.

4.  Geben Sie die folgende Informationen unter **Gruppe** und klicken Sie dann auf **OK**:

    -   **Gruppe Name: group1**

5.  Klicken Sie auf **group1**, und klicken Sie dann unter der **Aufgaben** Bereich, klicken Sie auf **Eigenschaften**.

6.  Klicken Sie auf **Mitglieder**, klicken Sie auf **hinzufügen**, Typ **test1; test2**, und klicken Sie dann auf **OK**.

![Einführung in die AD-Admin center](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```
Add-ADGroupMember -Identity group1 -Member test1
```

##### <a name="to-create-an-organizational-unit"></a>Erstellen eine Organisationseinheit

1.  Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2.  Klicken Sie auf **verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne in der **Navigationsknoten hinzufügen** Dialogfeld, und klicken Sie dann auf **OK**.

3.  In der **Aufgaben** Bereich, klicken Sie auf **neu** , und klicken Sie dann auf **Organisationseinheit**.

4.  Geben Sie die folgende Informationen unter **Organisationseinheit** , und klicken Sie dann auf **OK**:

    -   **NameOU1**

![Einführung in die AD-Admin center](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```
1..2 | ForEach-Object {New-ADUser -SamAccountName test$_ -Name "test$_" -Path "DC=fabrikam,DC=com" -AccountPassword (ConvertTo-SecureString -AsPlainText "p@ssword1" -Force) -Enabled $true}
New-ADGroup -Name "group1" -SamAccountName group1 -GroupCategory Security -GroupScope Global -DisplayName "group1"
New-ADOrganizationalUnit -Name OU1 -Path "DC=fabrikam,DC=com"

```

### <a name="bkmk_restore_del_obj"></a>Schritt 4: Wiederherstellen gelöschter Objekte
In den folgenden Verfahren stellen Sie gelöschte Objekte aus der **Gelöschte Objekte** Container an ihrem ursprünglichen Speicherort und an einen anderen Speicherort.

##### <a name="to-restore-deleted-objects-to-their-original-location"></a>Wiederherstellen gelöschter-Objekte an ihrem ursprünglichen Speicherort

1.  Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2.  Klicken Sie auf **verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne in der **Navigationsknoten hinzufügen** Dialogfeld, und klicken Sie dann auf **OK**.

3.  Wählen Sie Benutzer **test1** und **test2**, klicken Sie auf **löschen** in der **Aufgaben** Bereich, und klicken Sie dann auf **Ja** zu bestätigen.

    ![Einführung in die AD-Admin center](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

    Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

    ```
    Get-ADUser -Filter 'Name -Like "*test*"'|Remove-ADUser -Confirm:$false
    ```

4.  Navigieren Sie zu den **Gelöschte Objekte** Container, wählen **test2** und **test1** , und klicken Sie dann auf **wiederherstellen** in der **Aufgaben** Bereich.

5.  Um zu bestätigen, dass die Objekte an ihrem ursprünglichen Speicherort wiederhergestellt wurden, navigieren Sie zu der Zieldomäne, und stellen Sie sicher, dass die Benutzerkonten dort aufgeführt sind.

    > [!NOTE]
    > Wenn Sie zum Navigieren der **Eigenschaften** Benutzerkonten **test1** und **test2** , und klicken Sie dann auf **Mitglied von**, sehen Sie, dass auch deren Gruppenmitgliedschaft wiederhergestellt wurde.

Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

![Einführung in die AD-Admin center](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

```
Get-ADObject -Filter 'Name -Like "*test*"' -IncludeDeletedObjects | Restore-ADObject
```

##### <a name="to-restore-deleted-objects-to-a-different-location"></a>Wiederherstellen gelöschter-Objekte an einen anderen Speicherort

1.  Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2.  Klicken Sie auf **verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne in der **Navigationsknoten hinzufügen** Dialogfeld, und klicken Sie dann auf **OK**.

3.  Wählen Sie Benutzer **test1** und **test2**, klicken Sie auf **löschen** in der **Aufgaben** Bereich, und klicken Sie dann auf **Ja** zu bestätigen.

4.  Navigieren Sie zu den **Gelöschte Objekte** Container, wählen **test2** und **test1** , und klicken Sie dann auf **wiederherstellen in** in der **Aufgaben** Bereich.

5.  Wählen Sie **OU1** , und klicken Sie dann auf **OK**.

6.  Um die Objekte zu bestätigen wiederhergestellt wurden **OU1**, navigieren Sie zu der Zieldomäne, doppelklicken Sie auf **OU1** und überprüfen Sie die Benutzerkonten dort aufgeführt sind.

![Einführung in die AD-Admin center](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```
Get-ADObject -Filter 'Name -Like "*test*"' -IncludeDeletedObjects | Restore-ADObject -TargetPath "OU=OU1,DC=contoso,DC=com"
```

## <a name="fine_grained_pswd_policy_mgmt"></a>Differenzierte Kennwortrichtlinie
Das Betriebssystem Windows Server 2008 bietet Organisationen eine Möglichkeit, unterschiedliche Kennwort- und Kontosperrungsrichtlinien für verschiedene Gruppen von Benutzern in einer Domäne zu definieren. In Active Directory-Domänen vor Windows Server 2008 können nur eine Kennwort- und Kontosperrungsrichtlinien für alle Benutzer in der Domäne angewendet werden. Diese Richtlinien wurden in der Standarddomänenrichtlinie für die Domäne angegeben. Daher mussten Organisationen, die unterschiedliche Kennwort- und kontosperrungseinstellungen für verschiedene Gruppen von Benutzern sollten entweder einen Kennwortfilter erstellen oder mehrere Domänen bereitstellen. Beide sind Optionen aufwändig.

Fein abgestimmte Kennwortrichtlinien können mehrere Kennwortrichtlinien innerhalb einer einzelnen Domäne und verschiedene Gruppen von Benutzern in einer Domäne unterschiedliche Einschränkungen bei Kennwort- und Kontosperrungsrichtlinien zuweisen. Sie können z. B. für privilegierte Konten strengere Einstellungen und weniger strengen Einstellungen auf die Konten anderer Benutzer anwenden. In anderen Fällen empfiehlt es sich um eine spezielle Kennwortrichtlinie für Konten anzuwenden, deren Kennwörter mit anderen Datenquellen synchronisiert werden. Eine ausführliche Beschreibung differenzierter Kennwortrichtlinien, finden Sie unter [AD DS: differenzierte Kennwortrichtlinien](https://technet.microsoft.com/library/cc770394(WS.10).aspx)

**Was ist neu?** In Windows Server 2012 Verwaltung differenzierter Kennwortrichtlinien einfacher und visuelle erfolgt durch Bereitstellen einer Benutzeroberfläche für die AD DS-Administratoren Richtlinien in ADAC verwalten. Administratoren können jetzt Richtlinienergebnis eines bestimmten Benutzers anzeigen, anzeigen und alle Kennwortrichtlinien innerhalb einer bestimmten Domäne zu sortieren und einzelne Kennwortrichtlinien visuell verwalten.

Wenn Sie die differenzierte Kennwortrichtlinien in Windows Server 2012 verwenden möchten, beachten Sie Folgendes:

-   Differenzierte Kennwortrichtlinien gelten nur globale Sicherheitsgruppen und Benutzerobjekte (oder InetOrgPerson-Objekte, wenn sie anstatt von Benutzerobjekten verwendet werden). Standardmäßig können nur Mitglieder der Gruppe der Domänenadministratoren fein abgestimmte Kennwortrichtlinien festgelegt. Allerdings können Sie auch die Möglichkeit, legen Sie diese Richtlinien an andere Benutzer delegieren. Die Domänenfunktionsebene muss WindowsServer 2008 oder höher sein.

-   Sie müssen die Windows Server 2012-Version des Active Directory-Verwaltungscenters verwalten fein abgestimmte Kennwortrichtlinien über eine grafische Benutzeroberfläche verwenden.

    > [!NOTE]
    > Sie können **Server-Manager** So installieren Sie Remoteserver-Verwaltungstools (RSAT) auf Windows Server 2012-Computern, um die richtige Version des Active Directory-Verwaltungscenters verwenden, um den Papierkorb über eine Benutzeroberfläche zu verwalten.
    > 
    > Sie können [Remoteserver-Verwaltungstools](https://go.microsoft.com/fwlink/?LinkID=238560) unter Windows&reg; 8 Computer auf die richtige Version des Active Directory-Verwaltungscenters verwenden Sie zum Verwalten des Papierkorbs über eine Benutzeroberfläche.

### <a name="fine-grained-password-policy-step-by-step"></a>Differenzierte Kennwortrichtlinien schrittweise
In den folgenden Schritten werden Sie ADAC verwenden, um folgende differenzierte Richtlinie Aufgaben ausführen:

-   [Schritt 1: Heraufstufen der Domänenfunktionsebene](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_raise_dfl)

-   [Schritt 2: Erstellen von Testbenutzern, Gruppe und Organisationseinheit](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk2_test_fgpp)

-   [Schritt 3: Erstellen einer neuen differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)

-   [Schritt 4: Anzeigen eines Richtlinienergebnissatzes für einen Benutzer](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_view_resultant_fgpp)

-   [Schritt 5: Bearbeiten einer differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_edit_fgpp)

-   [Schritt 6: Löschen einer differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_delete_fgpp)

> [!NOTE]
> Mitgliedschaft in der Gruppe "Domänen-Admins" oder entsprechende Berechtigungen ist erforderlich, um die folgenden Schritte ausführen.

#### <a name="bkmk_raise_dfl"></a>Schritt 1: Heraufstufen der Domänenfunktionsebene
In der folgenden Prozedur werden Sie die Domänenfunktionsebene der Zieldomäne auf Windows Server 2008 oder höher heraufstufen. Differenzierte Kennwortrichtlinien aktiviert ist eine Domänenfunktionsebene von Windows Server 2008 oder höher erforderlich.

###### <a name="to-raise-the-domain-functional-level"></a>Um die Domänenfunktionsebene heraufstufen

1.  Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2.  Klicken Sie auf **verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne in der **Navigationsknoten hinzufügen** Dialogfeld, und klicken Sie dann auf **OK**.

3.  Klicken Sie auf die Zieldomäne im linken Navigationsbereich und in der **Aufgaben** Bereich, klicken Sie auf **Heraufstufen der Domänenfunktionsebene**. Wählen Sie eine Gesamtstrukturfunktionsebene, die mindestens WindowsServer 2008 oder höher, und klicken Sie dann auf **OK**.

![Einführung in die AD-Admin center](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```
Set-ADDomainMode -Identity contoso.com -DomainMode 3
```

#### <a name="bkmk2_test_fgpp"></a>Schritt 2: Erstellen von Testbenutzern, Gruppe und Organisationseinheit
Führen Sie zum Erstellen der Testbenutzer und Gruppe für diesen Schritt benötigten, wie: [Schritt 3: Erstellen von Testbenutzern, Gruppe und Organisationseinheit](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_test_env) (Sie müssen nicht auf die Organisationseinheit, um die Vorführung der differenzierten Kennwortrichtlinie erstellen).

#### <a name="bkmk_create_fgpp"></a>Schritt 3: Erstellen einer neuen differenzierten Kennwortrichtlinie
Im folgenden Verfahren erstellen Sie eine neue differenzierte Kennwortrichtlinie, über die Benutzeroberfläche in ADAC.

###### <a name="to-create-a-new-fine-grained-password-policy"></a>Erstellen Sie eine neue differenzierte Kennwortrichtlinie

1.  Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2.  Klicken Sie auf **verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne in der **Navigationsknoten hinzufügen** Dialogfeld, und klicken Sie dann auf **OK**.

3.  Öffnen Sie im ADAC-Navigationsbereich das **System** Container, und klicken Sie dann auf **Kennworteinstellungscontainer**.

4.  In der **Aufgaben** Bereich, klicken Sie auf **neu**, und klicken Sie dann auf **Kennworteinstellungen**.

    Füllen Sie oder Bearbeiten von Feldern auf der Eigenschaftenseite zum Erstellen einer neuen **Kennworteinstellungen** Objekt. Die **Namen** und **Vorrang vor** Felder sind erforderlich.

    ![Einführung in die AD-Admin center](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/ADDS_ADACNewFGPP.gif)

5.  Klicken Sie unter **direkt anwendbar auf**, klicken Sie auf **hinzufügen**, Typ **group1**, und klicken Sie dann auf **OK**.

    Dadurch wird das Kennworteinstellungsobjekt mit den Mitgliedern der globalen Gruppe, die für die testumgebung erstellt verknüpft.

6.  Klicken Sie auf **OK** auf die Erstellung zu übermitteln.

![Einführung in die AD-Admin center](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```
New-ADFineGrainedPasswordPolicy TestPswd -ComplexityEnabled:$true -LockoutDuration:"00:30:00" -LockoutObservationWindow:"00:30:00" -LockoutThreshold:"0" -MaxPasswordAge:"42.00:00:00" -MinPasswordAge:"1.00:00:00" -MinPasswordLength:"7" -PasswordHistoryCount:"24" -Precedence:"1" -ReversibleEncryptionEnabled:$false -ProtectedFromAccidentalDeletion:$true
Add-ADFineGrainedPasswordPolicySubject TestPswd -Subjects group1
```

#### <a name="bkmk_view_resultant_fgpp"></a>Schritt 4: Anzeigen eines Richtlinienergebnissatzes für einen Benutzer
Im folgenden Verfahren zeigen Sie die resultierende kennworteinstellungen für Benutzer, der ein Mitglied der Gruppe ist, der Sie eine differenzierte Kennwortrichtlinie in zugewiesen [Schritt 3: erstellen eine neuen differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp).

###### <a name="to-view-a-resultant-set-of-policies-for-a-user"></a>Anzeigen ein Richtlinienergebnissatzes für einen Benutzer

1.  Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2.  Klicken Sie auf **verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne in der **Navigationsknoten hinzufügen** Dialogfeld, und klicken Sie dann auf **OK**.

3.  Wählen Sie einen Benutzer **test1** , die der Gruppe gehört **group1** , dass Sie eine differenzierte Kennwortrichtlinie verknüpft [Schritt 3: erstellen eine neuen differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp).

4.  Klicken Sie auf **resultierende Kennworteinstellungen anzeigen** in der **Aufgaben** Bereich.

5.  Überprüfen Sie die kennworteinstellungsrichtlinie, und klicken Sie dann auf **Abbrechen**.

![Einführung in die AD-Admin center](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```
Get-ADUserResultantPasswordPolicy test1
```

#### <a name="bkmk_edit_fgpp"></a>Schritt 5: Bearbeiten einer differenzierten Kennwortrichtlinie
Im folgenden Verfahren bearbeiten Sie die differenzierte Kennwortrichtlinie, die Sie erstellt, in haben [Schritt 3: erstellen eine neuen differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)

###### <a name="to-edit-a-fine-grained-password-policy"></a>So bearbeiten Sie eine differenzierte Kennwortrichtlinie

1.  Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2.  Klicken Sie auf **verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne in der **Navigationsknoten hinzufügen** Dialogfeld, und klicken Sie dann auf **OK**.

3.  In der ADAC **Navigationsbereich**, erweitern Sie **System** , und klicken Sie dann auf **Kennworteinstellungscontainer**.

4.  Wählen Sie die differenzierte Kennwortrichtlinie, die Sie erstellt, in haben [Schritt 3: erstellen eine neuen differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp) , und klicken Sie auf **Eigenschaften** in der **Aufgaben** Bereich.

5.  Klicken Sie unter **Kennwortchronik**, ändern Sie den Wert der **Anzahl der gespeicherten Kennwörter** auf **30**.

6.  Klicken Sie auf **OK**.

![Einführung in die AD-Admin center](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```
Set-ADFineGrainedPasswordPolicy TestPswd -PasswordHistoryCount:"30"
```

#### <a name="bkmk_delete_fgpp"></a>Schritt 6: Löschen einer differenzierten Kennwortrichtlinie

###### <a name="to-delete-a-fine-grained-password-policy"></a>So löschen Sie eine differenzierte Kennwortrichtlinie

1.  Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2.  Klicken Sie auf **verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne in der **Navigationsknoten hinzufügen** Dialogfeld, und klicken Sie dann auf **OK**.

3.  Erweitern Sie im ADAC-Navigationsbereich **System** , und klicken Sie dann auf **Kennworteinstellungscontainer**.

4.  Wählen Sie die differenzierte Kennwortrichtlinie, die Sie erstellt, in haben [Schritt 3: erstellen eine neuen differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp) und in der **Aufgaben** auf **Eigenschaften**.

5.  Deaktivieren der **vor zufälligem Löschen schützen** Kontrollkästchen und klicken Sie auf **OK**.

6.  Wählen Sie die differenzierte Kennwortrichtlinie aus, und in der **Aufgaben** auf **löschen**.

7.  Klicken Sie auf **OK** im Bestätigungsdialogfeld.

![Einführung in die AD-Admin center](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell entsprechende Befehle ***

Die folgenden Windows PowerShell-Cmdlet oder Cmdlets führen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden möglicherweise aufgrund von formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```
Set-ADFineGrainedPasswordPolicy -Identity TestPswd -ProtectedFromAccidentalDeletion $False
Remove-ADFineGrainedPasswordPolicy TestPswd -Confirm
```

## <a name="windows_powershell_history_viewer"></a>Windows PowerShell-Verlaufsanzeige
ADAC ist ein Benutzeroberflächentool basieren auf Windows PowerShell.  In Windows Server 2012 können IT-Administratoren ADAC Windows PowerShell für Active Directory-Cmdlets erhalten Sie, mithilfe von Windows PowerShell History Viewer nutzen. Wie Aktionen in der Benutzeroberfläche ausgeführt werden, wird der entsprechende Windows PowerShell-Befehl in Windows PowerShell History Viewer für den Benutzer angezeigt. Dadurch können Administratoren, automatisierte Skripts erstellen und sich wiederholende Aufgaben, wodurch sich die IT-Produktivität zu reduzieren.  Darüber hinaus wird dieses Feature reduziert die Zeit, um Windows PowerShell für Active Directory zu erfahren und erhöht das Vertrauen der Benutzer in die Richtigkeit Ihre.

Bei der Verwendung von Windows PowerShell History Viewer in Windows Server 2012 die folgenden Punkte:

-   Wenn Sie Windows PowerShell Script Viewer nutzen zu können, müssen Sie die Windows Server 2012-Version von ADAC verwenden.

    > [!NOTE]
    > Sie können **Server-Manager** So installieren Sie Remoteserver-Verwaltungstools (RSAT) auf Windows Server 2012-Computern, um die richtige Version des Active Directory-Verwaltungscenters verwenden, um den Papierkorb über eine Benutzeroberfläche zu verwalten.
    > 
    > Sie können [Remoteserver-Verwaltungstools](https://go.microsoft.com/fwlink/?LinkID=238560) unter Windows&reg; 8 Computer auf die richtige Version des Active Directory-Verwaltungscenters verwenden Sie zum Verwalten des Papierkorbs über eine Benutzeroberfläche.

-   Verfügen Sie über grundlegende Kenntnisse in Windows PowerShell. Beispielsweise müssen Sie wissen, wie Piping in Windows PowerShell ausgeführt. Weitere Informationen über Piping in Windows PowerShell finden Sie unter [Piping und die Pipeline in Windows PowerShell](https://technet.microsoft.com/library/ee176927.aspx).

### <a name="windows-powershell-history-viewer-step-by-step"></a>Windows PowerShell-Verlaufsanzeige schrittweise
Im folgenden Verfahren verwenden die Windows PowerShell History Viewer in ADAC Sie zum Erstellen eines Windows PowerShell-Skripts.  Bevor Sie damit beginnen, müssen Sie den Benutzer **test1** aus der Gruppe **group1**.

##### <a name="to-construct-a-script-using-powershell-history-viewer"></a>Zum Erstellen eines Skripts mit PowerShell-Verlaufsanzeige

1.  Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2.  Klicken Sie auf **verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne in der **Navigationsknoten hinzufügen** Dialogfeld, und klicken Sie dann auf **OK**.

3.  Erweitern Sie die **Windows PowerShell History** Bereich unten im ADAC-Bildschirm.

4.  Wählen Sie den Benutzer **test1**.

5.  Klicken Sie auf **zur Gruppe hinzufügen... ** in der **Aufgaben** Bereich.

6.  Navigieren Sie zu **group1** , und klicken Sie auf **OK** im Dialogfeld.

7.  Navigieren Sie zu den **Windows PowerShell History** Bereich, und suchen Sie den Befehl, der gerade generiert wurde.

8.  Kopieren Sie den Befehl ein, und fügen Sie ihn in den Editor Ihrer Wahl an Ihr Skript zu erstellen.

    Sie können z. B. den Befehl zum Hinzufügen eines anderen Benutzers ändern **group1**, oder fügen **test1** in eine andere Gruppe.

## <a name="see-also"></a>Siehe auch
[Erweiterte AD DS-Verwaltung mithilfe von Active Directory-Verwaltungscenter & #40; Level 200 & #41;](Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md)


