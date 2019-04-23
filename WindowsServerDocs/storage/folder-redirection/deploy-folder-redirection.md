---
title: Bereitstellen von Ordnerumleitung, Offlinedateien
description: Gewusst wie Windows-Server verwenden, um die Umleitung des Ordners mit Offlinedateien für Windows-Clientcomputer bereitstellen.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 33942db34314e0ff60b24d4b9c8e5e33b4ca92fd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831571"
---
# <a name="deploy-folder-redirection-with-offline-files"></a>Bereitstellen von Ordnerumleitung, Offlinedateien

>Gilt für: Windows 10, Windows 7, Windows 8, Windows 8.1, Windows Server 2008 R2, WindowsServer 2012, Windows Server 2012 R2, WindowsServer 2016, Windows Vista

Dieses Thema beschreibt, wie Sie Windows Server, um die Umleitung des Ordners mit Offlinedateien für Windows-Clientcomputer bereitstellen.

Eine Liste der zuletzt vorgenommenen Änderungen zu diesem Thema finden Sie [Änderungsverlauf](#change-history).

>[!IMPORTANT]
>Aufgrund der sicherheitsänderungen in [MS16-072](https://support.microsoft.com/en-us/help/3163622/ms16-072-security-update-for-group-policy-june-14-2016), wir aktualisiert [Schritt 3: Erstellen Sie ein Gruppenrichtlinienobjekt für die Ordnerumleitung](#step-3:-create-a-gpo-for-folder-redirection) dieses Themas, Windows kann die Ordnerumleitung-Richtlinie ordnungsgemäß angewendet (und nicht zurückgesetzt werden umgeleitete Ordnern auf betroffenen Computern).

## <a name="prerequisites"></a>Vorraussetzungen

### <a name="hardware-requirements"></a>Hardwareanforderungen

Ordnerumleitung erfordert einen X64 oder X86-basierten Computer. Sie wird nicht von Windows® RT unterstützt.

### <a name="software-requirements"></a>Softwareanforderungen

Ordnerumleitung hat die folgenden softwareanforderungen:

- Um die Ordnerumleitung zu verwalten, müssen Sie als Mitglied der Sicherheitsgruppe "Domänenadministratoren", die Sicherheitsgruppe der Organisationsadministratoren oder der Sicherheitsgruppe der Gruppenrichtlinienersteller-Besitzer angemeldet sein.
- Clientcomputer müssen Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ausführen.
- Clientcomputer müssen zu den Active Directory-Domänendiensten (AD DS) hinzugefügt werden, die Sie verwalten.
- Ein Computer müssen mit Gruppenrichtlinienverwaltung und installiertem Active Directory-Verwaltungscenter verfügbar sein.
- Ein Dateiserver muss zum Hosten der umgeleitete Ordner verfügbar sein.
    - Wenn die Dateifreigabe DFS-Namespaces verwendet, müssen die DFS-Ordner (Verknüpfungen) ein einzelnes Ziel aufweisen, damit Benutzer keine in Konflikt stehenden Änderungen auf unterschiedlichen Servern vornehmen können.
    - Wenn die Dateifreigabe die DFS-Replikation zum Replizieren der Inhalte mit einem anderen Server verwendet, dürfen Benutzer nur in der Lage sein, auf den Quellserver zuzugreifen, damit Benutzer keine in Konflikt stehenden Änderungen auf unterschiedlichen Servern vornehmen können.
    - Bei eine gruppierten Dateifreigabe verwenden möchten, deaktivieren Sie fortlaufende Verfügbarkeit für die Dateifreigabe, um Leistungsprobleme mit Ordnerumleitung und Offlinedateien zu vermeiden. Offlinedateien kann darüber hinaus nicht in den Offlinemodus wechseln, 3 bis 6 Minuten, nachdem ein Benutzer den Zugriff auf eine fortlaufend verfügbare Dateifreigabe, verliert, was Benutzer stören kann, die noch nicht von Offlinedateien immer Offlinemodus verwenden.

>[!NOTE]
>Einige neuere Funktionen in Sachen Ordnerumleitung müssen zusätzliche Clientcomputer- und Active Directory-Schema-Anforderungen. Weitere Informationen finden Sie unter [Bereitstellen von primären Computern](deploy-primary-computers.md), [deaktivieren Offlinedateien auf Ordner](disable-offline-files-on-folders.md), [aktivieren immer Offline-Modus](enable-always-offline.md), und [aktivieren optimiert Ordner verschieben ](enable-optimized-moving.md).

## <a name="step-1-create-a-folder-redirection-security-group"></a>Schritt 1: Erstellen einer Sicherheitsgruppe für Ordner-Umleitung

Wenn Ihre Umgebung nicht bereits mit Ordnerumleitung eingerichtet wurde, ist der erste Schritt, um eine Sicherheitsgruppe zu erstellen, die alle Benutzer enthält, zu denen Sie die Richtlinie für die Ordnerumleitung anwenden möchten.

Hier wird eine Sicherheitsgruppe für die Ordnerumleitung zu erstellen:

1. Server-Manager auf einem Computer mit Active Directory-Verwaltungscenter öffnen installiert.
2. Auf der **Tools** , wählen Sie im Menü **Active Directory-Verwaltungscenter**. Das Active Directory-Verwaltungscenter wird angezeigt.
3. Mit der rechten Maustaste die entsprechende Domäne oder Organisationseinheit auswählen **neu**, und wählen Sie dann **Gruppe**.
4. Geben Sie im Fenster **Gruppe erstellen** im Abschnitt **Gruppe** die folgenden Einstellungen an:
    - Geben Sie in das Feld **Gruppenname** den Namen der Sicherheitsgruppe ein, z. B.: **Ordner-Umleitung Benutzer**.
    - In **Gruppenbereich**Option **Sicherheit**, und wählen Sie dann **Global**.
5. In der **Mitglieder** wählen Sie im Abschnitt **hinzufügen**. Das Dialogfeld zum Auswählen von Benutzern, Kontakten Computern, Dienstkonten oder Gruppen wird angezeigt.
6. Geben Sie die Namen der Benutzer oder-Gruppen ein, wählen Sie zum Bereitstellen der Ordnerumleitung werden sollen **OK**, und wählen Sie dann **OK** erneut aus.

## <a name="step-2-create-a-file-share-for-redirected-folders"></a>Schritt 2: Erstellen einer Dateifreigabe für umgeleitete Ordner

Wenn Sie nicht bereits über eine Dateifreigabe für umgeleitete Ordner verfügen, verwenden Sie das folgende Verfahren zum Erstellen einer Dateifreigabe auf einem Server mit Windows Server 2012.

>[!NOTE]
>Einige Funktionen weichen möglicherweise voneinander ab oder sind nicht verfügbar, wenn Sie eine Dateifreigabe auf einem Server mit einer anderen Windows-Version erstellen.

Hier wird eine Dateifreigabe unter Windows Server 2012 und Windows Server 2016 zu erstellen:

1. Wählen Sie im Navigationsbereich des Server-Manager **Datei- und Speicherdienste**, und wählen Sie dann **Freigaben** auf der Seite "Freigaben" anzuzeigen.
2. In der **Freigaben** Kachel wählen **Aufgaben**, und wählen Sie dann **neue Freigabe**. Der Assistent für neue Freigaben wird angezeigt.
3. Auf der **Profil auswählen** Seite **SMB-Freigabe – schnell**. Wenn Sie Resource Manager für Dateiserver installiert haben und ordnerverwaltungseigenschaften verwenden, wählen Sie stattdessen **SMB-Freigabe - erweitert**.
4. Wählen Sie auf der Seite **Freigabeort** den Server und das Volume aus, auf dem Sie die Freigabe erstellen möchten.
5. Auf der **Freigabename** geben einen Namen für die Freigabe (z. B. **Benutzer$**) in der **Freigabename** Feld.
    >[!TIP]
    >Wenn Sie die Freigabe zu erstellen, die Freigabe ausblenden, indem Sie platzieren einen ```$``` nach dem Freigabenamen. Dadurch wird die Freigabe bei informellen Browsern ausgeblendet.
6. Auf der **Weitere Einstellungen** Seite das fortlaufende Verfügbarkeit aktivieren, deaktivieren, falls vorhanden, und wählen Sie optional die **zugriffsbasierte Aufzählung aktivieren** und **DatenzugriffVerschlüsseln** Kontrollkästchen.
7. Auf der **Berechtigungen** Seite **Berechtigungen anpassen...** . Das Dialogfeld "Erweiterte Sicherheitseinstellungen" wird angezeigt.
8. Wählen Sie **Vererbung deaktivieren**, und wählen Sie dann **vererbte Berechtigungen in explizite Berechtigungen im Objekt konvertieren**.
9. Legen Sie die Berechtigungen, als Tabelle 1 beschrieben und in Abbildung 1 dargestellt, Berechtigungen für nicht aufgeführte Gruppen und Konten entfernen, und fügen Sie spezielle Berechtigungen in die Ordner-Umleitung-Benutzergruppe, die Sie in Schritt 1 erstellt haben.
    
    ![Festlegen der Berechtigungen für die umgeleiteten Ordner-Freigabe](media/deploy-folder-redirection/setting-the-permissions-for-the-redirected-folders-share.png)
    
    **Abbildung 1** Festlegen der Berechtigungen aus, für die umgeleiteten Ordner freigeben
10. Wenn Sie das Profil **SMB-Freigabe – Erweitert** auswählen, müssen Sie auf der Seite **Verwaltungseigenschaften** unter **Benutzerdateien** den Wert "Ordnerverwendung" auswählen.
11. Wenn Sie das Profil **SMB-Freigabe – Erweitert** auswählen, können Sie auf der Seite **Kontingent** optional ein Kontingent auswählen, das für die Benutzer der Freigabe gelten soll.
12. Auf der **Bestätigung** Seite **erstellen.**

### <a name="required-permissions-for-the-file-share-hosting-redirected-folders"></a>Erforderliche Berechtigungen für die Datei freigeben umgeleiteten Ordner hosten

<table>
<tbody>
<tr class="odd">
<td>Benutzerkonto</td>
<td>Access</td>
<td>Betrifft</td>
</tr>
<tr class="even">
<td>System</td>
<td>Vollzugriff</td>
<td>Dieser Ordner, die Unterordner und Dateien</td>
</tr>
<tr class="odd">
<td>Administratoren</td>
<td>Vollzugriff</td>
<td>Nur dieser Ordner</td>
</tr>
<tr class="even">
<td>Ersteller/Besitzer</td>
<td>Vollzugriff</td>
<td>Nur Unterordner und Dateien</td>
</tr>
<tr class="odd">
<td>Sicherheitsgruppe der Benutzer, die Daten in der Freigabe (Ordner-Umleitung-Benutzer) speichern</td>
<td>Ordner auflisten / Daten lesen<sup>1</sup><br />
<br />
Ordner erstellen / Daten anhängen<sup>1</sup><br />
<br />
Attribute lesen<sup>1</sup><br />
<br />
Erweiterte Attribute lesen<sup>1</sup><br />
<br />
Berechtigungen zum Lesen von<sup>1</sup></td>
<td>Nur dieser Ordner</td>
</tr>
<tr class="even">
<td>Andere Gruppen und Konten</td>
<td>Keine (entfernen)</td>
<td></td>
</tr>
</tbody>
</table>

1 Erweiterte Berechtigungen

## <a name="step-3-create-a-gpo-for-folder-redirection"></a>Schritt 3: Erstellen Sie ein Gruppenrichtlinienobjekt für die Ordnerumleitung

Wenn Sie nicht bereits über ein Gruppenrichtlinienobjekt erstellt, die für die für die Ordnerumleitung verfügen, verwenden Sie das folgende Verfahren zum Erstellen.

Hier wird ein Gruppenrichtlinienobjekt für die Ordnerumleitung zu erstellen:

1. Öffnen Sie den Server-Manager auf einem Computer, auf dem die Gruppenrichtlinienverwaltung installiert ist.
2. Von der **Tools** , wählen Sie im Menü **Gruppenrichtlinienverwaltung**.
3. Mit der rechten Maustaste die Domäne oder Organisationseinheit, in dem Sie Ordnerumleitung einrichten, und wählen Sie dann möchten **erstellen Sie ein Gruppenrichtlinienobjekt in dieser Domäne, und hier**.
4. In der **neues Gruppenrichtlinienobjekt** Dialogfeld Geben Sie einen Namen für das Gruppenrichtlinienobjekt (z. B. **Ordnerumleitungseinstellungen**), und wählen Sie dann **OK**.
5. Klicken Sie mit der rechten Maustaste auf das neu erstellte Gruppenrichtlinienobjekt und deaktivieren Sie das Kontrollkästchen **Verknüpfung aktiviert** . Dadurch wird verhindert, dass das Gruppenrichtlinienobjekt angewendet wird, bis Sie es konfiguriert haben.
6. Wählen Sie das Gruppenrichtlinienobjekt aus. In der **Sicherheitsfilterung** Teil der **Bereich** Registerkarte **authentifizierte Benutzer**, und wählen Sie dann **entfernen** um zu verhindern, dass das GPO für alle Benutzer angewendet werden.
7. In der **Sicherheitsfilterung** wählen Sie im Abschnitt **hinzufügen**.
8. In der **Select User, Computer oder Gruppe** (Dialogfeld), Typ, der den Namen der Sicherheitsgruppe in Schritt 1 erstellte Gruppe (z. B. **Ordner-Umleitung Benutzer**), und wählen Sie dann **OK**.
9. Wählen Sie die **Delegierung** Registerkarte **hinzufügen**, Typ **authentifizierte Benutzer**Option **OK**, und wählen Sie dann **OK** erneut auf die Standardeinstellung übernehmen von Berechtigungen zum Lesen.
    
    Dieser Schritt ist notwendig, da Änderungen der Sicherheit in vorgenommenen [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14-2016).

>[!IMPORTANT]
>Aufgrund der sicherheitsänderungen in [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14-2016), Sie müssen nun die Leseberechtigungen für authentifizierte Benutzer delegiert Gruppe auf das Gruppenrichtlinienobjekt für die Ordnerumleitung gewähren – andernfalls das Gruppenrichtlinienobjekt auf Benutzer angewendet wird nicht oder wenn es bereits angewendet wird, wird das Gruppenrichtlinienobjekt Entfernt das Umleiten von Ordnern auf dem lokalen Computer zurück. Weitere Informationen finden Sie unter [bereitstellen Group Policy Security Update MS16-072](https://blogs.technet.microsoft.com/askds/2016/06/22/deploying-group-policy-security-update-ms16-072-kb3163622/).

## <a name="step-4-configure-folder-redirection-with-offline-files"></a>Schritt 4: Konfigurieren der ordnerumleitung mit Offlinedateien

Bearbeiten Sie nach der Erstellung des Gruppenrichtlinienobjekts für für die Ordnerumleitung die gruppenrichtlinieneinstellungen zum Aktivieren und Konfigurieren der Ordnerumleitung, wie im folgenden Verfahren beschrieben.

>[!NOTE]
>Offlinedateien ist für den umgeleiteten Ordnern auf Windows-Clientcomputern standardmäßig aktiviert und deaktiviert auf Computern unter Windows Server, es sei denn, vom Benutzer geändert. Verwenden Sie zum Verwenden der Gruppenrichtlinie zu steuern, ob Offlinedateien aktiviert ist, die **zulassen oder verbieten die Verwendung der Funktion für Offlinedateien** richtlinieneinstellung.
> Weitere Informationen zu einigen der anderen Offline Dateien gruppenrichtlinieneinstellungen, finden Sie unter [Aktivieren erweiterter Offline Funktion](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn270369(v%3dws.11)>), und [Konfigurieren der Gruppenrichtlinie für Offlinedateien](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc759721(v%3dws.10)>).

Hier ist Ordnerumleitung in Gruppenrichtlinien konfigurieren:

1. In der Gruppenrichtlinien-Verwaltungskonsole mit der Maustaste des Gruppenrichtlinienobjekts, das Sie erstellt haben (z. B. **Ordnerumleitungseinstellungen**), und wählen Sie dann **bearbeiten**.
2. Wechseln Sie in der Gruppenrichtlinienverwaltungs-Editor-Fenster zu **Benutzerkonfiguration**, klicken Sie dann **Richtlinien**, klicken Sie dann **Windows-Einstellungen**, und klicken Sie dann **Ordner Umleitung**.
3. Mit der rechten Maustaste in eines Ordners, die Sie umleiten möchten (z. B. **Dokumente**), und wählen Sie dann **Eigenschaften**.
4. In der **Eigenschaften** im Dialogfeld aus der **Einstellung** Kontrollkästchen **Basic - leitet alle Ordner am gleichen Speicherort**.

    > [!NOTE]
    > Wählen Sie zum Anwenden von Umleitung des Ordners auf Clientcomputern mit Windows XP oder Windows Server 2003 die **Einstellungen** Registerkarte, und wählen Sie die **Umleitungsrichtlinie auch auf Windows 2000, Windows 2000 Server, Windows XP, anwenden und Windows Server 2003-Betriebssysteme** Kontrollkästchen.
5. In der **Zielspeicherort für die Ordner** wählen Sie im Abschnitt **erstellen Sie einen Ordner für jeden Benutzer im Stammpfad** , und klicken Sie dann in der **Stammpfad** geben den Pfad zu der Datei-Freigabe speichern Ordner, z. B. umgeleitet:  **\\ \\fs1.corp.contoso.com\\Benutzer$**
6. Wählen Sie die **Einstellungen** Registerkarte, und klicken Sie in der **Entfernung der Richtlinie** optional wählen Sie im Abschnitt **zurück an den Speicherort des lokalen Benutzerprofils Ordner umleiten, wenn die Richtlinie entfernt wird** (diese Einstellung können Sie machen Ordnerumleitung Adminisitrators und Benutzern besser vorhersagbares Verhalten).
7. Wählen Sie **OK**, und wählen Sie dann **Ja** im Dialogfeld "Warnung".

## <a name="step-5-enable-the-folder-redirection-gpo"></a>Schritt 5: Aktivieren der Ordnerumleitung GPO

Nachdem Sie die Gruppenrichtlinie zur Ordnerumleitung-Einstellungen konfiguriert haben, werden im nächste Schritt aktivieren Sie das Gruppenrichtlinienobjekt, sodass es auf den betroffenen Benutzer angewendet werden.

>[!TIP]
>Wenn Sie die Unterstützung primärer Computer oder weiterer Richtlinieneinstellungen implementieren möchten, sollten Sie das jetzt vornehmen, bevor Sie das Gruppenrichtlinienobjekt aktivieren. Dadurch wird verhindert, dass Benutzerdaten auf nicht primäre Computer kopiert werden, bevor die Unterstützung primärer Computer aktiviert ist.

Hier ist das Gruppenrichtlinienobjekt für die Ordnerumleitung zu aktivieren:

1. Öffnen Sie die Gruppenrichtlinienverwaltung.
2. Mit der rechten Maustaste in des Gruppenrichtlinienobjekts, das Sie erstellt haben, und wählen Sie dann **Verknüpfung aktiviert**. Es wird ein Kontrollkästchen neben dem Menüelement angezeigt.

## <a name="step-6-test-folder-redirection"></a>Schritt 6: Testen Sie die Ordnerumleitung

Um die Ordnerumleitung zu testen, melden Sie sich auf einem Computer mit einem Benutzerkonto an, die für die Ordnerumleitung konfiguriert. Bestätigen Sie, dass die Ordner und Profile umgeleitet werden.

Hier ist zum Testen der Umleitung des Ordners ein:

1. Melden Sie sich an einem primären Computer (Wenn Sie die Unterstützung primärer Computer aktiviert haben) mit einem Benutzerkonto an, die für die Sie die Ordnerumleitung aktiviert haben.
2. Wenn sich der Benutzer zuletzt an dem Computer angemeldet hat, öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten und geben Sie folgenden Befehl ein, um sicherzustellen, dass die aktuellsten Gruppenrichtlinieneinstellungen auf dem Clientcomputer angewendet werden.
    
    ```PowerShell
    gpupdate /force
    ```
3. Öffnen Sie den Datei-Explorer.
4. Mit der rechten Maustaste in eines umgeleiteten Ordners (z. B. die Ordner Eigene Dokumente in der Bibliothek Dokumente), und wählen Sie dann **Eigenschaften**.
5. Wählen Sie die **Speicherort** Registerkarte, und bestätigen Sie, dass der Pfad die Dateifreigabe angezeigt, Sie anstelle eines lokalen Pfads angegeben.

## <a name="appendix-a-checklist-for-deploying-folder-redirection"></a>Anhang A: Prüfliste für die Bereitstellung der Ordnerumleitung

|Status|Aktion|
|:---:|---|
|☐<br>☐<br>☐|1. Bereiten Sie die Domäne vor<br>-Beitritts von Computern zur Domäne<br>– Erstellen von Benutzerkonten|
|☐<br><br><br>|2. Erstellen Sie die Sicherheitsgruppe für die Ordnerumleitung<br>-Group-Name:<br>-Mitglieder:|
|☐<br><br>|3. Erstellen einer Dateifreigabe für umgeleitete Ordner<br>-Dateifreigabename:|
|☐<br><br>|4. Erstellen Sie ein Gruppenrichtlinienobjekt für die Ordnerumleitung<br>-GPO-Name:|
|☐<br><br>☐<br>☐<br>☐<br>☐<br>☐|5. Konfigurieren von Einstellungen für Ordnerumleitung und Offlinedateien<br>-Die umgeleiteten Ordner:<br>-Windows 2000, Windows XP und Windows Server 2003-Unterstützung aktiviert?<br>-Offlinedateien aktiviert? (auf Windows-Clientcomputern standardmäßig aktiviert)<br>– Always Offline-Modus aktiviert?<br>-Hintergrundsynchronisierung aktiviert?<br>– Optimierte Verschieben der umgeleitete Ordner aktiviert?|
|☐<br><br>☐<br><br>☐<br>☐|6. (Optional) Aktivieren Sie die Unterstützung primärer computer<br>-Computer-basierte oder nutzerbasiert?<br>– Festlegen von hauptcomputern für Benutzer<br>-Speicherort der Benutzer- und primären computerzuordnungen:<br>– (Optional) aktivieren die Unterstützung primärer Computer für die Ordnerumleitung<br>– (Optional) aktivieren die Unterstützung primärer Computer für Roamingbenutzerprofile|
|☐|7. Aktivieren der Ordnerumleitung GPO|
|☐|8. Testen Sie die Ordnerumleitung|

## <a name="change-history"></a>Änderungsverlauf

In der folgenden Tabelle sind die wichtigsten Änderungen zu diesem Thema zusammengefasst.

|Datum|Beschreibung|Grund|
|---|---|---|
|18. Januar 2017|Einen Schritt hinzugefügt [Schritt 3: Erstellen Sie ein Gruppenrichtlinienobjekt für die Ordnerumleitung](#step-3:-create-a-gpo-for-folder-redirection) , delegieren Leseberechtigungen für authentifizierte Benutzer, das jetzt ist aufgrund der Aktualisierung der Gruppenrichtlinie Sicherheit erforderlich sind.|Kundenfeedback.|

## <a name="more-information"></a>Weitere Informationen

* [Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile](folder-redirection-rup-overview.md)
* [Bereitstellen von Hauptcomputern für Ordnerumleitung und Roamingbenutzerprofile](deploy-primary-computers.md)
* [Erweiterte Funktionen für Offlinedateien aktivieren](enable-always-offline.md)
* [Microsoft Support-Anweisung zu replizierten Benutzerprofildaten](https://blogs.technet.microsoft.com/askds/2010/09/01/microsofts-support-statement-around-replicated-user-profile-data/)
* [Querladen von Apps mit DISM](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh852635(v=win.10)>)
* [Problembehandlung bei Verpackung, Bereitstellung und Abfrage von Windows-Runtime-basierten apps](https://msdn.microsoft.com/library/windows/desktop/hh973484.aspx)