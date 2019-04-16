---
title: Bereitstellen von Ordnerumleitung, Offlinedateien
description: So verwenden Sie Windows Server Ordnerumleitung mit Offlinedateien auf Windows-Clientcomputern bereitstellen.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 33942db34314e0ff60b24d4b9c8e5e33b4ca92fd
ms.sourcegitcommit: 5549ac178f8f3d116e88761a95223063a636ac94
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/04/2018
ms.locfileid: "4376623"
---
# Bereitstellen von Ordnerumleitung, Offlinedateien

>Gilt für: Windows 10, Windows 7, Windows 8, Windows 8.1, Windows Server 2008 R2, WindowsServer 2012, Windows Server 2012 R2, WindowsServer 2016, Windows Vista

In diesem Thema wird beschrieben, wie Sie Windows Server verwenden, um Ordnerumleitung mit Offlinedateien auf Windows-Clientcomputern bereitstellen.

Eine Liste der aktuellen Änderungen an diesem Thema finden Sie unter [Änderungsprotokoll](#change-history).

>[!IMPORTANT]
>Aufgrund der Sicherheit Änderungen, die in [MS16-072](https://support.microsoft.com/en-us/help/3163622/ms16-072-security-update-for-group-policy-june-14-2016)vorgenommen, wir aktualisiert [Schritt 3: Erstellen eines Gruppenrichtlinienobjekts für Ordnerumleitung](#step-3:-create-a-gpo-for-folder-redirection) dieses Themas so, dass Windows kann ordnungsgemäß wenden Sie die Ordnerumleitung an (und nicht umgeleitete Ordner auf betroffene PCs zurückgesetzt).

## Voraussetzungen

### Hardwareanforderungen

Ordnerumleitung erfordert einen X64 oder X86-basierten Computer. Es wird nicht von Windows® RT zum Download zur unterstützt.

### Softwareanforderungen

Ordnerumleitung hat die folgenden softwareanforderungen:

- Um Ordnerumleitung zu verwalten, müssen Sie als Mitglied der Sicherheitsgruppe Domänen-Admins oder der Sicherheitsgruppe Administratoren in Unternehmen, die Sicherheitsgruppe Group Policy Creator Owners angemeldet sein.
- Clientcomputer müssen Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ausführen.
- Clientcomputer müssen die Active Directory-Domänendienste (AD DS) angehören, die Sie verwalten.
- Ein Computer muss verfügbar mit Gruppenrichtlinien-Verwaltungskonsole und Active Directory-Verwaltungscenter installiert sein.
- Ein Dateiserver muss zum Hosten von umgeleitete Ordner verfügbar sein.
    - Wenn die Dateifreigabe DFS-Namespaces verwendet, müssen die DFS-Ordner (Links) ein einzelnes Ziel zu verhindern, dass Benutzer in Konflikt stehenden Bearbeitungsschritte auf verschiedenen Servern vornehmen.
    - Wenn die Dateifreigabe DFS-Replikation zum Replizieren der Inhalte mit einem anderen Server verwendet, müssen Benutzer nur auf den Quellserver, Benutzer daran hindert auf verschiedenen Servern in Konflikt stehenden Bearbeitungsschritte zugreifen sein.
    - Wenn Sie eine gruppierten Dateifreigabe verwenden, deaktivieren Sie kontinuierlichen Verfügbarkeit für die Dateifreigabe, um Leistungsprobleme mit Ordnerumleitung und Offlinedateien zu vermeiden. Darüber hinaus kann Offlinedateien nicht Übergang zu offline-Modus 3 bis 6 Minuten nach dem ein Benutzer den Zugriff auf eine ständig verfügbare Dateifreigabe, verliert der Benutzer frustrierend sein könnte, die noch nicht immer Offlinemodus von Offlinedateien verwenden.

>[!NOTE]
>Einige neuere Features in Ordnerumleitung verfügen über zusätzliche Clientcomputer und Active Directory-Schema-Anforderungen. Weitere Informationen finden Sie unter [primäre Computer bereitstellen](deploy-primary-computers.md), [Offlinedateien in Ordnern deaktivieren](disable-offline-files-on-folders.md), [Aktivieren Sie immer Offlinemodus](enable-always-offline.md)und [ermöglichen das optimierte Ordner zu verschieben](enable-optimized-moving.md).

## Schritt 1: Erstellen einer Ordner Umleitung-Sicherheitsgruppe

Wenn Ihre Umgebung nicht bereits mit der Ordnerumleitung eingerichtet ist, ist der erste Schritt eine Sicherheitsgruppe erstellen, die alle Benutzer enthält, die ordnerumleitung-Richtlinien angewendet werden soll.

Hier ist eine Sicherheitsgruppe für Ordnerumleitung erstellen:

1. Open Server-Manager auf einem Computer mit Active Directory-Verwaltungscenter installiert ist.
2. Wählen Sie auf das Menü " **Extras** " **Active Directory-Verwaltungscenter**. Das Active Directory-Verwaltungscenter wird angezeigt.
3. Mit der rechten Maustaste der entsprechenden Domäne oder Organisationseinheit, wählen Sie **neu**, und wählen Sie dann die **Gruppe**.
4. Geben Sie im Fenster **Gruppe erstellen** im Abschnitt **Gruppe** die folgenden Einstellungen an:
    - Im **Namen der Gruppe**, geben Sie den Namen der Sicherheitsgruppe ein, z. B.: **Ordner Umleitung Benutzer**.
    - Wählen Sie im **Bereich Gruppe**die **Sicherheit**, und wählen Sie dann **Global**.
5. Wählen Sie im Abschnitt **Mitglieder** **Hinzufügen**. Das Dialogfeld zum Auswählen von Benutzern, Kontakten Computern, Dienstkonten oder Gruppen wird angezeigt.
6. Geben Sie die Namen der Benutzer oder Gruppen, die zum Bereitstellen von Ordnerumleitung, klicken Sie auf **OK**, und wählen Sie dann erneut auf **OK** werden soll.

## Schritt 2: Erstellen Sie eine Dateifreigabe für umgeleitete Ordner

Wenn Sie nicht bereits über eine Dateifreigabe für umgeleitete Ordner verfügen, verwenden Sie das folgende Verfahren, um eine Dateifreigabe auf einem Server mit Windows Server 2012 zu erstellen.

>[!NOTE]
>Einige Funktionen möglicherweise abweichen oder nicht verfügbar, wenn Sie die Dateifreigabe auf einem Server mit einer anderen Version von Windows Server erstellen.

Hier ist das Erstellen von einer Dateifreigabe auf Windows Server 2012 und Windows Server 2016:

1. Klicken Sie im Navigationsbereich Server-Manager wählen Sie **Datei- und Speicherdienste**, und wählen Sie dann **Freigaben** für die Freigaben Seite anzuzeigen.
2. Wählen Sie in der Kachel **Freigaben** **Aufgaben aus**, und wählen Sie dann auf **Neue Freigabe**. Der Assistent für neue wird angezeigt.
3. Wählen Sie auf der Seite **Profil auswählen** **SMB-Freigabe – schnell**. Wenn Sie Resource Manager für Dateiserver installiert haben und Ordnereigenschaften Management verwenden, wählen Sie stattdessen **SMB-Freigabe - Advanced**.
4. Wählen Sie auf der Seite **Teilen** der Server und das Volume, auf denen Sie die Bereitstellungsfreigabe erstellen möchten.
5. Geben Sie einen Namen für die Freigabe (z. B. **Benutzer$**) in das Feld **Name der Freigabe** , auf der Seite **Name der Freigabe** .
    >[!TIP]
    >Bei der Erstellung der Bereitstellungsfreigabe ausblenden die Freigabe Einfügen einer ```$``` nach der Name der Freigabe. Dadurch wird die Freigabe von einer zufälligen Browsern ausgeblendet.
6. Deaktivieren Sie auf der Seite **Andere Einstellungen** kontinuierlicher Verfügbarkeit aktivieren, wenn vorhanden, und wählen Sie optional die Kontrollkästchen **Aktivieren der zugriffsbasierten Aufzählung** und **Datenzugriff verschlüsseln** .
7. Wählen Sie auf der Seite " **Berechtigungen** " **... Berechtigungen anpassen**. Das Dialogfeld "Erweitert" wird angezeigt.
8. Wählen Sie **Deaktivieren der Vererbung**, und wählen Sie dann **Konvertieren von geerbten Berechtigungen in ausdrückliche Erlaubnis für dieses Objekt**.
9. Legen Sie die Berechtigungen als beschrieben in Tabelle 1 und dargestellt in Abbildung 1, Berechtigungen für nicht aufgeführten Gruppen und Konten entfernen und Hinzufügen von besondere Berechtigungen, die der Benutzer des Ordners Umleitung-Gruppe, die Sie in Schritt 1 erstellt haben.
    
    ![Festlegen der Berechtigungen für die Freigabe umgeleitete Ordner](media/deploy-folder-redirection/setting-the-permissions-for-the-redirected-folders-share.png)
    
    **Abbildung 1** Festlegen der Berechtigungen für die Freigabe umgeleitete Ordner
10. Wenn Sie das Profil **SMB-Freigabe - Advanced** ausgewählt haben, wählen Sie auf der Seite **Management-Eigenschaften** den **Benutzerdateien** Verwendung Ordner-Wert.
11. Wenn Sie das Profil **SMB-Freigabe - Advanced** auf der Seite das **Kontingent** haben wählen Sie optional ein Kontingent auf Benutzer der Freigabe anwenden.
12. Wählen Sie auf der Seite " **Bestätigung** " **erstellen.**

### Erforderliche Berechtigungen für die Datei Teilen hosten umgeleitete Ordner

<table>
<tbody>
<tr class="odd">
<td>Benutzerkonto</td>
<td>Access</td>
<td>Betrifft:</td>
</tr>
<tr class="even">
<td>System</td>
<td>Vollzugriff</td>
<td>Dieser Ordner, Unterordner und Dateien</td>
</tr>
<tr class="odd">
<td>Administratoren</td>
<td>Vollzugriff</td>
<td>Nur diesen Ordner</td>
</tr>
<tr class="even">
<td>Ersteller-Besitzer</td>
<td>Vollzugriff</td>
<td>Nur Unterordner und Dateien</td>
</tr>
<tr class="odd">
<td>Sicherheitsgruppe der Benutzer müssen von Daten freigeben (Ordner Umleitung Benutzer)</td>
<td>Ordner auflisten / Daten lesen<sup>1</sup><br />
<br />
Erstellen von Ordnern / Daten anhängen<sup>1</sup><br />
<br />
Lesen Sie Attribute<sup>1</sup><br />
<br />
Erweiterte Attribute lesen<sup>1</sup><br />
<br />
Berechtigungen Lesen<sup>1</sup></td>
<td>Nur diesen Ordner</td>
</tr>
<tr class="even">
<td>Gruppen und Konten</td>
<td>None (entfernen)</td>
<td></td>
</tr>
</tbody>
</table>

1 erweiterte Berechtigungen

## Schritt 3: Erstellen eines Gruppenrichtlinienobjekts für Ordnerumleitung

Wenn Sie nicht bereits ein Gruppenrichtlinienobjekts für Ordnerumleitung Einstellungen erstellt haben, verwenden Sie das folgende Verfahren, um eine zu erstellen.

Hier sehen Sie Informationen zum Erstellen eines Gruppenrichtlinienobjekts für Ordnerumleitung:

1. Open Server-Manager auf einem Computer mit Gruppenrichtlinien-Verwaltungskonsole installiert.
2. Wählen Sie aus dem Menü " **Extras** " **Die Gruppenrichtlinien-Verwaltungskonsole**.
3. Mit der rechten Maustaste die Domäne oder Organisationseinheit, in dem Sie Ordnerumleitung einrichten möchten, und wählen Sie dann **Erstellen Sie ein Gruppenrichtlinienobjekt in dieser Domäne und hier verknüpfen**.
4. Klicken Sie im Dialogfeld **Neues Gruppenrichtlinienobjekt** Geben Sie einen Namen für das Gruppenrichtlinienobjekt (z. B. **Ordner Umleitung Einstellungen**), und wählen Sie dann auf **OK**.
5. Mit der rechten Maustaste in des neu erstellten Gruppenrichtlinienobjekts, und deaktivieren Sie das Kontrollkästchen " **Aktiviert** ". Dadurch wird verhindert, dass das Gruppenrichtlinienobjekt angewendet wird, bis Sie es konfiguriert haben.
6. Wählen Sie das Gruppenrichtlinienobjekt. Im Abschnitt **Sicherheitsfilterung** der Registerkarte **Bereich** **Authentifizierte Benutzer**wählen Sie aus, und wählen Sie dann **Entfernen** , um zu verhindern, dass das Gruppenrichtlinienobjekt auf jeder angewendet wird.
7. Wählen Sie im Abschnitt **Sicherheitsfilterung** **Hinzufügen**.
8. Geben Sie im Dialogfeld **Benutzer, Computer oder Gruppe auswählen** den Namen der Sicherheitsgruppe ein, die Sie in Schritt 1 (z. B. **Ordner Umleitung Benutzer**) erstellt, und wählen Sie dann auf **OK**.
9. Wählen Sie die Registerkarte **Delegierung** , wählen Sie **Hinzufügen**, geben Sie **Authentifizierte Benutzer**, klicken Sie auf **OK**, und wählen Sie dann auf **OK** , um die Standard-Leseberechtigungen zu akzeptieren.
    
    Dieser Schritt ist aufgrund der Sicherheit Änderungen in [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14-2016)erforderlich.

>[!IMPORTANT]
>Aufgrund der Sicherheit, die Änderungen in [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14-2016), Sie jetzt zuweisen müssen die Gruppe Authentifizierte Benutzer delegierte Berechtigungen lesen, um das Gruppenrichtlinienobjekt Folder Redirection - andernfalls keine GPO angewendet abrufen, Benutzer oder wenn sie bereits angewendet wird, das Gruppenrichtlinienobjekt entfernt wird, Umleitung Ordner zurück an den lokalen PC. Weitere Informationen finden Sie unter [Bereitstellen von Group Policy Security Update MS16-072](https://blogs.technet.microsoft.com/askds/2016/06/22/deploying-group-policy-security-update-ms16-072-kb3163622/).

## Schritt 4: Konfigurieren von ordnerumleitung mit Offlinedateien

Bearbeiten Sie nach dem Erstellen eines Gruppenrichtlinienobjekts für Ordnerumleitung-Einstellungen, die Einstellungen für Gruppenrichtlinien zum Aktivieren und Konfigurieren von Ordnerumleitung, wie im folgenden Verfahren beschrieben.

>[!NOTE]
>Offlinedateien ist standardmäßig für umgeleitete Ordner auf dem Windows-Clientcomputer aktiviert und deaktiviert auf Computern unter Windows Server, es sei denn, die vom Benutzer geändert. Verwenden Sie zum Verwenden von Gruppenrichtlinien zu steuern, ob Offlinedateien aktiviert ist, die **Zulassen oder verbieten der Verwendung von Offlinedateien-Funktion** Einstellung.
> Finden Sie Informationen zu einigen der anderen Offline Dateien Gruppenrichtlinien-Einstellungen [Aktivieren Sie erweiterte Offline Dateien Funktionen](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn270369(v%3dws.11)>)und [Konfigurieren von Gruppenrichtlinien für Offlinedateien](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc759721(v%3dws.10)>).

Hier sehen Sie Ordnerumleitung in der Gruppenrichtlinie zu konfigurieren:

1. Klicken Sie in der Gruppenrichtlinien-Verwaltungskonsole mit der rechten Maustaste im GPOs, das Sie (z. B. **Ordner Umleitung Einstellungen**) erstellt haben, und wählen Sie dann **Bearbeiten**.
2. Navigieren Sie im Gruppenrichtlinienverwaltungs-Editor-Fenster zu **Benutzerkonfiguration**, **Richtlinien**, und klicken Sie dann **Windows-Einstellungen**und dann **Ordnerumleitung**.
3. Klicken Sie auf einen Ordner, den Sie umleiten (z. B. **Dokumente**), und wählen Sie dann **Eigenschaften**möchten.
4. Wählen Sie im Dialogfeld " **Eigenschaften** " aus dem Feld **Einstellung** **Basic – alle Ordner am selben Speicherort umleiten**.

    > [!NOTE]
    > Um Ordnerumleitung auf Clientcomputern mit Windows XP oder Windows Server 2003 anwenden, wählen die Registerkarte " **Einstellungen** " aus, und wählen Sie wenden Sie die **auch Umleitung an Windows 2000, Windows 2000 Server, Windows XP und Windows Server 2003-Betriebssystem Systeme** Kontrollkästchen.
5. Klicken Sie im Abschnitt **Zielordner** , wählen Sie **einen Ordner für jeden Benutzer im Stammpfad erstellen** , und klicken Sie im **Stammpfad** Geben Sie den Pfad zur Dateifreigabe speichern umgeleitete Ordner, z. B.: **\\\fs1.corp.contoso.com\\ Benutzer$**
6. Wählen Sie die Registerkarte " **Einstellungen** ", und klicken Sie im Abschnitt **Entfernen der Richtlinie** optional wählen Sie **leiten Sie den Ordner zurück an den Ort des lokalen Benutzerprofils Wenn die Richtlinie entfernt wird** (diese Einstellung kann beitragen Ordnerumleitung mehr Verhalten wie erwartet für Adminisitrators und Benutzer).
7. Klicken Sie auf **OK**, und wählen Sie dann im Dialogfeld "Warnung" **Ja** .

## Schritt 5: Aktivieren der Ordnerumleitung GPO

Nachdem Sie die Ordner Umleitung von Gruppenrichtlinien-Einstellungen konfigurieren abgeschlossen haben, besteht der nächste Schritt, aktivieren Sie das GPO, zuzulassen, dass dieser auf den betroffenen Benutzer angewendet werden.

>[!TIP]
>Wenn Sie Unterstützung für primäre Computer oder andere Einstellungen für implementieren möchten, holen Sie dies jetzt, bevor Sie das Gruppenrichtlinienobjekt aktivieren. Dadurch wird verhindert, dass Benutzerdaten zum nicht primären Computer kopiert werden, bevor die Unterstützung für primäre Computer aktiviert ist.

Hier sehen Sie das Gruppenrichtlinienobjekt Folder Redirection zu aktivieren:

1. Open Group Policy Management.
2. Maustaste auf das Gruppenrichtlinienobjekt, das Sie erstellt haben, und wählen Sie dann die **Verknüpfung aktiviert**. Neben dem Menüelement wird ein Kontrollkästchen angezeigt.

## Schritt 6: Testen der Ordnerumleitung

Um Ordnerumleitung zu testen, melden Sie sich an einem Computer mit einem Benutzerkonto für Ordnerumleitung konfiguriert. Stellen Sie dann sicher, dass die Ordner und Profile umgeleitet werden.

Hier sehen Sie Ordnerumleitung zu testen:

1. Melden Sie sich mit einem primären Computer (Wenn Sie Unterstützung für primäre Computer aktiviert) mit einem Benutzerkonto für den Ordnerumleitung aktiviert haben.
2. Wenn der Benutzer zuvor auf dem Computer angemeldet hat, öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, und geben Sie dann den folgenden Befehl, um sicherzustellen, dass die neuesten gruppenrichtlinieneinstellungen auf dem Clientcomputer angewendet werden:
    
    ```PowerShell
    gpupdate /force
    ```
3. Öffnen Sie die Datei-Explorer.
4. Mit der rechten Maustaste eines umgeleiteten Ordners (z. B. den Ordner "Eigene Dokumente" in die Dokumentbibliothek), und wählen Sie dann **Eigenschaften**.
5. Wählen Sie die Registerkarte " **Speicherort** ", und stellen Sie sicher, dass der Pfad die Dateifreigabe anzeigt, die Sie anstelle von einem lokalen Pfad angegeben.

## Anhang A: Prüfliste für die Bereitstellung von Ordnerumleitung

|Status|Aktion|
|:---:|---|
|☐<br>☐<br>☐|1. Vorbereiten der Domäne<br>-Computern Domäne beitreten<br>– Erstellen von Benutzerkonten|
|☐<br><br><br>|2. Erstellen der Sicherheitsgruppe für Ordnerumleitung<br>-Gruppenname:<br>-Member:|
|☐<br><br>|3. erstellen Sie eine Dateifreigabe für umgeleitete Ordner<br>-Name der Freigabe Datei:|
|☐<br><br>|4. erstellen Sie ein Gruppenrichtlinienobjekt für Ordnerumleitung<br>-GPO Name:|
|☐<br><br>☐<br>☐<br>☐<br>☐<br>☐|5. konfigurieren Sie Ordnerumleitung und Offlinedateien Richtlinieneinstellungen<br>-Umgeleitete Ordner:<br>– Windows 2000, Windows XP und Windows Server 2003-Unterstützung aktiviert?<br>-Offlinedateien aktiviert? (standardmäßig auf Windows-Clientcomputern aktiviert)<br>-Immer Offline-Modus aktiviert ist?<br>-Datei hintergrundsynchronisierung aktiviert?<br>-Optimierte verschoben umgeleitete Ordner aktiviert?|
|☐<br><br>☐<br><br>☐<br>☐|6. (Optional) Aktivieren der primären Computer Unterstützung<br>-Computer-basierten oder benutzerbasierte?<br>-Festlegen der primären Computer für Benutzer<br>-Speicherort der Benutzer- und Hauptcomputer Zuordnungen:<br>-(Optional) Aktivieren der primären Computer Unterstützung für Ordnerumleitung<br>-(Optional) Aktivieren der primären Computer Unterstützung für Roamingbenutzerprofile|
|☐|7. Aktivieren der Ordnerumleitung GPO|
|☐|8. Test Ordnerumleitung|

## Änderungsverlauf

Die folgende Tabelle fasst einige der wichtigsten Änderungen an diesem Thema.

|Date|Beschreibung|Grund|
|---|---|---|
|18 Januar 2017|Einen Schritt hinzugefügt [Schritt 3: Erstellen eines Gruppenrichtlinienobjekts für Ordnerumleitung](#step-3:-create-a-gpo-for-folder-redirection) Leseberechtigungen authentifizierte Benutzer delegieren der nun ist aufgrund einer Gruppenrichtlinie Sicherheitsupdate erforderlich.|Kundenfeedback.|

## Weitere Informationen

* [Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile](folder-redirection-rup-overview.md)
* [Bereitstellen von primären Computer für die Ordnerumleitung und Roamingbenutzerprofile](deploy-primary-computers.md)
* [Erweiterte Funktionen Offlinedateien aktivieren](enable-always-offline.md)
* [Microsoft Support-Anweisung ein, um Profildaten replizierten Benutzers](https://blogs.technet.microsoft.com/askds/2010/09/01/microsofts-support-statement-around-replicated-user-profile-data/)
* [Querladen von Apps mit DISM](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh852635(v=win.10)>)
* [Problembehandlung bei der Verpackung, Bereitstellung und Abfragen von Windows-Runtime-basierte apps](https://msdn.microsoft.com/library/windows/desktop/hh973484.aspx)