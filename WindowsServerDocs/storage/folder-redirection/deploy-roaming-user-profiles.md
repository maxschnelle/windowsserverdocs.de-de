---
Title: Bereitstellen von Roamingbenutzerprofilen
TOCTitle: Deploying Roaming User Profiles
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.date: 06/07/2019
ms.author: jgerend
ms.openlocfilehash: e6e2e32ff9aeb1b3bcfc8fed9027c7e92e13b118
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812485"
---
# <a name="deploying-roaming-user-profiles"></a>Bereitstellen von Roamingbenutzerprofilen

>Gilt für: Windows 10, Windows 8.1, Windows 8, Windows 7, WindowsServer 2019, WindowsServer 2016, WindowsServer (halbjährlicher Kanal), Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

In diesem Thema wird beschrieben, wie mit Windows Server bereitstellen [servergespeicherte Benutzerprofile](folder-redirection-rup-overview.md) für Windows-Clientcomputer. Servergespeicherte Benutzerprofile leiten Benutzerprofile an eine Dateifreigabe, damit Benutzer die dieselben Betriebssystem- und Anwendungseinstellungen auf mehreren Computern.

Eine Liste der zuletzt vorgenommenen Änderungen zu diesem Thema finden Sie die [Änderungsverlauf](#change-history) Abschnitt dieses Themas.

> [!IMPORTANT]
> Aufgrund der sicherheitsänderungen in [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016), wir aktualisiert [Schritt 4: Erstellen Sie optional ein Gruppenrichtlinienobjekt für Roamingbenutzerprofile](#step-4-optionally-create-a-gpo-for-roaming-user-profiles) in diesem Thema, Windows kann die Roamingbenutzerprofile-Richtlinie ordnungsgemäß angewendet (und nicht auf lokale Richtlinien auf betroffenen Computern zurückgesetzt).

> [!IMPORTANT]
>  Benutzeranpassungen Start bleibt nach einem Betriebssystemupgrade des direktes in der folgenden Konfiguration:
> - Benutzer werden für ein servergespeichertes Profil konfiguriert.
> - Benutzer dürfen, um den Start zu ändern
>
> Daher wird im Startmenü auf den Standardwert von der neuen Versionen des Betriebssystems zurückgesetzt, nachdem das Betriebssystem ein direktes Upgrade. Informationen zu problemumgehungen finden Sie unter [Anhang C: Arbeiten rund um Start Menülayouts zurücksetzen, nachdem Sie Upgrades](#appendix-c-working-around-reset-start-menu-layouts-after-upgrades).

## <a name="prerequisites"></a>Vorraussetzungen

### <a name="hardware-requirements"></a>Hardwareanforderungen

Servergespeicherte Benutzerprofile erfordert einen X64 oder X86-basierten Computer. Es wird von Windows RT nicht unterstützt

### <a name="software-requirements"></a>Softwareanforderungen

Für Roamingbenutzerprofile gelten folgende Softwarevoraussetzungen:

- Wenn Sie die Roamingbenutzerprofile mit Ordnerumleitung in einer Umgebung mit vorhandenen lokalen Benutzerprofilen bereitstellen, müssen Sie die Ordnerumleitung vor den Roamingbenutzerprofilen bereitstellen, damit die Größe der Roamingprofile verringert wird. Nachdem vorhandene Benutzerordner erfolgreich umgeleitet wurden, können Sie die Roamingbenutzerprofile bereitstellen.
- Zum Verwalten von Roamingbenutzerprofilen müssen Sie als Mitglied der Sicherheitsgruppe der Domänenadministratoren, der Sicherheitsgruppe der Organisationsadministratoren oder der Sicherheitsgruppe der Gruppenrichtlinienersteller-Besitzer angemeldet sein.
- Clientcomputer müssen Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008 ausführen.
- Clientcomputer müssen zu den Active Directory-Domänendiensten (AD DS) hinzugefügt werden, die Sie verwalten.
- Ein Computer müssen mit Gruppenrichtlinienverwaltung und installiertem Active Directory-Verwaltungscenter verfügbar sein.
- Zum Hosten der Roamingbenutzerprofile muss ein Dateiserver verfügbar sein.

    - Wenn die Dateifreigabe DFS-Namespaces verwendet, müssen die DFS-Ordner (Verknüpfungen) ein einzelnes Ziel aufweisen, damit Benutzer keine in Konflikt stehenden Änderungen auf unterschiedlichen Servern vornehmen können.
    - Wenn die Dateifreigabe die DFS-Replikation zum Replizieren der Inhalte mit einem anderen Server verwendet, dürfen Benutzer nur in der Lage sein, auf den Quellserver zuzugreifen, damit Benutzer keine in Konflikt stehenden Änderungen auf unterschiedlichen Servern vornehmen können.
    - Wenn die Dateifreigabe gruppiert ist, deaktivieren Sie die fortlaufende Verfügbarkeit für die Dateifreigabe, um Leistungsprobleme zu vermeiden.
- Um die Unterstützung primärer Computer in der servergespeicherte Benutzerprofile verwenden zu können, stehen zusätzliche Clientcomputer- und Active Directory-Schema-Anforderungen. Weitere Informationen finden Sie unter [Bereitstellen von Hauptcomputern für Ordnerumleitung und servergespeicherte Benutzerprofile](deploy-primary-computers.md).
- Das Layout eines Benutzers Start im Menü auf Windows 10, Windows Server-2019 oder Windows Server 2016 Roaming wird nicht, wenn sie mehr als ein PC, Remote Desktop Session Host oder virtualisierten Desktopinfrastruktur (VDI)-Server verwenden. Dieses Problem zu umgehen können Sie ein Layout Start angeben, wie in diesem Thema beschrieben. Oder Sie können mithilfe von Benutzerprofil-Datenträgern, die ordnungsgemäß starten im menüeinstellungen bei der Verwendung mit Remotedesktop-Sitzungshostserver oder VDI-Server nutzen. Weitere Informationen finden Sie unter [einfachere Datenverwaltung für Benutzer mit dem Benutzerprofil-Datenträgern in Windows Server 2012](https://blogs.technet.microsoft.com/enterprisemobility/2012/11/13/easier-user-data-management-with-user-profile-disks-in-windows-server-2012/).

### <a name="considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows"></a>Überlegungen zur Verwendung von Roamingbenutzerprofilen in mehreren Windows-Versionen

Wenn Sie Roamingbenutzerprofile mit mehreren Windows-Versionen verwenden möchten, wird empfohlen, folgende Aktionen auszuführen:

- Konfigurieren Sie Windows so, dass für jede Betriebssystemversion separate Profilversionen gespeichert werden. Dadurch werden unerwünschte und unvorhersehbare Probleme wie ein beschädigtes Profil vermieden.
- Verwenden Sie die Ordnerumleitung, um Benutzerdateien wie z. B. Dokumente und Bilder außerhalb der Benutzerprofile zu speichern. Somit stehen den Benutzern mit unterschiedlichen Betriebssystemen die gleichen Dateien zur Verfügung. Dadurch bleiben die Profile klein und die Anmeldung erfolgt schnell.
- Weisen Sie den Roamingbenutzerprofilen ausreichend Speicherplatz zu. Wenn Sie zwei Betriebssystemversionen unterstützen, verdoppelt sich die Anzahl der Profile (somit auch der verbrauchte Speicherplatz), da für jede Betriebssystemversion ein separates Profil gespeichert wird.
- Verwenden Sie keine Roamingbenutzerprofile auf Computern unter Windows Vista/Windows Server 2008 und Windows 7/Windows Server 2008 R2. Roaming zwischen diesen Betriebssystemversionen wird aufgrund von Inkompatibilitäten in den Profilversionen nicht unterstützt.
- Informieren Sie Ihre Benutzer darüber, dass an einer Betriebssystemversion vorgenommene Änderungen nicht zu einer anderen Betriebssystemversion "wandern".
- Beim Verschieben Ihrer Umgebung auf eine Version von Windows, die eine anderes Profil-Version verwendet (z. B. von Windows 10, um Windows 10 Version 1607, finden Sie unter [Anhang B: Referenzinformationen zur Profilversion](#appendix-b-profile-version-reference-information) eine Liste), erhalten Benutzer ein neue, leere servergespeichertes Benutzerprofil. Sie können die Auswirkungen der Abrufen eines neuen Profils mit Ordnerumleitung gemeinsamen Ordner umleiten minimieren. Es gibt keine Methode zum Migrieren von servergespeicherte Benutzerprofile aus ein Profilversion in einen anderen.

## <a name="step-1-enable-the-use-of-separate-profile-versions"></a>Schritt 1: Aktivieren Sie die Verwendung separater Profilversionen

Wenn Sie Roamingbenutzerprofile auf Computern unter Windows 8.1, Windows 8, Windows Server 2012 R2 oder Windows Server 2012 bereitstellen, wird empfohlen, eine Reihe von Änderungen an Ihrer Windows-Umgebung vor der Bereitstellung vorzunehmen. Durch diese Änderungen wird dafür gesorgt, dass zukünftige Betriebssystemupgrades problemlos verlaufen und mehrere Windows-Versionen mit Roamingbenutzerprofilen gleichzeitig ausgeführt werden können.

Verwenden Sie folgendes Verfahren, um diese Änderungen vorzunehmen.

1. Laden Sie das entsprechende Softwareupdate herunter und installieren Sie es auf allen Computern, auf denen Roaming-, verbindliche, superverbindliche oder Domänen-Standardprofile verwendet werden:

    - Windows 8.1 oder Windows Server 2012 R2: Installation des Softwareupdates, die im Artikel beschriebenen [2887595](http://support.microsoft.com/kb/2887595) in der Microsoft Knowledge Base (wenn veröffentlicht).
    - Windows 8 oder Windows Server 2012: Installieren das im Artikel [2887239](http://support.microsoft.com/kb/2887239) in der Microsoft Knowledge Base beschriebene Softwareupdate.

2. Verwenden Sie auf allen Computern mit Windows 8.1, Windows 8, Windows Server 2012 R2 oder Windows Server 2012 auf dem Sie Roamingbenutzerprofile verwenden, den Registrierungs-Editor oder Gruppenrichtlinien auf den folgenden Registrierungsschlüssel erstellen-Schlüssels DWORD, und legen Sie ihn `1`. Weitere Informationen zum Erstellen von Registrierungsschlüsseln mithilfe der Gruppenrichtlinie finden Sie unter [Konfigurieren eines Registrierungselements](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753092(v=ws.11)>).

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

Hier wird eine Sicherheitsgruppe für Roamingbenutzerprofile zu erstellen:

1. Server-Manager auf einem Computer mit Active Directory-Verwaltungscenter öffnen installiert.
2. Auf der **Tools** , wählen Sie im Menü **Active Directory-Verwaltungscenter**. Das Active Directory-Verwaltungscenter wird angezeigt.
3. Mit der rechten Maustaste die entsprechende Domäne oder Organisationseinheit auswählen **neu**, und wählen Sie dann **Gruppe**.
4. Geben Sie im Fenster **Gruppe erstellen** im Abschnitt **Gruppe** die folgenden Einstellungen an:

    - Geben Sie in das Feld **Gruppenname** den Namen der Sicherheitsgruppe ein, z. B.: **Roamingbenutzerprofil-Benutzer und -Computer**.
    - In **Gruppenbereich**Option **Sicherheit**, und wählen Sie dann **Global**.

5. In der **Mitglieder** wählen Sie im Abschnitt **hinzufügen**. Das Dialogfeld zum Auswählen von Benutzern, Kontakten Computern, Dienstkonten oder Gruppen wird angezeigt.
6. Wenn Sie dieser Sicherheitsgruppe Computerkonten hinzuzufügen möchten, wählen Sie **Objekttypen**, wählen die **Computer** Kontrollkästchen, und wählen Sie dann **OK**.
7. Geben Sie die Namen der Benutzer, Gruppen und/oder Computer, der Sie Roamingbenutzerprofile bereitstellen, wählen Sie möchten **OK**, und wählen Sie dann **OK** erneut aus.

## <a name="step-3-create-a-file-share-for-roaming-user-profiles"></a>Schritt 3: Erstellen Sie eine Dateifreigabe für Roamingbenutzerprofile

Wenn Sie noch nicht über eine separate Dateifreigabe für Roamingbenutzerprofile verfügen gehen (unabhängig von Freigaben für umgeleitete Ordner zur Vermeidung von unbeabsichtigtem Zwischenspeichern des roamingprofilordners), Sie zum Erstellen einer Dateifreigabe auf einem Server unter Windows Server.

> [!NOTE]
> Einige Funktionen möglicherweise unterscheiden oder ist nicht verfügbar, abhängig von der Version von Windows Server, die Sie verwenden.

Hier wird eine Dateifreigabe unter Windows Server zu erstellen:

1. Wählen Sie im Navigationsbereich des Server-Manager **Datei- und Speicherdienste**, und wählen Sie dann **Freigaben** auf der Seite "Freigaben" anzuzeigen.
2. Wählen Sie in der Kachel "Freigaben" **Aufgaben**, und wählen Sie dann **neue Freigabe**. Der Assistent für neue Freigaben wird angezeigt.
3. Auf der **Profil auswählen** Seite **SMB-Freigabe – schnell**. Wenn Sie Resource Manager für Dateiserver installiert haben und ordnerverwaltungseigenschaften verwenden, wählen Sie stattdessen **SMB-Freigabe - erweitert**.
4. Wählen Sie auf der Seite **Freigabeort** den Server und das Volume aus, auf dem Sie die Freigabe erstellen möchten.
5. Geben Sie auf der Seite **Freigabename** einen Namen für die Freigabe ein (z. B. **Benutzerprofile$** ) in dem Feld **Freigabename**.

    > [!TIP]
    > Wenn Sie die Freigabe zu erstellen, die Freigabe ausblenden, indem Sie platzieren einen ```$``` nach dem Freigabenamen. So wird die Freigabe bei informellen Browsern ausgeblendet.

6. Auf der Seite **Weitere Einstellungen** können Sie das Kontrollkästchen **Aktivieren Sie fortlaufende Verfügbarkeit auf diesem Client**, sofern vorhanden, deaktivieren und optional die Kontrollkästchen **Zugriffsbasierte Aufzählung aktivieren** und **Datenzugriff verschlüsseln** aktivieren.
7. Auf der **Berechtigungen** Seite **Berechtigungen anpassen...** . Das Dialogfeld "Erweiterte Sicherheitseinstellungen" wird angezeigt.
8. Wählen Sie **Vererbung deaktivieren**, und wählen Sie dann **vererbte Berechtigungen in explizite Berechtigungen im Objekt konvertieren**.
9. Legen Sie die Berechtigungen aus, wie in beschrieben [erforderliche Berechtigungen für die Datei freigeben mit servergespeicherten Benutzerprofilen für](#required-permissions-for-the-file-share-hosting-roaming-user-profiles) und in der folgenden bildschirmabbildung, hinzufügen und Entziehen von Berechtigungen für nicht aufgeführte Gruppen und Konten spezielle angezeigt Berechtigungen auf den Roamingbenutzerprofil-Benutzer und Computer, die Sie in Schritt 1 erstellt haben.
    
    ![Advanced Security Settings-Fenster, die mit Berechtigungen wie in Tabelle 1 beschrieben.](media/advanced-security-user-profiles.jpg)
    
    **Abbildung 1** Festlegen der Berechtigungen für die Roamingbenutzerprofilfreigabe
10. Wenn Sie das Profil **SMB-Freigabe – Erweitert** auswählen, müssen Sie auf der Seite **Verwaltungseigenschaften** unter **Benutzerdateien** den Wert "Ordnerverwendung" auswählen.
11. Wenn Sie das Profil **SMB-Freigabe – Erweitert** auswählen, können Sie auf der Seite **Kontingent** optional ein Kontingent auswählen, das für die Benutzer der Freigabe gelten soll.
12. Auf der **Bestätigung** Seite **erstellen.**

### <a name="required-permissions-for-the-file-share-hosting-roaming-user-profiles"></a>Die erforderlichen Berechtigungen für die Datei-Freigabe hosting servergespeicherte Profile

| Benutzerkonto | Zugriff | Betrifft |
|   -   |   -   |   -   |
|   System    |  Vollzugriff     |  Dieser Ordner, die Unterordner und Dateien     |
|  Administratoren     |  Vollzugriff     |  Nur dieser Ordner     |
|  Ersteller/Besitzer     |  Vollzugriff     |  Nur Unterordner und Dateien     |
| Sicherheitsgruppe der Benutzer, die Daten in der Freigabe speichern müssen (Roamingbenutzerprofil-Benutzer und -Computer)      |  Ordner auflisten / Daten lesen *(erweiterte Berechtigungen)* <br />Ordner erstellen / Daten anhängen *(erweiterte Berechtigungen)* |  Nur dieser Ordner     |
| Andere Gruppen und Konten   |  Keine (entfernen)     |       |

## <a name="step-4-optionally-create-a-gpo-for-roaming-user-profiles"></a>Schritt 4: Erstellen Sie optional ein Gruppenrichtlinienobjekt für Roamingbenutzerprofile

Wenn Sie für die Roamingbenutzerprofileinstellungen noch kein Gruppenrichtlinienobjekt erstellt haben, verwenden Sie folgendes Verfahren, um ein leeres Gruppenrichtlinienobjekt für Roamingbenutzerprofile zu erstellen. Mit diesem Gruppenrichtlinienobjekt können Sie die Roamingbenutzerprofileinstellungen (z. B. der primäre Computersupport, der separat erläutert wird) konfigurieren, außerdem können Sie damit Roamingbenutzerprofile auf Computern aktivieren, wie es in der Regel beim Bereitstellen in virtualisierten Desktopumgebungen oder von Remotedesktopdiensten erfolgt.

Hier wird ein Gruppenrichtlinienobjekt für Roamingbenutzerprofile zu erstellen:

1. Öffnen Sie den Server-Manager auf einem Computer, auf dem die Gruppenrichtlinienverwaltung installiert ist.
2. Von der **Tools** Menü die Option **Gruppenrichtlinienverwaltung**. Die Gruppenrichtlinienverwaltung wird angezeigt.
3. Mit der rechten Maustaste die Domäne oder Organisationseinheit, in denen Sie Roamingbenutzerprofile einrichten, und wählen Sie dann möchten **erstellen Sie ein Gruppenrichtlinienobjekt in dieser Domäne, und hier**.
4. In der **neues Gruppenrichtlinienobjekt** Dialogfeld Geben Sie einen Namen für das Gruppenrichtlinienobjekt (z. B. **Roamingbenutzerprofileinstellungen**), und wählen Sie dann **OK**.
5. Klicken Sie mit der rechten Maustaste auf das neu erstellte Gruppenrichtlinienobjekt und deaktivieren Sie das Kontrollkästchen **Verknüpfung aktiviert** . Dadurch wird verhindert, dass das Gruppenrichtlinienobjekt angewendet wird, bis Sie es konfiguriert haben.
6. Wählen Sie das Gruppenrichtlinienobjekt aus. In der **Sicherheitsfilterung** Teil der **Bereich** Registerkarte **authentifizierte Benutzer**, und wählen Sie dann **entfernen** um zu verhindern, dass das GPO für alle Benutzer angewendet werden.
7. In der **Sicherheitsfilterung** wählen Sie im Abschnitt **hinzufügen**.
8. In der **Select User, Computer oder Gruppe** (Dialogfeld), Typ, der den Namen der Sicherheitsgruppe in Schritt 1 erstellte Gruppe (z. B. **Roamingbenutzerprofil-Benutzer und-Computer**), und wählen Sie dann **OK** .
9. Wählen Sie die **Delegierung** Registerkarte **hinzufügen**, Typ **authentifizierte Benutzer**Option **OK**, und wählen Sie dann **OK** erneut auf die Standardeinstellung übernehmen von Berechtigungen zum Lesen.
    
    Dieser Schritt ist notwendig, da Änderungen der Sicherheit in vorgenommenen [MS16-072](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016).

>[!IMPORTANT]
>Aufgrund der sicherheitsänderungen in [MS16-072A](https://support.microsoft.com/help/3163622/ms16-072-security-update-for-group-policy-june-14%2c-2016), Sie müssen die authentifizierte Benutzer delegiert lesen Berechtigungen jetzt erteilen, auf dem Gruppenrichtlinienobjekt – andernfalls wird nicht das Gruppenrichtlinienobjekt auf Benutzer angewendet, oder wenn es bereits angewendet wird, wird das GPO entfernt, Umleiten von Benutzerprofilen zurück an den lokalen Computer. Weitere Informationen finden Sie unter [bereitstellen Group Policy Security Update MS16-072](https://blogs.technet.microsoft.com/askds/2016/06/22/deploying-group-policy-security-update-ms16-072-kb3163622/).

## <a name="step-5-optionally-set-up-roaming-user-profiles-on-user-accounts"></a>Schritt 5: Richten Sie optional Roamingbenutzerprofile in den Benutzerkonten ein

Wenn Sie Roamingbenutzerprofile für Benutzerkonten bereitstellen, verwenden Sie folgendes Verfahren, um Roamingbenutzerprofile für Benutzerkonten in Active Directory-Domänendiensten anzugeben. Wenn Sie Roamingbenutzerprofile auf Computern bereitstellen wie in der Regel für Remotedesktopdienste oder virtualisierte desktopbereitstellungen, verwenden stattdessen das Verfahren finden Sie im [Schritt 6: Richten Sie optional Roamingbenutzerprofile auf Computern](#step-6-optionally-set-up-roaming-user-profiles-on-computers).

> [!NOTE]
> Wenn Sie in Benutzerkonten Roamingbenutzerprofile mithilfe von Active Directory und auf Computern mithilfe der Gruppenrichtlinie einrichten, hat die computerbasierte Richtlinieneinstellung eine höhere Priorität.

Hier ist so richten Sie Roamingbenutzerprofile für Benutzerkonten:

1. Navigieren Sie im Active Directory-Verwaltungscenter in der entsprechenden Domäne zum Container **Benutzer** (oder Organisationseinheit).
2. Wählen Sie alle Benutzer, die Sie möchten ein Roamingbenutzerprofil zuweisen, mit der rechten Maustaste in die Benutzer aus, und wählen Sie dann **Eigenschaften**.
3. In der **Profil** wählen Sie im Abschnitt der **Profilpfad:** Kontrollkästchen und geben Sie dann den Pfad zur Dateifreigabe, wo Sie möchten des Benutzers Roamingbenutzerprofil, gefolgt von Speichern `%username%` (d.h. automatisch ersetzt durch den Benutzer bei der erstmaligen Verwendung, die, den der Benutzer sich meldet). Zum Beispiel:
    
    `\\fs1.corp.contoso.com\User Profiles$\%username%`
    
    Ein verbindliches Roamingbenutzerprofil anzugeben, geben Sie den Pfad zur Datei "Ntuser.man" angeben, die Sie zuvor z.B. erstellt `fs1.corp.contoso.comUser Profiles$default`. Weitere Informationen finden Sie unter [erstellen verbindliche](https://docs.microsoft.com/windows/client-management/mandatory-user-profile).
4. Wählen Sie **OK**.

> [!NOTE]
> Standardmäßig ist beim Verwenden von Roamingbenutzerprofilen die Bereitstellung aller Windows® Laufzeit-basierten (Windows Store) Apps zulässig. Bei der Verwendung eines speziellen Profils werden Apps jedoch nicht standardmäßig bereitgestellt. Bei speziellen Profilen handelt es sich um Benutzerprofile, in denen Änderungen verworfen werden, nachdem sich der Benutzer abgemeldet hat:
> <br><br>Um bei der App-Bereitstellung für spezielle Profile Einschränkungen zu entfernen, müssen Sie die Richtlinieneinstellung **Allow deployment operations in special profiles** aktivieren (befindet sich unter Computerkonfiguration\Richtlinien\Administrative Vorlagen\Windows-Komponenten\App-Paketbereitstellung). In diesem Szenario bereitgestellte Apps speichern jedoch einige Daten auf dem Computer, die sich ansammeln könnten, z. B. wenn sich Hunderte Benutzer auf einem einzelnen Computer befinden. Klicken Sie zum Bereinigen von apps suchen, oder entwickeln Sie ein Tool, verwendet der [CleanupPackageForUserAsync](https://msdn.microsoft.com/library/windows/apps/windows.management.deployment.packagemanager.cleanuppackageforuserasync.aspx) -API zum Bereinigen von app-Pakete für Benutzer, die ein Profil auf dem Computer nicht mehr vorhanden.
> <br><br>Zusätzliche Hintergrundinformationen zu Windows Store-Apps finden Sie unter [Verwalten des Clientzugriffs auf den Windows Store](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh832040(v=ws.11)>).

## <a name="step-6-optionally-set-up-roaming-user-profiles-on-computers"></a>Schritt 6: Richten Sie optional Roamingbenutzerprofile auf den Computern ein

Wenn Sie Roamingbenutzerprofile für Computer bereitstellen, wie es in der Regel für Remotedesktopdienste oder virtualisierte Desktopbereitstellungen erfolgt, verwenden Sie das folgende Verfahren. Wenn Sie Roamingbenutzerprofile für Benutzerkonten bereitstellen, verwenden Sie die Verfahren in [Schritt 5: Richten Sie optional Roamingbenutzerprofile in den Benutzerkonten](#step-5-optionally-set-up-roaming-user-profiles-on-user-accounts).

Sie können Gruppenrichtlinien verwenden, anzuwendende Roamingbenutzerprofile auf Computern mit Windows 8.1, Windows 8, Windows 7, Windows Vista, Windows Server-2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008.

> [!NOTE]
> Wenn Sie auf Computern Roamingbenutzerprofile mithilfe von Active Directory und in Benutzerkonten mithilfe der Gruppenrichtlinie einrichten, hat die computerbasierte Richtlinieneinstellung eine höhere Priorität.

Hier ist so richten Sie Roamingbenutzerprofile auf Computern:

1. Öffnen Sie den Server-Manager auf einem Computer, auf dem die Gruppenrichtlinienverwaltung installiert ist.
2. Von der **Tools** , wählen Sie im Menü **Gruppenrichtlinienverwaltung**. Die Gruppenrichtlinien-Verwaltungskonsole wird angezeigt.
3. In der Gruppenrichtlinien-Verwaltungskonsole mit der Maustaste des Gruppenrichtlinienobjekts, das Sie in Schritt 3 erstellt haben (z. B. **Roamingbenutzerprofileinstellungen**), und wählen Sie dann **bearbeiten**.
4. Navigieren Sie im Fenster des Gruppenrichtlinienverwaltungs-Editors zu **Computerkonfiguration**, **Richtlinien**, **Administrative Vorlagen**, **System** und dann zu **Benutzerprofile**.
5. Mit der rechten Maustaste **Festlegen der Pfad des servergespeicherten Profils für alle Benutzer, die an diesem Computer anmelden** und wählen Sie dann **bearbeiten**.
    > [!TIP]
    > Ein Benutzer-Basisordner (sofern konfiguriert) ist der von einigen Programmen (z. B. Windows PowerShell) verwendete Standardordner. Sie können einen alternativen lokalen oder Netzwerkspeicherort pro Benutzer konfigurieren, indem Sie den Abschnitt **Basisordner** der Benutzerkontoeigenschaften in AD DS verwenden. Um den basisordnerspeicherort für alle Benutzer eines Computers mit Windows 8.1, Windows 8, Windows Server-2019, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 in einer virtuellen desktopumgebung konfigurieren zu können, aktivieren die **benutzerbasisordner festlegen**  richtlinieneinstellung, und geben Sie dann die Datei-Freigabe und den Laufwerkbuchstaben zuzuordnen (oder geben Sie einen lokalen Ordner). Verwenden Sie keine Umgebungsvariablen oder Ellipsen. Der Benutzeralias wird an das Ende des während der Benutzeranmeldung angegebenen Pfads angefügt.
6. In der **Eigenschaften** wählen Sie im Dialogfeld **aktiviert**
7. In der **Benutzer, die an diesem Computer anmelden, sollten diesen Profilpfad für servergespeicherte verwenden** Geben Sie den Pfad zur Dateifreigabe, wo Sie möchten des Benutzers Roamingbenutzerprofil, gefolgt von Speichern `%username%` (wird automatisch durch ersetzt mit den Benutzer bei der erstmaligen Verwendung der Benutzer angemeldet). Zum Beispiel:

    `\\fs1.corp.contoso.com\User Profiles$\%username%`

    Um ein verbindliches Roamingbenutzerprofil anzugeben, die ist ein vordefiniertes Profil Benutzer kann nicht auf die dauerhafte Änderungen (Änderungen werden zurückgesetzt, wenn der Benutzer abmeldet,), geben Sie den Pfad zur Datei "Ntuser.man" angeben, die Sie zuvor z.B. erstellt, `\\fs1.corp.contoso.com\User Profiles$\default`. Weitere Informationen finden Sie unter [Erstellen eines verbindlichen Benutzerprofils](https://docs.microsoft.com/windows/client-management/mandatory-user-profile).
8. Wählen Sie **OK**.

## <a name="step-7-optionally-specify-a-start-layout-for-windows-10-pcs"></a>Schritt 7: Geben Sie optional ein Start-Layout für Windows 10-PCs

Sie können Gruppenrichtlinien verwenden, zu einem bestimmten startmenülayout anwenden, sodass Benutzer auf allen PCs dasselbe Layout Start finden Sie unter. Wenn die Benutzer melden sich mit mehr als ein PC, und Sie ein konsistentes Layout für den Start auf PCs haben sollen, stellen Sie sicher, dass das Gruppenrichtlinienobjekt auf alle ihre PCs angewendet wird.

Um ein Start-Layout anzugeben, führen Sie folgende Schritte aus:

1. Aktualisieren Sie Ihre Windows 10-PCs auf Windows 10 Version 1607 (auch bekannt als das Anniversary Update) oder höher, und installieren Sie das kumulative Update für 14. März 2017 ([KB4013429](https://support.microsoft.com/kb/4013429)) oder höher.
2. Erstellen einer vollständigen oder teilweisen Start Menü Layout XML-Datei an. Zu diesem Zweck finden Sie unter [anpassen und Export startlayouts](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout).
    * Bei Angabe einer *vollständige* startlayouts, ein Benutzer kann keine Teil des Startmenüs anpassen. Bei Angabe einer *teilweise* Start Layout mit Ausrichtung von Benutzern angepasst werden können alle Elemente außer den gesperrten Gruppen von Kacheln, die Sie angeben. Allerdings wird nicht mit einem partiellen Layout heraus starten benutzeranpassungen im Startmenü auf anderen PCs das Roaming durchgeführt.
3. Mithilfe der Gruppenrichtlinie das Gruppenrichtlinienobjekt für Roamingbenutzerprofile erstellten der benutzerdefinierten startlayouts zuweisen. Zu diesem Zweck finden Sie unter [mithilfe von Gruppenrichtlinien auf einem benutzerdefinierten startlayouts in einer Domäne anwenden](https://docs.microsoft.com/windows/configuration/customize-windows-10-start-screens-by-using-group-policy#bkmk-domaingpodeployment).
4. Verwenden Sie die Gruppenrichtlinie, um den folgenden Registrierungswert auf Ihrem Windows 10-PCs festzulegen. Zu diesem Zweck finden Sie unter [Konfigurieren eines Registrierungselements](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753092(v=ws.11)>).

| **Aktion**   | **Update**                  |
| ------------ | ------------                |
| Hive         | **HKEY_LOCAL_MACHINE**      |
| Schlüsselpfad     | **Software\Microsoft\Windows\CurrentVersion\Explorer** |
| Wertname   | **SpecialRoamingOverrideAllowed** |
| Werttyp   | **REG_DWORD**               |
| Wertdaten   | **1** (oder **0** deaktivieren) |
| Base         | **Decimal**                 |

5. (Optional) Aktivieren Sie die erstmalige Anmeldung Optimierungen verwenden, stellen schneller für Benutzer anmelden. Zu diesem Zweck finden Sie unter [Anwenden von Richtlinien zur Verbesserung der Zeitpunkt der Anmeldung](https://docs.microsoft.com/windows/client-management/mandatory-user-profile#apply-policies-to-improve-sign-in-time).
6. (Optional) Zur Verringerung von Anmeldezeiten durch das Entfernen unnötiger apps aus dem Windows 10-Basis-Image, die, das Sie zum Bereitstellen von Client-PCs verwenden. 2019 für Windows Server und Windows Server 2016 keine vorab bereitgestellte apps, damit Sie auf Server-Images können diesen Schritt überspringen.
    - Um apps zu entfernen, verwenden Sie die [Remove-AppxProvisionedPackage](https://docs.microsoft.com/powershell/module/dism/remove-appxprovisionedpackage?view=win10-ps) Cmdlet in Windows PowerShell die folgenden Anwendungen deinstallieren. Wenn Sie Ihre PCs bereits bereitgestellt wurden, können Sie das Entfernen dieser Apps mithilfe von Skripts die [Remove-AppxPackage](https://docs.microsoft.com/powershell/module/appx/remove-appxpackage?view=win10-ps).
    
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
>Deinstallieren diese apps Anmeldezeiten verringert, aber lassen Sie, wenn Ihre diese bereitstellungsanforderungen zu installieren.

## <a name="step-8-enable-the-roaming-user-profiles-gpo"></a>Schritt 8: Aktivieren Sie das Gruppenrichtlinienobjekt der Roamingbenutzerprofile

Wenn Sie Roamingbenutzerprofile mithilfe der Gruppenrichtlinie auf Computern einrichten, oder andere Roamingbenutzerprofileinstellungen mit der Gruppenrichtlinie angepasst haben, besteht der nächste Schritt darin, das Gruppenrichtlinienobjekt zu aktivieren, damit es auf die betroffenen Benutzer angewendet werden kann.

>[!TIP]
>Wenn Sie planen, implementieren die Unterstützung primärer Computer, das jetzt vornehmen Sie, bevor Sie das Gruppenrichtlinienobjekt aktivieren. Dadurch wird verhindert, dass Benutzerdaten auf nicht primäre Computer kopiert werden, bevor die Unterstützung primärer Computer aktiviert ist. Die spezifische Richtlinieneinstellungen finden Sie unter [Bereitstellen von Hauptcomputern für Ordnerumleitung und servergespeicherte Benutzerprofile](deploy-primary-computers.md).

Hier ist das Gruppenrichtlinienobjekt Roaming zu aktivieren:

1. Öffnen Sie die Gruppenrichtlinienverwaltung.
2. Mit der rechten Maustaste in des Gruppenrichtlinienobjekts, das Sie erstellt haben, und wählen Sie dann **Verknüpfung aktiviert**. Neben dem Menüelement wird ein Kontrollkästchen angezeigt.

## <a name="step-9-test-roaming-user-profiles"></a>Schritt 9: Testen von Roamingbenutzerprofilen

Melden Sie sich mit einem für Roamingbenutzerprofile konfigurierten Benutzerkonto an einem Computer an oder melden Sie sich an einem für Roamingbenutzerprofile konfigurierten Computer an, um die Roamingbenutzerprofile zu testen. Bestätigen Sie anschließend, dass das Profil umgeleitet wird.

Hier ist zum Testen von Roamingbenutzerprofilen:

1. Melden Sie sich mit einem Benutzerkonto an einem primären Computer an (bei aktivierter Unterstützung primärer Computer), für das Roamingbenutzerprofile aktiviert sind. Wenn Sie Roamingbenutzerprofile auf bestimmten Computern aktiviert haben, melden Sie sich an einem dieser Computer an.
2. Wenn sich der Benutzer zuletzt an dem Computer angemeldet hat, öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten und geben Sie folgenden Befehl ein, um sicherzustellen, dass die aktuellsten Gruppenrichtlinieneinstellungen auf dem Clientcomputer angewendet werden.
    
    ```PowerShell
    GpUpdate /Force
    ```
3. Bestätigen, dass das Benutzerprofil gewechselt wird, öffnen Sie **Systemsteuerung**Option **System und Sicherheit**Option **System**Option **Erweiterte Systemeinstellungen** Option **Einstellungen** der Benutzerprofile aus, und suchen Sie nach **Roaming** in die **Typ** Spalte.

## <a name="appendix-a-checklist-for-deploying-roaming-user-profiles"></a>Anhang A: Prüfliste zur Bereitstellung von Roamingbenutzerprofilen

| Status                     | Aktion                                                |
| ---                        | ------                                                |
| ☐<br>☐<br>☐<br>☐<br>☐   | 1. Bereiten Sie die Domäne vor<br>-Beitritts von Computern zur Domäne<br>-Aktivieren Sie die Verwendung separater Profilversionen<br>– Erstellen von Benutzerkonten<br>– (Optional) Bereitstellen von Ordnerumleitung |
| ☐<br><br><br>             | 2. Erstellen Sie eine Sicherheitsgruppe für Roamingbenutzerprofile<br>-Group-Name:<br>-Mitglieder: |
| ☐<br><br>                 | 3. Erstellen Sie eine Dateifreigabe für Roamingbenutzerprofile<br>-Dateifreigabename: |
| ☐<br><br>                 | 4. Erstellen Sie ein Gruppenrichtlinienobjekt für Roamingbenutzerprofile<br>-GPO-Name:|
| ☐                         | 5. Konfigurieren Sie die Richtlinieneinstellungen der Roamingbenutzerprofile    |
| ☐<br>☐<br>☐              | 6. Aktivieren von Roamingbenutzerprofilen<br>-Auf Benutzerkonten in AD DS aktiviert?<br>-Bei Computerkonten in der Gruppenrichtlinie aktiviert?<br> |
| ☐                         | 7. (Optional) Geben Sie eine obligatorische startlayouts für Windows 10-PCs |
| ☐<br>☐<br><br>☐<br><br>☐ | 8. (Optional) Aktivieren Sie die Unterstützung primärer computer<br>– Festlegen von hauptcomputern für Benutzer<br>-Speicherort der Benutzer- und primären computerzuordnungen:<br>– (Optional) aktivieren die Unterstützung primärer Computer für die Ordnerumleitung<br>-Computer-basierte oder nutzerbasiert?<br>– (Optional) aktivieren die Unterstützung primärer Computer für Roamingbenutzerprofile |
| ☐                        | 9. Aktivieren Sie das Gruppenrichtlinienobjekt der Roamingbenutzerprofile                |
| ☐                        | 10. Testen von Roamingbenutzerprofilen                         |

## <a name="appendix-b-profile-version-reference-information"></a>Anhang B: Referenzinformationen zur Profilversion

Jedes Profil hat eine Profilversion, die ungefähr entspricht der Version von Windows auf dem das Profil verwendet wird. Z. B. Windows 10, Version 1703 und Version 1607 beide verwenden die. IPv6-Profilversion. Microsoft erstellt eine neue Profilversion nur bei Bedarf, um die Kompatibilität, erhalten die ist, warum nicht jede Version von Windows eine neue Profilversion enthält.

In der folgenden Tabelle sind die Speicherorte von Roamingbenutzerprofilen in verschiedenen Windows-Versionen aufgeführt.

| Version des Betriebssystems | Speicherort der Roamingbenutzerprofile |
| --- | --- |
| Windows XP und Windows Server 2003 | ```\\<servername>\<fileshare>\<username>``` |
| Windows Vista und Windows Server 2008 | ```\\<servername>\<fileshare>\<username>.V2``` |
| Windows 7 und Windows Server 2008 R2 | ```\\<servername>\<fileshare>\<username>.V2``` |
| Windows 8 und Windows Server 2012 | ```\\<servername>\<fileshare>\<username>.V3``` (nachdem das Softwareupdate und der Registrierungsschlüssel angewendet wurden)<br>```\\<servername>\<fileshare>\<username>.V2``` (bevor die Software und der Registrierungsschlüssel angewendet wurden) |
| Windows 8.1 und Windows Server 2012 R2 | ```\\<servername>\<fileshare>\<username>.V4``` (nachdem das Softwareupdate und der Registrierungsschlüssel angewendet wurden)<br>```\\<servername>\<fileshare>\<username>.V2``` (bevor die Software und der Registrierungsschlüssel angewendet wurden) |
| Windows 10 | ```\\<servername>\<fileshare>\<username>.V5``` |
| Windows 10, Version 1703 und Version 1607 | ```\\<servername>\<fileshare>\<username>.V6``` |

## <a name="appendix-c-working-around-reset-start-menu-layouts-after-upgrades"></a>Anhang C: Arbeit zurücksetzen Start Menülayouts etwa nach upgrades

Hier sind einige Möglichkeiten zum Umgehen der Start-Menülayouts erste zurücksetzen, nachdem Sie ein direktes Upgrade aus:

- Wenn nur ein Benutzer ständig das Gerät verwendet und der IT-Administrator einer verwalteten Betriebssystem-Strategie für die Bereitstellung wie SCCM können sie Folgendes tun:
    
  1. Exportieren der startmenülayout mit Export-Startlayout vor dem upgrade 
  2. Importieren Sie mit Import-StartLayout startmenülayout nach OOBE, aber bevor der Benutzer anmeldet  
 
     > [!NOTE] 
     > Importieren einer StartLayout ändert das Standardbenutzerprofil. Alle Benutzerprofile, die erstellt werden, nachdem der Import aufgetreten ist, erhalten die importierten Startlayouts.
 
- IT-Administratoren können entscheiden, um Startlayouts mit der Gruppenrichtlinie zu verwalten. Mithilfe der Gruppenrichtlinie bietet ein zentralisiertes Verwaltungssystem, um einen standardisierten Layouts starten auf Benutzer anzuwenden. Es gibt 2 Modi, Modi, um mithilfe der Gruppenrichtlinie für die Verwaltung. Vollständige Sperrung und partielle sperren. Das Szenario für die vollständige Sperrung wird verhindert, dass den Benutzer Änderungen an den Start-Layout. Das partielle Lockdown-Szenario kann Benutzer, um einen bestimmten Bereich für die Startzeit zu ändern. Weitere Informationen finden Sie unter [anpassen und Export startlayouts](https://docs.microsoft.com/windows/configuration/customize-and-export-start-layout).
        
   > [!NOTE]
   > Vorgenommenen benutzeränderungen in die partielle Lockdown-Szenario noch verloren während des Upgrades.

- Lassen Sie Beginn Layout zurücksetzen auftreten und Endbenutzer Start neu konfigurieren können. Eine e-Mail-Benachrichtigung oder einer sonstigen Benachrichtigung kann an Endbenutzer gesendet werden, erwartet ihre startlayouts zurückgesetzt werden sollen, nach dem upgrade des Betriebssystems zu Auswirkungen. 

# <a name="change-history"></a>Änderungsverlauf

In der folgenden Tabelle sind die wichtigsten Änderungen zu diesem Thema zusammengefasst.

| date | Beschreibung |Grund|
| --- | ---         | ---   |
| 1. Mai 2019 | Zusätzliche Updates für Windows Server-2019 |
| 10. April 2018 | Zusätzliche Erläuterung der Wenn benutzeranpassungen Start nach einem Betriebssystemupgrade des direktes nicht mehr vorhanden sind|Legende bekanntes Problem. |
| 13. März 2018 | Für WindowsServer 2016 aktualisiert | Verschoben aus früheren Versionen-Bibliothek und aktualisiert die aktuelle Version von Windows Server. |
| Am 13. April 2017 | Informationen zum Eigenschaftsprofil für Windows 10, Version 1703, hinzugefügt und es wird erläutert wie servergespeicherte Profile Versionen Arbeit bei der Aktualisierung von Betriebssystemen, finden Sie unter [Überlegungen zur Verwendung von Roamingbenutzerprofilen in mehreren Versionen von Windows](#considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows). | Kundenfeedback. |
| 14. März 2017 | Hinzugefügte Optionaler Schritt zum Angeben von für Windows 10-PCs in eine obligatorische startlayouts [Anhang A: Checkliste für die Bereitstellung von Roamingbenutzerprofilen](#appendix-a-checklist-for-deploying-roaming-user-profiles). |Featureänderungen Sie das aktuellste Update für Windows. |
| 23. Januar 2017 | Einen Schritt hinzugefügt [Schritt 4: Erstellen Sie optional ein Gruppenrichtlinienobjekt für Roamingbenutzerprofile](#step-4-optionally-create-a-gpo-for-roaming-user-profiles) , delegieren Leseberechtigungen für authentifizierte Benutzer, das jetzt ist aufgrund der Aktualisierung der Gruppenrichtlinie Sicherheit erforderlich sind.|Sicherheitsbezogene Änderungen an der gruppenrichtlinienverarbeitung. |
| Am 29. Dezember 2016 | Einen Link hinzugefügt [Schritt 8: Aktivieren Sie das Gruppenrichtlinienobjekt Roaming User Profiles](#step-8-enable-the-roaming-user-profiles-gpo) zu beim Abrufen von Informationen zum Festlegen von Gruppenrichtlinien für die primären Computern vereinfachen. Einige Verweise auf die Schritte 5 und 6, die die Zahlen hatten falsche auch behoben.|Kundenfeedback. |
| 5. Dezember 2016 | Hinzugefügte Informationen, die eine Start-menüeinstellungen roaming Problem erläutert. | Kundenfeedback. |
| 6. Juli 2016 | Hinzugefügt von Windows 10-profilversionensuffixe in [Anhang B: Referenzinformationen zur Profilversion](#appendix-b-profile-version-reference-information). Auch Windows XP und Windows Server 2003 aus der Liste der unterstützten Betriebssysteme entfernt werden. | Updates für die neuen Versionen von Windows und entfernte Informationen zu Versionen von Windows, die nicht mehr unterstützt werden. |
| 7. Juli 2015 | Anforderung und Schritt zum Deaktivieren der kontinuierlichen Verfügbarkeit bei Verwendung eines gruppierten Dateiservers hinzugefügt. | Gruppierte Dateifreigaben bieten eine bessere Leistung für kleine Schreibvorgänge (die für Roamingbenutzerprofile typisch sind), wenn die kontinuierliche Verfügbarkeit deaktiviert ist. |
| 19. März 2014 | Großgeschriebene profilversionensuffixe (. V2. V3. V4) in [Anhang B: Referenzinformationen zur Profilversion](#appendix-b-profile-version-reference-information). | Obwohl Windows Groß-/Kleinschreibung ist bei der Verwendung von NFS mit der Dateifreigabe ist es wichtig, dass die richtigen profilsuffix für das Profil-Suffix haben. |
| 09. Oktober 2013 | Überarbeitet, Windows Server 2012 R2 und Windows 8.1, es wird ein paar Dinge erläutert und hinzugefügt der [Überlegungen zur Verwendung von Roamingbenutzerprofilen in mehreren Versionen von Windows](#considerations-when-using-roaming-user-profiles-on-multiple-versions-of-windows) und [Anhang B: Referenzinformationen zur Profilversion](#appendix-b-profile-version-reference-information) Abschnitte. | Updates für die neue version Kundenfeedback. |

## <a name="more-information"></a>Weitere Informationen

- [Bereitstellen von Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile](deploy-folder-redirection.md)
- [Bereitstellen von Hauptcomputern für Ordnerumleitung und Roamingbenutzerprofile](deploy-primary-computers.md)
- [Implementieren der Benutzerstatusverwaltung](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc784645(v=ws.10)>)
- [Microsoft Support-Anweisung zu replizierten Benutzerprofildaten](https://blogs.technet.microsoft.com/askds/2010/09/01/microsofts-support-statement-around-replicated-user-profile-data/)
- [Querladen von Apps mit DISM](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh852635(v=win.10)>)
- [Problembehandlung bei Verpackung, Bereitstellung und Abfrage von Windows-Runtime-basierten apps](https://msdn.microsoft.com/library/windows/desktop/hh973484.aspx)