---
title: Bereitstellen von hauptcomputern für Ordnerumleitung und Roamingbenutzerprofile
description: Informationen zum Aktivieren der Unterstützung für Hauptcomputer und Festlegen von hauptcomputern für Benutzer mit der Ordnerumleitung und servergespeicherte Benutzerprofile.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 39b790f39a2bf9c6334eb2176aa2e5f2e0196c0c
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475967"
---
# <a name="deploy-primary-computers-for-folder-redirection-and-roaming-user-profiles"></a>Bereitstellen von hauptcomputern für Ordnerumleitung und Roamingbenutzerprofile

>Gilt für: Windows 10, Windows 8, Windows 8.1, WindowsServer 2019, WindowsServer 2016, WindowsServer 2012, Windows Server 2012 R2

In diesem Thema wird beschrieben, wie die Unterstützung primärer Computer aktivieren und Festlegen von hauptcomputern für Benutzer. Auf diese Weise können Sie steuern, welchen Computern die Ordnerumleitung und servergespeicherte Benutzerprofile verwenden.

>[!IMPORTANT]
>Wenn Sie die Unterstützung primärer Computer für Roamingbenutzerprofile zu aktivieren, sollten Sie die aktivieren Sie Unterstützung primärer Computer für die Ordnerumleitung auch jederzeit. Auf diese Weise Dokumente und andere Benutzerdateien aus der Benutzerprofile, wodurch Profile klein bleiben, und melden Sie sich Mal schnell zu bleiben.

## <a name="prerequisites"></a>Vorraussetzungen

## <a name="software-requirements"></a>Softwareanforderungen

Die Unterstützung primärer Computer ist Folgendes erforderlich:

- Das Schema der Active Directory Domain Services (AD DS) muss aktualisiert werden, um Windows Server 2012 schemaerweiterungen für enthält (einen Windows Server 2012-Domänencontroller automatisch installieren, aktualisiert das Schema). Informationen zum Aktualisieren des AD DS-Schemas finden Sie unter [Adprep.exe Integration](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh472161(v=ws.11)#adprepexe-integration>) und [Running Adprep.exe](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd464018(v=ws.10)>).
- Clientcomputer müssen Windows 10, Windows 8.1, Windows 8, Windows Server-2019, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausführen.

>[!TIP]
>Obwohl die Unterstützung primärer Computer Ordnerumleitung und/oder servergespeicherte Benutzerprofile, erfordert, wenn Sie diese Technologien zum ersten Mal bereitstellen, empfiehlt sich, richten Sie die Unterstützung primärer Computer vor der Aktivierung die GPOs, die Ordnerumleitung zu konfigurieren und Roaming-Benutzerprofile Dadurch wird verhindert, dass Benutzerdaten auf nicht primäre Computer kopiert werden, bevor die Unterstützung primärer Computer aktiviert ist. Weitere Informationen zu Konfigurationen finden Sie unter [Bereitstellen der Ordnerumleitung](deploy-folder-redirection.md) und [Roamingbenutzerprofile bereitstellen](deploy-roaming-user-profiles.md).

## <a name="step-1-designate-primary-computers-for-users"></a>Schritt 1: Legen Sie die primären Computer für die Benutzer fest

Der erste Schritt beim Bereitstellen von Unterstützung für Hauptcomputer ist der primäre Computer für jeden Benutzer festlegen. Zu diesem Zweck verwenden Sie Active Directory-Verwaltungscenter erhalten den distinguished Name des betroffenen Computern, und legen Sie dann die **MsDs-PrimaryComputer** Attribut.

>[!TIP]
>Zur Verwendung von Windows PowerShell mit primären Computern finden Sie im Blogbeitrag [zuwenden vertrauter Windows 8-Hauptcomputer](<https://blogs.technet.microsoft.com/askds/2012/10/23/digging-a-little-deeper-into-windows-8-primary-computer/>).

Hier ist das Angeben der verwendeten primären Computern für Benutzer:

1. Öffnen Sie den Server-Manager auf einem Computer, auf dem Active Directory-Verwaltungstools installiert sind.
2. Auf der **Tools** , wählen Sie im Menü **Active Directory-Verwaltungscenter**. Das Active Directory-Verwaltungscenter wird angezeigt.
3. Navigieren Sie zu der **Computer** Container in der entsprechenden Domäne.
4. Mit der rechten Maustaste in eines Computers, die Sie verwenden möchten, als Hauptcomputer festlegen, und wählen Sie dann **Eigenschaften**.
5. Wählen Sie im Navigationsbereich **Erweiterungen**.
6. Wählen Sie die **Attribut-Editor** Registerkarte, scrollen Sie zum **"distinguishedName"** Option **Ansicht**mit der rechten Maustaste auf den aufgeführten Wert, wählen Sie **Kopie**, Wählen Sie **OK**, und wählen Sie dann **Abbrechen**.
7. Navigieren Sie zu der **Benutzer** Container in der entsprechenden Domäne, mit der rechten Maustaste des Benutzers, Sie weisen Sie den Computer, und wählen Sie dann möchten **Eigenschaften**.
8. Wählen Sie im Navigationsbereich **Erweiterungen**.
9. Wählen Sie die **Attribut-Editor** Registerkarte **MsDs-PrimaryComputer** und wählen Sie dann **bearbeiten**. Das Dialogfeld %%amp;quot;Editor für mehrwertige Zeichenfolgen%%amp;quot; wird angezeigt.
10. Mit der rechten Maustaste in des Textfeld ein, wählen Sie **einfügen**Option **hinzufügen**Option **OK**, und wählen Sie dann **OK** erneut aus.

## <a name="step-2-optionally-enable-primary-computers-for-folder-redirection-in-group-policy"></a>Schritt 2: Aktivieren Sie optional die primäre Computern für die Ordnerumleitung in Gruppenrichtlinien

Der nächste Schritt ist optional Gruppenrichtlinien zum Aktivieren der Unterstützung für Hauptcomputer für Ordnerumleitung konfigurieren. Auf diese Weise kann die Ordner auf Computern, die als Hauptcomputer des Benutzers festgelegt, aber nicht auf andere Computer umgeleitet werden. Sie können den primäre Computern für die Ordnerumleitung auf einer computerspezifischen Basis oder pro Benutzer steuern.

Hier ist Hauptcomputer für Ordnerumleitung aktivieren:

1. In der Gruppenrichtlinien-Verwaltungskonsole mit der Maustaste des Gruppenrichtlinienobjekts, das Sie erstellt haben, bei der anfänglichen Konfiguration der Umleitung des Ordners bzw. Roaming User Profiles (z. B. **Ordnerumleitungseinstellungen** oder **Roaming-Benutzer Roamingbenutzerprofileinstellungen**), und wählen Sie dann **bearbeiten**.
2. Um Unterstützung für Hauptcomputer mithilfe von Gruppenrichtlinien-basierte Computer aktivieren, navigieren Sie zu **Computerkonfiguration**. Für eine benutzerbasierte Gruppenrichtlinien, navigieren Sie zu **Benutzerkonfiguration**.
    - Computerbasierte der Gruppenrichtlinie gilt die Verarbeitung der primären Computer auf allen Computern, die für die Gruppenrichtlinienobjekt gilt Auswirkungen auf alle Benutzer der Computer wurde.
    - Benutzerbasierte der Gruppenrichtlinie für Hauptcomputer Verarbeitung für alle Benutzerkonten, die das Gruppenrichtlinienobjekt gilt, die Auswirkungen auf alle Computer, auf die der Benutzer sich anmelden, gilt.
3. Unter **Computerkonfiguration** oder **Benutzerkonfiguration**, navigieren Sie zu **Richtlinien**, klicken Sie dann **Administrative Vorlagen**, und klicken Sie dann  **System**, klicken Sie dann **Ordnerumleitung**.
4. Mit der rechten Maustaste **Ordner nur auf hauptcomputern umleiten**, und wählen Sie dann **bearbeiten**.
5. Wählen Sie **aktiviert**, und wählen Sie dann **OK**.

## <a name="step-3-optionally-enable-primary-computers-for-roaming-user-profiles-in-group-policy"></a>Schritt 3: Aktivieren Sie optional die primäre Computern für Roamingbenutzerprofile in der Gruppenrichtlinie

Der nächste Schritt ist so konfigurieren Sie optional auf der Gruppenrichtlinie, um die Unterstützung primärer Computer für Roamingbenutzerprofile zu aktivieren. Dadurch können dem Profil eines Benutzers, der auf Computern, die als Hauptcomputer des Benutzers festgelegt, aber nicht auf andere Computer Roaming zulässt.

So wird zum Aktivieren von hauptcomputern für servergespeicherte Benutzerprofile:

1. Aktivieren Sie Unterstützung für Hauptcomputer für Ordnerumleitung, sofern Sie noch nicht geschehen.
    * Auf diese Weise Dokumente und andere Benutzerdateien aus der Benutzerprofile, wodurch Profile klein bleiben, und melden Sie sich Mal schnell zu bleiben.
2. In der Gruppenrichtlinien-Verwaltungskonsole mit der Maustaste des Gruppenrichtlinienobjekts, das Sie erstellt haben (z. B. **Ordnerumleitung und Roamingbenutzerprofileinstellungen**), und wählen Sie dann **bearbeiten**.
3. Navigieren Sie zu **Computerkonfiguration**, klicken Sie dann **Richtlinien**, klicken Sie dann **Administrative Vorlagen**, klicken Sie dann **System**, und klicken Sie dann **Benutzerprofile**.
4. Mit der rechten Maustaste **herunterladen, servergespeicherte Profile auf primären Computern nur** und wählen Sie dann **bearbeiten**.
5. Wählen Sie **aktiviert**, und wählen Sie dann **OK**.

## <a name="step-4-enable-the-gpo"></a>Schritt 4: Aktivieren Sie das Gruppenrichtlinienobjekt

Sie nach Abschluss der Konfiguration von Ordnerumleitung und servergespeicherte Benutzerprofile, aktivieren Sie das Gruppenrichtlinienobjekt ein, wenn Sie noch nicht getan haben. Auf diese Weise ermöglicht es, die auf den betroffenen Benutzer und-Computer angewendet werden.

Hier ist die Ordnerumleitung und/oder Roaming User Profiles GPOs zu aktivieren:

1. Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole
2. Mit der rechten Maustaste in der Gruppenrichtlinienobjekten, die Sie erstellt haben, und wählen Sie dann **Verknüpfung aktiviert**. Ein Kontrollkästchen sollte neben dem Menüelement, das angezeigt werden.

## <a name="step-5-test-primary-computer-function"></a>Schritt 5: Testen Sie primäre Computer-Funktion

Um die Unterstützung primärer Computer testen, melden Sie sich an einem primären Computer aus, vergewissern Sie sich, dass die Ordner und Profile umgeleitet werden, melden Sie sich bei einem nicht primären Computer aus, und vergewissern Sie sich, dass die Ordner und die Profile nicht weitergeleitet werden.

Hier wird Hauptcomputer Funktionalität zu testen:

1. Melden Sie sich an einem angegebenen primären Computer mit einem Benutzerkonto an, die für die Umleitung des Ordners bzw. Roamingbenutzerprofile aktiviert haben.
2. Wenn das Benutzerkonto, das zuvor am Computer angemeldet hat, öffnen Sie ein Windows PowerShell-Sitzung oder ein Eingabeaufforderungsfenster als Administrator, geben Sie den folgenden Befehl, und melden Sie sich dann deaktiviert, wenn Sie aufgefordert werden, um sicherzustellen, dass die aktuellsten gruppenrichtlinieneinstellungen, um angewendet werden die Client-Computer:
    ```PowerShell
    Gpupdate /force
    ```
3. Öffnen Sie den Datei-Explorer.
4. Mit der rechten Maustaste in eines umgeleiteten Ordners (z. B. die Ordner Eigene Dokumente in der Bibliothek Dokumente), und wählen Sie dann **Eigenschaften**.
5. Wählen Sie die **Speicherort** Registerkarte, und bestätigen Sie, dass der Pfad die Dateifreigabe angezeigt, Sie anstelle eines lokalen Pfads angegeben. Bestätigen, dass das Benutzerprofil gewechselt wird, öffnen Sie **Systemsteuerung**Option **System und Sicherheit**Option **System**Option **Erweiterte Systemeinstellungen** Option **Einstellungen** der Benutzerprofile aus, und suchen Sie nach **Roaming** in die **Typ** Spalte.
6. Melden Sie sich mit dem gleichen Benutzerkonto auf einem Computer, der nicht als primäre Computer des Benutzers festgelegt ist.
7. Wiederholen Sie die Schritte 2 bis 5, suchen Sie stattdessen für lokale Pfade und ein **lokalen** Profiltyp.

>[!NOTE]
>Wenn Ordner auf einem Computer umgeleitet wurden, bevor Sie die Unterstützung primärer Computer aktiviert, verbleibt die Ordner umgeleitet, es sei denn, die folgende Einstellung in jedem Ordner die Ordner-Umleitung-richtlinieneinstellung konfiguriert ist: **Zurück zum lokalen Benutzerprofilpfad Ordner umleiten, wenn die Richtlinie entfernt wird**. Auf ähnliche Weise zeigt Profile, die zuvor auf einem bestimmten Computer roaming wurden **Roaming** in die **Typ** Spalten, aber die **Status** Spalte zeigt **Lokalen**.

## <a name="more-information"></a>Weitere Informationen

- [Bereitstellen von Ordnerumleitung, Offlinedateien](deploy-folder-redirection.md)
- [Bereitstellen von Roamingbenutzerprofilen](deploy-roaming-user-profiles.md)
- [Übersicht über die Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile](folder-redirection-rup-overview.md)
- [Genauerer Blick etwas auf Hauptcomputer für Windows 8](https://blogs.technet.com/b/askds/archive/2012/10/23/digging-a-little-deeper-into-windows-8-primary-computer.aspx)