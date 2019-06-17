---
ms.assetid: 074e63e9-976c-49da-8cba-9ae0b3325e34
title: Einführung in die Erweiterungen des ActiveDirectory Verwaltungscenters (Stufe100)
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d3b5f3eee338128fb424c28e7280bb7f543c9f58
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443002"
---
# <a name="introduction-to-active-directory-administrative-center-enhancements-level-100"></a>Einführung in die Erweiterungen des ActiveDirectory Verwaltungscenters (Stufe100)

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die Active Directory Administrative Center in Windows Server umfasst Funktionen zur dokumentverwaltung für Folgendes:

- [Active Directory-Papierkorb](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#ad_recycle_bin_mgmt)
- [Differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#fine_grained_pswd_policy_mgmt)
- [Windows PowerShell-Verlaufsanzeige](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#windows_powershell_history_viewer)

## <a name="ad_recycle_bin_mgmt"></a>Active Directory-Papierkorb

Versehentliches Löschen von Active Directory-Objekten kommt bei Benutzern von AD DS (Active Directory Domain Services) und AD LDS (Active Directory Lightweight Directory Services) häufig vor. In früheren Versionen von Windows Server vor Windows Server 2008 R2 konnten wiederhergestellt versehentlich gelöschte Objekte in Active Directory, aber die Lösungen haben jeweils vor-und Nachteile.

In Windows Server 2008 konnten Sie mit der Windows Server-Sicherung und dem autorisierenden Wiederherstellungsbefehl **ntdsutil** Objekte als autorisierend kennzeichnen, um sicherzustellen, dass die wiederhergestellten Daten innerhalb der gesamten Domäne repliziert werden. Der Nachteil des Ansatzes zur autorisierenden Wiederherstellung lag darin, dass dieser im Verzeichnisdienst-Wiederherstellungsmodus (Directory Services Restore Mode, DSRM) ausgeführt werden musste. Während des Verzeichnisdienst-Wiederherstellungsmodus musste der wiederherzustellende Domänencontroller offline bleiben. Deshalb war er nicht in der Lage, Clientanforderungen zu verarbeiten.

In Windows Server 2003 Active Directory und Windows Server 2008 AD DS konnten Sie gelöschte Active Directory-Objekte mittels Wiederbelebung veralteter Objekte (Tombstone-Wiederbelebung) wiederherstellen. Attribute mit verknüpften Werten von wiederbelebten Objekten (beispielsweise Gruppenmitgliedschaften von Benutzerkonten), die physisch entfernt wurden, sowie Attribute mit nicht verknüpften Werten, die gelöscht wurden, wurden jedoch nicht wiederhergestellt. Deshalb konnten sich Administratoren bei versehentlich gelöschten Objekten nicht auf die Wiederbelebung von veralteten Objekten als ultimative Lösung verlassen. Weitere Informationen zur Wiederbelebung veralteter Objekte finden Sie unter [Reanimating Active Directory Tombstone Objects](https://go.microsoft.com/fwlink/?LinkID=125452).

Der Active Directory-Papierkorb baut ab Windows Server 2008 R2 auf der vorhandenen Infrastruktur zur Wiederbelebung veralteter Objekte auf und räumt Ihnen mehr Möglichkeiten ein, versehentlich gelöschte Active Directory-Objekte zu erhalten und wiederherzustellen.

Wenn Sie den Active Directory-Papierkorb aktivieren, bleiben alle Attribute mit verknüpften Werten und mit nicht verknüpften Werten der gelöschten Active Directory-Objekte erhalten, und die Objekte werden vollständig in ihrem durchgängig logischen Zustand, den sie vor dem Löschen aufwiesen, wiederhergestellt. So erhalten beispielsweise wiederhergestellte Benutzerkonten automatisch alle Gruppenmitgliedschaften und entsprechenden Zugriffsrechte zurück, die sie unmittelbar vor dem Löschen sowohl innerhalb als auch zwischen den Domänen innehatten. Der Active Directory-Papierkorb kann in AD DS- und in AD LDS-Umgebungen verwendet werden. Eine detaillierte Beschreibung des Active Directory-Papierkorbs, finden Sie unter [Neuigkeiten in AD DS: Active Directory-Papierkorb](https://technet.microsoft.com/library/dd391916(WS.10).aspx).

**Was ist neu?** In Windows Server 2012 und höher wird das Active Directory-Papierkorb-Feature mit einer neuen grafischen Benutzeroberfläche für Benutzer verwalten und Wiederherstellen gelöschter Objekte erweitert. Benutzer können gelöschte Objekte jetzt in einer Liste anzeigen und an ihren ursprünglichen oder an neuen Standorten wiederherstellen.

Wenn Sie Active Directory-Papierkorb in Windows Server aktivieren möchten, beachten Sie Folgendes:

- In der Standardeinstellung ist der Active Directory-Papierkorb deaktiviert. Um es zu aktivieren, müssen Sie zuerst die Funktionsebene der Gesamtstruktur Ihrer AD DS- oder AD LDS-Umgebung auf Windows Server 2008 R2 oder höher heraufstufen. Dies wiederum erfordert, dass alle Domänencontroller in der Gesamtstruktur oder alle Server, Instanzen von AD LDS-Konfigurationssätzen hosten, unter Windows Server 2008 R2 oder höher.
- Das Aktivieren des Active Directory-Papierkorbs kann nicht mehr rückgängig gemacht werden. Nachdem Sie den Active Directory-Papierkorb in Ihrer Umgebung aktiviert haben, können Sie ihn nicht mehr deaktivieren.
- Zum Verwalten des Papierkorbs per Benutzeroberfläche müssen Sie die Version des Active Directory-Verwaltungscenter unter Windows Server 2012 installieren.

    > [!NOTE]
    > Sie können **Server-Manager** Remote Server-Verwaltungstools (RSAT) um die richtige Version des Active Directory-Verwaltungscenters zu verwenden, um die Verwaltung des Papierkorbs per Benutzeroberfläche zu installieren.
    >
    > Informationen zum Installieren der Remoteserver-Verwaltungstools, finden Sie im Artikel [Remoteserver-Verwaltungstools](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools).

### <a name="active-directory-recycle-bin-step-by-step"></a>Schrittweise Anleitung für den Active Directory-Papierkorb

In den folgenden Schritten verwenden Sie ADAC, führen Sie die folgenden Aufgaben für die Active Directory-Papierkorb in Windows Server 2012:

- [Schritt 1: Heraufstufen der Gesamtstrukturfunktionsebene](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_raise_ffl)
- [Schritt 2: Papierkorb aktivieren](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_enable_recycle_bin)
- [Schritt 3: Erstellen von Testbenutzern, Gruppe und Organisationseinheit](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_test_env)
- [Schritt 4: Wiederherstellen gelöschter Objekte](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_restore_del_obj)

> [!NOTE]
> Um die folgenden Schritte durchführen zu können, müssen Sie Mitglied in der Gruppe der Unternehmensadministratoren sein oder über gleichwertige Berechtigungen verfügen.

### <a name="bkmk_raise_ffl"></a>Schritt 1: Heraufstufen der Gesamtstrukturfunktionsebene

In diesem Schritt werden Sie die Funktionsebene der Gesamtstruktur heraufstufen. Sie müssen zuerst die Funktionsebene für die Zielgesamtstruktur auf mindestens Windows Server 2008 R2 werden, bevor Sie die Active Directory-Papierkorb aktivieren auslösen.

#### <a name="to-raise-the-functional-level-on-the-target-forest"></a>So stufen Sie die Funktionsebene für die Zielgesamtstruktur herauf

1. Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2. Klicken Sie auf **Verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne im Dialogfeld **Navigationsknoten hinzufügen** aus. Klicken Sie anschließend auf **OK**.

3. Klicken Sie auf die Zieldomäne im linken Navigationsbereich, und klicken Sie im Bereich **Aufgaben** auf **Gesamtstrukturfunktionsebene heraufstufen**. Wählen Sie eine Gesamtstrukturfunktionsebene, die mindestens Windows Server 2008 R2 oder höher, und klicken Sie dann auf **OK**.

![Einführung in Active Directory-Verwaltungscenter](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```powershell
Set-ADForestMode -Identity contoso.com -ForestMode Windows2008R2Forest -Confirm:$false
```

Für die **-Identität** -Argument, die den vollqualifizierten DNS-Domänennamen angeben.

### <a name="bkmk_enable_recycle_bin"></a>Schritt 2: Papierkorb aktivieren

In diesem Schritt aktivieren Sie den Papierkorb zum Wiederherstellen gelöschter Objekte in AD DS.

#### <a name="to-enable-active-directory-recycle-bin-in-adac-on-the-target-domain"></a>So aktivieren Sie den Active Directory-Papierkorb in ADAC für die Zieldomäne

1. Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2. Klicken Sie auf **Verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne im Dialogfeld **Navigationsknoten hinzufügen** aus. Klicken Sie anschließend auf **OK**.

3. Klicken Sie im Bereich **Aufgaben** auf **Papierkorb aktivieren...** , klicken Sie im Warnhinweisfeld auf **OK** **** , und klicken Sie dann auf **OK**, um die ADAC-Meldung zu aktualisieren.

4. Drücken Sie auf F5, um ADAC zu aktualisieren.

![Einführung in Active Directory-Verwaltungscenter](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```powershell
Enable-ADOptionalFeature -Identity 'CN=Recycle Bin Feature,CN=Optional Features,CN=Directory Service,CN=Windows NT,CN=Services,CN=Configuration,DC=contoso,DC=com' -Scope ForestOrConfigurationSet -Target 'contoso.com'
```

### <a name="bkmk_create_test_env"></a>Schritt 3: Erstellen von Testbenutzern, Gruppe und Organisationseinheit

Mit den folgenden Schritten erstellen Sie zwei Testbenutzer. Anschließend werden Sie eine Testgruppe erstellen und ihr die Testbenutzer zuweisen. Außerdem erstellen Sie eine Organisationseinheit.

#### <a name="to-create-test-users"></a>So erstellen Sie Testbenutzer

1. Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2. Klicken Sie auf **Verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne im Dialogfeld **Navigationsknoten hinzufügen** aus. Klicken Sie anschließend auf **OK**.

3. Klicken Sie im Bereich **Aufgaben** auf **Neu** und dann auf **Benutzer**.

    ![Einführung in AD Admin center](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/ADDS_ADACNewUser.gif)

4. Geben Sie unter **Konto** die folgenden Informationen ein, und klicken Sie anschließend auf %%amp;quot;OK%%amp;quot;:

   - Vollständiger Name: test1
   - SamAccountName-Benutzeranmeldung: test1
   - Kennwort: p@ssword1
   - Bestätigen Sie Kennwort: p@ssword1

5. Wiederholen Sie diese Schritte, um den Benutzer %%amp;quot;test2%%amp;quot; zu erstellen.

#### <a name="to-create-a-test-group-and-add-users-to-the-group"></a>So erstellen Sie eine Testgruppe und fügen ihr Benutzer hinzu

1. Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.
2. Klicken Sie auf **Verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne im Dialogfeld **Navigationsknoten hinzufügen** aus. Klicken Sie anschließend auf **OK**.
3. Klicken Sie im Bereich **Aufgaben** auf **Neu**, und klicken Sie dann auf **Gruppe**.
4. Geben Sie unter **Gruppe** die folgenden Informationen ein, und klicken Sie anschließend auf **OK**:

    -   **Group-Name: gruppe1**

5. Klicken Sie auf **group1**, und klicken Sie dann unter dem Bereich **Aufgaben** auf **Eigenschaften**.
6. Klicken Sie auf **Mitglieder**, klicken Sie auf **Hinzufügen**, geben Sie **test1;test2**ein, und klicken Sie dann auf **OK**.

![Einführung in Active Directory-Verwaltungscenter](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```powershell
Add-ADGroupMember -Identity group1 -Member test1
```

#### <a name="to-create-an-organizational-unit"></a>So erstellen Sie eine Organisationseinheit

1. Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.
2. Klicken Sie auf **verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne im der **Navigationsknoten hinzufügen** Dialogfeld und klicken Sie auf ** OK
3. Klicken Sie im Bereich **Aufgaben** auf **Neu** , und klicken Sie dann auf **Organisationseinheit**.
4. Geben Sie unter **Organisationseinheit** die folgenden Informationen ein, und klicken Sie anschließend auf **OK**:

   - **NameOU1**

![Einführung in Active Directory-Verwaltungscenter](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```powershell
1..2 | ForEach-Object {New-ADUser -SamAccountName test$_ -Name "test$_" -Path "DC=fabrikam,DC=com" -AccountPassword (ConvertTo-SecureString -AsPlainText "p@ssword1" -Force) -Enabled $true}
New-ADGroup -Name "group1" -SamAccountName group1 -GroupCategory Security -GroupScope Global -DisplayName "group1"
New-ADOrganizationalUnit -Name OU1 -Path "DC=fabrikam,DC=com"
```

### <a name="bkmk_restore_del_obj"></a>Schritt 4: Wiederherstellen gelöschter Objekte

In den folgenden Anleitungen stellen Sie gelöschte Objekte aus dem Container **Gelöschte Objekte** an ihrem ursprünglichen Speicherort und an einem anderen Speicherort wieder her.

#### <a name="to-restore-deleted-objects-to-their-original-location"></a>So stellen Sie gelöschte Objekte an ihrem ursprünglichen Speicherort wieder her

1. Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2. Klicken Sie auf **Verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne im Dialogfeld **Navigationsknoten hinzufügen** aus. Klicken Sie anschließend auf **OK**.

3. Wählen Sie die Benutzer **test1** und **test2**aus, klicken Sie auf **Löschen** im Bereich **Aufgaben** , und klicken Sie dann auf **Ja** , um den Löschvorgang zu bestätigen.

    ![Einführung in Active Directory-Verwaltungscenter](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***

    Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

    ```powershell
    Get-ADUser -Filter 'Name -Like "*test*"'|Remove-ADUser -Confirm:$false
    ```

4. Navigieren Sie zu dem Container **Gelöschte Objekte** , wählen Sie **test2** und **test1** aus, und klicken Sie dann auf **Wiederherstellen** im Bereich **Aufgaben** .

5. Wenn Sie sich davon überzeugen möchten, dass die Objekte an ihrem ursprünglichen Speicherort wiederhergestellt wurden, navigieren Sie zu der Zieldomäne und überprüfen Sie, dass die Benutzerkonten dort aufgeführt sind.

    > [!NOTE]
    > Wenn Sie zu den **Eigenschaften** der Benutzerkonten **test1** und **test2** navigieren und dann auf **Mitglied von** klicken, können Sie sehen, dass auch deren Gruppenmitgliedschaft wiederhergestellt wurde.

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

![Einführung in Active Directory-Verwaltungscenter](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***

```powershell
Get-ADObject -Filter 'Name -Like "*test*"' -IncludeDeletedObjects | Restore-ADObject
```

#### <a name="to-restore-deleted-objects-to-a-different-location"></a>So stellen Sie gelöschte Objekte an einem anderen Speicherort wieder her

1. Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2. Klicken Sie auf **Verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne im Dialogfeld **Navigationsknoten hinzufügen** aus. Klicken Sie anschließend auf **OK**.

3. Wählen Sie die Benutzer **test1** und **test2**aus, klicken Sie auf **Löschen** im Bereich **Aufgaben** , und klicken Sie dann auf **Ja** , um den Löschvorgang zu bestätigen.

4. Navigieren Sie zu dem Container **Gelöschte Objekte** , wählen Sie **test2** und **test1** aus, und klicken Sie dann auf **Wiederherstellen in** im Bereich **Aufgaben** .

5. Wählen Sie **OU1** aus, und klicken Sie dann auf **OK**.

6. Wenn Sie sich davon überzeugen möchten, dass die Objekte in **OU1** wiederhergestellt wurden, navigieren Sie zu der Zieldomäne, doppelklicken Sie auf **OU1** und überprüfen Sie, dass die Benutzerkonten dort aufgeführt sind.

![Einführung in Active Directory-Verwaltungscenter](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```powershell
Get-ADObject -Filter 'Name -Like "*test*"' -IncludeDeletedObjects | Restore-ADObject -TargetPath "OU=OU1,DC=contoso,DC=com"
```

## <a name="fine_grained_pswd_policy_mgmt"></a>Differenzierten Kennwortrichtlinie

Windows Server 2008 bietet Organisationen die Möglichkeit, für verschiedene Gruppen von Benutzern in einer Domäne unterschiedliche Kennwort- und Kontosperrungsrichtlinien festzulegen. In Active Directory-Domänen vor Windows Server 2008 konnten auf alle Benutzer in der Domäne nur eine Kennwortrichtlinie und nur eine Kontosperrungsrichtlinie angewendet werden. Diese Richtlinien wurden in der Standarddomänenrichtlinie für die Domäne angegeben. Daher mussten Organisationen, die mehrere Kennwort- und Kontosperrungseinstellungen für verschiedene Gruppen von Benutzern haben wollten, entweder einen Kennwortfilter erstellen oder mehrere Domänen bereitstellen. Beide Optionen sind aufwändig.

Mithilfe differenzierter Kennwortrichtlinien können mehrere Kennwortrichtlinien innerhalb einer einzigen Domäne festgelegt und für verschiedene Gruppen von Benutzern in einer Domäne unterschiedliche Einschränkungen bei Kennwort- und Kontosperrungsrichtlinien angewendet werden. So könnten zum Beispiel für privilegierte Konten strengere Einstellungen und für die Konten der anderen Benutzer weniger strenge Einstellungen gelten. In anderen Fällen könnte es für Konten, deren Kennwörter mit anderen Datenquellen synchronisiert werden, eine spezielle Kennwortrichtlinie geben. Eine ausführliche Beschreibung differenzierter Kennwortrichtlinien, finden Sie unter [AD DS: Fein abgestimmte Kennwortrichtlinien](https://technet.microsoft.com/library/cc770394(WS.10).aspx)

**Was ist neu?**

In Windows Server 2012 und neuere, präzise Kennwort richtlinienverwaltung einfacher erfolgt durch Bereitstellen einer Benutzeroberfläche für die AD DS-Administratoren Richtlinien in ADAC verwalten. Administratoren können jetzt eines bestimmten Benutzers resultierende Richtlinie anzeigen, anzeigen und alle Kennwortrichtlinien innerhalb einer bestimmten Domäne zu sortieren und einzelne Kennwortrichtlinien visuell verwalten.

Wenn Sie die differenzierte Kennwortrichtlinien in Windows Server 2012 verwenden möchten, beachten Sie Folgendes:

- Differenzierte Kennwortrichtlinien gelten nur für globale Sicherheitsgruppen und Benutzerobjekte (oder inetOrgPerson-Objekte, wenn diese anstatt von Benutzerobjekten verwendet werden). In der Standardeinstellung können differenzierte Kennwortrichtlinien nur von Mitgliedern der Gruppe der Domänenadministratoren festgelegt werden. Sie können die Fähigkeit zum Festlegen dieser Richtlinien jedoch auch an andere Benutzer delegieren. Die Domänenfunktionsebene muss Windows Server 2008 (oder höher) sein.

- Sie müssen die Windows Server 2012 oder eine neuere Version des Active Directory-Verwaltungscenters verwenden, differenzierter Kennwortrichtlinien mithilfe einer grafischen Benutzeroberfläche zu verwalten.

    > [!NOTE]
    > Sie können **Server-Manager** Remote Server-Verwaltungstools (RSAT) um die richtige Version des Active Directory-Verwaltungscenters zu verwenden, um die Verwaltung des Papierkorbs per Benutzeroberfläche zu installieren.
    >
    > Informationen zum Installieren der Remoteserver-Verwaltungstools, finden Sie im Artikel [Remoteserver-Verwaltungstools](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools).

### <a name="fine-grained-password-policy-step-by-step"></a>Schrittweise Anleitung für differenzierte Kennwortrichtlinien

In den folgenden Schritten werden Sie mithilfe des Active Directory-Verwaltungscenters (ADAC) die folgenden Aufgaben bezüglich der differenzierten Kennwortrichtlinie durchführen:

- [Schritt 1: Heraufstufen der Domänenfunktionsebene](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_raise_dfl)
- [Schritt 2: Erstellen von Testbenutzern, Gruppe und Organisationseinheit](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk2_test_fgpp)
- [Schritt 3: Erstellen einer neuen differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)
- [Schritt 4: Anzeigen eines Richtlinienergebnissatzes für einen Benutzer](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_view_resultant_fgpp)
- [Schritt 5: Bearbeiten einer differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_edit_fgpp)
- [Schritt 6: Löschen einer differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_delete_fgpp)

> [!NOTE]
> Um die folgenden Schritte durchführen zu können, müssen Sie Mitglied in der Gruppe der Domänenadministratoren sein oder über gleichwertige Berechtigungen verfügen.

#### <a name="bkmk_raise_dfl"></a>Schritt 1: Heraufstufen der Domänenfunktionsebene

Im folgenden Verfahren werden Sie die Domänenfunktionsebene der Zieldomäne auf Windows Server 2008 oder höher heraufstufen. Eine Domänenfunktionsebene von Windows Server 2008 oder höher ist erforderlich, differenzierte Kennwortrichtlinien aktiviert werden.

##### <a name="to-raise-the-domain-functional-level"></a>So stufen Sie die Domänenfunktionsebene herauf

1. Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2. Klicken Sie auf **Verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne im Dialogfeld **Navigationsknoten hinzufügen** aus. Klicken Sie anschließend auf **OK**.

3. Klicken Sie auf die Zieldomäne im linken Navigationsbereich, und klicken Sie im **Aufgabenbereich** auf **Domänenfunktionsebene heraufstufen**. Wählen Sie eine Gesamtstrukturfunktionsebene, die mindestens WindowsServer 2008 oder höher, und klicken Sie dann auf **OK**.

![Einführung in Active Directory-Verwaltungscenter](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```powershell
Set-ADDomainMode -Identity contoso.com -DomainMode 3
```

#### <a name="bkmk2_test_fgpp"></a>Schritt 2: Erstellen von Testbenutzern, Gruppe und Organisationseinheit

Erstellen Testbenutzer und Gruppe für diesen Schritt benötigten, gehen Sie wie die hier: [Schritt 3: Erstellen von Testbenutzern, Gruppe und Organisationseinheit](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_test_env) (Sie müssen nicht zum Erstellen der Organisationseinheit ist für die Vorführung der differenzierten Kennwortrichtlinie).

#### <a name="bkmk_create_fgpp"></a>Schritt 3: Erstellen einer neuen differenzierten Kennwortrichtlinie

In der folgenden Anleitung erstellen Sie mithilfe der grafischen Benutzeroberfläche der Active Directory-Verwaltungstools (ADAC) eine neue differenzierte Kennwortrichtlinie.

##### <a name="to-create-a-new-fine-grained-password-policy"></a>So erstellen Sie eine neue differenzierte Kennwortrichtlinie

1. Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2. Klicken Sie auf **Verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne im Dialogfeld **Navigationsknoten hinzufügen** aus. Klicken Sie anschließend auf **OK**.

3. Öffnen Sie im ADAC-Navigationsbereich den Container **System**, und klicken Sie dann auf **Password Settings Container**.

4. Klicken Sie im Bereich **Aufgaben** auf **Neu**, und klicken Sie dann auf **Kennworteinstellungen**.

    Nehmen Sie in den Feldern auf der Eigenschaftenseite die gewünschten Eintragungen oder Änderungen vor, um ein neues **Kennworteinstellungsobjekt** zu erstellen. Die Felder **Name** und **Rangfolge** sind erforderlich.

    ![Einführung in AD Admin center](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/ADDS_ADACNewFGPP.gif)

5. Klicken Sie unter **Direkt anwendbar auf**, klicken Sie auf **Hinzufügen**, geben Sie **group1**ein, und klicken Sie dann auf **OK**.

    Dadurch wird das Kennworteinstellungsobjekt mit den Mitgliedern der globalen Gruppe verknüpft, die Sie für die Testumgebung erstellt haben.

6. Klicken Sie auf **OK** , um die Erstellung zu übermitteln.

![Einführung in Active Directory-Verwaltungscenter](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```powershell
New-ADFineGrainedPasswordPolicy TestPswd -ComplexityEnabled:$true -LockoutDuration:"00:30:00" -LockoutObservationWindow:"00:30:00" -LockoutThreshold:"0" -MaxPasswordAge:"42.00:00:00" -MinPasswordAge:"1.00:00:00" -MinPasswordLength:"7" -PasswordHistoryCount:"24" -Precedence:"1" -ReversibleEncryptionEnabled:$false -ProtectedFromAccidentalDeletion:$true
Add-ADFineGrainedPasswordPolicySubject TestPswd -Subjects group1
```

#### <a name="bkmk_view_resultant_fgpp"></a>Schritt 4: Anzeigen eines Richtlinienergebnissatzes für einen Benutzer

Im folgenden Verfahren zeigen Sie an, die kennworteinstellungen für einen Benutzer, der ein Mitglied der Gruppe ist, der Sie in eine differenzierte Kennwortrichtlinie zugewiesen haben [Schritt 3: Erstellen eine neuen differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp).

##### <a name="to-view-a-resultant-set-of-policies-for-a-user"></a>So zeigen Sie einen Richtlinienergebnissatz für einen Benutzer an

1. Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2. Klicken Sie auf **Verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne im Dialogfeld **Navigationsknoten hinzufügen** aus. Klicken Sie anschließend auf **OK**.

3. Wählen Sie einen Benutzer, **test1** , die Mitglieder der Gruppe, **group1** , dass Sie mit in eine differenzierten Kennwortrichtlinie verknüpft [Schritt 3: Erstellen eine neuen differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp).

4. Klicken Sie auf **Resultierende Kennworteinstellungen anzeigen** im Bereich **Aufgaben**.

5. Überprüfen Sie die Kennworteinstellungsrichtlinie, und klicken Sie dann auf **Abbrechen**.

![Einführung in Active Directory-Verwaltungscenter](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```powershell
Get-ADUserResultantPasswordPolicy test1
```

#### <a name="bkmk_edit_fgpp"></a>Schritt 5: Bearbeiten einer differenzierten Kennwortrichtlinie

Im folgenden Verfahren bearbeiten Sie die differenzierte Kennwortrichtlinie, die Sie erstellt, in haben [Schritt 3: Erstellen einer neuen differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)

##### <a name="to-edit-a-fine-grained-password-policy"></a>So bearbeiten Sie eine differenzierte Kennwortrichtlinie

1. Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2. Klicken Sie auf **Verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne im Dialogfeld **Navigationsknoten hinzufügen** aus. Klicken Sie anschließend auf **OK**.

3. Erweitern Sie im ADAC-**Navigationsbereich** das Element **System**, und klicken Sie dann auf **Kennworteinstellungscontainer**.

4. Wählen Sie die differenzierte Kennwortrichtlinie, die Sie erstellt, in haben [Schritt 3: Erstellen eine neuen differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp) , und klicken Sie auf **Eigenschaften** in die **Aufgaben** Bereich.

5. Ändern Sie unter **Kennwortchronik erzwingen** den Wert von **Anzahl der gespeicherten Kennwörter** auf **30**.

6. Klicken Sie auf **OK**.

![Einführung in Active Directory-Verwaltungscenter](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```powershell
Set-ADFineGrainedPasswordPolicy TestPswd -PasswordHistoryCount:"30"
```

#### <a name="bkmk_delete_fgpp"></a>Schritt 6: Löschen einer differenzierten Kennwortrichtlinie

##### <a name="to-delete-a-fine-grained-password-policy"></a>So löschen Sie eine differenzierte Kennwortrichtlinie

1. Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2. Klicken Sie auf **Verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne im Dialogfeld **Navigationsknoten hinzufügen** aus. Klicken Sie anschließend auf **OK**.

3. Erweitern Sie im ADAC-Navigationsbereich das Element **System** , und klicken Sie dann auf **Kennworteinstellungscontainer**.

4. Wählen Sie die differenzierte Kennwortrichtlinie, die Sie erstellt, in haben [Schritt 3: Erstellen eine neuen differenzierten Kennwortrichtlinie](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp) und klicken Sie in der **Aufgaben** auf **Eigenschaften**.

5. Deaktivieren Sie das Kontrollkästchen **Vor versehentlichem Löschen schützen**, und klicken Sie auf **OK**.

6. Wählen Sie die differenzierte Kennwortrichtlinie aus, und klicken Sie im Bereich **Aufgaben** auf **Löschen**.

7. Klicken Sie im Bestätigungsdialogfeld auf **OK**.

![Einführung in Active Directory-Verwaltungscenter](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

```powershell
Set-ADFineGrainedPasswordPolicy -Identity TestPswd -ProtectedFromAccidentalDeletion $False
Remove-ADFineGrainedPasswordPolicy TestPswd -Confirm
```

## <a name="windows_powershell_history_viewer"></a>Windows PowerShell-Verlaufsanzeige

ADAC ist ein Benutzeroberflächentool, das auf Windows PowerShell basiert. In Windows Server 2012 und höher können IT-Administratoren ADAC, um Windows PowerShell für Active Directory-Cmdlets zu erhalten, mithilfe der Windows PowerShell History Viewer nutzen. Beim Ausführen von Aktionen in der Benutzeroberfläche werden dem Benutzer die entsprechenden Windows PowerShell-Befehle in Windows PowerShell History Viewer angezeigt. Dies ermöglicht es Administratoren, automatisierte Skripte zu erstellen und sich wiederholende Aufgaben zu reduzieren, wodurch sich die IT-Produktivität verbessert. Darüber hinaus wird diese Funktion verringert die Zeit zum Erlernen von Windows PowerShell für Active Directory und erhöht sich die Benutzer Ihre automatisierungsskripte korrekt funktionieren.

Beachten Sie Folgendes, wenn Sie die Windows PowerShell History Viewer in Windows Server 2012 oder höher verwenden:

- Um Windows PowerShell Script Viewer verwenden zu können, müssen Sie die Windows Server 2012 oder neuere Version von ADAC verwenden.

    > [!NOTE]
    > Sie können **Server-Manager** Remote Server-Verwaltungstools (RSAT) um die richtige Version des Active Directory-Verwaltungscenters zu verwenden, um die Verwaltung des Papierkorbs per Benutzeroberfläche zu installieren.
    >
    > Informationen zum Installieren der Remoteserver-Verwaltungstools, finden Sie im Artikel [Remoteserver-Verwaltungstools](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools).

- Haben Sie ein grundlegendes Verständnis der Windows PowerShell. So müssen Sie zum Beispiel wissen, wie das Piping in Windows PowerShell funktioniert. Weitere Informationen über Piping in Windows PowerShell finden Sie unter [Piping and the Pipeline in Windows PowerShell](https://technet.microsoft.com/library/ee176927.aspx).

### <a name="windows-powershell-history-viewer-step-by-step"></a>Schrittweise Anleitung zu Windows PowerShell History Viewer

In der folgenden Anleitung verwenden Sie Windows PowerShell History Viewer in ADAC, um ein Windows PowerShell-Skript zu erstellen.  Bevor Sie damit beginnen, müssen Sie den Benutzer **test1** aus der Gruppe **group1**entfernen.

#### <a name="to-construct-a-script-using-powershell-history-viewer"></a>So erstellen Sie ein Skript mithilfe von PowerShell History Viewer

1. Klicken Sie mit der rechten Maustaste auf das Windows PowerShell-Symbol, klicken Sie auf **als Administrator ausführen** und **dsac.exe** um ADAC zu öffnen.

2. Klicken Sie auf **Verwalten**, klicken Sie auf **Navigationsknoten hinzufügen** , und wählen Sie die entsprechende Zieldomäne im Dialogfeld **Navigationsknoten hinzufügen** aus. Klicken Sie anschließend auf **OK**.

3. Erweitern Sie unten im ADAC-Bildschirm den Bereich **Windows PowerShell History**.

4. Wählen Sie den Benutzer **test1** aus.

5. Klicken Sie auf **zur Gruppe hinzufügen...**  in die **Aufgaben** Bereich.

6. Navigieren Sie zu **group1**, und klicken Sie im Dialogfeld auf **OK**.

7. Wechseln Sie zu dem Bereich **Windows PowerShell History** , und suchen Sie den Befehl, der gerade generiert wurde.

8. Kopieren Sie den Befehl und fügen Sie ihn in einen Editor Ihrer Wahl ein, um Ihr Skript zu erstellen.

    So könnten Sie zum Beispiel den Befehl so ändern, dass ein anderer Benutzer zur Gruppe **group1** oder der Benutzer **test1** zu einer anderen Gruppe hinzugefügt wird.

## <a name="see-also"></a>Siehe auch

[Erweiterte AD DS-Verwaltung mithilfe von Active Directory-Verwaltungscenter &#40;Stufe 200&#41;](Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md)
