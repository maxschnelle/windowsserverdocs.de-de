---
title: Aktivieren optimierter Verschiebungen umgeleiteter Ordner
description: Ausführen einer optimierten Verschiebung umgeleiteter Ordner auf eine neue Dateifreigabe.
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 895bf41a5a42bd4578e99ba12205b56da18b9ba2
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942190"
---
# <a name="enable-optimized-moves-of-redirected-folders"></a>Aktivieren optimierter Verschiebungen umgeleiteter Ordner

>Gilt für: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server (halbjährlicher Kanal)

In diesem Thema wird beschrieben, wie eine optimierte Verschiebung umgeleiteter Ordner (Ordnerumleitung) auf eine neue Dateifreigabe durchgeführt wird. Wenn Sie diese Richtlinieneinstellung aktivieren, wird, wenn ein Administrator die umgeleiteten Ordner des Dateifreigabehostings verschiebt und den Zielpfad der umgeleiteten Ordner in der Gruppenrichtlinie aktualisiert, der zwischengespeicherte Inhalt einfach im lokalen Offlinedateicache umbenannt, ohne dass es zu Verzögerungen oder potenziellen Datenverlusten für den Benutzer kommt.

Zuvor konnten Administratoren den Zielpfad der umgeleiteten Ordner in der Gruppenrichtlinie ändern und die Clientcomputer die Dateien beim nächsten Anmelden des betroffenen Benutzers kopieren lassen, was zu einer verzögerten Anmeldung führte. Alternativ dazu können Administratoren die Dateifreigabe verschieben und den Zielpfad der umgeleiteten Ordner in der Gruppenrichtlinie aktualisieren. Alle Änderungen, die zwischen dem Beginn der Verschiebung und der ersten Synchronisierung nach der Verschiebung lokal auf den Clientcomputern vorgenommen wurden, würden jedoch verloren gehen.

## <a name="prerequisites"></a>Voraussetzungen

Für das optimierte Verschieben gelten die folgenden Anforderungen:

- Ordnerumleitung muss eingerichtet sein. Weitere Informationen finden Sie unter [Bereitstellen von Ordnerumleitung mit Offlinedateien](deploy-folder-redirection.md).
- Clientcomputer müssen Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 oder Windows Server (halbjährlicher Kanal) ausführen.

## <a name="step-1-enable-optimized-move-in-group-policy"></a>Schritt 1: Aktivieren optimierter Verschiebung in der Gruppenrichtlinie

Um das Verschieben von Ordnerumleitungsdaten zu optimieren, verwenden Sie die Gruppenrichtlinie, um die Richtlinieneinstellung **Optimiertes Verschieben von Inhalt im Offlinedateicache bei Änderung des Serverpfads für die Ordnerumleitung aktivieren** für das entsprechende Gruppenrichtlinienobjekt (GPO) zu aktivieren. Wenn Sie diese Richtlinieneinstellung als **Deaktiviert** oder **Nicht konfiguriert** konfigurieren, wird der gesamte Inhalt der Ordnerumleitung vom Client an den neuen Speicherort kopiert. Anschließend wird der Inhalt aus dem alten Speicherort gelöscht, wenn sich der Serverpfad ändert.

So aktivieren Sie das optimierte Verschieben umgeleiteter Ordner:

1. Klicken Sie in der Gruppenrichtlinienverwaltung mit der rechten Maustaste auf das Gruppenrichtlinienobjekt, das Sie für Ordnerumleitungseinstellungen erstellt haben (z. B. **Ordnerumleitung und Roamingbenutzerprofil-Einstellungen**), und wählen Sie dann **Bearbeiten** aus.
2. Navigieren Sie unter **Benutzerkonfiguration** zu **Richtlinien**, **Administrative Vorlagen**, **System** und **Ordnerumleitung**.
3. Klicken Sie mit der rechten Maustaste auf **Optimiertes Verschieben von Inhalt im Offlinedateicache bei Änderung des Serverpfads für die Ordnerumleitung aktivieren**, und wählen Sie dann **Bearbeiten**aus.
4. Wählen Sie **Aktiviert** aus, und klicken Sie dann auf **OK**.

## <a name="step-2-relocate-the-file-share-for-redirected-folders"></a>Schritt 2: Verschieben der Dateifreigabe für umgeleitete Ordner

Wenn Sie die Dateifreigabe verschieben, die umgeleitete Ordner der Benutzer enthält, ist es wichtig, Vorkehrungen zu treffen, um sicherzustellen, dass die Ordner ordnungsgemäß verschoben werden.

>[!IMPORTANT]
>Wenn die Dateien der Benutzer aktuell verwendet werden oder der vollständige Dateistatus beim Verschieben nicht beibehalten wird, treten bei den Benutzern möglicherweise schlechte Leistung auf, wenn die Dateien über das Netzwerk kopiert werden, durch Offlinedateien generierte Synchronisierungskonflikte oder sogar Datenverluste.

1. Benachrichtigen Sie Benutzer im voraus, dass sich der Server, der die umgeleiteten Ordner hostet, ändert. Benutzer sollten die folgenden Aktionen ausführen:

      - Synchronisieren Sie die Inhalte ihres Caches für Offlinedateien, und lösen Sie etwaiger Konflikte auf.
      - Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, geben Sie **GpUpdate /Target:User/Force** ein, und melden Sie sich dann ab und erneut an, um sicherzustellen, dass die neusten Gruppenrichtlinieneinstellungen auf den Clientcomputer angewendet werden.

        >[!NOTE]
        >Standardmäßig aktualisieren Clientcomputer Gruppenrichtlinien alle 90 Minuten. Wenn Sie also ausreichend Zeit bereitstellen, damit Clientcomputer aktualisierte Richtlinien erhalten können, müssen Sie Benutzer nicht zur Verwendung von **GpUpdate** auffordern.
2. Entfernen Sie die Dateifreigabe vom Server, um sicherzustellen, dass keine Dateien in der Dateifreigabe aktuell verwendet werden. Klicken Sie dazu in Server-Manager auf der Seite **Freigaben** auf „Datei- und Speicherdienste“, klicken Sie mit der rechten Maustaste auf die entsprechende Dateifreigabe, und wählen Sie dann **Entfernen** aus.

    Benutzer arbeiten mit Offlinedateien offline, bis die Verschiebung abgeschlossen ist, und sie erhalten die aktualisierten Ordnerumleitungseinstellungen von der Gruppenrichtlinie.

3. Verschieben Sie den Inhalt der Dateifreigabe mithilfe eines Kontos mit Sicherungsrechten an den neuen Speicherort, indem Sie eine Methode verwenden, die Dateizeitstempel beibehält, z. B. mit einem Hilfsprogramm für Sicherung und Wiederherstellung. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, und geben Sie dann folgenden Befehl ein, um den Befehl **Robocopy** zu verwenden. Dabei ist ```<Source>``` der aktuelle Speicherort der Dateifreigabe und ```<Destination>``` der neue Speicherort:

    ```PowerShell
    Robocopy /B <Source> <Destination> /Copyall /MIR /EFSRAW
    ```

    >[!NOTE]
    >Der Befehl **Xcopy** behält nicht den gesamten Dateizustand bei.
4. Bearbeiten Sie die Richtlinieneinstellungen für die Ordnerumleitung, und aktualisieren Sie den Speicherort des Zielordners für jeden umgeleiteten Ordner, den Sie verschieben möchten. Weitere Informationen finden Sie in Schritt 4 von [Bereitstellen von Ordnerumleitung mit Offlinedateien](deploy-folder-redirection.md).
5. Benachrichtigen Sie Benutzer, dass sich der Server, auf dem die umgeleiteten Ordner gehostet werden, geändert hat, und dass Sie den Befehl **GpUpdate /Target: User /Force** verwenden sollten. Melden Sie sich ab und dann erneut an, um die aktualisierte Konfiguration zu erhalten und die ordnungsgemäße Dateisynchronisierung fortzusetzen.

    Benutzer sollten sich mindestens ein Mal bei allen Computern anmelden, um sicherzustellen, dass die Daten in jedem Offlinedateicache ordnungsgemäß verschoben werden.

## <a name="more-information"></a>Weitere Informationen

* [Bereitstellen von Ordnerumleitung mit Offlinedateien](deploy-folder-redirection.md)
* [Bereitstellen von Roamingbenutzerprofilen](deploy-roaming-user-profiles.md)
* [Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile – Übersicht](folder-redirection-rup-overview.md)