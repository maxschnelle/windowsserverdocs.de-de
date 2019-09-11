---
title: Bereitstellen der Ordner Umleitung mit Offlinedateien
description: Verwenden von Windows Server zum Bereitstellen der Ordner Umleitung mit Offlinedateien auf Windows-Client Computern.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: 90b3e3d0b5030f8c0140e54c8b0bf55317437427
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867305"
---
# <a name="deploy-folder-redirection-with-offline-files"></a>Bereitstellen der Ordner Umleitung mit Offlinedateien

>Gilt für: Windows 10, Windows 7, Windows 8, Windows 8.1, Windows Vista, Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2, Windows Server 2008 R2, Windows Server (halbjährlicher Kanal)

In diesem Thema wird beschrieben, wie Windows Server zum Bereitstellen der Ordner Umleitung mit Offlinedateien auf Windows-Client Computern verwendet wird.

Eine Liste der zuletzt vorgenommenen Änderungen an diesem Thema finden Sie unter [Change History (Änderungs Verlauf](#change-history)).

> [!IMPORTANT]
> Aufgrund der in [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14-2016)vorgenommenen Sicherheitsänderungen haben wir Schritt [3 aktualisiert: Erstellen Sie ein Gruppenrichtlinien Objekt für](#step-3-create-a-gpo-for-folder-redirection) die Ordner Umleitung dieses Themas, damit Windows die Ordner Umleitungs Richtlinie ordnungsgemäß anwenden kann (und die umgeleiteten Ordner auf betroffenen PCs nicht zurückgesetzt werden).

## <a name="prerequisites"></a>Erforderliche Komponenten

### <a name="hardware-requirements"></a>Hardwareanforderungen

Die Ordner Umleitung erfordert einen x64-basierten oder x86-basierten Computer. Sie wird von Windows® RT nicht unterstützt.

### <a name="software-requirements"></a>Softwareanforderungen

Die Ordner Umleitung umfasst die folgenden Softwareanforderungen:

- Zum Verwalten der Ordner Umleitung müssen Sie als Mitglied der Sicherheitsgruppe "Domänen Administratoren", der Sicherheitsgruppe "Unternehmens Administratoren" oder der Sicherheitsgruppe "Gruppenrichtlinie Creator-Besitzer" angemeldet sein.
- Auf Client Computern muss Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ausgeführt werden.
- Clientcomputer müssen zu den Active Directory-Domänendiensten (AD DS) hinzugefügt werden, die Sie verwalten.
- Ein Computer müssen mit Gruppenrichtlinienverwaltung und installiertem Active Directory-Verwaltungscenter verfügbar sein.
- Zum Hosten umgeleiteter Ordner muss ein Dateiserver verfügbar sein.
    - Wenn die Dateifreigabe DFS-Namespaces verwendet, müssen die DFS-Ordner (Verknüpfungen) ein einzelnes Ziel aufweisen, damit Benutzer keine in Konflikt stehenden Änderungen auf unterschiedlichen Servern vornehmen können.
    - Wenn die Dateifreigabe die DFS-Replikation zum Replizieren der Inhalte mit einem anderen Server verwendet, dürfen Benutzer nur in der Lage sein, auf den Quellserver zuzugreifen, damit Benutzer keine in Konflikt stehenden Änderungen auf unterschiedlichen Servern vornehmen können.
    - Wenn Sie eine gruppierte Dateifreigabe verwenden, deaktivieren Sie die fortlaufende Verfügbarkeit auf der Dateifreigabe, um Leistungsprobleme bei der Ordner Umleitung und der Offlinedateien zu vermeiden. Darüber hinaus wird Offlinedateien möglicherweise für 3-6 Minuten nicht in den Offline Modus versetzt, nachdem ein Benutzer den Zugriff auf eine fortlaufend verfügbare Dateifreigabe verloren hat, was Benutzer stören kann, die noch nicht den Modus "immer offline" von Offlinedateien verwenden.

> [!NOTE]
> Für einige neuere Features bei der Ordner Umleitung gelten zusätzliche Client Computer-und Active Directory Schema Anforderungen. Weitere Informationen finden Sie unter Bereitstellen von [primären Computern](deploy-primary-computers.md), [Deaktivieren der Offlinedateien für Ordner](disable-offline-files-on-folders.md), [Aktivieren des Modus "immer offline](enable-always-offline.md)" und Aktivieren des Verschiebens [optimierter Ordner](enable-optimized-moving.md).

## <a name="step-1-create-a-folder-redirection-security-group"></a>Schritt 1: Erstellen einer Sicherheitsgruppe für die Ordner Umleitung

Wenn Ihre Umgebung nicht bereits mit der Ordner Umleitung eingerichtet ist, besteht der erste Schritt darin, eine Sicherheitsgruppe zu erstellen, die alle Benutzer enthält, auf die Sie Einstellungen für die Ordner Umleitungs Richtlinie anwenden möchten.

So erstellen Sie eine Sicherheitsgruppe für die Ordner Umleitung:

1. Öffnen Sie Server-Manager auf einem Computer, auf dem Active Directory-Verwaltungs Center installiert ist.
2. Wählen Sie **im Menü Extras** **Active Directory Verwaltungs Center**aus. Das Active Directory-Verwaltungscenter wird angezeigt.
3. Klicken Sie mit der rechten Maustaste auf die entsprechende Domäne oder Organisationseinheit, und wählen Sie **neu**und dann **Gruppe**aus.
4. Geben Sie im Fenster **Gruppe erstellen** im Abschnitt **Gruppe** die folgenden Einstellungen an:
    - Geben Sie in das Feld **Gruppenname** den Namen der Sicherheitsgruppe ein, z. B.: **Ordner Umleitungs Benutzer**.
    - Wählen Sie unter **Gruppenbereich**die Option **Sicherheit**aus, und wählen Sie dann **Global**aus.
5. Wählen Sie im Abschnitt **Members** die Option **Hinzufügen**aus. Das Dialogfeld zum Auswählen von Benutzern, Kontakten Computern, Dienstkonten oder Gruppen wird angezeigt.
6. Geben Sie die Namen der Benutzer oder Gruppen ein, für die Sie die Ordner Umleitung bereitstellen möchten, wählen Sie **OK**aus, und klicken Sie dann erneut auf **OK** .

## <a name="step-2-create-a-file-share-for-redirected-folders"></a>Schritt 2: Erstellen einer Dateifreigabe für umgeleitete Ordner

Wenn Sie noch nicht über eine Dateifreigabe für umgeleitete Ordner verfügen, verwenden Sie das folgende Verfahren zum Erstellen einer Dateifreigabe auf einem Server, auf dem Windows Server 2012 ausgeführt wird.

> [!NOTE]
> Einige Funktionen weichen möglicherweise voneinander ab oder sind nicht verfügbar, wenn Sie eine Dateifreigabe auf einem Server mit einer anderen Windows-Version erstellen.

So erstellen Sie eine Dateifreigabe unter Windows Server 2019, Windows Server 2016 und Windows Server 2012:

1. Wählen Sie im Navigationsbereich Server-Manager die Option **Datei-und Speicherdienste**aus, und klicken Sie dann auf Freigaben **, um die** Seite Freigaben anzuzeigen.
2. Wählen Sie **auf der Kachel** Freigaben die Option **Tasks**aus, und wählen Sie dann **neue Freigabe**aus. Der Assistent für neue Freigaben wird angezeigt.
3. Wählen Sie auf der Seite **Profil auswählen** die Option **SMB-Freigabe – schnell**aus. Wenn Sie Datei Server Ressourcen-Manager installiert haben und Ordner Verwaltungs Eigenschaften verwenden, klicken Sie stattdessen auf **SMB-Freigabe-erweitert**.
4. Wählen Sie auf der Seite **Freigabeort** den Server und das Volume aus, auf dem Sie die Freigabe erstellen möchten.
5. Geben Sie auf der Seite **Freigabe Name** im Feld **Freigabe Name** einen Namen für die Freigabe ein (z. b. **Benutzer $** ).
    >[!TIP]
    >Wenn Sie die Freigabe erstellen, blenden Sie die Freigabe aus ```$``` , indem Sie eine nach dem Freigabe Namen einfügen. Dadurch wird die Freigabe von gelegentlichen Browsern ausgeblendet.
6. Deaktivieren Sie auf der Seite **andere Einstellungen** das Kontrollkästchen fortlaufende Verfügbarkeit aktivieren, falls vorhanden, und aktivieren Sie optional die Kontrollkästchen **Zugriffs basierte Enumeration aktivieren** und **Datenzugriff verschlüsseln** .
7. Wählen Sie auf der Seite **Berechtigungen** die Option **Berechtigungen anpassen...** aus. Das Dialogfeld "Erweiterte Sicherheitseinstellungen" wird angezeigt.
8. Wählen Sie **Vererbung deaktivieren**aus, und wählen Sie dann **geerbte Berechtigungen in explizite Berechtigung für dieses Objekt konvertieren aus**.
9. Legen Sie die Berechtigungen wie in Abbildung 1 beschrieben fest, und entfernen Sie die Berechtigungen für nicht aufgeführte Gruppen und Konten, und fügen Sie der Gruppe Ordner Umleitungs Benutzer, die Sie in Schritt 1 erstellt haben, spezielle Berechtigungen hinzu.
    
    ![Festlegen der Berechtigungen für die Freigabe von umgeleiteten Ordnern](media/deploy-folder-redirection/setting-the-permissions-for-the-redirected-folders-share.png)
    
    **Abbildung 1** Festlegen der Berechtigungen für die Freigabe von umgeleiteten Ordnern
10. Wenn Sie das Profil **SMB-Freigabe – Erweitert** auswählen, müssen Sie auf der Seite **Verwaltungseigenschaften** unter **Benutzerdateien** den Wert "Ordnerverwendung" auswählen.
11. Wenn Sie das Profil **SMB-Freigabe – Erweitert** auswählen, können Sie auf der Seite **Kontingent** optional ein Kontingent auswählen, das für die Benutzer der Freigabe gelten soll.
12. Wählen Sie auf der Seite **Bestätigung** die Option **erstellen aus.**

### <a name="required-permissions-for-the-file-share-hosting-redirected-folders"></a>Erforderliche Berechtigungen für die Dateifreigabe, auf der umgeleitete Ordner gehostet werden

| Benutzerkonto  | Zugriff  | Betrifft  |
| --------- | --------- | --------- |
| Benutzerkonto | Zugriff | Betrifft |
| System     | Vollzugriff        |    Dieser Ordner, die Unterordner und Dateien     |
| Administratoren     | Vollzugriff       | Nur dieser Ordner        |
| Ersteller/Besitzer     |   Vollzugriff      |   Nur Unterordner und Dateien      |
| Sicherheitsgruppe von Benutzern, die Daten auf der Freigabe ablegen müssen (Ordner Umleitungs Benutzer)     |   Ordner auflisten/Daten lesen *(erweiterte Berechtigungen)* <br /><br />Ordner erstellen/Daten anfügen *(erweiterte Berechtigungen)* <br /><br />Lese Attribute *(erweiterte Berechtigungen)* <br /><br />Erweiterte Attribute lesen *(erweiterte Berechtigungen)* <br /><br />Leseberechtigungen *(erweiterte Berechtigungen)*      |  Nur dieser Ordner       |
| Andere Gruppen und Konten     |  Keine (entfernen)       |         |

## <a name="step-3-create-a-gpo-for-folder-redirection"></a>Schritt 3: Erstellen eines Gruppenrichtlinien Objekts für die Ordner Umleitung

Wenn Sie noch kein Gruppenrichtlinien Objekt erstellt haben, das für die Ordner Umleitungseinstellungen erstellt wurde, verwenden Sie das folgende Verfahren, um eines zu erstellen.

So erstellen Sie ein Gruppenrichtlinien Objekt für die Ordner Umleitung:

1. Öffnen Sie den Server-Manager auf einem Computer, auf dem die Gruppenrichtlinienverwaltung installiert ist.
2. Wählen Sie **im Menü** Extras die Option **Gruppenrichtlinie Verwaltung**aus.
3. Klicken Sie mit der rechten Maustaste auf die Domäne oder die Organisationseinheit, in der Sie die Ordner Umleitung einrichten möchten, und wählen Sie dann Gruppenrichtlinien Objekt **in dieser Domäne erstellen und verknüpfen**aus.
4. Geben Sie im Dialogfeld **Neues** Gruppenrichtlinien Objekt einen Namen für das Gruppenrichtlinien Objekt ein (z. b. **Ordner Umleitungseinstellungen**), und klicken Sie dann auf **OK**.
5. Klicken Sie mit der rechten Maustaste auf das neu erstellte Gruppenrichtlinienobjekt und deaktivieren Sie das Kontrollkästchen **Verknüpfung aktiviert** . Dadurch wird verhindert, dass das Gruppenrichtlinienobjekt angewendet wird, bis Sie es konfiguriert haben.
6. Wählen Sie das Gruppenrichtlinienobjekt aus. Wählen Sie auf der Registerkarte **Bereich** im Abschnitt **Sicherheits Filterung** die Option **Authentifizierte Benutzer**aus, und wählen Sie dann **Entfernen** aus, um zu verhindern, dass das GPO auf alle Benutzer angewendet wird.
7. Wählen Sie im Abschnitt **Sicherheits Filterung** die Option **Hinzufügen**aus.
8. Geben Sie im Dialogfeld **Benutzer, Computer oder Gruppe auswählen** den Namen der Sicherheitsgruppe ein, die Sie in Schritt 1 erstellt haben (z. b. **Ordner Umleitungs Benutzer**), und klicken Sie dann auf **OK**.
9. Wählen Sie die Registerkarte **Delegierung** und dann **Hinzufügen**aus, geben Sie **Authentifizierte Benutzer**ein, klicken Sie auf **OK**, und klicken Sie dann erneut auf **OK** , um die Standard Berechtigungen für
    
    Dieser Schritt ist aufgrund von Sicherheitsänderungen, die in [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14-2016)vorgenommen werden, erforderlich.

> [!IMPORTANT]
> Aufgrund der in [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14-2016)vorgenommenen Sicherheitsänderungen müssen Sie der Gruppe "authentifizierte Benutzer" nun Delegierte Leseberechtigungen für das Gruppenrichtlinien Objekt für die Ordner Umleitung geben. andernfalls wird das Gruppenrichtlinien Objekt nicht auf Benutzer angewendet, oder wenn es bereits angewendet wurde, wird das Gruppenrichtlinien Objekt entfernt und umgeleitet. Ordner zurück zum lokalen PC. Weitere Informationen finden Sie unter Bereitstellen [Gruppenrichtlinie Sicherheitsupdates MS16-072](https://blogs.technet.microsoft.com/askds/2016/06/22/deploying-group-policy-security-update-ms16-072-kb3163622/).

## <a name="step-4-configure-folder-redirection-with-offline-files"></a>Schritt 4: Konfigurieren der Ordner Umleitung mit Offlinedateien

Nachdem Sie ein Gruppenrichtlinien Objekt für die Ordner Umleitungseinstellungen erstellt haben, bearbeiten Sie die Gruppenrichtlinie Einstellungen, um die Ordner Umleitung zu aktivieren und zu konfigurieren, wie im folgenden Verfahren beschrieben.

> [!NOTE]
> Offlinedateien ist standardmäßig für umgeleitete Ordner auf Windows-Client Computern aktiviert und auf Computern, auf denen Windows Server ausgeführt wird, deaktiviert, sofern Sie nicht vom Benutzer geändert werden. Wenn Sie mit Gruppenrichtlinie steuern möchten, ob Offlinedateien aktiviert ist, verwenden Sie die Richtlinien Einstellung **Offlinedateien der Funktion zulassen oder nicht zulassen** .
> Weitere Informationen zu einigen der anderen Offlinedateien Gruppenrichtlinie Einstellungen finden Sie unter [Aktivieren der erweiterten Offlinedateien Funktionalität](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn270369(v%3dws.11)>)und [Konfigurieren Gruppenrichtlinie für Offlinedateien](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc759721(v%3dws.10)>).

So konfigurieren Sie die Ordner Umleitung in Gruppenrichtlinie:

1. Klicken Sie in Gruppenrichtlinie Verwaltung mit der rechten Maustaste auf das von Ihnen erstellte GPO (z. b. **Ordner Umleitungseinstellungen**), und wählen Sie dann **Bearbeiten**aus.
2. Navigieren Sie im Fenster Gruppenrichtlinienverwaltungs-Editor zu **Benutzerkonfiguration**, **Richtlinien**, Windows- **Einstellungen**, und klicken Sie dann auf **Ordner Umleitung**.
3. Klicken Sie mit der rechten Maustaste auf einen Ordner, den Sie umleiten möchten (z. b. **Dokumente**), und wählen Sie dann **Eigenschaften**aus.
4. Wählen Sie im Dialogfeld **Eigenschaften** im Feld **Einstellung** die Option einfach aus, und **leiten Sie den Ordner jeder an denselben Speicherort um**.

    > [!NOTE]
    > Wenn Sie die Ordner Umleitung auf Client Computer unter Windows XP oder Windows Server 2003 anwenden möchten, klicken Sie auf die Registerkarte **Einstellungen** , und wählen Sie die Option **Richtlinie zum Anwenden der Umleitung auf Windows 2000, Windows 2000 Server, Windows XP und Windows Server 2003 aus.** Kontrollkästchen für Systeme.

5. Wählen Sie im Abschnitt **Zielordner Speicherort** die Option **einen Ordner für jeden Benutzer unter dem Stammpfad erstellen aus** , und geben Sie dann im Feld **Stammpfad** den Pfad zu der Dateifreigabe ein, in der umgeleitete Ordner gespeichert werden. Beispiel:  **\\ \\ FS1.Corp.contoso.com\\Benutzer $**
6. Wählen Sie die Registerkarte **Einstellungen** aus, und wählen Sie im Abschnitt **Entfernen der Richtlinie** optional **den Ordner an den Speicherort des lokalen Benutzerprofils zurückleiten aus, wenn die Richtlinie entfernt wird** (diese Einstellung kann dazu beitragen, die Ordner Umleitung zu ändern. vorhersagbares für Administratoren und Benutzer).
7. Wählen Sie **OK**aus, und wählen Sie dann im Dialogfeld Warnung die Option **Ja** aus.

## <a name="step-5-enable-the-folder-redirection-gpo"></a>Schritt 5: Aktivieren des Ordners für die Ordner Umleitung

Nachdem Sie die Konfiguration der Ordner Umleitung Gruppenrichtlinie Einstellungen abgeschlossen haben, besteht der nächste Schritt darin, das Gruppenrichtlinien Objekt zu aktivieren, damit es auf die betroffenen Benutzer angewendet werden kann.

> [!TIP]
> Wenn Sie die Unterstützung primärer Computer oder weiterer Richtlinieneinstellungen implementieren möchten, sollten Sie das jetzt vornehmen, bevor Sie das Gruppenrichtlinienobjekt aktivieren. Dadurch wird verhindert, dass Benutzerdaten auf nicht primäre Computer kopiert werden, bevor die Unterstützung primärer Computer aktiviert ist.

So aktivieren Sie das Gruppenrichtlinien Objekt für die Ordner Umleitung:

1. Öffnen Sie die Gruppenrichtlinienverwaltung.
2. Klicken Sie mit der rechten Maustaste auf das von Ihnen erstellte Gruppenrichtlinien Objekt, und wählen Sie dann **Link aktiviert**aus. Neben dem Menü Element wird ein Kontrollkästchen angezeigt.

## <a name="step-6-test-folder-redirection"></a>Schritt 6: Test Ordner Umleitung

Um die Ordner Umleitung zu testen, melden Sie sich bei einem Computer mit einem Benutzerkonto an, das für die Ordner Umleitung konfiguriert ist. Vergewissern Sie sich dann, dass die Ordner und Profile umgeleitet werden.

So testen Sie die Ordner Umleitung:

1. Melden Sie sich bei einem primären Computer (wenn Sie die Unterstützung primärer Computer aktiviert haben) mit einem Benutzerkonto an, für das Sie die Ordner Umleitung aktiviert haben.
2. Wenn sich der Benutzer zuletzt an dem Computer angemeldet hat, öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten und geben Sie folgenden Befehl ein, um sicherzustellen, dass die aktuellsten Gruppenrichtlinieneinstellungen auf dem Clientcomputer angewendet werden.
    
    ```PowerShell
    gpupdate /force
    ```
3. Öffnen Sie den Datei-Explorer.
4. Klicken Sie mit der rechten Maustaste auf einen umgeleiteten Ordner (z. b. auf den Ordner Eigene Dokumente in der Bibliothek Dokumente), und wählen Sie dann **Eigenschaften**aus.
5. Wählen Sie die Registerkarte **Speicherort** aus, und vergewissern Sie sich, dass der Pfad die angegebene Dateifreigabe anstelle eines lokalen Pfads anzeigt.

## <a name="appendix-a-checklist-for-deploying-folder-redirection"></a>Anhang A: Prüfliste für die Bereitstellung der

| Status           | Aktion |
| ---              | ---    |
| ☐<br>☐<br>☐    | 1. Bereiten Sie die Domäne vor<br>-Computer der Domäne beitreten<br>-Benutzerkonten erstellen |
| ☐<br><br><br>   | 2. Erstellen einer Sicherheitsgruppe für die Ordner Umleitung<br>-Gruppenname:<br>Parlamentariern |
| ☐<br><br>       | 3. Erstellen einer Dateifreigabe für umgeleitete Ordner<br>-Dateifreigabe Name: |
| ☐<br><br>       | 4. Erstellen eines Gruppenrichtlinien Objekts für die Ordner Umleitung<br>-GPO-Name: |
| ☐<br><br>☐<br>☐<br>☐<br>☐<br>☐ | 5. Konfigurieren der Ordner Umleitung und der Offlinedateien Richtlinien Einstellungen<br>Umgeleitete Ordner:<br>-Unterstützung für Windows 2000, Windows XP und Windows Server 2003 aktiviert?<br>-Offlinedateien aktiviert? (standardmäßig auf Windows-Client Computern aktiviert)<br>-Der Offline Modus ist aktiviert?<br>-Hintergrund Datei Synchronisierung aktiviert?<br>-Optimierte Verschiebung umgeleiteter Ordner aktiviert? |
| ☐<br><br>☐<br><br>☐<br>☐ | 6. Optionale Unterstützung für primäre Computer aktivieren<br>-Computer-oder Benutzer basiert?<br>-Primäre Computer für Benutzer festlegen<br>-Speicherort der Benutzer-und primären Computer Zuordnungen:<br>-(Optional) Aktivieren der Unterstützung primärer Computer für die Ordner Umleitung<br>-(Optional) Aktivieren der Unterstützung primärer Computer für Roamingbenutzerprofile |
| ☐         | 7. Aktivieren des Ordners für die Ordner Umleitung |
| ☐         | 8. Test Ordner Umleitung |

## <a name="change-history"></a>Änderungsverlauf

In der folgenden Tabelle sind die wichtigsten Änderungen zu diesem Thema zusammengefasst.

| date | Beschreibung | Grund|
| --- | --- | --- |
| 18. Januar 2017 | Sie haben einen Schritt [zu Schritt 3 hinzugefügt: Erstellen Sie ein Gruppenrichtlinien Objekt für](#step-3-create-a-gpo-for-folder-redirection) die Ordner Umleitung, um Leseberechtigungen an authentifizierte Benutzer zu delegieren, was jetzt aufgrund eines Gruppenrichtlinie Sicherheitsupdates erforderlich ist. | Kundenfeedback |

## <a name="more-information"></a>Weitere Informationen

* [Ordner Umleitung, Offlinedateien und Roamingbenutzerprofile](folder-redirection-rup-overview.md)
* [Primäre Computer für Ordner Umleitung und Roamingbenutzerprofile bereitstellen](deploy-primary-computers.md)
* [Erweiterte Offlinedateien Funktionen aktivieren](enable-always-offline.md)
* [Microsoft-Support-Anweisung zu replizierten Benutzerprofil Daten](https://blogs.technet.microsoft.com/askds/2010/09/01/microsofts-support-statement-around-replicated-user-profile-data/)
* [Querladen von apps mit der-Funktion](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh852635(v=win.10)>)
* [Problembehandlung bei der Paket Erstellung, Bereitstellung und Abfrage von Windows-Runtime basierten apps](https://msdn.microsoft.com/library/windows/desktop/hh973484.aspx)