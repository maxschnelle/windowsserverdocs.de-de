---
title: Bereitstellen von Server gespeicherten Benutzerprofilen
TOCTitle: Deploying Roaming User Profiles
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.date: 06/07/2019
ms.author: jgerend
ms.openlocfilehash: 1fcabf890c0c54e12c1650c31a072d17a33e292f
ms.sourcegitcommit: 23a6e83b688119c9357262b6815c9402c2965472
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/16/2019
ms.locfileid: "69560545"
---
# <a name="deploying-roaming-user-profiles"></a>Bereitstellen von Server gespeicherten Benutzerprofilen

>Gilt für: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

In diesem Thema wird beschrieben, wie Sie mithilfe von Windows Server [Roamingbenutzerprofile](folder-redirection-rup-overview.md) für Windows-Client Computer bereitstellen Roamingbenutzerprofile leiten Benutzerprofile an eine Dateifreigabe um, damit Benutzer auf mehreren Computern dieselben Betriebssystem-und Anwendungseinstellungen erhalten.

Eine Liste der zuletzt vorgenommenen Änderungen an diesem Thema finden Sie im Abschnitt [Änderungs Verlauf](#change-history) dieses Themas.

> [!IMPORTANT]
> Aufgrund der in [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016)vorgenommenen Sicherheitsänderungen haben wir Schritt [4 aktualisiert: Erstellen Sie optional ein Gruppenrichtlinien Objekt für Roamingbenutzerprofile](#step-4-optionally-create-a-gpo-for-roaming-user-profiles) in diesem Thema, damit Windows die Richtlinie für Roamingbenutzerprofile ordnungsgemäß anwenden kann.

> [!IMPORTANT]
>  Die zu Start Ende Benutzeranpassungen gehen nach einem direkten Upgrade des Betriebssystems in der folgenden Konfiguration verloren:
> - Benutzer sind für ein Roamingprofil konfiguriert.
> - Benutzer dürfen Änderungen am Anfang vornehmen
>
> Folglich wird das Startmenü nach dem direkten Upgrade des Betriebssystems auf den Standardwert der neuen Betriebssystemversion zurückgesetzt. Informationen zu Problem Umgehungen finden [Sie in Anhang C: Arbeiten mit dem Zurücksetzen von Start Menü](#appendix-c-working-around-reset-start-menu-layouts-after-upgrades)Layouts nach Upgrades.

## <a name="prerequisites"></a>Erforderliche Komponenten

### <a name="hardware-requirements"></a>Hardwareanforderungen

Roamingbenutzerprofile erfordern einen x64-basierten oder x86-basierten Computer. Sie wird von Windows RT nicht unterstützt.

### <a name="software-requirements"></a>Softwareanforderungen

Für Roamingbenutzerprofile gelten folgende Softwarevoraussetzungen:

- Wenn Sie die Roamingbenutzerprofile mit Ordnerumleitung in einer Umgebung mit vorhandenen lokalen Benutzerprofilen bereitstellen, müssen Sie die Ordnerumleitung vor den Roamingbenutzerprofilen bereitstellen, damit die Größe der Roamingprofile verringert wird. Nachdem vorhandene Benutzerordner erfolgreich umgeleitet wurden, können Sie die Roamingbenutzerprofile bereitstellen.
- Zum Verwalten von Roamingbenutzerprofilen müssen Sie als Mitglied der Sicherheitsgruppe der Domänenadministratoren, der Sicherheitsgruppe der Organisationsadministratoren oder der Sicherheitsgruppe der Gruppenrichtlinienersteller-Besitzer angemeldet sein.
- Auf Client Computern muss Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ausgeführt werden.
- Clientcomputer müssen zu den Active Directory-Domänendiensten (AD DS) hinzugefügt werden, die Sie verwalten.
- Ein Computer müssen mit Gruppenrichtlinienverwaltung und installiertem Active Directory-Verwaltungscenter verfügbar sein.
- Zum Hosten der Roamingbenutzerprofile muss ein Dateiserver verfügbar sein.

    - Wenn die Dateifreigabe DFS-Namespaces verwendet, müssen die DFS-Ordner (Verknüpfungen) ein einzelnes Ziel aufweisen, damit Benutzer keine in Konflikt stehenden Änderungen auf unterschiedlichen Servern vornehmen können.
    - Wenn die Dateifreigabe die DFS-Replikation zum Replizieren der Inhalte mit einem anderen Server verwendet, dürfen Benutzer nur in der Lage sein, auf den Quellserver zuzugreifen, damit Benutzer keine in Konflikt stehenden Änderungen auf unterschiedlichen Servern vornehmen können.
    - Wenn die Dateifreigabe gruppiert ist, deaktivieren Sie die fortlaufende Verfügbarkeit für die Dateifreigabe, um Leistungsprobleme zu vermeiden.
- Um die Unterstützung primärer Computer in Roamingbenutzerprofilen zu verwenden, gibt es zusätzliche Client Computer-und Active Directory Schema Anforderungen. Weitere Informationen finden Sie unter Bereitstellen [von primären Computern für die Ordner Umleitung und Roamingbenutzerprofile](deploy-primary-computers.md).
- Das Layout des Start Menüs eines Benutzers wird nicht auf Windows 10, Windows Server 2019 oder Windows Server 2016 gewechselt, wenn Sie mehr als einen PC, Remotedesktop-Sitzungshost oder einen VDI-Server (Virtualized Desktop Infrastructure) verwenden. Um dieses Problem zu umgehen, können Sie ein Start Layout angeben, wie in diesem Thema beschrieben. Oder Sie können Benutzerprofil-Datenträger verwenden, die die Start Menü Einstellungen ordnungsgemäß durchlaufen, wenn Sie mit Remotedesktop-Sitzungshost Servern oder VDI-Servern verwendet werden. Weitere Informationen finden Sie unter [einfacheres Benutzer Datenverwaltung mit Benutzerprofil-Datenträgern in Windows Server 2012](https://blogs.technet.microsoft.com/enterprisemobility/2012/11/13/easier-user-data-management-with-user-profile-disks-in-windows-server-2012/).

### <a name="considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows"></a>Überlegungen zur Verwendung von Roamingbenutzerprofilen in mehreren Windows-Versionen

Wenn Sie Roamingbenutzerprofile mit mehreren Windows-Versionen verwenden möchten, wird empfohlen, folgende Aktionen auszuführen:

- Konfigurieren Sie Windows so, dass für jede Betriebssystemversion separate Profilversionen gespeichert werden. Dadurch werden unerwünschte und unvorhersehbare Probleme wie ein beschädigtes Profil vermieden.
- Verwenden Sie die Ordnerumleitung, um Benutzerdateien wie z. B. Dokumente und Bilder außerhalb der Benutzerprofile zu speichern. Somit stehen den Benutzern mit unterschiedlichen Betriebssystemen die gleichen Dateien zur Verfügung. Dadurch bleiben die Profile klein und die Anmeldung erfolgt schnell.
- Weisen Sie den Roamingbenutzerprofilen ausreichend Speicherplatz zu. Wenn Sie zwei Betriebssystemversionen unterstützen, verdoppelt sich die Anzahl der Profile (somit auch der verbrauchte Speicherplatz), da für jede Betriebssystemversion ein separates Profil gespeichert wird.
- Verwenden Sie keine Roamingbenutzerprofile auf Computern, auf denen Windows Vista/Windows Server 2008 und Windows 7/Windows Server 2008 R2 ausgeführt wird. Das Roaming zwischen diesen Betriebssystemversionen wird aufgrund von Inkompatibilitäten in den Profil Versionen nicht unterstützt.
- Informieren Sie Ihre Benutzer darüber, dass an einer Betriebssystemversion vorgenommene Änderungen nicht zu einer anderen Betriebssystemversion "wandern".
- Wenn Sie Ihre Umgebung in eine Version von Windows verschieben, die eine andere Profil Version verwendet (z. b. von Windows 10 auf Windows 10, [Version 1607 – siehe Anhang B: Profil Versions Referenzinformationen](#appendix-b-profile-version-reference-information) für eine Liste), erhalten Benutzer ein neues, leeres Roamingbenutzerprofil. Sie können die Auswirkung eines neuen Profils minimieren, indem Sie die Ordner Umleitung zum Umleiten allgemeiner Ordner verwenden. Es gibt keine unterstützte Methode, Roamingbenutzerprofile von einer Profil Version zu einer anderen zu migrieren.

## <a name="step-1-enable-the-use-of-separate-profile-versions"></a>Schritt 1: Aktivieren Sie die Verwendung separater Profilversionen

Wenn Sie Roamingbenutzerprofile auf Computern bereitstellen, auf denen Windows 8.1, Windows 8, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird, wird empfohlen, vor der Bereitstellung einige Änderungen an Ihrer Windows-Umgebung vorzunehmen. Durch diese Änderungen wird dafür gesorgt, dass zukünftige Betriebssystemupgrades problemlos verlaufen und mehrere Windows-Versionen mit Roamingbenutzerprofilen gleichzeitig ausgeführt werden können.

Verwenden Sie folgendes Verfahren, um diese Änderungen vorzunehmen.

1. Laden Sie das entsprechende Softwareupdate herunter und installieren Sie es auf allen Computern, auf denen Roaming-, verbindliche, superverbindliche oder Domänen-Standardprofile verwendet werden:

    - Windows 8.1 oder Windows Server 2012 R2: Installieren Sie das im Artikel [2887595](http://support.microsoft.com/kb/2887595) der Microsoft Knowledge Base (bei Veröffentlichung) beschriebene Software Update.
    - Windows 8 oder Windows Server 2012: Installieren das im Artikel [2887239](http://support.microsoft.com/kb/2887239) in der Microsoft Knowledge Base beschriebene Softwareupdate.

2. Verwenden Sie auf allen Computern, auf denen Windows 8.1, Windows 8, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird, auf denen Roamingbenutzerprofile verwendet werden, den Registrierungs-Editor oder Gruppenrichtlinie, um den folgenden `1`Registrierungsschlüssel Wert DWORD zu erstellen und ihn auf festzulegen. Weitere Informationen zum Erstellen von Registrierungsschlüsseln mithilfe der Gruppenrichtlinie finden Sie unter [Konfigurieren eines Registrierungselements](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753092(v=ws.11)>).

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

1. Öffnen Sie Server-Manager auf einem Computer, auf dem Active Directory-Verwaltungs Center installiert ist.
2. Wählen Sie im Menü Extras **Active Directory Verwaltungs Center**aus. Das Active Directory-Verwaltungscenter wird angezeigt.
3. Klicken Sie mit der rechten Maustaste auf die entsprechende Domäne oder Organisationseinheit, und wählen Sie **neu**und dann **Gruppe**aus.
4. Geben Sie im Fenster **Gruppe erstellen** im Abschnitt **Gruppe** die folgenden Einstellungen an:

    - Geben Sie in das Feld **Gruppenname** den Namen der Sicherheitsgruppe ein, z. B.: **Roamingbenutzerprofil-Benutzer und -Computer**.
    - Wählen Sie unter **Gruppenbereich**die Option **Sicherheit**aus, und wählen Sie dann **Global**aus.

5. Wählen Sie im Abschnitt **Members** die Option **Hinzufügen**aus. Das Dialogfeld zum Auswählen von Benutzern, Kontakten Computern, Dienstkonten oder Gruppen wird angezeigt.
6. Wenn Sie Computer Konten in die Sicherheitsgruppe einschließen möchten, wählen Sie **Objekttypen**aus, aktivieren Sie das Kontrollkästchen **Computer** , und klicken Sie dann auf **OK**.
7. Geben Sie die Namen der Benutzer, Gruppen und/oder Computer ein, für die Sie Roamingbenutzerprofile bereitstellen möchten, wählen Sie **OK**aus, und klicken Sie dann erneut auf **OK** .

## <a name="step-3-create-a-file-share-for-roaming-user-profiles"></a>Schritt 3: Erstellen Sie eine Dateifreigabe für Roamingbenutzerprofile

Wenn Sie nicht bereits über eine separate Dateifreigabe für Roamingbenutzerprofile verfügen (unabhängig von Freigaben für umgeleitete Ordner, um unbeabsichtigtes Zwischenspeichern des roamingprofilordners zu verhindern), verwenden Sie das folgende Verfahren zum Erstellen einer Dateifreigabe auf einem Server unter Windows. Servers.

> [!NOTE]
> Abhängig von der verwendeten Windows Server-Version können einige Funktionen abweichen oder nicht verfügbar sein.

So erstellen Sie eine Dateifreigabe unter Windows Server:

1. Wählen Sie im Navigationsbereich Server-Manager die Option **Datei-und Speicherdienste**aus, und klicken Sie dann auf Freigaben, um die Seite Freigaben anzuzeigen.
2. Wählen Sie auf der Kachel Freigaben die Option **Tasks**aus, und wählen Sie dann **neue Freigabe**aus. Der Assistent für neue Freigaben wird angezeigt.
3. Wählen Sie auf der Seite **Profil auswählen** die Option **SMB-Freigabe – schnell**aus. Wenn Sie Datei Server Ressourcen-Manager installiert haben und Ordner Verwaltungs Eigenschaften verwenden, klicken Sie stattdessen auf **SMB-Freigabe-erweitert**.
4. Wählen Sie auf der Seite **Freigabeort** den Server und das Volume aus, auf dem Sie die Freigabe erstellen möchten.
5. Geben Sie auf der Seite **Freigabename** einen Namen für die Freigabe ein (z. B. **Benutzerprofile$** ) in dem Feld **Freigabename**.

    > [!TIP]
    > Wenn Sie die Freigabe erstellen, blenden Sie die Freigabe aus ```$``` , indem Sie eine nach dem Freigabe Namen einfügen. So wird die Freigabe bei informellen Browsern ausgeblendet.

6. Auf der Seite **Weitere Einstellungen** können Sie das Kontrollkästchen **Aktivieren Sie fortlaufende Verfügbarkeit auf diesem Client**, sofern vorhanden, deaktivieren und optional die Kontrollkästchen **Zugriffsbasierte Aufzählung aktivieren** und **Datenzugriff verschlüsseln** aktivieren.
7. Wählen Sie auf der Seite **Berechtigungen** die Option **Berechtigungen anpassen...** aus. Das Dialogfeld "Erweiterte Sicherheitseinstellungen" wird angezeigt.
8. Wählen Sie **Vererbung deaktivieren**aus, und wählen Sie dann **geerbte Berechtigungen in explizite Berechtigung für dieses Objekt konvertieren aus**.
9. Legen Sie die Berechtigungen fest, wie unter [erforderliche Berechtigungen für die Dateifreigabe, die Roamingbenutzerprofile gehostet](#required-permissions-for-the-file-share-hosting-roaming-user-profiles) , und in der folgenden Bildschirm Abbildung beschrieben, Entfernen der Berechtigungen für nicht aufgeführte Gruppen und Konten und Hinzufügen spezieller Berechtigungen zum Roamingbenutzer. Profile Benutzer und Computergruppe, die Sie in Schritt 1 erstellt haben.
    
    ![Fenster "Erweiterte Sicherheitseinstellungen", das die in Tabelle 1 beschriebenen Berechtigungen anzeigt](media/advanced-security-user-profiles.jpg)
    
    **Abbildung 1** Festlegen der Berechtigungen für die Roamingbenutzerprofilfreigabe
10. Wenn Sie das Profil **SMB-Freigabe – Erweitert** auswählen, müssen Sie auf der Seite **Verwaltungseigenschaften** unter **Benutzerdateien** den Wert "Ordnerverwendung" auswählen.
11. Wenn Sie das Profil **SMB-Freigabe – Erweitert** auswählen, können Sie auf der Seite **Kontingent** optional ein Kontingent auswählen, das für die Benutzer der Freigabe gelten soll.
12. Wählen Sie auf der Seite **Bestätigung** die Option **erstellen aus.**

### <a name="required-permissions-for-the-file-share-hosting-roaming-user-profiles"></a>Erforderliche Berechtigungen für die Dateifreigabe, die Roamingbenutzerprofile gehostet

| Benutzerkonto | Zugriff | Betrifft |
|   -   |   -   |   -   |
|   System    |  Vollzugriff     |  Dieser Ordner, die Unterordner und Dateien     |
|  Administratoren     |  Vollzugriff     |  Nur dieser Ordner     |
|  Ersteller/Besitzer     |  Vollzugriff     |  Nur Unterordner und Dateien     |
| Sicherheitsgruppe der Benutzer, die Daten in der Freigabe speichern müssen (Roamingbenutzerprofil-Benutzer und -Computer)      |  Ordner auflisten/Daten lesen *(erweiterte Berechtigungen)* <br />Ordner erstellen/Daten anfügen *(erweiterte Berechtigungen)* |  Nur dieser Ordner     |
| Andere Gruppen und Konten   |  Keine (entfernen)     |       |

## <a name="step-4-optionally-create-a-gpo-for-roaming-user-profiles"></a>Schritt 4: Erstellen Sie optional ein Gruppenrichtlinienobjekt für Roamingbenutzerprofile

Wenn Sie für die Roamingbenutzerprofileinstellungen noch kein Gruppenrichtlinienobjekt erstellt haben, verwenden Sie folgendes Verfahren, um ein leeres Gruppenrichtlinienobjekt für Roamingbenutzerprofile zu erstellen. Mit diesem Gruppenrichtlinienobjekt können Sie die Roamingbenutzerprofileinstellungen (z. B. der primäre Computersupport, der separat erläutert wird) konfigurieren, außerdem können Sie damit Roamingbenutzerprofile auf Computern aktivieren, wie es in der Regel beim Bereitstellen in virtualisierten Desktopumgebungen oder von Remotedesktopdiensten erfolgt.

So erstellen Sie ein Gruppenrichtlinien Objekt für Roamingbenutzerprofile:

1. Öffnen Sie den Server-Manager auf einem Computer, auf dem die Gruppenrichtlinienverwaltung installiert ist.
2. Wählen Sie im Menü Extras die Option **Gruppenrichtlinie Verwaltung**aus. Die Gruppenrichtlinienverwaltung wird angezeigt.
3. Klicken Sie mit der rechten Maustaste auf die Domäne oder die Organisationseinheit, in der Sie Roamingbenutzerprofile einrichten möchten, und klicken Sie dann auf Gruppenrichtlinien Objekt **in dieser Domäne erstellen und verknüpfen**.
4. Geben Sie im Dialogfeld **Neues** Gruppenrichtlinien Objekt einen Namen für das Gruppenrichtlinien Objekt ein (z. b. **roamingbenutzerprofileinstellungen**), und klicken Sie dann auf **OK**.
5. Klicken Sie mit der rechten Maustaste auf das neu erstellte Gruppenrichtlinienobjekt und deaktivieren Sie das Kontrollkästchen **Verknüpfung aktiviert** . Dadurch wird verhindert, dass das Gruppenrichtlinienobjekt angewendet wird, bis Sie es konfiguriert haben.
6. Wählen Sie das Gruppenrichtlinienobjekt aus. Wählen Sie auf der Registerkarte **Bereich** im Abschnitt **Sicherheits Filterung** die Option **Authentifizierte Benutzer**aus, und wählen Sie dann **Entfernen** aus, um zu verhindern, dass das GPO auf alle Benutzer angewendet wird.
7. Wählen Sie im Abschnitt **Sicherheits Filterung** die Option **Hinzufügen**aus.
8. Geben Sie im Dialogfeld **Benutzer, Computer oder Gruppe auswählen** den Namen der Sicherheitsgruppe ein, die Sie in Schritt 1 erstellt haben (z. b. **Roamingbenutzerprofile Benutzer und Computer**), und klicken Sie dann auf **OK**.
9. Wählen Sie die Registerkarte Delegierung und dann **Hinzufügen**aus, geben Sie **Authentifizierte Benutzer**ein, klicken Sie auf **OK**, und klicken Sie dann erneut auf **OK** , um die Standard Berechtigungen für
    
    Dieser Schritt ist aufgrund von Sicherheitsänderungen, die in [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016)vorgenommen werden, erforderlich.

>[!IMPORTANT]
>Aufgrund der in [MS16-072a](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016)vorgenommenen Sicherheitsänderungen müssen Sie der Gruppe "authentifizierte Benutzer" nun Delegierte Leseberechtigungen für das Gruppenrichtlinien Objekt bereitstellen. andernfalls wird das Gruppenrichtlinien Objekt nicht auf Benutzer angewendet, oder wenn es bereits angewendet wurde, wird das Gruppenrichtlinien Objekt entfernt, und die Benutzerprofile werden zurückgeleitet. auf den lokalen PC. Weitere Informationen finden Sie unter Bereitstellen [Gruppenrichtlinie Sicherheitsupdates MS16-072](https://blogs.technet.microsoft.com/askds/2016/06/22/deploying-group-policy-security-update-ms16-072-kb3163622/).

## <a name="step-5-optionally-set-up-roaming-user-profiles-on-user-accounts"></a>Schritt 5: Richten Sie optional Roamingbenutzerprofile in den Benutzerkonten ein

Wenn Sie Roamingbenutzerprofile für Benutzerkonten bereitstellen, verwenden Sie folgendes Verfahren, um Roamingbenutzerprofile für Benutzerkonten in Active Directory-Domänendiensten anzugeben. Wenn Sie Roamingbenutzerprofile auf Computern bereitstellen, wie es in der Regel für Remotedesktopdienste oder virtualisierte Desktop Bereitstellungen erfolgt, verwenden Sie [stattdessen das Verfahren, das in Schritt 6: Richten Sie optional Roamingbenutzerprofile auf Computern](#step-6-optionally-set-up-roaming-user-profiles-on-computers)ein.

> [!NOTE]
> Wenn Sie in Benutzerkonten Roamingbenutzerprofile mithilfe von Active Directory und auf Computern mithilfe der Gruppenrichtlinie einrichten, hat die computerbasierte Richtlinieneinstellung eine höhere Priorität.

So richten Sie Roamingbenutzerprofile für Benutzerkonten ein:

1. Navigieren Sie im Active Directory-Verwaltungscenter in der entsprechenden Domäne zum Container **Benutzer** (oder Organisationseinheit).
2. Wählen Sie alle Benutzer aus, denen Sie ein Roamingbenutzerprofil zuweisen möchten, klicken Sie mit der rechten Maustaste auf Benutzer, und wählen Sie **Eigenschaften**aus.
3. Wählen Sie im Abschnitt **Profil** das Kontrollkästchen **Profilpfad:** aus, und geben Sie dann den Pfad zu der Dateifreigabe ein, in der Sie das Roamingbenutzerprofil des Benutzers speichern möchten, gefolgt von `%username%` (das automatisch durch den Benutzernamen ersetzt wird. der Zeitpunkt, an dem sich der Benutzer anmeldet. Zum Beispiel:
    
    `\\fs1.corp.contoso.com\User Profiles$\%username%`
    
    Um ein obligatorisches Roamingbenutzerprofil anzugeben, geben Sie den Pfad zur Ntuser. man-Datei an, `fs1.corp.contoso.comUser Profiles$default`die Sie zuvor erstellt haben, z. b. Weitere Informationen finden Sie unter [Erstellen von obligatorischen Benutzerprofilen](https://docs.microsoft.com/windows/client-management/mandatory-user-profile).
4. Wählen Sie **OK**.

> [!NOTE]
> Standardmäßig ist beim Verwenden von Roamingbenutzerprofilen die Bereitstellung aller Windows® Laufzeit-basierten (Windows Store) Apps zulässig. Bei der Verwendung eines speziellen Profils werden Apps jedoch nicht standardmäßig bereitgestellt. Bei speziellen Profilen handelt es sich um Benutzerprofile, in denen Änderungen verworfen werden, nachdem sich der Benutzer abgemeldet hat:
> <br><br>Um bei der App-Bereitstellung für spezielle Profile Einschränkungen zu entfernen, müssen Sie die Richtlinieneinstellung **Allow deployment operations in special profiles** aktivieren (befindet sich unter Computerkonfiguration\Richtlinien\Administrative Vorlagen\Windows-Komponenten\App-Paketbereitstellung). In diesem Szenario bereitgestellte Apps speichern jedoch einige Daten auf dem Computer, die sich ansammeln könnten, z. B. wenn sich Hunderte Benutzer auf einem einzelnen Computer befinden. Suchen oder entwickeln Sie zum Bereinigen von apps ein Tool, das die [cleanuppackageforuserasync](https://msdn.microsoft.com/library/windows/apps/windows.management.deployment.packagemanager.cleanuppackageforuserasync.aspx) -API verwendet, um App-Pakete für Benutzer zu bereinigen, die kein Profil mehr auf dem Computer haben.
> <br><br>Zusätzliche Hintergrundinformationen zu Windows Store-Apps finden Sie unter [Verwalten des Clientzugriffs auf den Windows Store](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh832040(v=ws.11)>).

## <a name="step-6-optionally-set-up-roaming-user-profiles-on-computers"></a>Schritt 6: Richten Sie optional Roamingbenutzerprofile auf den Computern ein

Wenn Sie Roamingbenutzerprofile für Computer bereitstellen, wie es in der Regel für Remotedesktopdienste oder virtualisierte Desktopbereitstellungen erfolgt, verwenden Sie das folgende Verfahren. Wenn Sie Roamingbenutzerprofile für Benutzerkonten bereitstellen, verwenden Sie stattdessen [das in Schritt 5: Richten Sie optional Roamingbenutzerprofile](#step-5-optionally-set-up-roaming-user-profiles-on-user-accounts)für Benutzerkonten ein.

Sie können Gruppenrichtlinie verwenden, um Roamingbenutzerprofile auf Computern anzuwenden, auf denen Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ausgeführt wird.

> [!NOTE]
> Wenn Sie auf Computern Roamingbenutzerprofile mithilfe von Active Directory und in Benutzerkonten mithilfe der Gruppenrichtlinie einrichten, hat die computerbasierte Richtlinieneinstellung eine höhere Priorität.

So richten Sie Roamingbenutzerprofile auf Computern ein:

1. Öffnen Sie den Server-Manager auf einem Computer, auf dem die Gruppenrichtlinienverwaltung installiert ist.
2. Wählen Sie im Menü Extras die Option **Gruppenrichtlinie Verwaltung**aus. Gruppenrichtlinie Verwaltung wird angezeigt.
3. Klicken Sie in Gruppenrichtlinie Verwaltung mit der rechten Maustaste auf das GPO, das Sie in Schritt 3 erstellt haben (z.b. **roamingbenutzerprofileinstellungen**), und wählen Sie dann **Bearbeiten**aus.
4. Navigieren Sie im Fenster des Gruppenrichtlinienverwaltungs-Editors zu **Computerkonfiguration**, **Richtlinien**, **Administrative Vorlagen**, **System** und dann zu **Benutzerprofile**.
5. Klicken Sie mit der rechten Maustaste auf **roamingprofilpfad festlegen für alle Benutzer, die sich auf diesem Computer anmelden**
    > [!TIP]
    > Ein Benutzer-Basisordner (sofern konfiguriert) ist der von einigen Programmen (z. B. Windows PowerShell) verwendete Standardordner. Sie können einen alternativen lokalen oder Netzwerkspeicherort pro Benutzer konfigurieren, indem Sie den Abschnitt **Basisordner** der Benutzerkontoeigenschaften in AD DS verwenden. Um den Basisordner Speicherort für alle Benutzer eines Computers zu konfigurieren, auf dem Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 in einer virtuellen Desktopumgebung ausgeführt wird, aktivieren Sie den **Startordner des Benutzers** . Richtlinien Einstellung, und geben Sie dann die Dateifreigabe und den zuzuordnenden Laufwerk Buchstaben an (oder geben Sie einen lokalen Ordner an). Verwenden Sie keine Umgebungsvariablen oder Ellipsen. Der Benutzeralias wird an das Ende des während der Benutzeranmeldung angegebenen Pfads angefügt.
6. Wählen Sie im Dialogfeld **Eigenschaften** die **Option aktiviert** aus.
7. Geben Sie im Feld Benutzer, die sich **auf diesem Computer anmelden, sollte diesen roamingprofilpfad verwenden** den Pfad zu der Dateifreigabe ein, in der Sie das Roamingbenutzerprofil des Benutzers speichern möchten, gefolgt von `%username%` (das automatisch durch den Benutzernamen ersetzt wird. das erste Mal, wenn sich der Benutzer anmeldet. Zum Beispiel:

    `\\fs1.corp.contoso.com\User Profiles$\%username%`

    Zum Angeben eines obligatorischen roamingbenutzerprofils, bei dem es sich um ein vorkonfiguriertes Profil handelt, für das Benutzer keine permanenten Änderungen vornehmen können (Änderungen werden zurückgesetzt, wenn sich der Benutzer abmeldet), geben Sie den Pfad zur Ntuser. man-Datei an, die Sie zuvor erstellt haben, z.b. `\\fs1.corp.contoso.com\User Profiles$\default` Weitere Informationen finden Sie unter [Erstellen eines verbindlichen Benutzerprofils](https://docs.microsoft.com/windows/client-management/mandatory-user-profile).
8. Wählen Sie **OK**.

## <a name="step-7-optionally-specify-a-start-layout-for-windows-10-pcs"></a>Schritt 7: Optional ein Start Layout für Windows 10-PCs angeben

Mit Gruppenrichtlinie können Sie ein bestimmtes Start Menü Layout anwenden, sodass Benutzer das gleiche Start Layout auf allen PCs sehen. Wenn sich Benutzer bei mehreren PCs anmelden und Sie ein konsistentes Start Layout auf PCs benötigen, stellen Sie sicher, dass das Gruppenrichtlinien Objekt auf alle PCs angewendet wird.

Gehen Sie folgendermaßen vor, um ein Start Layout anzugeben:

1. Aktualisieren Sie Ihre Windows 10-PCs auf Windows 10, Version 1607 (auch als Anniversary Update bezeichnet) oder höher, und installieren Sie das kumulative Update vom 14. März 2017 ([KB4013429](https://support.microsoft.com/kb/4013429)) oder höher.
2. Erstellen Sie eine vollständige oder partielle Start Menü Layout-XML-Datei. Informationen hierzu finden Sie unter [anpassen und Exportieren des Start Layouts](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout).
    * Wenn Sie ein *vollständiges* Start Layout angeben, kann ein Benutzer keinen Teil des Startmenüs anpassen. Wenn Sie ein *partielles* Start Layout angeben, können Benutzer alles anpassen, aber die gesperrten Gruppen von Kacheln, die Sie angeben. Bei einem partiellen Start Layout wechseln Benutzeranpassungen im Startmenü jedoch nicht zu anderen PCs.
3. Verwenden Sie Gruppenrichtlinie, um das angepasste Start Layout auf das GPO anzuwenden, das Sie für Roamingbenutzerprofile erstellt haben. Informationen hierzu finden Sie unter [Verwenden von Gruppenrichtlinie, um ein angepasstes Start Layout in einer Domäne anzuwenden](https://docs.microsoft.com/windows/configuration/customize-windows-10-start-screens-by-using-group-policy#bkmk-domaingpodeployment).
4. Verwenden Sie Gruppenrichtlinie, um den folgenden Registrierungs Wert auf Ihren Windows 10-PCs festzulegen. Informationen hierzu finden Sie unter [Konfigurieren eines Registrierungs Elements](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753092(v=ws.11)>).

| **Aktion**   | **Update**                  |
| ------------ | ------------                |
| Höheren         | **HKEY_LOCAL_MACHINE**      |
| Schlüssel Pfad     | **Software\microsoft\windows\currentversion\explorer** |
| Wertname   | **Specialroamingoverriunallowed** |
| Werttyp   | **REG_DWORD**               |
| Wertdaten   | **1** (oder **0** zum Deaktivieren) |
| Base         | **Decimal**                 |

5. Optionale Aktivieren Sie erstmalige Anmelde Optimierungen, um die Anmeldung für Benutzer zu beschleunigen. Informationen hierzu finden Sie unter [Anwenden von Richtlinien zum Verbessern der Anmeldezeit](https://docs.microsoft.com/windows/client-management/mandatory-user-profile#apply-policies-to-improve-sign-in-time).
6. Optionale Verringern Sie die Anmeldezeiten weiter, indem Sie unnötige Apps aus dem Windows 10-Basis Image entfernen, das Sie zum Bereitstellen von Client-PCs verwenden. Windows Server 2019 und Windows Server 2016 verfügen über keine vorab bereitgestellten apps, sodass Sie diesen Schritt auf Server Images überspringen können.
    - Verwenden Sie zum Entfernen von apps das [Remove-appxprovisionedpackage](https://docs.microsoft.com/powershell/module/dism/remove-appxprovisionedpackage?view=win10-ps) -Cmdlet in Windows PowerShell, um die folgenden Anwendungen zu deinstallieren. Wenn Ihre PCs bereits bereitgestellt sind, können Sie mithilfe von [Remove-appxpackage](https://docs.microsoft.com/powershell/module/appx/remove-appxpackage?view=win10-ps)Skripts für das Entfernen dieser Apps erstellen.
    
      - Microsoft. windowscommunicationsapps\_8wekyb3d8bbwe
      - Microsoft. bingweather\_8wekyb3d8bbwe
      - Microsoft. desktopappinstaller\_8wekyb3d8bbwe
      - Microsoft. getStarted\_8wekyb3d8bbwe
      - Microsoft. Windows. Photos\_8wekyb3d8bbwe
      - Microsoft. windowscamera\_8wekyb3d8bbwe
      - Microsoft. windowsfeedbackhub\_8wekyb3d8bbwe
      - Microsoft. windowsstore\_8wekyb3d8bbwe
      - Microsoft. xboxapp\_8wekyb3d8bbwe
      - Microsoft. xboxidentityprovider\_8wekyb3d8bbwe
      - Microsoft. zunemusic\_8wekyb3d8bbwe

>[!NOTE]
>Wenn Sie diese apps deinstallieren, können Sie die Anmeldezeiten verringern, Sie können Sie jedoch unverändert lassen, wenn Sie von Ihrer Bereitstellung benötigt werden.

## <a name="step-8-enable-the-roaming-user-profiles-gpo"></a>Schritt 8: Aktivieren Sie das Gruppenrichtlinienobjekt der Roamingbenutzerprofile

Wenn Sie Roamingbenutzerprofile mithilfe der Gruppenrichtlinie auf Computern einrichten, oder andere Roamingbenutzerprofileinstellungen mit der Gruppenrichtlinie angepasst haben, besteht der nächste Schritt darin, das Gruppenrichtlinienobjekt zu aktivieren, damit es auf die betroffenen Benutzer angewendet werden kann.

>[!TIP]
>Wenn Sie beabsichtigen, die Unterstützung für primäre Computer zu implementieren, sollten Sie dies jetzt tun, bevor Sie das Gruppenrichtlinien Objekt aktivieren. Dadurch wird verhindert, dass Benutzerdaten auf nicht primäre Computer kopiert werden, bevor die Unterstützung primärer Computer aktiviert ist. Informationen zu bestimmten Richtlinien Einstellungen finden Sie unter Bereitstellen [von primären Computern für die Ordner Umleitung und Roamingbenutzerprofile](deploy-primary-computers.md).

So aktivieren Sie das Gruppenrichtlinien Objekt für Roamingbenutzerprofile:

1. Öffnen Sie die Gruppenrichtlinienverwaltung.
2. Klicken Sie mit der rechten Maustaste auf das von Ihnen erstellte Gruppenrichtlinien Objekt, und wählen Sie **Link aktiviert**aus. Neben dem Menüelement wird ein Kontrollkästchen angezeigt.

## <a name="step-9-test-roaming-user-profiles"></a>Schritt 9: Testen von Roamingbenutzerprofilen

Melden Sie sich mit einem für Roamingbenutzerprofile konfigurierten Benutzerkonto an einem Computer an oder melden Sie sich an einem für Roamingbenutzerprofile konfigurierten Computer an, um die Roamingbenutzerprofile zu testen. Bestätigen Sie anschließend, dass das Profil umgeleitet wird.

So testen Sie Roamingbenutzerprofile:

1. Melden Sie sich mit einem Benutzerkonto an einem primären Computer an (bei aktivierter Unterstützung primärer Computer), für das Roamingbenutzerprofile aktiviert sind. Wenn Sie Roamingbenutzerprofile auf bestimmten Computern aktiviert haben, melden Sie sich an einem dieser Computer an.
2. Wenn sich der Benutzer zuletzt an dem Computer angemeldet hat, öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten und geben Sie folgenden Befehl ein, um sicherzustellen, dass die aktuellsten Gruppenrichtlinieneinstellungen auf dem Clientcomputer angewendet werden.
    
    ```PowerShell
    GpUpdate /Force
    ```
3. Um zu bestätigen, dass das Benutzerprofil roamingbasiert, öffnen Sie die System **Steuerung**, wählen Sie **System und Sicherheit**, **System**, **Erweiterte System Einstellungen**aus, wählen Sie im Abschnitt Benutzerprofile die Option **Einstellungen** aus, und suchen Sie nach **. Roaming** in der **Type** -Spalte.

## <a name="appendix-a-checklist-for-deploying-roaming-user-profiles"></a>Anhang A: Prüfliste zur Bereitstellung von Roamingbenutzerprofilen

| Status                     | Aktion                                                |
| ---                        | ------                                                |
| ☐<br>☐<br>☐<br>☐<br>☐   | 1. Bereiten Sie die Domäne vor<br>-Computer der Domäne beitreten<br>-Aktivieren der Verwendung separater Profil Versionen<br>-Benutzerkonten erstellen<br>-(Optional) Bereitstellen der Ordner Umleitung |
| ☐<br><br><br>             | 2. Erstellen Sie eine Sicherheitsgruppe für Roamingbenutzerprofile<br>-Gruppenname:<br>Parlamentariern |
| ☐<br><br>                 | 3. Erstellen Sie eine Dateifreigabe für Roamingbenutzerprofile<br>-Dateifreigabe Name: |
| ☐<br><br>                 | 4. Erstellen Sie ein Gruppenrichtlinienobjekt für Roamingbenutzerprofile<br>-GPO-Name:|
| ☐                         | 5. Konfigurieren Sie die Richtlinieneinstellungen der Roamingbenutzerprofile    |
| ☐<br>☐<br>☐              | 6. Roamingbenutzerprofile aktivieren<br>-Aktiviert in AD DS für Benutzerkonten?<br>-In Gruppenrichtlinie für Computer Konten aktiviert?<br> |
| ☐                         | 7. Optionale Festlegen eines obligatorischen Start Layouts für Windows 10-PCs |
| ☐<br>☐<br><br>☐<br><br>☐ | 8. Optionale Unterstützung für primäre Computer aktivieren<br>-Primäre Computer für Benutzer festlegen<br>-Speicherort der Benutzer-und primären Computer Zuordnungen:<br>-(Optional) Aktivieren der Unterstützung primärer Computer für die Ordner Umleitung<br>-Computer-oder Benutzer basiert?<br>-(Optional) Aktivieren der Unterstützung primärer Computer für Roamingbenutzerprofile |
| ☐                        | 9. Aktivieren Sie das Gruppenrichtlinienobjekt der Roamingbenutzerprofile                |
| ☐                        | 10. Testen von Roamingbenutzerprofilen                         |

## <a name="appendix-b-profile-version-reference-information"></a>Anhang B: Referenzinformationen zur Profilversion

Jedes Profil verfügt über eine Profil Version, die ungefähr der Windows-Version entspricht, in der das Profil verwendet wird. Beispielsweise verwenden Windows 10, Version 1703 und Version 1607, beide. V6-Profil Version. Microsoft erstellt nur bei Bedarf eine neue Profil Version, um die Kompatibilität aufrechtzuerhalten. aus diesem Grund enthält nicht jede Version von Windows eine neue Profil Version.

In der folgenden Tabelle sind die Speicherorte von Roamingbenutzerprofilen in verschiedenen Windows-Versionen aufgeführt.

| Version des Betriebssystems | Speicherort der Roamingbenutzerprofile |
| --- | --- |
| Windows XP und Windows Server 2003 | ```\\<servername>\<fileshare>\<username>``` |
| Windows Vista und Windows Server 2008 | ```\\<servername>\<fileshare>\<username>.V2``` |
| Windows 7 und Windows Server 2008 R2 | ```\\<servername>\<fileshare>\<username>.V2``` |
| Windows 8 und Windows Server 2012 | ```\\<servername>\<fileshare>\<username>.V3```(nachdem das Software Update und der Registrierungsschlüssel angewendet wurden)<br>```\\<servername>\<fileshare>\<username>.V2```(bevor das Software Update und der Registrierungsschlüssel angewendet werden) |
| Windows 8.1 und Windows Server 2012 R2 | ```\\<servername>\<fileshare>\<username>.V4```(nachdem das Software Update und der Registrierungsschlüssel angewendet wurden)<br>```\\<servername>\<fileshare>\<username>.V2```(bevor das Software Update und der Registrierungsschlüssel angewendet werden) |
| Windows 10 | ```\\<servername>\<fileshare>\<username>.V5``` |
| Windows 10, Version 1703 und Version 1607 | ```\\<servername>\<fileshare>\<username>.V6``` |

## <a name="appendix-c-working-around-reset-start-menu-layouts-after-upgrades"></a>Anhang C: Problem Umgehung beim Zurücksetzen von Start Menü Layouts nach Upgrades

Im folgenden finden Sie einige Möglichkeiten, um die Start Menü Layouts zu umgehen, die nach einem direkten Upgrade zurückgesetzt werden:

- Wenn nur ein Benutzer das Gerät verwendet und der IT-Administrator eine Strategie für die Bereitstellung verwalteter Betriebssysteme wie z. b. SCCM verwendet, können Sie Folgendes tun:
    
  1. Exportieren des Start Menü Layouts mit "Export-Startlayout" vor dem Upgrade 
  2. Importieren Sie das Layout des Start Menüs mit Import-Startlayout nach OOBE, aber bevor der Benutzer sich anmeldet.  
 
     > [!NOTE] 
     > Durch das Importieren eines Startlayout wird das Standardbenutzer Profil geändert. Alle Benutzerprofile, die nach dem Import erstellt werden, erhalten das importierte Start Layout.
 
- IT-Administratoren können sich dafür entscheiden, das Layout des Starts mit Gruppenrichtlinie zu verwalten. Die Verwendung von Gruppenrichtlinie bietet eine zentralisierte Verwaltungs Lösung, mit der Benutzer ein standardisiertes Start Layout anwenden können. Es gibt zwei Modi für die Verwendung von Gruppenrichtlinie für die Start Verwaltung. Vollständige Sperrung und partielle Sperrung. Das vollständige Sperr Szenario verhindert, dass der Benutzer Änderungen am Layout des Starts vornimmt. Das Szenario für die partielle Sperrung ermöglicht es Benutzern, Änderungen an einem bestimmten Start Bereich vorzunehmen. Weitere Informationen finden Sie unter [anpassen und Exportieren des Start Layouts](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout).
        
   > [!NOTE]
   > Vom Benutzer vorgenommene Änderungen im Teil Sperr Szenario bleiben während des Upgrades verloren.

- Lassen Sie das Start Layout zurücksetzen, und lassen Sie die Endbenutzer die Neukonfiguration des Starts zu. Eine Benachrichtigungs-e-Mail oder andere Benachrichtigung kann an Endbenutzer gesendet werden, um zu erwarten, dass Ihre Start Layouts nach dem Betriebssystem Upgrade auf minimierte Auswirkungen zurückgesetzt werden. 

# <a name="change-history"></a>Änderungsverlauf

In der folgenden Tabelle sind die wichtigsten Änderungen zu diesem Thema zusammengefasst.

| date | Beschreibung |Grund|
| --- | ---         | ---   |
| 1\. Mai, 2019 | Hinzugefügte Updates für Windows Server 2019 |
| 10. April, 2018 | Es wurde erläutert, wann Benutzeranpassungen gestartet werden, nachdem ein direktes Betriebssystem Upgrade durchgeführt wurde.|Bekanntes Problem. |
| 13. März, 2018 | Aktualisiert für Windows Server 2016 | Aus früheren Versionen der Bibliothek verschoben und für die aktuelle Version von Windows Server aktualisiert. |
| 13. April, 2017 | Hinzugefügte Profilinformationen für Windows 10, Version 1703 und die Funktionsweise von roamingprofilversionen beim Aktualisieren von Betriebssystemen – weitere Informationen finden [Sie unter Überlegungen zur Verwendung von Roamingbenutzerprofilen in mehreren Versionen](#considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows) | Kundenfeedback. |
| 14. März, 2017 | Es wurde ein optionaler Schritt zum Angeben eines obligatorischen Start Layouts für Windows [10-PCs in Anhang a hinzugefügt: Prüfliste für die bereit](#appendix-a-checklist-for-deploying-roaming-user-profiles)Stellung von Server gespeicherten Benutzerprofilen |Funktionsänderungen in der aktuellen Version von Windows Update. |
| 23. Januar 2017 | [Schritt 4: Erstellen Sie optional ein Gruppenrichtlinien Objekt für Roamingbenutzerprofile](#step-4-optionally-create-a-gpo-for-roaming-user-profiles) , um Leseberechtigungen an authentifizierte Benutzer zu delegieren, was jetzt aufgrund eines Gruppenrichtlinie Sicherheitsupdates erforderlich ist.|Sicherheitsänderungen an der Gruppenrichtlinie Verarbeitung. |
| 29. Dezember, 2016 | In [Schritt 8 wurde ein Link hinzugefügt: Aktivieren Sie das Gruppenrichtlinien Objekt für](#step-8-enable-the-roaming-user-profiles-gpo) Roamingbenutzerprofile, damit Sie leichter Informationen zum Festlegen von Gruppenrichtlinie für primäre Computer erhalten. Außerdem wurden einige Verweise auf die Schritte 5 und 6 korrigiert, bei denen die Zahlen falsch waren.|Kundenfeedback. |
| 5\. Dezember 2016 | Es wurden Informationen hinzugefügt, die ein roamingproblem beim Start Menü | Kundenfeedback. |
| 6\. Juli, 2016 | Hinzugefügte Windows 10 profile Version Suffixe in [Anhang B: Referenzinformationen](#appendix-b-profile-version-reference-information)zur Profil Version. Außerdem wurden Windows XP und Windows Server 2003 aus der Liste der unterstützten Betriebssysteme entfernt. | Updates für die neuen Versionen von Windows und entfernte Informationen zu Versionen von Windows, die nicht mehr unterstützt werden. |
| 7\. Juli 2015 | Anforderung und Schritt zum Deaktivieren der kontinuierlichen Verfügbarkeit bei Verwendung eines gruppierten Dateiservers hinzugefügt. | Gruppierte Dateifreigaben bieten eine bessere Leistung für kleine Schreibvorgänge (die für Roamingbenutzerprofile typisch sind), wenn die kontinuierliche Verfügbarkeit deaktiviert ist. |
| 19. März 2014 | Versions Suffixe für groß geschriebene Profile (. V2,. V3,. V4) in [Anhang B: Referenzinformationen](#appendix-b-profile-version-reference-information)zur Profil Version. | Obwohl bei Windows die Groß-/Kleinschreibung nicht beachtet wird, ist es wichtig, wenn Sie NFS mit der Dateifreigabe verwenden, dass die richtige Groß-/Kleinschreibung für das Profil Suffix vorliegt. |
| 09. Oktober 2013 | Überarbeitet für Windows Server 2012 R2 und Windows 8.1, hat einige Dinge erläutert und die [Überlegungen bei der Verwendung von Roamingbenutzerprofilen in mehreren Windows-Versionen](#considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows) und [Anhang B hinzugefügt: Abschnitte der Profil Versions](#appendix-b-profile-version-reference-information) Referenzinformationen. | Updates für die neue Version; Kundenfeedback. |

## <a name="more-information"></a>Weitere Informationen

- [Bereitstellen von Ordner Umleitung, Offlinedateien und Roamingbenutzerprofilen](deploy-folder-redirection.md)
- [Primäre Computer für Ordner Umleitung und Roamingbenutzerprofile bereitstellen](deploy-primary-computers.md)
- [Implementieren der Benutzer Zustands Verwaltung](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784645(v=ws.10)>)
- [Microsoft-Support-Anweisung zu replizierten Benutzerprofil Daten](https://blogs.technet.microsoft.com/askds/2010/09/01/microsofts-support-statement-around-replicated-user-profile-data/)
- [Querladen von apps mit der-Funktion](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh852635(v=win.10)>)
- [Problembehandlung bei der Paket Erstellung, Bereitstellung und Abfrage von Windows-Runtime basierten apps](https://msdn.microsoft.com/library/windows/desktop/hh973484.aspx)