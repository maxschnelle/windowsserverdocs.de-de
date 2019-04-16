---
title: Optimierte wechselt der umgeleitete Ordner aktivieren
description: Wie Sie eine optimierte Wechsel umgeleitete Ordner in eine neue Dateifreigabe ausführen.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 98fd5d50645ad454204dcf9dabf58e97c246ab1a
ms.sourcegitcommit: 505505b7ec99506e7ff50eddbdd6aa94a602abe6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/11/2018
ms.locfileid: "3831380"
---
# Optimierte wechselt der umgeleitete Ordner aktivieren

>Gilt für: Windows 10, Windows 8, Windows 8.1, WindowsServer 2012, Windows Server 2012 R2, WindowsServer 2016

In diesem Thema wird beschrieben, wie eine optimierte Wechsel umgeleitete Ordner (Ordnerumleitung) in eine neue Dateifreigabe ausführen. Wenn Sie diese Einstellung, wenn ein Administrator verschiebt die Dateifreigabe umgeleitete Ordner hosten und den Zielpfad der umgeleitete Ordner in der Gruppenrichtlinie aktualisiert zu aktivieren, wird die zwischengespeicherte Inhalt einfach im lokalen Cache Offlinedateien ohne Verzögerungen umbenannt oder Datenverluste für den Benutzer.

Bisher konnte Administratoren ändern und den Zielpfad umgeleitete Ordner in Gruppenrichtlinien und mit denen die Clientcomputer die Dateien auf den betreffenden Benutzer nächsten Anmeldung, kopieren dadurch eine verzögerten anmelden. Alternativ könnten Administratoren verschieben die Dateifreigabe und den Zielpfad der umgeleitete Ordner in der Gruppenrichtlinie zu aktualisieren. Alle Änderungen lokal auf den Clientcomputern zwischen dem Start des wechseln und die erste Synchronisierung nach dem Verschieben wäre jedoch verloren.

## Voraussetzungen

Optimierte verschieben ist Folgendes erforderlich:

- Ordnerumleitung muss eingerichtet sein. Weitere Informationen finden Sie in der [Ordnerumleitung mit Offlinedateien bereitstellen](deploy-folder-redirection.md).
- Client-Computer müssen Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt.

## Schritt 1: Aktivieren optimiert verschieben in "Gruppenrichtlinie"

Um die Umsetzung der Ordnerumleitung Daten zu optimieren, verwenden Sie Gruppenrichtlinien zum **Aktivieren optimiert Verschieben von Inhalt im Cache für Ordnerumleitung Server Pfad Änderung Offlinedateien** Einstellung der Richtlinie für das entsprechende Gruppenrichtlinienobjekt (GPO) aktivieren. Konfigurieren diese Einstellung **deaktiviert** oder **Nicht konfiguriert** bewirkt, dass den Client alle Ordnerumleitung Inhalte an den neuen Speicherort kopieren und löschen Sie den Inhalt der alten Speicherort, wenn der Serverpfad ändert.

Hier sehen Sie zum Aktivieren der optimierten Verschieben von umgeleitete Ordner:

1. In der Gruppenrichtlinien-Verwaltungskonsole mit der rechten Maustaste im GPOs, die Sie für Ordnerumleitung-Einstellungen (z. B. **Ordnerumleitung und Roamingeinstellungen für Benutzer-Profile**) erstellt, und wählen Sie dann **Bearbeiten**.
2. Navigieren Sie unter **Benutzerkonfiguration**zu **Richtlinien**, dann **Administrative Vorlagen**, dann **System**, dann **Ordnerumleitung**.
3. Mit der rechten Maustaste **Aktivieren Verschieben von Inhalt im Cache für Ordnerumleitung Server Pfad Änderung Offlinedateien optimiert**, und wählen Sie dann **Bearbeiten**.
4. Wählen Sie **aktiviert**, und wählen Sie dann auf **OK**.

## Schritt 2: Verschieben Sie die Dateifreigabe für umgeleitete Ordner

Beim Verschieben der Dateifreigabe, die Benutzer enthält Ordner umgeleitet, ist es importieren, Vorsichtsmaßnahmen, um sicherzustellen, dass die Ordner ordnungsgemäß verschoben werden.

>[!IMPORTANT]
>Wenn der Benutzer Dateien sind verwenden oder wenn die kompletten Zustand nicht beim Wechsel beibehalten wird, Benutzer können auftreten, eine schlechte Leistung als über das Netzwerk, Synchronisierungskonflikte durch Offlinedateien oder sogar Datenverlust generiert die Dateien kopiert werden.

1. Benachrichtigen Sie Benutzer im voraus, dass der Hostserver für deren umgeleitete Ordner ändert und wird empfohlen, dass sie die folgenden Aktionen ausführen:

      - Synchronisieren des Inhalts des Cache Offlinedateien und Konflikte.
      - Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, geben Sie **GpUpdate/target: User/Force**, und klicken Sie dann melden Sie ab und wieder melden Sie an, um sicherzustellen, dass die neuesten gruppenrichtlinieneinstellungen auf dem Clientcomputer angewendet werden

        >[!NOTE]
        >Standardmäßig Aktualisieren von Clientcomputern Gruppenrichtlinie alle 90 Minuten, wenn Sie genügend Zeit für Client Computer zum Empfangen von aktualisierte Richtlinie ermöglichen, müssen Sie nicht Benutzer dazu auffordern, **GpUpdate**verwenden.
2. Entfernen Sie die Dateifreigabe aus der Server, um sicherzustellen, dass keine Dateien in der Dateifreigabe verwendet werden. Hierzu im Server-Manager auf der Seite **Freigaben** von Datei- und Speicherdienste mit der rechten Maustaste in der entsprechenden Dateifreigabe, und wählen Sie dann **Entfernen**.

    Offlinedateien offline zu verwenden, bis der Wechsel abgeschlossen ist, und sie die aktualisierten Ordnerumleitung Einstellungen von den Gruppenrichtlinien erhalten funktioniert Benutzer.

3. Mit einem Konto mit Rechte zum Sichern, den Inhalt der Dateifreigabe an eine Methode, die Zeitstempel für Dateien, z. B. eine Sicherung behält mit neuen Speicherort verschieben und Hilfsprogramm wiederherstellen. Den **Robocopy** -Befehl, öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten, und geben Sie folgenden Befehl ein, wobei ```<Source>``` ist die aktuelle Position der Dateifreigabe, und ```<Destination>``` ist der neue Speicherort:

    ```PowerShell
    Robocopy /B <Source> <Destination> /Copyall /MIR /EFSRAW
    ```

    >[!NOTE]
    >Der Befehl **Xcopy** wird nicht alle über den Dateistatus beibehalten.
4. Bearbeiten Sie die Richtlinieneinstellungen Ordnerumleitung, aktualisieren das Zielverzeichnis für jeden umgeleitete Ordner, die Sie verschieben möchten. Weitere Informationen finden Sie unter Schritt 4 des [Ordnerumleitung mit Offlinedateien bereitstellen](deploy-folder-redirection.md).
5. Benutzer zu benachrichtigen, dass der Hostserver für deren umgeleitete Ordner geändert hat, und sie den Befehl **GpUpdate/target: User/Force** verwenden soll, und klicken Sie dann abmelden und sich erneut anmelden, erhalten die aktualisierte Konfiguration und richtigen dateisynchronisierung fortsetzen.

    Benutzer sollten für alle Computer mindestens einmal anmelden um sicherzustellen, dass die Daten im Cache für jeden Offlinedateien ordnungsgemäß verschoben ruft.

## Weitere Informationen

* [Bereitstellen von Ordnerumleitung, Offlinedateien](deploy-folder-redirection.md)
* [Bereitstellen von Roamingbenutzerprofilen](deploy-roaming-user-profiles.md)
* [Übersicht über die Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile](folder-redirection-rup-overview.md)