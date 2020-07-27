---
title: Bereitstellen von Roamingbenutzerprofilen
TOCTitle: Deploying Roaming User Profiles
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.date: 06/07/2019
ms.author: jgerend
ms.openlocfilehash: 514dd9be3f7f634cf021a8a154f4b64c9018743e
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961632"
---
# <a name="deploying-roaming-user-profiles"></a>Bereitstellen von Roamingbenutzerprofilen

>Gilt für: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

In diesem Thema wird beschrieben, wie Windows Server zum Bereitstellen von [Roamingbenutzerprofilen](folder-redirection-rup-overview.md) auf Windows-Clientcomputern verwendet werden kann. Roamingbenutzerprofile leiten Benutzerprofile an eine Dateifreigabe um, damit Benutzer auf mehreren Computern dieselben Betriebssystem- und Anwendungseinstellungen verwenden.

Eine Liste der zuletzt vorgenommenen Änderungen an diesem Thema finden Sie im Abschnitt [Änderungsverlauf](#change-history) dieses Themas.

> [!IMPORTANT]
> Aufgrund der in [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016) vorgenommenen Sicherheitsänderungen haben wir [Schritt 4: Optionales Erstellen eines Gruppenrichtlinienobjekts für Roamingbenutzerprofile](#step-4-optionally-create-a-gpo-for-roaming-user-profiles) in diesem Thema so aktualisiert, dass Windows die Richtlinie des Roamingbenutzerprofils ordnungsgemäß anwenden kann (und keine Zurücksetzung auf lokale Richtlinien auf betroffenen Computern ausführt).

> [!IMPORTANT]
>  Benutzeranpassungen von „Start“ gehen verloren, nachdem ein In-Place-Upgrade des Betriebssystems in der folgenden Konfiguration vorgenommen wurde:
> - Benutzer sind für ein Roamingprofil konfiguriert.
> - Benutzer dürfen Änderungen an „Start“ vornehmen.
>
> Folglich wird das Startmenü nach dem In-Place-Upgrade des Betriebssystems auf den Standardwert der neuen Betriebssystemversion zurückgesetzt. Problemumgehungen finden Sie in [Anhang C: Problemumgehungen für das Zurücksetzen des Startmenülayouts nach Upgrades](#appendix-c-working-around-reset-start-menu-layouts-after-upgrades).

## <a name="prerequisites"></a>Voraussetzungen

### <a name="hardware-requirements"></a>Hardwareanforderungen

Für Roamingbenutzerprofile ist ein x64- oder x86-basierter Computer erforderlich. Von Windows RT werden diese nicht unterstützt.

### <a name="software-requirements"></a>Softwareanforderungen

Für Roamingbenutzerprofile gelten folgende Softwarevoraussetzungen:

- Wenn Sie die Roamingbenutzerprofile mit Ordnerumleitung in einer Umgebung mit vorhandenen lokalen Benutzerprofilen bereitstellen, müssen Sie die Ordnerumleitung vor den Roamingbenutzerprofilen bereitstellen, damit die Größe der Roamingprofile verringert wird. Nachdem vorhandene Benutzerordner erfolgreich umgeleitet wurden, können Sie die Roamingbenutzerprofile bereitstellen.
- Zum Verwalten von Roamingbenutzerprofilen müssen Sie als Mitglied der Sicherheitsgruppe der Domänenadministratoren, der Sicherheitsgruppe der Organisationsadministratoren oder der Sicherheitsgruppe der Gruppenrichtlinienersteller-Besitzer angemeldet sein.
- Clientcomputer müssen Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ausführen.
- Clientcomputer müssen zu den Active Directory-Domänendiensten (AD DS) hinzugefügt werden, die Sie verwalten.
- Ein Computer müssen mit Gruppenrichtlinienverwaltung und installiertem Active Directory-Verwaltungscenter verfügbar sein.
- Zum Hosten der Roamingbenutzerprofile muss ein Dateiserver verfügbar sein.

    - Wenn die Dateifreigabe DFS-Namespaces verwendet, müssen die DFS-Ordner (Verknüpfungen) ein einzelnes Ziel aufweisen, damit Benutzer keine in Konflikt stehenden Änderungen auf unterschiedlichen Servern vornehmen können.
    - Wenn die Dateifreigabe die DFS-Replikation zum Replizieren der Inhalte mit einem anderen Server verwendet, dürfen Benutzer nur in der Lage sein, auf den Quellserver zuzugreifen, damit Benutzer keine in Konflikt stehenden Änderungen auf unterschiedlichen Servern vornehmen können.
    - Wenn die Dateifreigabe gruppiert ist, deaktivieren Sie die fortlaufende Verfügbarkeit für die Dateifreigabe, um Leistungsprobleme zu vermeiden.
- Zur Nutzung des Supports für Hauptcomputer in Roamingbenutzerprofilen gelten zusätzliche Anforderungen an Clientcomputer und das Active Directory-Schema. Weitere Informationen finden Sie unter [Bereitstellen von Hauptcomputern für Ordnerumleitung und Roamingbenutzerprofile](deploy-primary-computers.md).
- Für das Layout des Startmenüs eines Benutzers erfolgt unter Windows 10, Windows Server 2019 oder Windows Server 2016 kein Roaming, wenn er mehrere PCs, Remotedesktop-Sitzungshosts oder VDI-Server (Virtualized Desktop Infrastructure) verwendet. Um dieses Problem zu umgehen, können Sie ein Startlayout wie in diesem Thema beschrieben angeben. Oder Sie können Benutzerprofildatenträger verwenden, die ordnungsgemäßes Roaming der Einstellungen des Startmenüs ausführen, wenn sie mit Remotedesktop-Sitzungshostservern oder VDI-Servern verwendet werden. Weitere Informationen finden Sie unter [Einfachere Benutzerdatenverwaltung mit Benutzerprofildatenträgern in Windows Server 2012](https://techcommunity.microsoft.com/t5/microsoft-security-and/easier-user-data-management-with-user-profile-disks-in-windows/ba-p/247555).

### <a name="considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows"></a>Überlegungen zur Verwendung von Roamingbenutzerprofilen in mehreren Windows-Versionen

Wenn Sie Roamingbenutzerprofile mit mehreren Windows-Versionen verwenden möchten, wird empfohlen, folgende Aktionen auszuführen:

- Konfigurieren Sie Windows so, dass für jede Betriebssystemversion separate Profilversionen gespeichert werden. Dadurch werden unerwünschte und unvorhersehbare Probleme wie ein beschädigtes Profil vermieden.
- Verwenden Sie die Ordnerumleitung, um Benutzerdateien wie z. B. Dokumente und Bilder außerhalb der Benutzerprofile zu speichern. Somit stehen den Benutzern mit unterschiedlichen Betriebssystemen die gleichen Dateien zur Verfügung. Dadurch bleiben die Profile klein und die Anmeldung erfolgt schnell.
- Weisen Sie den Roamingbenutzerprofilen ausreichend Speicherplatz zu. Wenn Sie zwei Betriebssystemversionen unterstützen, verdoppelt sich die Anzahl der Profile (somit auch der verbrauchte Speicherplatz), da für jede Betriebssystemversion ein separates Profil gespeichert wird.
- Verwenden Sie keine Roamingbenutzerprofile auf Computern, die Windows Vista/Windows Server 2008 und Windows 7/Windows Server 2008 R2 ausführen. Roaming zwischen diesen Betriebssystemversionen wird aufgrund von Inkompatibilitäten in ihren Profilversionen nicht unterstützt.
- Informieren Sie Ihre Benutzer darüber, dass an einer Betriebssystemversion vorgenommene Änderungen nicht in einer anderen Betriebssystemversion übernommen werden.
- Wenn Sie Ihre Umgebung in eine Version von Windows verschieben, die eine andere Profilversion verwendet (z. B. aus Windows 10 zu Windows 10, Version 1607, siehe [Anhang B: Referenzinformationen zu Profilversionen](#appendix-b-profile-version-reference-information) für eine Liste), erhalten Benutzer ein neues, leeres Roamingbenutzerprofil. Sie können die Auswirkung des Erhalts eines neuen Profils minimieren, indem Sie die Ordnerumleitung zum Umleiten allgemeiner Ordner verwenden. Es gibt keine unterstützte Methode zum Migrieren von Roamingbenutzerprofilen von einer Profilversion zu einer anderen.

## <a name="step-1-enable-the-use-of-separate-profile-versions"></a>Schritt 1: Aktivieren Sie die Verwendung separater Profilversionen

Wenn Sie Roamingbenutzerprofile auf Computern bereitstellen, auf denen Windows 8.1, Windows 8, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird, wird empfohlen, vor dem Bereitstellen einige Änderungen an Ihrer Windows-Umgebung vorzunehmen. Durch diese Änderungen wird dafür gesorgt, dass zukünftige Betriebssystemupgrades problemlos verlaufen und mehrere Windows-Versionen mit Roamingbenutzerprofilen gleichzeitig ausgeführt werden können.

Verwenden Sie folgendes Verfahren, um diese Änderungen vorzunehmen.

1. Laden Sie das entsprechende Softwareupdate herunter, und installieren Sie es auf allen Computern, auf denen Roaming-, verbindliche, superverbindliche oder Domänenstandardprofile verwendet werden:

    - Windows 8.1 oder Windows Server 2012 R2: Installieren Sie das in Artikel [2887595](https://support.microsoft.com/kb/2887595) in der Microsoft Knowledge Base beschriebene Softwareupdate (nach Veröffentlichung).
    - Windows 8 oder Windows Server 2012: Installieren das im Artikel [2887239](https://support.microsoft.com/kb/2887239) in der Microsoft Knowledge Base beschriebene Softwareupdate.

2. Auf allen Computern, auf denen Windows 8.1, Windows 8, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird und Sie Roamingbenutzerprofile verwenden, müssen Sie den Registrierungs-Editor oder Gruppenrichtlinien verwenden, um den folgenden Registrierungsschlüsselwert DWORD zu erstellen und ihn auf `1` festzulegen. Weitere Informationen zum Erstellen von Registrierungsschlüsseln mithilfe der Gruppenrichtlinie finden Sie unter [Konfigurieren eines Registrierungselements](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753092(v=ws.11)>).

    ```
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ProfSvc\Parameters\UseProfilePathExtensionVersion
    ```

    > [!WARNING]
    > Durch eine fehlerhafte Bearbeitung der Registrierung können schwerwiegende Schäden am System verursacht werden. Bevor Sie Änderungen an der Registrierung vornehmen, sollten Sie alle wichtigen Computerdaten sichern.
3. Starten Sie die Computer neu.

## <a name="step-2-create-a-roaming-user-profiles-security-group"></a>Schritt 2: Erstellen einer Sicherheitsgruppe für Roamingbenutzerprofile

Wenn Ihre Umgebung nicht bereits mit Roamingbenutzerprofilen eingerichtet wurde, erstellen Sie im ersten Schritt eine Sicherheitsgruppe, die alle Benutzer und/oder Computer enthält, auf die Sie die Roamingbenutzerprofil-Richtlinieneinstellungen anwenden möchten.

- Administratoren von allgemeinen Roamingbenutzerprofilbereitstellungen erstellen in der Regel eine Sicherheitsgruppe für die Benutzer.
- Administratoren von Remotedesktopdiensten oder virtuellen Desktopbereitstellungen verwenden in der Regel eine Sicherheitsgruppe für die Benutzer und die freigegebenen Benutzer.

So erstellen Sie eine Sicherheitsgruppe für Roamingbenutzerprofile:

1. Öffnen Sie den Server-Manager auf einem Computer, auf dem das Active Directory-Verwaltungscenter installiert ist.
2. Wählen Sie im Menü **Extras** die Option für das **Active Directory-Verwaltungscenter** aus. Das Active Directory-Verwaltungscenter wird angezeigt.
3. Klicken Sie mit der rechten Maustaste auf die entsprechende Domäne oder Organisationseinheit, wählen Sie **Neu** und dann **Gruppe** aus.
4. Geben Sie im Fenster **Gruppe erstellen** im Abschnitt **Gruppe** die folgenden Einstellungen an:

    - Geben Sie in das Feld **Gruppenname** den Namen der Sicherheitsgruppe ein, z. B.: **Roamingbenutzerprofil-Benutzer und -Computer**.
    - Wählen Sie in **Gruppenbereich** die Option **Sicherheit** aus, und wählen Sie dann **Global** aus.

5. Wählen Sie im Abschnitt **Mitglieder** die Option **Hinzufügen** aus. Das Dialogfeld zum Auswählen von Benutzern, Kontakten Computern, Dienstkonten oder Gruppen wird angezeigt.
6. Um dieser Sicherheitsgruppe Computerkonten hinzuzufügen, wählen Sie **Objekttypen** aus, aktivieren Sie das Kontrollkästchen **Computer**, und klicken Sie dann auf **OK**.
7. Geben Sie die Namen der Benutzer, die Gruppen und/oder Computer ein, für die Sie Roamingbenutzerprofile bereitstellen möchten, klicken Sie auf **OK**und dann erneut auf **OK**.

## <a name="step-3-create-a-file-share-for-roaming-user-profiles"></a>Schritt 3: Erstellen Sie eine Dateifreigabe für Roamingbenutzerprofile

Wenn sie keine separate Dateifreigabe für Roamingbenutzerprofile besitzen (unabhängig von Freigaben für umgeleitete Ordner zur Vermeidung von unbeabsichtigtem Zwischenspeichern des Roamingprofilordners), müssen Sie zum Erstellen einer Dateifreigabe auf einem Server mit Windows Server folgendes Verfahren verwenden.

> [!NOTE]
> Abhängig von der verwendeten Windows Server-Version können einige Funktionen abweichen oder nicht verfügbar sein.

So erstellen Sie eine Dateifreigabe unter Windows Server:

1. Wählen Sie im Navigationsbereich des Server-Managers **Datei- und Speicherdienste** aus, und klicken Sie anschließend auf **Freigaben**, um die Seite „Freigaben“ anzuzeigen.
2. Wählen Sie auf der Kachel „Freigaben“ die Option **Aufgaben** aus, und wählen Sie dann **Neue Freigabe** aus. Der Assistent für neue Freigaben wird angezeigt.
3. Wählen Sie auf der Seite **Profil auswählen** die Option **SMB-Freigabe – Schnell** aus. Wenn Sie den Ressourcen-Manager für Dateiserver installiert haben und Ordnerverwaltungseigenschaften verwenden, wählen Sie stattdessen **SMB-Freigabe – Erweitert** aus.
4. Wählen Sie auf der Seite **Freigabeort** den Server und das Volume aus, auf dem Sie die Freigabe erstellen möchten.
5. Geben Sie auf der Seite **Freigabename** einen Namen für die Freigabe ein (z. B. **Benutzerprofile$** ) in dem Feld **Freigabename** .

    > [!TIP]
    > Beim Erstellen der Freigabe können Sie die Freigabe ausblenden, indem Sie ein ```$``` nach dem Freigabenamen einfügen. So wird die Freigabe bei informellen Browsern ausgeblendet.

6. Auf der Seite **Weitere Einstellungen** können Sie das Kontrollkästchen **Aktivieren Sie fortlaufende Verfügbarkeit auf diesem Client** , sofern vorhanden, deaktivieren und optional die Kontrollkästchen **Zugriffsbasierte Aufzählung aktivieren** und **Datenzugriff verschlüsseln** aktivieren.
7. Wählen Sie auf der Seite **Berechtigungen** die Option **Berechtigungen anpassen** aus. Das Dialogfeld "Erweiterte Sicherheitseinstellungen" wird angezeigt.
8. Wählen Sie **Vererbung deaktivieren** aus, und wählen Sie dann **Vererbte Berechtigungen in explizite Berechtigungen im Objekt konvertieren** aus.
9. Legen Sie die Berechtigungen wie unter [Erforderliche Berechtigungen für die Dateifreigabe, die Roamingbenutzerprofile hostet](#required-permissions-for-the-file-share-hosting-roaming-user-profiles) beschrieben und im folgenden Screenshot gezeigt fest. Entfernen Sie dabei die Berechtigungen für nicht aufgeführte Gruppen und Konten, und fügen Sie spezielle Berechtigungen für Roamingbenutzerprofile und Computergruppen, die Sie in Schritt 1 erstellt haben, hinzu.
    
    ![Fenster „Erweiterte Sicherheitseinstellungen“, in dem die in Tabelle 1 beschriebenen Berechtigungen angezeigt werden](media/advanced-security-user-profiles.jpg)
    
    **Abbildung 1** Festlegen der Berechtigungen für die Roamingbenutzerprofilfreigabe
10. Wenn Sie das Profil **SMB-Freigabe – Erweitert** auswählen, müssen Sie auf der Seite **Verwaltungseigenschaften** unter **Benutzerdateien** den Wert "Ordnerverwendung" auswählen.
11. Wenn Sie das Profil **SMB-Freigabe – Erweitert** auswählen, können Sie auf der Seite **Kontingent** optional ein Kontingent auswählen, das für die Benutzer der Freigabe gelten soll.
12. Wählen Sie auf der Seite **Bestätigung** die Option **Erstellen** aus.

### <a name="required-permissions-for-the-file-share-hosting-roaming-user-profiles"></a>Erforderliche Berechtigungen für die Dateifreigabe, die Roamingbenutzerprofile hostet

| Benutzerkonto | Access | Gilt für |
|   -   |   -   |   -   |
|   System    |  Vollzugriff     |  Dieser Ordner, die Unterordner und Dateien     |
|  Administratoren     |  Vollzugriff     |  Nur dieser Ordner     |
|  Ersteller/Besitzer     |  Vollzugriff     |  Nur Unterordner und Dateien     |
| Sicherheitsgruppe der Benutzer, die Daten in der Freigabe speichern müssen (Roamingbenutzerprofil-Benutzer und -Computer)      |  Ordner auflisten/Daten lesen *(Erweiterte Berechtigungen)* <br />Ordner erstellen/Daten anfügen *(Erweiterte Berechtigungen)* |  Nur dieser Ordner     |
| Andere Gruppen und Konten   |  Keine (entfernen)     |       |

## <a name="step-4-optionally-create-a-gpo-for-roaming-user-profiles"></a>Schritt 4: Erstellen Sie optional ein Gruppenrichtlinienobjekt für Roamingbenutzerprofile

Wenn Sie für die Roamingbenutzerprofileinstellungen noch kein Gruppenrichtlinienobjekt erstellt haben, verwenden Sie folgendes Verfahren, um ein leeres Gruppenrichtlinienobjekt für Roamingbenutzerprofile zu erstellen. Mit diesem Gruppenrichtlinienobjekt können Sie die Roamingbenutzerprofileinstellungen (z. B. der primäre Computersupport, der separat erläutert wird) konfigurieren, außerdem können Sie damit Roamingbenutzerprofile auf Computern aktivieren, wie es in der Regel beim Bereitstellen in virtualisierten Desktopumgebungen oder von Remotedesktopdiensten erfolgt.

So erstellen Sie ein Gruppenrichtlinienobjekt für Roamingbenutzerprofile:

1. Öffnen Sie den Server-Manager auf einem Computer, auf dem die Gruppenrichtlinienverwaltung installiert ist.
2. Wählen Sie im Menü **Extras** die Option **Gruppenrichtlinienverwaltung** aus. Die Gruppenrichtlinienverwaltung wird angezeigt.
3. Klicken Sie mit der rechten Maustaste auf die Domäne oder die Organisationseinheit, in der Sie Roamingbenutzerprofile einrichten möchten, und wählen Sie dann **Gruppenrichtlinienobjekt hier erstellen und verknüpfen** aus.
4. Geben Sie im Dialogfeld **Neues Gruppenrichtlinienobjekt** einen Namen für das Gruppenrichtlinienobjekt ein (z. B. **Roamingbenutzerprofileinstellungen**), und wählen Sie dann **OK** aus.
5. Klicken Sie mit der rechten Maustaste auf das neu erstellte Gruppenrichtlinienobjekt und deaktivieren Sie das Kontrollkästchen **Verknüpfung aktiviert** . Dadurch wird verhindert, dass das Gruppenrichtlinienobjekt angewendet wird, bis Sie es konfiguriert haben.
6. Wählen Sie das Gruppenrichtlinienobjekt aus. Wählen Sie im Abschnitt **Sicherheitsfilterung** der Registerkarte **Bereich** die Option **Authentifizierte Benutzer** aus, und wählen Sie dann **Entfernen** aus, um zu verhindern, dass das Gruppenrichtlinienobjekt auf alle Benutzer angewendet wird.
7. Wählen Sie im Abschnitt **Sicherheitsfilterung** die Option **Hinzufügen** aus.
8. Geben Sie im Dialogfeld **Benutzer, Computer oder Gruppe auswählen** den Namen der Sicherheitsgruppe ein, die Sie in Schritt 1 erstellt haben (z. B. **Roamingbenutzerprofil-Benutzer und -Computer**), und klicken Sie dann auf **OK**.
9. Wählen Sie die Registerkarte **Delegierung** aus, klicken Sie auf **Hinzufügen**, geben Sie **Authentifizierte Benutzer** ein, wählen Sie **OK** aus, und wählen Sie dann **OK** erneut aus, um die Standardleseberechtigungen zu akzeptieren.
    
    Dieser Schritt ist aufgrund von Sicherheitsänderungen erforderlich, die in [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016) vorgenommen wurden.

>[!IMPORTANT]
>Aufgrund der in [MS16-072a](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016) vorgenommenen Sicherheitsänderungen müssen Sie der Gruppe „Authentifizierte Benutzer“ nun delegierte Leseberechtigungen für das Gruppenrichtlinienobjekt erteilen. Andernfalls wird das Gruppenrichtlinienobjekt nicht auf Benutzer angewendet. Wenn es bereits angewendet wurde, wird das Gruppenrichtlinienobjekt entfernt, und Benutzerprofile werden zurück an den lokalen PC umgeleitet. Weitere Informationen finden Sie unter [Bereitstellen des Gruppenrichtlinien-Sicherheitsupdates MS16-072](/archive/blogs/askds/deploying-group-policy-security-update-ms16-072-kb3163622).

## <a name="step-5-optionally-set-up-roaming-user-profiles-on-user-accounts"></a>Schritt 5: Richten Sie optional Roamingbenutzerprofile in den Benutzerkonten ein

Wenn Sie Roamingbenutzerprofile für Benutzerkonten bereitstellen, verwenden Sie folgendes Verfahren, um Roamingbenutzerprofile für Benutzerkonten in Active Directory-Domänendiensten anzugeben. Wenn Sie Roamingbenutzerprofile für Computer bereitstellen, wie es in der Regel für Remotedesktopdienste oder virtualisierte Desktopbereitstellungen erfolgt, verwenden Sie stattdessen das in [Schritt 6: Richten Sie optional Roamingbenutzerprofile auf den Computern ein](#step-6-optionally-set-up-roaming-user-profiles-on-computers) dieses Themas dokumentierte Verfahren.

> [!NOTE]
> Wenn Sie in Benutzerkonten Roamingbenutzerprofile mithilfe von Active Directory und auf Computern mithilfe der Gruppenrichtlinie einrichten, hat die computerbasierte Richtlinieneinstellung eine höhere Priorität.

So richten Sie Roamingbenutzerprofile für Benutzerkonten ein:

1. Navigieren Sie im Active Directory-Verwaltungscenter in der entsprechenden Domäne zum Container **Benutzer** (oder Organisationseinheit).
2. Wählen Sie alle Benutzer aus, denen Sie ein Roamingbenutzerprofil zuweisen möchten, klicken Sie mit der rechten Maustaste auf die Benutzer, und wählen Sie dann **Eigenschaften** aus.
3. Aktivieren Sie im Abschnitt **Profil** das Kontrollkästchen **Profilpfad:** und geben Sie dann den Pfad der Dateifreigabe ein, in dem Sie das Roamingbenutzerprofil des Benutzers speichern möchten, gefolgt von `%username%` (wird automatisch bei der erstmaligen Anmeldung des Benutzers durch den Benutzernamen ersetzt). Beispiel:
    
    `\\fs1.corp.contoso.com\User Profiles$\%username%`
    
    Um ein verbindliches Roamingbenutzerprofil anzugeben, müssen Sie den Pfad der Datei „NTuser.man“ angeben, den Sie zuvor erstellt haben, z. B. `fs1.corp.contoso.comUser Profiles$default`. Weitere Informationen finden Sie unter [Erstellen verbindlicher Benutzerprofile](/windows/client-management/mandatory-user-profile).
4. Wählen Sie **OK** aus.

> [!NOTE]
> Standardmäßig ist beim Verwenden von Roamingbenutzerprofilen die Bereitstellung aller Windows® Laufzeit-basierten (Windows Store) Apps zulässig. Bei der Verwendung eines speziellen Profils werden Apps jedoch nicht standardmäßig bereitgestellt. Bei speziellen Profilen handelt es sich um Benutzerprofile, in denen Änderungen verworfen werden, nachdem sich der Benutzer abgemeldet hat:
> <br><br>Um bei der App-Bereitstellung für spezielle Profile Einschränkungen zu entfernen, müssen Sie die Richtlinieneinstellung **Allow deployment operations in special profiles** aktivieren (befindet sich unter Computerkonfiguration\Richtlinien\Administrative Vorlagen\Windows-Komponenten\App-Paketbereitstellung). In diesem Szenario bereitgestellte Apps speichern jedoch einige Daten auf dem Computer, die sich ansammeln könnten, z. B. wenn sich Hunderte Benutzer auf einem einzelnen Computer befinden. Suchen oder entwickeln Sie zum Bereinigen von Apps ein Tool, das die [CleanupPackageForUserAsync](/uwp/api/Windows.Management.Deployment.PackageManager?view=winrt-19041#windows_management_deployment_packagemanager_cleanuppackageforuserasync_system_string_system_string_)-API verwendet, um App-Pakete für Benutzer zu bereinigen, die kein Profil mehr auf dem Computer haben.
> <br><br>Zusätzliche Hintergrundinformationen zu Windows Store-Apps finden Sie unter [Verwalten des Clientzugriffs auf den Windows Store](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh832040(v=ws.11)>).

## <a name="step-6-optionally-set-up-roaming-user-profiles-on-computers"></a>Schritt 6: Richten Sie optional Roamingbenutzerprofile auf den Computern ein

Wenn Sie Roamingbenutzerprofile für Computer bereitstellen, wie es in der Regel für Remotedesktopdienste oder virtualisierte Desktopbereitstellungen erfolgt, verwenden Sie das folgende Verfahren. Wenn Sie Roamingbenutzerprofile für Benutzerkonten bereitstellen, verwenden Sie stattdessen das in [Schritt 5: Richten Sie optional Roamingbenutzerprofile in den Benutzerkonten ein](#step-5-optionally-set-up-roaming-user-profiles-on-user-accounts) dieses Themas beschriebene Verfahren.

Sie können die Gruppenrichtlinie verwenden, um die Roamingbenutzerprofile auf Computern anzuwenden, die Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ausführen.

> [!NOTE]
> Wenn Sie auf Computern Roamingbenutzerprofile mithilfe von Active Directory und in Benutzerkonten mithilfe der Gruppenrichtlinie einrichten, hat die computerbasierte Richtlinieneinstellung eine höhere Priorität.

So richten Sie Roamingbenutzerprofile auf den Computern ein:

1. Öffnen Sie den Server-Manager auf einem Computer, auf dem die Gruppenrichtlinienverwaltung installiert ist.
2. Wählen Sie im Menü **Extras** die Option **Gruppenrichtlinienverwaltung** aus. Die Gruppenrichtlinienverwaltung wird angezeigt.
3. Klicken Sie in der Gruppenrichtlinienverwaltung mit der rechten Maustaste auf das Gruppenrichtlinienobjekt, das Sie in Schritt 3 erstellt haben (z. B. **Roamingbenutzerprofileinstellungen**), und wählen Sie dann **Bearbeiten** aus.
4. Navigieren Sie im Fenster des Gruppenrichtlinienverwaltungs-Editors zu **Computerkonfiguration**, **Richtlinien**, **Administrative Vorlagen**, **System**und dann zu **Benutzerprofile**.
5. Klicken Sie mit der rechten Maustaste auf **Pfad des servergespeicherten Profils für alle Benutzer festlegen, die sich an diesem Computer anmelden**, und wählen Sie dann **Bearbeiten** aus.
    > [!TIP]
    > Ein Benutzer-Basisordner (sofern konfiguriert) ist der von einigen Programmen (z. B. Windows PowerShell) verwendete Standardordner. Sie können einen alternativen lokalen oder Netzwerkspeicherort pro Benutzer konfigurieren, indem Sie den Abschnitt **Basisordner** der Benutzerkontoeigenschaften in AD DS verwenden. Um den Basisordnerspeicherort für alle Benutzer eines Computers zu konfigurieren, auf dem Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, oder Windows Server 2012 in einer virtuellen Desktopumgebung ausgeführt wird, müssen Sie die Richtlinieneinstellung **Benutzerbasisordner festlegen** aktivieren und dann die Dateifreigabe und den zuzuordnenden Laufwerkbuchstaben angeben (oder einen lokalen Ordner). Verwenden Sie keine Umgebungsvariablen oder Ellipsen. Der Benutzeralias wird an das Ende des während der Benutzeranmeldung angegebenen Pfads angefügt.
6. Wählen Sie im Dialogfeld **Eigenschaften** die Option **Aktiviert** aus.
7. Geben Sie in das Feld **Benutzer, die sich an diesem Computer anmelden, sollten diesen Pfad für servergespeicherte Profile verwenden** den Pfad zu der Dateifreigabe an, an dem Sie das Roamingbenutzerprofil des Benutzers speichern möchten, gefolgt von `%username%` (wird automatisch bei der erstmaligen Anmeldung des Benutzers durch den Benutzernamen ersetzt). Beispiel:

    `\\fs1.corp.contoso.com\User Profiles$\%username%`

    Um ein verbindliches Roamingbenutzerprofil anzugeben, bei dem es sich um ein vordefiniertes Profil handelt, in dem Benutzer keine permanenten Änderungen vornehmen können (Änderungen werden bei der Abmeldung des Benutzers zurückgesetzt), müssen Sie den Pfad zu der Datei „NTuser.man“ angeben, die Sie zuvor erstellt haben, z. B. `\\fs1.corp.contoso.com\User Profiles$\default`. Weitere Informationen finden Sie unter [Erstellen eines verbindlichen Benutzerprofils](/windows/client-management/mandatory-user-profile).
8. Wählen Sie **OK** aus.

## <a name="step-7-optionally-specify-a-start-layout-for-windows-10-pcs"></a>Schritt 7: Geben Sie optional ein Startlayout für Windows 10-PCs an

Mit Gruppenrichtlinie können Sie ein bestimmtes Startmenülayout anwenden, sodass Benutzer das gleiche Startlayout auf allen PCs sehen. Wenn sich Benutzer bei mehreren PCs anmelden und Sie ein konsistentes Startlayout auf PCs benötigen, stellen Sie sicher, dass das Gruppenrichtlinienobjekt auf alle PCs angewendet wird.

Gehen Sie folgendermaßen vor, um ein Startlayout anzugeben:

1. Aktualisieren Sie Ihre Windows 10-PCs auf Windows 10, Version 1607 (auch als Anniversary Update bezeichnet) oder höher, und installieren Sie das kumulative Update vom 14. März 2017 ([KB4013429](https://support.microsoft.com/kb/4013429)) oder neuer.
2. Erstellen Sie eine vollständige oder partielle XML-Datei mit de Startmenülayout. Weitere Informationen finden Sie unter [Anpassen und Exportieren des Startlayouts](/windows/configuration/customize-and-export-start-layout).
    * Wenn Sie ein *vollständiges* Startlayout angeben, kann ein Benutzer keinen Teil des Startmenüs anpassen. Wenn Sie ein *partielles* Startlayout angeben, können Benutzer alle Elemente mit Ausnahme der gesperrten Gruppen von Kacheln anpassen, die Sie angeben. Bei einem partiellen Startlayout erfolgt jedoch kein Roaming von Benutzeranpassungen zu anderen PCs.
3. Verwenden Sie die Gruppenrichtlinie, um das angepasste Startlayout auf das Gruppenrichtlinienobjekt anzuwenden, das Sie für Roamingbenutzerprofile erstellt haben. Weitere Informationen dazu finden Sie unter [Verwenden von Gruppenrichtlinien zum Anwenden eines angepassten Startlayouts in einer Domäne](/windows/configuration/customize-windows-10-start-screens-by-using-group-policy#bkmk-domaingpodeployment).
4. Verwenden Sie die Gruppenrichtlinie, um den folgenden Registrierungswert auf Ihren Windows 10-PCs festzulegen. Weitere Informationen dazu finden Sie unter [Konfigurieren eines Registrierungselements](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753092(v=ws.11)>).

| **Aktion**   | **Update**                  |
| ------------ | ------------                |
| Struktur         | **HKEY_LOCAL_MACHINE**      |
| Schlüsselpfad     | **Software\Microsoft\Windows\CurrentVersion\Explorer** |
| Wertname   | **SpecialRoamingOverrideAllowed** |
| Werttyp   | **REG_DWORD**               |
| Wertdaten   | **1** (oder **0** zum Deaktivieren) |
| Basis         | **Dezimal**                 |

5. (Optional) Aktivieren Sie Optimierungen bei erstmaliger Anmeldung, um die Anmeldung für Benutzer zu beschleunigen. Weitere Informationen dazu finden Sie unter [Anwenden von Richtlinien zum Verbessern der Anmeldezeit](/windows/client-management/mandatory-user-profile#apply-policies-to-improve-sign-in-time).
6. (Optional) Verringern Sie die Anmeldezeiten weiter, indem Sie unnötige Apps aus dem Windows 10-Basisimage entfernen, das Sie zum Bereitstellen von Client-PCs verwenden. Windows Server 2019 und Windows Server 2016 verfügen über keine vorab bereitgestellten Apps, sodass Sie diesen Schritt für Serverimages überspringen können.
    - Verwenden Sie zum Entfernen von Apps das Cmdlet [Remove-AppxProvisionedPackage](/powershell/module/dism/remove-appxprovisionedpackage?view=win10-ps) in Windows PowerShell, um die folgenden Anwendungen zu deinstallieren. Wenn Ihre PCs bereits bereitgestellt sind, können Sie mithilfe von [Remove-AppxPackage](/powershell/module/appx/remove-appxpackage?view=win10-ps) ein Skript für das Entfernen dieser Apps erstellen.
    
      - Microsoft.windowscommunicationsapps\_8wekyb3d8bbwe
      - Microsoft.BingWeather\_8wekyb3d8bbwe
      - Microsoft.DesktopAppInstaller\_8wekyb3d8bbwe
      - Microsoft.Getstarted\_8wekyb3d8bbwe
      - Microsoft.Windows.Photos\_8wekyb3d8bbwe
      - Microsoft.WindowsCamera\_8wekyb3d8bbwe
      - Microsoft.WindowsFeedbackHub\_8wekyb3d8bbwe
      - Microsoft.WindowsStore\_8wekyb3d8bbwe
      - Microsoft.XboxApp\_8wekyb3d8bbwe
      - Microsoft.XboxIdentityProvider\_8wekyb3d8bbwe
      - Microsoft.ZuneMusic\_8wekyb3d8bbwe

>[!NOTE]
>Wenn Sie diese Apps deinstallieren, können Sie die Anmeldezeiten verringern. Sie können Sie jedoch installiert lassen, wenn sie von Ihrer Bereitstellung benötigt werden.

## <a name="step-8-enable-the-roaming-user-profiles-gpo"></a>Schritt 8: Aktivieren Sie das Gruppenrichtlinienobjekt der Roamingbenutzerprofile

Wenn Sie Roamingbenutzerprofile mithilfe der Gruppenrichtlinie auf Computern einrichten, oder andere Roamingbenutzerprofileinstellungen mit der Gruppenrichtlinie angepasst haben, besteht der nächste Schritt darin, das Gruppenrichtlinienobjekt zu aktivieren, damit es auf die betroffenen Benutzer angewendet werden kann.

>[!TIP]
>Wenn Sie Unterstützung primärer Computer implementieren möchten, sollte dies jetzt geschehen, bevor Sie das Gruppenrichtlinienobjekt aktivieren. Dadurch wird verhindert, dass Benutzerdaten auf nicht primäre Computer kopiert werden, bevor die Unterstützung primärer Computer aktiviert ist. Weitere Informationen zu den entsprechenden Richtlinieneinstellungen finden Sie unter [Bereitstellen von primären Computern für Ordnerumleitung und Roamingbenutzerprofile](deploy-primary-computers.md).

So aktivieren Sie das Gruppenrichtlinienobjekt der Roamingbenutzerprofile:

1. Öffnen Sie die Gruppenrichtlinienverwaltung.
2. Klicken Sie mit der rechten Maustaste auf das Gruppenrichtlinienobjekt, und wählen Sie dann **Verknüpfung aktiviert** aus. Neben dem Menüelement wird ein Kontrollkästchen angezeigt.

## <a name="step-9-test-roaming-user-profiles"></a>Schritt 9: Testen von Roamingbenutzerprofilen

Melden Sie sich mit einem für Roamingbenutzerprofile konfigurierten Benutzerkonto an einem Computer an oder melden Sie sich an einem für Roamingbenutzerprofile konfigurierten Computer an, um die Roamingbenutzerprofile zu testen. Bestätigen Sie anschließend, dass das Profil umgeleitet wird.

So testen Sie Roamingbenutzerprofile:

1. Melden Sie sich mit einem Benutzerkonto an einem primären Computer an (bei aktivierter Unterstützung primärer Computer), für das Roamingbenutzerprofile aktiviert sind. Wenn Sie Roamingbenutzerprofile auf bestimmten Computern aktiviert haben, melden Sie sich an einem dieser Computer an.
2. Wenn sich der Benutzer zuletzt an dem Computer angemeldet hat, öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten und geben Sie folgenden Befehl ein, um sicherzustellen, dass die aktuellsten Gruppenrichtlinieneinstellungen auf dem Clientcomputer angewendet werden.
    
    ```PowerShell
    GpUpdate /Force
    ```
3. Um zu überprüfen, dass das Benutzerprofil gewechselt wird, öffnen Sie die **Systemsteuerung**, wählen Sie **System und Sicherheit**, **System**, **Erweiterte Systemeinstellungen** aus, wählen Sie dann im Abschnitt Benutzerprofile die Option **Einstellungen** aus, und suchen Sie in der Spalte **Typ** nach **Roaming**.

## <a name="appendix-a-checklist-for-deploying-roaming-user-profiles"></a>Anhang A: Prüfliste zur Bereitstellung von Roamingbenutzerprofilen

| Status                     | Action                                                |
| ---                        | ------                                                |
| ☐<br>☐<br>☐<br>☐<br>☐   | 1. Bereiten Sie die Domäne vor<br>– Fügen Sie der Domäne Computer hinzu<br>– Aktivieren Sie die Verwendung separater Profilversionen<br>– Erstellen Sie Benutzerkonten<br>– (Optional) Stellen Sie Ordnerumleitung bereit |
| ☐<br><br><br>             | 2. Erstellen Sie eine Sicherheitsgruppe für Roamingbenutzerprofile<br>– Gruppenname:<br>– Mitglieder: |
| ☐<br><br>                 | 3. Erstellen Sie eine Dateifreigabe für Roamingbenutzerprofile<br>– Dateifreigabename: |
| ☐<br><br>                 | 4. Erstellen Sie ein Gruppenrichtlinienobjekt für Roamingbenutzerprofile<br>– Name des Gruppenrichtlinienobjekts:|
| ☐                         | 5. Konfigurieren Sie die Richtlinieneinstellungen der Roamingbenutzerprofile    |
| ☐<br>☐<br>☐              | 6. Aktivieren Sie Roamingbenutzerprofile<br>– Sind sie in den Benutzerkonten in AD DS aktiviert?<br>– Sind sie in den Benutzerkonten in der Gruppenrichtlinie aktiviert?<br> |
| ☐                         | 7. (Optional) Geben Sie ein obligatorisches Startlayout für Windows 10-PCs an |
| ☐<br>☐<br><br>☐<br><br>☐ | 8. (Optional) Aktivieren Sie Unterstützung von primären Computern<br>– Legen Sie die primären Computer für die Benutzer fest<br>– Speicherort der Benutzer- und primären Computerzuordnungen:<br>– (Optional) Aktivieren Sie Unterstützung primärer Computer für Ordnerumleitung<br>– Computer- oder nutzerbasiert?<br>– (Optional) Aktivieren Sie Unterstützung primärer Computer für Roamingbenutzerprofile |
| ☐                        | 9. Aktivieren Sie das Gruppenrichtlinienobjekt der Roamingbenutzerprofile                |
| ☐                        | 10. Testen von Roamingbenutzerprofilen                         |

## <a name="appendix-b-profile-version-reference-information"></a>Anhang B: Referenzinformationen zur Profilversion

Jedes Profil verfügt über eine Profilversion, die ungefähr der Windows-Version entspricht, in der das Profil verwendet wird. Beispielsweise verwenden Windows 10, Version 1703 und Version 1607 beide die .V6-Profilversion. Microsoft erstellt nur bei Bedarf eine neue Profilversion, um die Kompatibilität aufrechtzuerhalten. Aus diesem Grund enthält nicht jede Version von Windows eine neue Profilversion.

In der folgenden Tabelle sind die Speicherorte von Roamingbenutzerprofilen in verschiedenen Windows-Versionen aufgeführt.

| Version des Betriebssystems | Speicherort der Roamingbenutzerprofile |
| --- | --- |
| Windows XP und Windows Server 2003 | ```\\<servername>\<fileshare>\<username>``` |
| Windows Vista und Windows Server 2008 | ```\\<servername>\<fileshare>\<username>.V2``` |
| Windows 7 und Windows Server 2008 R2 | ```\\<servername>\<fileshare>\<username>.V2``` |
| Windows 8 und Windows Server 2012 | ```\\<servername>\<fileshare>\<username>.V3``` (nachdem das Softwareupdate und der Registrierungsschlüssel angewendet wurden)<br>```\\<servername>\<fileshare>\<username>.V2``` (bevor das Softwareupdate und der Registrierungsschlüssel angewendet werden) |
| Windows 8.1 und Windows Server 2012 R2 | ```\\<servername>\<fileshare>\<username>.V4``` (nachdem das Softwareupdate und der Registrierungsschlüssel angewendet wurden)<br>```\\<servername>\<fileshare>\<username>.V2``` (bevor das Softwareupdate und der Registrierungsschlüssel angewendet werden) |
| Windows 10 | ```\\<servername>\<fileshare>\<username>.V5``` |
| Windows 10, Version 1703 und Version 1607 | ```\\<servername>\<fileshare>\<username>.V6``` |

## <a name="appendix-c-working-around-reset-start-menu-layouts-after-upgrades"></a>Anhang C: Problemumgehungen für das Zurücksetzen des Startmenülayouts nach Upgrades

Im Folgenden finden Sie einige Möglichkeiten, um zu verhindern, dass die Startmenülayouts nach einem In-Place-Upgrade zurückgesetzt werden:

- Wenn nur ein Benutzer das Gerät verwendet und der IT-Administrator eine Strategie für die Bereitstellung verwalteter Betriebssysteme verwendet (z. B. Configuration Manager), kann er folgendermaßen vorgehen:
    
  1. Exportieren des Startmenülayouts mit „Export-StartLayout“ vor dem Upgrade 
  2. Importieren des Startmenülayouts mit Import-StartLayout nach der Willkommenseite, aber bevor sich der Benutzer anmeldet  
 
     > [!NOTE] 
     > Durch das Importieren eines StartLayout wird das Standardbenutzerprofil geändert. Alle Benutzerprofile, die nach dem Import erstellt werden, erhalten das importierte StartLayout.
 
- IT-Administratoren können das Startlayout wahlweise mit der Gruppenrichtlinie verwalten. Die Verwendung von Gruppenrichtlinien bietet eine zentralisierte Verwaltungslösung zur Anwendung eines standardisierten Startlayouts für Benutzer. Es gibt 2 Modi für die Verwendung der Gruppenrichtlinie für die Startverwaltung. Vollständige Sperrung und partielle Sperrung. Das vollständige Sperrszenario verhindert, dass der Benutzer Änderungen am Startlayout vornehmen kann. Das teilweise Sperrszenario ermöglicht es Benutzern, Änderungen an einem bestimmten Bereich des Startmenüs vorzunehmen. Weitere Informationen dazu finden Sie unter [Anpassen und Exportieren des Startlayouts](/windows/configuration/customize-and-export-start-layout).
        
   > [!NOTE]
   > Vom Benutzer vorgenommene Änderungen im teilweisen Sperrszenario gehen während des Upgrades weiterhin verloren.

- Warten Sie auf die Zurücksetzung des Startlayouts, und erlauben Sie Endbenutzern die Neukonfiguration des Startmenüs. Eine Benachrichtigungs-E-Mail oder andere Benachrichtigung kann an Endbenutzer gesendet werden, um sie zu informieren, dass ihre Startlayouts nach dem Betriebssystemupgrade zurückgesetzt werden, um die Auswirkungen möglichst gering zu halten. 

## <a name="change-history"></a>Änderungsverlauf

In der folgenden Tabelle sind die wichtigsten Änderungen zu diesem Thema zusammengefasst.

| Datum | Beschreibung |Grund|
| --- | ---         | ---   |
| 1\. Mai 2019 | Hinzugefügt: Updates für Windows Server 2019 |
| 10. April 2018 | Hinzugefügt: Erläuterungen, wann Benutzeranpassungen am Startmenü nach einem In-Place-Betriebssystemupgrade verloren gehen.|Legende bekanntes Problem. |
| 13. März 2018 | Update für Windows Server 2016 | Aus der Bibliothek früherer Versionen verschoben und für die aktuelle Version von Windows Server aktualisiert. |
| 13. April 2017 | Hinzugefügt: Profilinformationen für Windows 10, Version 1703, und Klarstellung, wie Roamingprofilversionen beim Aktualisieren von Betriebssystemen funktionieren, siehe [Überlegungen zur Verwendung von Roamingbenutzerprofilen in mehreren Versionen von Windows](#considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows). | Kundenfeedback. |
| 14. März 2017 | Hinzugefügt: Optionaler Schritt zum Angeben eines obligatorischen Startlayouts für Windows 10-PCs in [Anhang A: Prüfliste zur Bereitstellung von Roamingbenutzerprofilen](#appendix-a-checklist-for-deploying-roaming-user-profiles). |Funktionsänderungen im neuesten Windows-Update. |
| 23. Januar 2017 | Hinzugefügt: Schritt zu [Schritt 4: Erstellen Sie optional ein Gruppenrichtlinien Objekt für Roamingbenutzerprofile](#step-4-optionally-create-a-gpo-for-roaming-user-profiles) zum Delegieren von Leseberechtigungen an authentifizierte Benutzer, was jetzt aufgrund eines Gruppenrichtlinien-Sicherheitsupdates erforderlich ist.|Sicherheitsänderungen an der Gruppenrichtlinienverarbeitung. |
| 29. Dezember 2016 | Hinzugefügt: Link in [Schritt 8: Aktivieren Sie das Gruppenrichtlinienobjekt für Roamingbenutzerprofile](#step-8-enable-the-roaming-user-profiles-gpo), um Informationen zum Festlegen von Gruppenrichtlinie für primäre Computer leichter abrufen zu können. Außerdem wurden einige Verweise auf die Schritte 5 und 6 korrigiert, bei denen die Zahlen falsch waren.|Kundenfeedback. |
| 5\. Dezember 2016 | Hinzugefügt: Informationen, die ein Roamingproblem der Einstellungen des Startmenüs erläutern. | Kundenfeedback. |
| 6\. Juli 2016 | Hinzugefügt: Windows 10-Profileversionsuffixe in [Anhang B: Referenzinformationen zur Profilversion](#appendix-b-profile-version-reference-information). Außerdem wurden Windows XP und Windows Server 2003 aus der Liste der unterstützten Betriebssysteme entfernt. | Updates für die neuen Versionen von Windows und entfernte Informationen zu Versionen von Windows, die nicht mehr unterstützt werden. |
| 7\. Juli 2015 | Anforderung und Schritt zum Deaktivieren der kontinuierlichen Verfügbarkeit bei Verwendung eines gruppierten Dateiservers hinzugefügt. | Gruppierte Dateifreigaben bieten eine bessere Leistung für kleine Schreibvorgänge (die für Roamingbenutzerprofile typisch sind), wenn die kontinuierliche Verfügbarkeit deaktiviert ist. |
| 19. März 2014 | Profilversionensuffixe in Großbuchstaben (.V2, .V3, .V4) in [Anhang B: Referenzinformationen zur Profilversion](#appendix-b-profile-version-reference-information). | Obwohl die Groß-/Kleinschreibung in Windows nicht beachtet wird, muss das Profilsuffix die richtige Großschreibung aufweisen, wenn Sie NFS mit der Dateifreigabe verwenden. |
| 09. Oktober 2013 | Die Abschnitte zu Windows Server 2012 R2 und Windows 8.1 wurden überarbeitet, einige Sachverhalte wurden geklärt, und [Überlegungen zur Verwendung von Roamingbenutzerprofilen in mehreren Windows-Versionen](#considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows) und [Anhang B: Referenzinformationen zur Profilversion](#appendix-b-profile-version-reference-information) wurden hinzugefügt. | Updates für die neue Version; Kundenfeedback. |

## <a name="more-information"></a>Weitere Informationen

- [Bereitstellen der Ordnerumleitung, von Offlinedateien und Roamingbenutzerprofilen](deploy-folder-redirection.md)
- [Bereitstellen von primären Computern für die Ordnerumleitung und Roamingbenutzerprofile](deploy-primary-computers.md)
- [Implementieren der Benutzerstatusverwaltung](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784645(v=ws.10)>)
- [Anweisung des Microsoft-Supports zu replizierten Benutzerprofildaten](/archive/blogs/askds/microsofts-support-statement-around-replicated-user-profile-data)
- [Querladen von Apps mit DISM](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh852635(v=win.10)>)
- [Problembehandlung beim Packen, Bereitstellen und Abfragen von Windows Runtime-basierten Apps](/windows/win32/appxpkg/troubleshooting)
