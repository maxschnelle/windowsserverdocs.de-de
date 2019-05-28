---
title: Optimierte Verschiebungen von umgeleiteten Ordnern aktivieren
description: So führen Sie eine optimierte Verschieben der umgeleitete Ordner in eine neue Dateifreigabe aus.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7bdf30a4f721568add4e7902245da2a803b72db1
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475871"
---
# <a name="enable-optimized-moves-of-redirected-folders"></a>Optimierte Verschiebungen von umgeleiteten Ordnern aktivieren

>Gilt für: Windows 10, Windows 8, Windows 8.1, WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, WindowsServer (halbjährlicher Kanal)

Dieses Thema beschreibt, wie eine optimierte Verschieben der umgeleitete Ordner (Ordner-Umleitung) in eine neue Dateifreigabe ausgeführt wird. Durch Aktivieren dieser richtlinieneinstellung wird festgelegt, wenn ein Administrator verschiebt die Dateifreigaben mit umgeleitete Ordnern und den Zielpfad der umgeleiteten Ordner in der Gruppenrichtlinie aktualisiert der zwischengespeicherte Inhalt einfach in den lokalen Offlinedateicache ohne keine Verzögerungen umbenannt oder möglichen Datenverlust für den Benutzer.

Zuvor konnten Administratoren ändern den Zielpfad der umgeleiteten Ordner in der Gruppenrichtlinie und die Clientcomputern die Dateien auf der nächsten Anmeldung des betroffenen Benutzers, kopieren lassen verursacht eine verzögerte Anmeldung. Alternativ können Administratoren die Dateifreigabe zu verschieben und aktualisieren den Zielpfad der umgeleiteten Ordner in der Gruppenrichtlinie. Alle Änderungen lokal auf den Clientcomputern zwischen dem Start der Verschiebung und die erste Synchronisierung nach dem Verschieben würden jedoch verloren.

## <a name="prerequisites"></a>Vorraussetzungen

Optimierte verschieben, hat die folgenden Anforderungen:

- Ordnerumleitung muss eingerichtet werden. Weitere Informationen finden Sie unter [Bereitstellen von Ordnerumleitung mit Offlinedateien](deploy-folder-redirection.md).
- Clientcomputer müssen Windows 10, Windows 8.1, Windows 8, Windows Server-2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server (halbjährlicher Kanal) ausführen.

## <a name="step-1-enable-optimized-move-in-group-policy"></a>Schritt 1: Optimierte verschieben in der Gruppenrichtlinie aktivieren

Um das Verschieben von Daten der Ordnerumleitung zu optimieren, mithilfe von Gruppenrichtlinien zum Aktivieren der **aktivieren optimiert Verschieben der Inhalte im Cache für Offlinedateien auf Folder Redirection Server pfadänderung** richtlinieneinstellung für die entsprechende Gruppenrichtlinie Gruppenrichtlinienobjekt (GPO). Konfigurieren diese richtlinieneinstellung **deaktiviert** oder **nicht konfiguriert** bewirkt, dass den Client alle Inhalte für die Umleitung des Ordners an den neuen Speicherort kopieren, und klicken Sie dann den Inhalt aus dem alten Speicherort löschen, wenn die Änderungen am Server-Pfad.

Hier ist so aktivieren Sie die optimierte Verschieben der umgeleitete Ordner:

1. In der Gruppenrichtlinien-Verwaltungskonsole mit der Maustaste des Gruppenrichtlinienobjekts, das Sie für die für die Ordnerumleitung erstellt haben (z. B. **Ordnerumleitung und Roamingbenutzerprofileinstellungen**), und wählen Sie dann **bearbeiten**.
2. Klicken Sie unter **Benutzerkonfiguration**, navigieren Sie zu **Richtlinien**, klicken Sie dann **Administrative Vorlagen**, klicken Sie dann **System**, klicken Sie dann  **Ordnerumleitung**.
3. Mit der rechten Maustaste **aktivieren optimiert Verschieben der Inhalte im Cache für Offlinedateien auf Folder Redirection Server pfadänderung**, und wählen Sie dann **bearbeiten**.
4. Wählen Sie **aktiviert**, und wählen Sie dann **OK**.

## <a name="step-2-relocate-the-file-share-for-redirected-folders"></a>Schritt 2: Die Dateifreigabe für umgeleitete Ordner verschieben

Wenn das Verschieben der Dateifreigabe, die Benutzer enthält Ordner umgeleitet werden, ist es Import Vorsichtsmaßnahmen ergreifen, um sicherzustellen, dass der Ordner ordnungsgemäß verschoben werden.

>[!IMPORTANT]
>Wenn der Benutzer Dateien in sind, verwenden oder wenn der vollständige Zustand beim Übergang nicht beibehalten wird, Benutzern treten möglicherweise auf eine schlechte Leistung wie die Dateien über das Netzwerk von Offlinedateien und sogar Daten verloren gehen generierten Synchronisierungskonflikte kopiert werden.

1. Benachrichtigen von Benutzern im voraus, dass der Hostserver, die ihren umgeleiteten Ordnern ändert und wird empfohlen, dass sie die folgenden Aktionen ausführen:

      - Synchronisieren Sie die Inhalte von ihrem Offlinedateien-Cache, und beheben Sie alle Konflikte.
      - Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, geben Sie **GpUpdate /Target:User/Force**, und klicken Sie dann melden Sie sich ab und wieder anmelden, um sicherzustellen, dass die aktuellsten gruppenrichtlinieneinstellungen auf dem Clientcomputer angewendet werden

        >[!NOTE]
        >Standardmäßig aktualisiert Clientcomputer Gruppenrichtlinien alle 90 Minuten, wenn Sie genügend Zeit für Client-Computern mit aktualisierte Richtlinie empfangen zu ermöglichen, müssen Sie keine Benutzer dazu auffordern, verwenden Sie **GpUpdate**.
2. Entfernen Sie die Dateifreigabe, aus dem Server, um sicherzustellen, dass keine Dateien in der Dateifreigabe verwendet werden. Dazu im Server-Manager auf die **Freigaben** Seite der Datei- und Speicherdienste, mit der rechten Maustaste in der entsprechende Dateifreigabe aus, und wählen Sie **entfernen**.

    Benutzer funktioniert mit Offlinedateien offline, bis der Verschiebevorgang abgeschlossen ist und sie die aktualisierten Einstellungen für die Umleitung des Ordners, von der Gruppenrichtlinie erhalten.

3. Mit einem Konto mit Privilegien zum Sichern, verschieben Sie den Inhalt der Dateifreigabe an den neuen Speicherort mit einer Methode, die Zeitstempel der Dateien, z. B. einer Sicherung beibehalten und Wiederherstellen Sie des Hilfsprogramms. Verwenden der **Robocopy** Befehl Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und geben Sie dann den folgenden Befehl ein, in denen ```<Source>``` ist der aktuelle Speicherort der Dateifreigabe, und ```<Destination>``` ist der neue Speicherort:

    ```PowerShell
    Robocopy /B <Source> <Destination> /Copyall /MIR /EFSRAW
    ```

    >[!NOTE]
    >Die **Xcopy** Befehl werden alle der Zustand nicht beibehalten.
4. Bearbeiten Sie die Richtlinie für die Ordnerumleitung, aktualisieren den Zielordner für jeden umgeleiteten Ordner, den Sie verschieben möchten. Weitere Informationen finden Sie unter Schritt 4 des [Bereitstellen von Ordnerumleitung mit Offlinedateien](deploy-folder-redirection.md).
5. Benachrichtigen von Benutzern, das der Hostserver für die umgeleiteten Ordner geändert hat, und sollten, die **GpUpdate /Target:User/Force** Befehl, und klicken Sie dann melden Sie sich ab und wieder anmelden, rufen Sie die aktualisierte Konfiguration und die richtige Datei fortsetzen Synchronisierung.

    Benutzer sollten für alle Computer mindestens einmal anmelden, stellen Sie sicher, dass die Daten ordnungsgemäß in den einzelnen Offlinedateien verschoben ruft.

## <a name="more-information"></a>Weitere Informationen

* [Bereitstellen von Ordnerumleitung, Offlinedateien](deploy-folder-redirection.md)
* [Bereitstellen von Roamingbenutzerprofilen](deploy-roaming-user-profiles.md)
* [Übersicht über die Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile](folder-redirection-rup-overview.md)