---
title: Optimierte Verschiebungen von umgeleiteten Ordnern aktivieren
description: So führen Sie eine optimierte Verschiebung umgeleiteter Ordner zu einer neuen Dateifreigabe aus
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: edf6596f7daaa2f496b8b4da36e98ee72b05dfcd
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867257"
---
# <a name="enable-optimized-moves-of-redirected-folders"></a>Optimierte Verschiebungen von umgeleiteten Ordnern aktivieren

>Gilt für: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server (halbjährlicher Kanal)

In diesem Thema wird beschrieben, wie ein optimiertes verschieben umgeleiteter Ordner (Ordner Umleitung) zu einer neuen Dateifreigabe durchgeführt wird. Wenn Sie diese Richtlinien Einstellung aktivieren und ein Administrator die Dateifreigabe, die umgeleitete Ordner gehostet, verschiebt und den Zielpfad der umgeleiteten Ordner in Gruppenrichtlinie aktualisiert, wird der zwischengespeicherte Inhalt einfach im lokalen Offlinedateien Cache ohne Verzögerungen umbenannt oder möglicher Datenverlust für den Benutzer.

Zuvor konnten Administratoren den Zielpfad der umgeleiteten Ordner in Gruppenrichtlinie ändern und den Client Computern die Dateien bei der nächsten Anmeldung des betroffenen Benutzers kopieren. Dies führt zu einer verzögerten Anmeldung. Alternativ dazu können Administratoren die Dateifreigabe verschieben und den Zielpfad der umgeleiteten Ordner in Gruppenrichtlinie aktualisieren. Alle Änderungen, die zwischen dem Start des Verschiebens und der ersten Synchronisierung nach dem Verschieben lokal auf den Client Computern vorgenommen wurden, gehen jedoch verloren.

## <a name="prerequisites"></a>Erforderliche Komponenten

Für das optimierte verschieben gelten die folgenden Anforderungen:

- Die Ordner Umleitung muss eingerichtet werden. Weitere Informationen finden Sie unter Bereitstellen der [Ordner Umleitung mit Offlinedateien](deploy-folder-redirection.md).
- Auf Client Computern muss Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server (halbjährlicher Kanal) ausgeführt werden.

## <a name="step-1-enable-optimized-move-in-group-policy"></a>Schritt 1: Optimierte Verschiebung in Gruppenrichtlinie aktivieren

Um die Verschiebung von Ordner Umleitungs Daten zu optimieren, verwenden Sie Gruppenrichtlinie, um die Richtlinien Einstellung **optimiertes Verschieben von Inhalten in Offlinedateien Cache auf Ordner Umleitung Serverpfad ändern** für das entsprechende Gruppenrichtlinie Objekt (GPO) zu aktivieren. Wenn Sie diese Richtlinien Einstellung auf **deaktiviert** oder **nicht konfiguriert** konfigurieren, kopiert der Client den gesamten Ordner Umleitungs Inhalt an den neuen Speicherort und löscht dann den Inhalt aus dem alten Speicherort, wenn sich der Serverpfad ändert.

So aktivieren Sie das optimierte verschieben umgeleiteter Ordner:

1. Klicken Sie in Gruppenrichtlinie Verwaltung mit der rechten Maustaste auf das GPO, das Sie für die Ordner Umleitungseinstellungen (z. b. **Ordner Umleitung und Roamingbenutzerprofile**) erstellt haben, und wählen Sie dann **Bearbeiten**
2. Navigieren Sie unter **Benutzerkonfiguration**zu **Richtlinien**, **Administrative Vorlagen**und anschließend **System**, und klicken Sie dann auf **Ordner Umleitung**.
3. Klicken Sie mit **der rechten Maustaste auf optimiertes Verschieben von Inhalten in Offlinedateien Cache auf Serverpfad Änderung für Ordner Umleitung aktivieren**, und wählen Sie dann **Bearbeiten**aus.
4. Wählen Sie **aktiviert**aus, und klicken Sie dann auf **OK**.

## <a name="step-2-relocate-the-file-share-for-redirected-folders"></a>Schritt 2: Verschieben der Dateifreigabe für umgeleitete Ordner

Beim Verschieben der Dateifreigabe, die umgeleitete Ordner der Benutzer enthält, wird der Import Vorgang durchführen, um sicherzustellen, dass die Ordner ordnungsgemäß verschoben werden.

>[!IMPORTANT]
>Wenn die Dateien der Benutzer verwendet werden oder der vollständige Dateistatus beim Verschieben nicht beibehalten wird, treten bei den Benutzern möglicherweise schlechte Leistung auf, wenn die Dateien über das Netzwerk kopiert werden, durch Offlinedateien generierte Synchronisierungs Konflikte oder sogar Datenverluste.

1. Benachrichtigen Sie die Benutzer im voraus, dass sich der Server, der die umgeleiteten Ordner hostet, ändert, und Sie sollten die folgenden Aktionen ausführen:

      - Synchronisieren Sie die Inhalte Ihrer Offlinedateien Cache, und lösen Sie Konflikte.
      - Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, geben Sie **gpupdate/Target: User/Force**ein, und melden Sie sich dann erneut an, um sicherzustellen, dass die neuesten Gruppenrichtlinie Einstellungen auf den Client Computer angewendet werden.

        >[!NOTE]
        >Standardmäßig werden Client Computer Gruppenrichtlinie alle 90 Minuten aktualisiert. Wenn Sie also ausreichend Zeit haben, damit Client Computer aktualisierte Richtlinien erhalten, müssen Sie die Benutzer nicht zur Verwendung von **gpupdate**auffordern.
2. Entfernen Sie die Dateifreigabe vom Server, um sicherzustellen, dass keine Dateien in der Dateifreigabe verwendet werden. Um dies in Server-Manager zu tun, klicken Sie auf der Seite Freigaben von Datei-und Speicherdienste mit der rechten Maustaste **auf die entsprechende** Dateifreigabe, und wählen Sie dann **Entfernen**aus.

    Benutzer arbeiten mit Offlinedateien offline, bis die Verschiebung beendet ist, und Sie erhalten die aktualisierten Ordner Umleitungseinstellungen von Gruppenrichtlinie.

3. Verschieben Sie den Inhalt der Dateifreigabe mithilfe eines Kontos mit Sicherungsrechten an den neuen Speicherort, indem Sie eine Methode verwenden, die Datei Zeitstempel beibehält, z. b. ein Sicherungs-und Wiederherstellungs Hilfsprogramm. Um den **Robocopy** -Befehl zu verwenden, öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und geben Sie ```<Source>``` dann den folgenden Befehl ein, wobei der aktuelle Speicherort der Dateifreigabe und ```<Destination>``` der neue Speicherort ist:

    ```PowerShell
    Robocopy /B <Source> <Destination> /Copyall /MIR /EFSRAW
    ```

    >[!NOTE]
    >Der **xcopy** -Befehl behält nicht den gesamten Datei Zustand bei.
4. Bearbeiten Sie die Einstellungen für die Ordner Umleitung, und aktualisieren Sie den Speicherort des Ziel Ordners für jeden umgeleiteten Ordner, den Sie verschieben möchten. Weitere Informationen finden Sie unterschritt 4: Bereitstellen der [Ordner Umleitung mit Offlinedateien](deploy-folder-redirection.md).
5. Benachrichtigen Sie die Benutzer, dass sich der Server, auf dem die umgeleiteten Ordner gehostet werden, geändert hat, und dass Sie den Befehl **gpupdate/Target: User/Force** verwenden sollten. Melden Sie sich ab, und melden Sie sich erneut an, um die aktualisierte Konfiguration zu erhalten und die ordnungsgemäße

    Benutzer sollten sich mindestens einmal bei allen Computern anmelden, um sicherzustellen, dass die Daten in jedem Offlinedateien Cache ordnungsgemäß verschoben werden.

## <a name="more-information"></a>Weitere Informationen

* [Bereitstellen der Ordner Umleitung mit Offlinedateien](deploy-folder-redirection.md)
* [Bereitstellen von Roamingbenutzerprofilen](deploy-roaming-user-profiles.md)
* [Übersicht über Ordner Umleitung, Offlinedateien und Roamingbenutzerprofile](folder-redirection-rup-overview.md)