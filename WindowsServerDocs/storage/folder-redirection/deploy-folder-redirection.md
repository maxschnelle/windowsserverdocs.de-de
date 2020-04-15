---
title: Bereitstellen von Ordnerumleitung mit Offlinedateien, Bereitstellen von Ordnerumleitung mit Offlinedateien
description: Verwenden von Windows Server zum Bereitstellen von Ordnerumleitung mit Offlinedateien auf Windows-Clientcomputern.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: e8e6e5a29c75c117f6faa3c1d1b3f288582d81a2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855883"
---
# <a name="deploy-folder-redirection-with-offline-files"></a>Bereitstellen von Ordnerumleitung mit Offlinedateien

>Gilt für: Windows 10, Windows 7, Windows 8, Windows 8.1, Windows Vista, Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2, Windows Server 2008 R2, Windows Server (halbjährlicher Kanal)

In diesem Thema wird die Verwendung von Windows Server zum Bereitstellen von Ordnerumleitung mit Offlinedateien auf Windows-Clientcomputern beschrieben.

Eine Liste der zuletzt vorgenommenen Änderungen an diesem Thema finden Sie unter [Änderungsverlauf](#change-history).

> [!IMPORTANT]
> Aufgrund der in [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14-2016) vorgenommenen Sicherheitsänderungen haben wir [Schritt 3: Erstellen eines Gruppenrichtlinienobjekts für die Ordnerumleitung](#step-3-create-a-gpo-for-folder-redirection) dieses Themas aktualisiert, sodass Windows die Richtlinie zur Ordnerumleitung ordnungsgemäß anwenden kann (und umgeleitete Ordner auf betroffenen PCs nicht zurücksetzt).

## <a name="prerequisites"></a>Voraussetzungen

### <a name="hardware-requirements"></a>Hardwareanforderungen

Für die Ordnerumleitung ist ein x64- oder x86-basierter Computer erforderlich, von Windows&reg; RT wird sie nicht unterstützt.

### <a name="software-requirements"></a>Softwareanforderungen

Für Ordnerumleitung gelten folgende Softwarevoraussetzungen:

- Zum Verwalten der Ordnerumleitung müssen Sie als Mitglied der Sicherheitsgruppe der Domänenadministratoren, der Sicherheitsgruppe der Organisationsadministratoren oder der Sicherheitsgruppe der Gruppenrichtlinienersteller-Besitzer angemeldet sein.
- Auf den Clientcomputern muss Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ausgeführt werden.
- Clientcomputer müssen zu den Active Directory-Domänendiensten (AD DS) hinzugefügt werden, die Sie verwalten.
- Ein Computer müssen mit Gruppenrichtlinienverwaltung und installiertem Active Directory-Verwaltungscenter verfügbar sein.
- Zum Hosten der umgeleiteten Ordner muss ein Dateiserver verfügbar sein.
    - Wenn die Dateifreigabe DFS-Namespaces verwendet, müssen die DFS-Ordner (Verknüpfungen) ein einzelnes Ziel aufweisen, damit Benutzer keine in Konflikt stehenden Änderungen auf unterschiedlichen Servern vornehmen können.
    - Wenn die Dateifreigabe die DFS-Replikation zum Replizieren der Inhalte mit einem anderen Server verwendet, dürfen Benutzer nur in der Lage sein, auf den Quellserver zuzugreifen, damit Benutzer keine in Konflikt stehenden Änderungen auf unterschiedlichen Servern vornehmen können.
    - Wenn Sie eine gruppierte Dateifreigabe verwenden, deaktivieren Sie die fortlaufende Verfügbarkeit in der Dateifreigabe, um Leistungsprobleme bei der Ordnerumleitung und Offlinedateien zu vermeiden. Darüber hinaus wechseln Offlinedateien ggf. 3–6 Minuten lang nicht in den Offlinemodus, nachdem ein Benutzer den Zugriff auf eine fortlaufend verfügbare Dateifreigabe verloren hat, was Benutzer stören kann, die noch nicht den Modus „Immer offline“ von Offlinedateien nutzen.

> [!NOTE]
> Für einige neuere Features bei der Ordnerumleitung bestehen zusätzliche Anforderungen an die Clientcomputer und das Active Directory-Schema. Weitere Informationen finden Sie unter [Bereitstellen von primären Computern](deploy-primary-computers.md), [Offlinedateien auf Ordnern deaktivieren](disable-offline-files-on-folders.md), [Aktivieren des permanenten Offlinemodus](enable-always-offline.md) und [Aktivieren der optimierten Ordnerverschiebung](enable-optimized-moving.md).

## <a name="step-1-create-a-folder-redirection-security-group"></a>Schritt 1: Erstellen einer Sicherheitsgruppe für die Ordnerumleitung

Wenn Ihre Umgebung nicht bereits mit Ordnerumleitung eingerichtet wurde, erstellen Sie im ersten Schritt eine Sicherheitsgruppe, die alle Benutzer enthält, auf die Sie die Richtlinieneinstellungen für die Ordnerumleitung anwenden möchten.

So erstellen Sie eine Sicherheitsgruppe für die Ordnerumleitung:

1. Öffnen Sie den Server-Manager auf einem Computer, auf dem das Active Directory-Verwaltungscenter installiert ist.
2. Wählen Sie im Menü **Extras** die Option für das **Active Directory-Verwaltungscenter** aus. Das Active Directory-Verwaltungscenter wird angezeigt.
3. Klicken Sie mit der rechten Maustaste auf die entsprechende Domäne oder Organisationseinheit, wählen Sie **Neu** und dann **Gruppe** aus.
4. Geben Sie im Fenster **Gruppe erstellen** im Abschnitt **Gruppe** die folgenden Einstellungen an:
    - Geben Sie in das Feld **Gruppenname** den Namen der Sicherheitsgruppe ein, z. B.: **Benutzer der Ordnerumleitung**.
    - Wählen Sie in **Gruppenbereich** die Option **Sicherheit** aus, und wählen Sie dann **Global** aus.
5. Wählen Sie im Abschnitt **Mitglieder** die Option **Hinzufügen** aus. Das Dialogfeld zum Auswählen von Benutzern, Kontakten Computern, Dienstkonten oder Gruppen wird angezeigt.
6. Geben Sie die Namen der Benutzer oder Gruppen ein, für die Sie Ordnerumleitung bereitstellen möchten, wählen Sie **OK** und dann erneut **OK** aus.

## <a name="step-2-create-a-file-share-for-redirected-folders"></a>Schritt 2: Erstellen einer Dateifreigabe für umgeleitete Ordner

Wenn Sie noch nicht über eine Dateifreigabe für umgeleitete Ordner verfügen, verwenden Sie die folgende Vorgehensweise, um eine Dateifreigabe auf einem Server zu erstellen, der Windows Server 2012 ausführt.

> [!NOTE]
> Einige Funktionen weichen möglicherweise voneinander ab oder sind nicht verfügbar, wenn Sie eine Dateifreigabe auf einem Server mit einer anderen Windows-Version erstellen.

So wird eine Dateifreigabe unter Windows Server 2019, Windows Server 2016 und Windows Server 2012 erstellt:

1. Wählen Sie im Navigationsbereich des Server-Managers **Datei- und Speicherdienste** aus, und klicken Sie anschließend auf **Freigaben**, um die Seite „Freigaben“ anzuzeigen.
2. Wählen Sie auf der Kachel **Freigaben** die Option **Aufgaben** aus, und wählen Sie dann **Neue Freigabe** aus. Der Assistent für neue Freigaben wird angezeigt.
3. Wählen Sie auf der Seite **Profil auswählen** die Option **SMB-Freigabe – Schnell** aus. Wenn Sie den Ressourcen-Manager für Dateiserver installiert haben und Ordnerverwaltungseigenschaften verwenden, wählen Sie stattdessen **SMB-Freigabe – Erweitert** aus.
4. Wählen Sie auf der Seite **Freigabeort** den Server und das Volume aus, auf dem Sie die Freigabe erstellen möchten.
5. Geben Sie auf der Seite **Freigabename** einen Namen für die Freigabe (z. B. **Benutzer$** ) in das Feld **Freigabename** ein.
    >[!TIP]
    >Beim Erstellen der Freigabe können Sie die Freigabe ausblenden, indem Sie ein ```$``` nach dem Freigabenamen einfügen. Dadurch wird die Freigabe bei informellen Browsern ausgeblendet.
6. Deaktivieren Sie auf der Seite **Weitere Einstellungen** das Kontrollkästchen „Fortlaufende Verfügbarkeit aktivieren“, sofern vorhanden, und aktivieren Sie die Kontrollkästchen **Zugriffsbasierte Aufzählung aktivieren** und **Datenzugriff verschlüsseln**.
7. Wählen Sie auf der Seite **Berechtigungen** die Option **Berechtigungen anpassen…** aus. Das Dialogfeld "Erweiterte Sicherheitseinstellungen" wird angezeigt.
8. Wählen Sie **Vererbung deaktivieren** aus, und wählen Sie dann **Vererbte Berechtigungen in explizite Berechtigungen im Objekt konvertieren** aus.
9. Legen Sie die Berechtigungen wie in Tabelle 1 beschrieben und in Abbildung 1 dargestellt fest. Entfernen Sie dabei die Berechtigungen für nicht aufgeführte Gruppen, und fügen Sie den Benutzergruppen für Ordnerumleitung, die Sie in Schritt 1 erstellt haben, besondere Berechtigungen hinzu.
    
    ![Festlegen der Berechtigungen für die Freigabe mit den umgeleiteten Ordnern](media/deploy-folder-redirection/setting-the-permissions-for-the-redirected-folders-share.png)
    
    **Abbildung 1** Festlegen der Berechtigungen für die Freigabe mit den umgeleiteten Ordnern
10. Wenn Sie das Profil **SMB-Freigabe – Erweitert** auswählen, müssen Sie auf der Seite **Verwaltungseigenschaften** unter **Benutzerdateien** den Wert "Ordnerverwendung" auswählen.
11. Wenn Sie das Profil **SMB-Freigabe – Erweitert** auswählen, können Sie auf der Seite **Kontingent** optional ein Kontingent auswählen, das für die Benutzer der Freigabe gelten soll.
12. Wählen Sie auf der Seite **Bestätigung** die Option **Erstellen** aus.

### <a name="required-permissions-for-the-file-share-hosting-redirected-folders"></a>Erforderliche Berechtigungen für die Dateifreigabe, die umgeleitete Ordner hostet

| Benutzerkonto  | Access  | Gilt für  |
| --------- | --------- | --------- |
| Benutzerkonto | Access | Gilt für |
| System     | Vollzugriff        |    Dieser Ordner, die Unterordner und Dateien     |
| Administratoren     | Vollzugriff       | Nur dieser Ordner        |
| Ersteller/Besitzer     |   Vollzugriff      |   Nur Unterordner und Dateien      |
| Sicherheitsgruppe der Benutzer, die Daten in der Freigabe speichern müssen (Benutzer der Ordnerumleitung)     |   Ordner auflisten/Daten lesen *(Erweiterte Berechtigungen)* <p>Ordner erstellen/Daten anfügen *(Erweiterte Berechtigungen)* <p>Attribute lesen *(Erweiterte Berechtigungen)* <p>Erweiterte Attribute lesen *(Erweiterte Berechtigungen)* <p>Leseberechtigungen *(Erweiterte Berechtigungen)*      |  Nur dieser Ordner       |
| Andere Gruppen und Konten     |  Keine (entfernen)       |         |

## <a name="step-3-create-a-gpo-for-folder-redirection"></a>Schritt 3: Erstellen eines Gruppenrichtlinienobjekts für die Ordnerumleitung

Wenn Sie noch kein Gruppenrichtlinienobjekt erstellt haben, das für die Einstellungen der Ordnerumleitung erstellt wurde, verwenden Sie das folgende Verfahren, um eins zu erstellen.

So erstellen Sie ein Gruppenrichtlinienobjekt für die Ordnerumleitung:

1. Öffnen Sie den Server-Manager auf einem Computer, auf dem die Gruppenrichtlinienverwaltung installiert ist.
2. Wählen Sie im Menü **Extras** die Option **Gruppenrichtlinienverwaltung** aus.
3. Klicken Sie mit der rechten Maustaste auf die Domäne oder die Organisationseinheit, in der Sie Ordnerumleitung einrichten möchten, und wählen Sie dann **Gruppenrichtlinienobjekt hier erstellen und verknüpfen** aus.
4. Geben Sie im Dialogfeld **Neues Gruppenrichtlinienobjekt** einen Namen für das Gruppenrichtlinienobjekt ein (z. B. **Einstellungen für die Ordnerumleitung**), und wählen Sie dann **OK** aus.
5. Klicken Sie mit der rechten Maustaste auf das neu erstellte Gruppenrichtlinienobjekt und deaktivieren Sie das Kontrollkästchen **Verknüpfung aktiviert** . Dadurch wird verhindert, dass das Gruppenrichtlinienobjekt angewendet wird, bis Sie es konfiguriert haben.
6. Wählen Sie das Gruppenrichtlinienobjekt aus. Wählen Sie im Abschnitt **Sicherheitsfilterung** der Registerkarte **Bereich** die Option **Authentifizierte Benutzer** aus, und wählen Sie dann **Entfernen** aus, um zu verhindern, dass das Gruppenrichtlinienobjekt auf alle Benutzer angewendet wird.
7. Wählen Sie im Abschnitt **Sicherheitsfilterung** die Option **Hinzufügen** aus.
8. Geben Sie im Dialogfeld **Benutzer, Computer oder Gruppe auswählen** den Namen der Sicherheitsgruppe ein, die Sie in Schritt 1 erstellt haben (z. B. **Benutzer der Ordnerumleitung**), und klicken Sie dann auf **OK**.
9. Wählen Sie die Registerkarte **Delegierung** aus, klicken Sie auf **Hinzufügen**, geben Sie **Authentifizierte Benutzer** ein, wählen Sie **OK** und dann erneut **OK** aus, um die Standardleseberechtigungen zu akzeptieren.
    
    Dieser Schritt ist aufgrund von Sicherheitsänderungen erforderlich, die in [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14-2016) vorgenommen wurden.

> [!IMPORTANT]
> Aufgrund der in [MS16-072a](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14-2016) vorgenommenen Sicherheitsänderungen müssen Sie der Gruppe „Authentifizierte Benutzer“ nun delegierte Leseberechtigungen für das Gruppenrichtlinienobjekt der Ordnerumleitung erteilen. Andernfalls wird das Gruppenrichtlinienobjekt nicht auf Benutzer angewendet. Wenn es bereits angewendet wurde, wird das Gruppenrichtlinienobjekt entfernt, und Ordner werden zurück an den lokalen PC umgeleitet. Weitere Informationen finden Sie unter [Bereitstellen des Gruppenrichtlinien-Sicherheitsupdates MS16-072](https://blogs.technet.microsoft.com/askds/2016/06/22/deploying-group-policy-security-update-ms16-072-kb3163622/).

## <a name="step-4-configure-folder-redirection-with-offline-files"></a>Schritt 4: Konfigurieren von Ordnerumleitung mit Offlinedateien

Bearbeiten Sie nach dem Erstellen eines Gruppenrichtlinienobjekts für Einstellungen zur Ordnerumleitung die Gruppenrichtlinieneinstellungen, um die Ordnerumleitung zu aktivieren und zu konfigurieren, wie in der folgenden Vorgehensweise erörtert.

> [!NOTE]
> „Offlinedateien“ ist für umgeleitete Ordner auf Windows-Clientcomputern standardmäßig aktiviert und auf Computern, auf denen Windows Server ausgeführt wird, deaktiviert, sofern dies nicht vom Benutzer geändert wurde. Wenn Sie Gruppenrichtlinie verwenden möchten, um zu steuern, ob „Offlinedateien“ aktiviert ist, verwenden Sie die Richtlinieneinstellung **Die Funktion „Offlinedateien“ zulassen bzw. nicht zulassen**.
> Informationen über einige der weiteren Gruppenrichtlinieneinstellungen für Offlinedateien finden Sie unter [Aktivieren von erweiterten Funktionen für Offlinedateien](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn270369(v%3dws.11)>) und [Konfigurieren von Gruppenrichtlinien für Offlinedateien](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc759721(v%3dws.10)>).

So konfigurieren Sie die Ordnerumleitung in Gruppenrichtlinien:

1. Klicken Sie in der Gruppenrichtlinienverwaltung mit der rechten Maustaste auf das Gruppenrichtlinienobjekt, das Sie erstellt haben (z. B. **Ordnerumleitungseinstellungen**), und wählen Sie dann **Bearbeiten** aus.
2. Wechseln Sie im Gruppenrichtlinienverwaltungs-Editor zu **Benutzerkonfiguration**, navigieren Sie zu **Richtlinien**, dann **Windows-Einstellungen** und anschließend zu **Ordnerumleitung**.
3. Klicken Sie mit der rechten Maustaste auf einen Ordner, den Sie umleiten möchten (beispielsweise **Dokumente**), und wählen Sie dann **Eigenschaften** aus.
4. Wählen Sie im Dialogfeld **Eigenschaften** im Feld **Einstellung** **Basic - Redirect everyone's folder to the same location** (Standard – die Ordner aller Benutzer an den gleichen Speicherort umleiten) aus.

    > [!NOTE]
    > Um Ordnerumleitung auf Computer anzuwenden, auf denen Windows XP oder Windows Server 2003 ausgeführt wird, wählen Sie die Registerkarte **Einstellungen** aus, und aktivieren Sie das Kontrollkästchen **Also apply redirection policy to Windows 2000, Windows 2000 Server, Windows XP, and Windows Server 2003 operating systems** (Umleitungsrichtlinie auch auf die Betriebssysteme Windows 2000, Windows 2000 Server, Windows XP und Windows Server 2003 anwenden).

5. Wählen Sie im Abschnitt **Zielordner** **Einen Ordner für jeden Benutzer im Stammpfad erstellen** aus, und geben Sie dann im Feld **Stammpfad** den Pfad zu der Dateifreigabe ein, auf der die umgeleiteten Ordner gespeichert werden sollen, beispielsweise: **\\\\fs1.corp.contoso.com\\users$**
6. Wähle die Registerkarte **Einstellungen** aus, und aktiviere im Abschnitt **Entfernen der Richtlinie** optional **Ordner nach Entfernen der Richtlinie zurück an den Speicherort des lokalen Benutzerprofils umleiten** (diese Einstellung kann hilfreich sein, um das Verhalten der Ordnerumleitung für Administratoren und Benutzer vorhersagbarer zu machen).
7. Wählen Sie **OK** und dann im Dialogfeld Warnung **Ja** aus.

## <a name="step-5-enable-the-folder-redirection-gpo"></a>Schritt 5: Aktivieren der Gruppenrichtlinie für die Ordnerumleitung

Nachdem Sie die Konfiguration der Gruppenrichtlinie für die Ordnerumleitung abgeschlossen haben, besteht der nächste Schritt in ihrer Aktivierung, die es erlaubt, sie auf die betroffenen Benutzer anzuwenden.

> [!TIP]
> Wenn Sie die Unterstützung primärer Computer oder weiterer Richtlinieneinstellungen implementieren möchten, sollten Sie das jetzt vornehmen, bevor Sie das Gruppenrichtlinienobjekt aktivieren. Dadurch wird verhindert, dass Benutzerdaten auf nicht primäre Computer kopiert werden, bevor die Unterstützung primärer Computer aktiviert ist.

So aktivieren Sie die Gruppenrichtlinie für die Ordnerumleitung:

1. Öffnen Sie die Gruppenrichtlinienverwaltung.
2. Klicken Sie mit der rechten Maustaste auf das von Ihnen erstellte Gruppenrichtlinienobjekt, und wählen Sie dann **Verknüpfung aktiviert** aus. Neben dem Menüelement wird ein Kontrollkästchen angezeigt.

## <a name="step-6-test-folder-redirection"></a>Schritt 6: Testen der Ordnerumleitung

Um die Ordnerumleitung testen zu können, melden Sie sich bei einem Computer mit einem Benutzerkonto an, das für Ordnerumleitung konfiguriert ist. Vergewissern Sie sich dann, dass die Ordner und Profile umgeleitet werden.

So testen Sie die Ordnerumleitung:

1. Melden Sie sich mit einem Benutzerkonto an einem primären Computer an (bei aktivierter Unterstützung primärer Computer), für das Ordnerumleitung aktiviert ist.
2. Wenn sich der Benutzer zuletzt an dem Computer angemeldet hat, öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten und geben Sie folgenden Befehl ein, um sicherzustellen, dass die aktuellsten Gruppenrichtlinieneinstellungen auf dem Clientcomputer angewendet werden.
    
    ```PowerShell
    gpupdate /force
    ```
3. Öffnen Sie den Datei-Explorer.
4. Klicken Sie mit der rechten Maustaste auf einen umgeleiteten Ordner (z. B. auf den Ordner „Eigene Dokumente“ in der Dokumentbibliothek), und wählen Sie dann **Eigenschaften** aus.
5. Wählen Sie die Registerkarte **Speicherort** aus, und vergewissern Sie sich, dass der Pfad die von Ihnen angegebene Dateifreigabe anstelle eines lokalen Pfads anzeigt.

## <a name="appendix-a-checklist-for-deploying-folder-redirection"></a>Anhang A: Checkliste zum Bereitstellen der Ordnerumleitung

| Status           | Action |
| ---              | ---    |
| ☐<br>☐<br>☐    | 1. Bereiten Sie die Domäne vor<br>– Fügen Sie der Domäne Computer hinzu<br>– Erstellen Sie Benutzerkonten |
| ☐<br><br><br>   | 2. Erstellen einer Sicherheitsgruppe für die Ordnerumleitung<br>– Gruppenname:<br>– Mitglieder: |
| ☐<br><br>       | 3. Erstellen einer Dateifreigabe für umgeleitete Ordner<br>– Dateifreigabename: |
| ☐<br><br>       | 4. Erstellen eines Gruppenrichtlinienobjekts für die Ordnerumleitung<br>– Name des Gruppenrichtlinienobjekts: |
| ☐<br><br>☐<br>☐<br>☐<br>☐<br>☐ | 5. Konfigurieren von Richtlinieneinstellungen für Ordnerumleitung und Offlinedateien<br>– Umgeleitete Ordner:<br>– Unterstützung für Windows 2000, Windows XP und Windows Server 2003 aktiviert?<br>– Offlinedateien aktiviert? (auf Windows-Clientcomputern standardmäßig aktiviert).<br>– „Immer Offlinemodus“ aktiviert?<br>– Dateisynchronisierung im Hintergrund aktiviert?<br>– Optimiertes Verschieben von umgeleiteten Ordnern aktiviert? |
| ☐<br><br>☐<br><br>☐<br>☐ | 6. (Optional) Aktivieren Sie Unterstützung von primären Computern<br>– Computer- oder nutzerbasiert?<br>– Legen Sie die primären Computer für die Benutzer fest<br>– Speicherort der Benutzer- und primären Computerzuordnungen:<br>– (Optional) Aktivieren Sie Unterstützung primärer Computer für Ordnerumleitung<br>– (Optional) Aktivieren Sie Unterstützung primärer Computer für Roamingbenutzerprofile |
| ☐         | 7. Aktivieren der Gruppenrichtlinie für die Ordnerumleitung |
| ☐         | 8. Testen der Ordnerumleitung |

## <a name="change-history"></a>Änderungsverlauf

In der folgenden Tabelle sind die wichtigsten Änderungen zu diesem Thema zusammengefasst.

| Datum | Beschreibung | Grund|
| --- | --- | --- |
| 18. Januar 2017 | Zu [Schritt 3: Erstellen eines Gruppenrichtlinienobjekts für die Ordnerumleitung](#step-3-create-a-gpo-for-folder-redirection) zum Delegieren von Leseberechtigungen an authentifizierte Benutzer, wurde ein Schritt hinzugefügt, was jetzt aufgrund eines Gruppenrichtlinien-Sicherheitsupdates erforderlich ist. | Kundenfeedback |

## <a name="more-information"></a>Weitere Informationen

* [Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile](folder-redirection-rup-overview.md)
* [Bereitstellen von primären Computern für die Ordnerumleitung und Roamingbenutzerprofile](deploy-primary-computers.md)
* [Erweiterte Funktionen für Offlinedateien aktivieren](enable-always-offline.md)
* [Anweisung des Microsoft-Supports zu replizierten Benutzerprofildaten](https://blogs.technet.microsoft.com/askds/2010/09/01/microsofts-support-statement-around-replicated-user-profile-data/)
* [Querladen von Apps mit DISM](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh852635(v=win.10)>)
* [Problembehandlung beim Packen, Bereitstellen und Abfragen von Windows Runtime-basierten Apps](https://msdn.microsoft.com/library/windows/desktop/hh973484.aspx)
