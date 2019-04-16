---
title: Bereitstellen von primären Computer für die Ordnerumleitung und Roamingbenutzerprofile
description: Wie Sie Unterstützung für primäre Computer aktivieren und primären Computer für Benutzer mit der Ordnerumleitung und Roamingbenutzerprofile festlegen.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7b3c87597e07102d00fc068b7ecd5744e4ba366f
ms.sourcegitcommit: 505505b7ec99506e7ff50eddbdd6aa94a602abe6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/11/2018
ms.locfileid: "3831400"
---
# Bereitstellen von primären Computer für die Ordnerumleitung und Roamingbenutzerprofile

>Gilt für: Windows 10, Windows 8, Windows 8.1, WindowsServer 2012, Windows Server 2012 R2, WindowsServer 2016

Dieses Thema beschreibt, wie Sie Unterstützung für primäre Computer aktivieren und Festlegen der primären Computer für Benutzer. Auf diese Weise können Sie steuern, welche Computer Ordnerumleitung und Roamingbenutzerprofile verwenden.

>[!IMPORTANT]
>Wenn Sie Unterstützung für Roamingbenutzerprofile primären Computer zu aktivieren, aktivieren Sie immer Hauptcomputer-Unterstützung für Ordnerumleitung sowie. Hierdurch bleibt Dokumente und andere Benutzerdateien außerhalb der Benutzerprofile, wodurch Profile klein bleiben, und melden Sie sich wie oft fast bleiben.

## Voraussetzungen

## Softwareanforderungen

Unterstützung für primäre Computer ist Folgendes erforderlich:

- Das Active Directory Domain Services (AD DS)-Schema aktualisiert werden muss, um Windows Server 2012 Schema Ergänzungen enthalten (Installieren von einem Windows Server 2012-Domänencontroller automatisch Aktualisierung des Schemas). Informationen zum Aktualisieren der AD DS-Schema finden Sie unter [Adprep.exe Integration](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh472161(v=ws.11)#adprepexe-integration>) und [Adprep.exe ausgeführt](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd464018(v=ws.10)>).
- Client-Computer müssen Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt.

>[!TIP]
>Obwohl Hauptcomputer Unterstützung Ordnerumleitung bzw. Roamingbenutzerprofile, erfordert, wenn Sie diese Technologien zum ersten Mal bereitstellen, es empfiehlt sich, richten Sie Unterstützung für primäre Computer vor der Aktivierung die Gruppenrichtlinienobjekte, die Ordnerumleitung konfigurieren und Roamingbenutzerprofilen. Dadurch wird verhindert, dass Benutzerdaten zum nicht primären Computer kopiert werden, bevor die Unterstützung für primäre Computer aktiviert ist. Informationen zur Konfiguration finden Sie unter [Bereitstellen Ordnerumleitung](deploy-folder-redirection.md) und [Roamingbenutzerprofile bereitstellen](deploy-roaming-user-profiles.md).

## Schritt 1: Festlegen Sie primären Computer für Benutzer

Der erste Schritt bei der Bereitstellung von primären Computer-Unterstützung ist primären Computer für jeden Benutzer festlegen. Zu diesem Zweck verwenden Sie Active Directory-Verwaltungscenter, um den definierten Namen des betroffenen Computer zu erhalten, und legen Sie dann das **MsDs-PrimaryComputer** -Attribut.

>[!TIP]
>Zur Verwendung von Windows PowerShell mit primären Computern finden Sie im Blogbeitrag [etwas tiefere Einblicke in Windows 8 primären Computer](<https://blogs.technet.microsoft.com/askds/2012/10/23/digging-a-little-deeper-into-windows-8-primary-computer/>).

Hier ist die primäre Computer für Benutzer angeben von:

1. Öffnen Sie den Server-Manager auf einem Computer, auf dem Active Directory-Verwaltungstools installiert sind.
2. Wählen Sie auf das Menü " **Extras** " **Active Directory-Verwaltungscenter**. Das Active Directory-Verwaltungscenter wird angezeigt.
3. Navigieren Sie zu den Container **Computer** in der entsprechenden Domäne.
4. Klicken Sie auf einem Computer, den Sie festlegen möchten als primären Computer und wählen Sie dann **Eigenschaften**.
5. Wählen Sie im Navigationsbereich **Erweiterungen**.
6. Wählen Sie die Registerkarte **Attribut-Editor** , einen Bildlauf zum **DistinguishedName**, **Ansicht**auswählen, mit der rechten Maustaste des Wert aufgeführt, wählen Sie **Kopieren**, klicken Sie auf **OK**, und wählen Sie dann **Abbrechen**.
7. Navigieren Sie zu der Container " **Benutzer** " in der entsprechenden Domäne rechten Maustaste auf den Benutzer, den Sie den Computer zuweisen möchten, und wählen Sie dann **Eigenschaften**.
8. Wählen Sie im Navigationsbereich **Erweiterungen**.
9. Wählen Sie die Registerkarte **Attribut-Editor** , wählen Sie **MsDs-PrimaryComputer** , und wählen Sie dann **Bearbeiten**. Das Dialogfeld "Editor für mehrwertige Zeichenfolgen" wird angezeigt.
10. Mit der rechten Maustaste in des Textfeld ein, wählen Sie **Einfügen**, wählen Sie **Hinzufügen**, klicken Sie auf **OK**, und wählen Sie dann erneut auf **OK** .

## Schritt 2: Aktivieren Sie primären Computer optional für Ordnerumleitung in der Gruppenrichtlinie

Der nächste Schritt ist optional Gruppenrichtlinien zum Aktivieren der Unterstützung für Ordnerumleitung primären Computer konfigurieren. Dies ermöglicht Ordner eines Benutzers auf Computern, die als primäre Computer des Benutzers, aber nicht auf anderen Computern umgeleitet werden. Sie können primäre Computern für Ordnerumleitung auf einer pro-Computer-Basis oder einzelne Benutzer steuern.

Hier ist primären Computer Aktivieren von für Ordnerumleitung:

1. In der Gruppenrichtlinien-Verwaltungskonsole mit der Maustaste des Gruppenrichtlinienobjekts, das Sie erstellt haben, bei der erstmaligen Konfiguration von Ordnerumleitung bzw. Roamingbenutzerprofile (z. B. **Ordner Umleitung Einstellungen** oder **Roamingeinstellungen für Benutzer-Profile**), und klicken Sie dann Wählen Sie **Bearbeiten**.
2. Navigieren Sie zu **Computerkonfiguration**, um primäre Computer Unterstützung mithilfe von Gruppenrichtlinien computerbasierte. Benutzerbasierte Group Policy wechseln Sie zu **Benutzerkonfiguration**.
    - Gruppenrichtlinien computerbasierte gelten Hauptcomputer Verarbeitung auf allen Computern, die mit denen das Gruppenrichtlinienobjekt wendet Auswirkung auf alle Benutzer des Computers.
    - Benutzer-basierte Gruppenrichtlinien für Hauptcomputer Verarbeitung für alle Benutzerkonten, die mit dem das Gruppenrichtlinienobjekt wendet Auswirkung auf allen Computern, die Benutzer sich anmelden, gilt.
3. Navigieren Sie unter **Computerkonfiguration** oder **Benutzerkonfiguration**zu **Richtlinien**, dann **Administrative Vorlagen**, dann **System**, dann **Ordnerumleitung**.
4. Mit der rechten Maustaste **Ordner auf dem primären Computer nur umgeleitet**, und wählen Sie dann **Bearbeiten**.
5. Wählen Sie **aktiviert**, und wählen Sie dann auf **OK**.

## Schritt 3: Aktivieren Sie primären Computer optional für Roamingbenutzerprofile in "Gruppenrichtlinie"

Der nächste Schritt ist optional Gruppenrichtlinien zum Aktivieren der Unterstützung für Roamingbenutzerprofile primären Computer konfigurieren. Dies ermöglicht eine Benutzerprofil auf Computern, die als primäre Computer des Benutzers, aber nicht auf anderen Computern als Roamingdaten verwenden möchten.

Hier ist primären Computer für Roamingbenutzerprofile aktivieren:

1. Aktivieren Sie primäre Computer-Unterstützung für Ordnerumleitung, wenn Sie nicht bereits geschehen.
    * Hierdurch bleibt Dokumente und andere Benutzerdateien außerhalb der Benutzerprofile, wodurch Profile klein bleiben, und melden Sie sich wie oft fast bleiben.
2. Klicken Sie in der Gruppenrichtlinien-Verwaltungskonsole mit der rechten Maustaste im GPOs, das Sie (z. B. **Ordnerumleitung und Roamingeinstellungen für Benutzer-Profile**) erstellt haben, und wählen Sie dann **Bearbeiten**.
3. Navigieren Sie zu **Computerkonfiguration**, **Richtlinien**, und klicken Sie dann **Administrative Vorlagen**, und klicken Sie dann **System**und dann **Benutzerprofile**.
4. Mit der rechten Maustaste **servergespeicherte Profilen auf primären Computern nur herunterladen** , und wählen Sie dann **Bearbeiten**.
5. Wählen Sie **aktiviert**, und wählen Sie dann auf **OK**.

## Schritt 4: Aktivieren Sie das Gruppenrichtlinienobjekt

Nachdem Sie die Konfiguration von Ordnerumleitung und Roamingbenutzerprofile abgeschlossen haben, aktivieren Sie das Gruppenrichtlinienobjekt, wenn Sie noch nicht getan haben. Dies ermöglicht es auf betroffene-Benutzer und-Computer angewendet werden.

Hier ist der Ordnerumleitung bzw. die Gruppenrichtlinienobjekte für einen Benutzer Profile Roaming zu aktivieren:

1. Öffnen die Gruppenrichtlinien-Verwaltungskonsole
2. Mit der rechten Maustaste die Gruppenrichtlinienobjekte, die Sie erstellt haben, und wählen Sie dann **Link aktiviert**. Ein Kontrollkästchen sollte neben dem Menüelement angezeigt werden.

## Schritt 5: Testen der primären Computer-Funktion

Um Unterstützung für primäre Computer zu testen, melden Sie sich mit einem primären Computer, stellen Sie sicher, dass die Ordner und Profile umgeleitet wurden, melden Sie sich auf einem Computer nicht primären und stellen Sie sicher, dass die Ordner und Profile nicht umgeleitet werden.

Hier ist primären Computer Funktionen zu testen:

1. Melden Sie sich bei einem bestimmten primären Computer mit einem Benutzerkonto für den Ordnerumleitung bzw. Roamingbenutzerprofile aktiviert haben.
2. Wenn das Benutzerkonto auf dem Computer bereits angemeldet hat, öffnen Sie eine Windows PowerShell-Sitzung oder Eingabeaufforderungsfenster als Administrator, geben Sie den folgenden Befehl und melden Sie sich dann deaktivieren, wenn Sie aufgefordert werden, um sicherzustellen, dass die neuesten gruppenrichtlinieneinstellungen für gelten die Clientcomputer:
    ```PowerShell
    Gpupdate /force
    ```
3. Öffnen Sie die Datei-Explorer.
4. Mit der rechten Maustaste eines umgeleiteten Ordners (z. B. den Ordner "Eigene Dokumente" in der Bibliothek Dokumente), und wählen Sie dann **Eigenschaften**.
5. Wählen Sie die Registerkarte " **Speicherort** ", und stellen Sie sicher, dass der Pfad die Dateifreigabe anzeigt, die Sie anstelle von einem lokalen Pfad angegeben. Um zu bestätigen, dass das Benutzerprofil roaming, öffnen Sie **Systemsteuerung**, wählen Sie **System und Sicherheit**, wählen Sie **System**, **Erweiterte Systemeinstellungen**wählen Sie aus, wählen Sie die **Einstellungen** im Abschnitt Benutzerprofile und suchen Sie nach ** Roaming** in der Spalte **Typ** .
6. Melden Sie sich mit demselben Benutzerkonto auf einem Computer, der nicht als primäre Computer des Benutzers festgelegt ist.
7. Wiederholen Sie die Schritte 2 bis 5, lokale Pfade und einen **lokalen** Profiltyp stattdessen suchen.

>[!NOTE]
>Wenn der Ordner auf einem Computer umgeleitet wurden, bevor Sie Unterstützung für primäre Computer aktiviert, die Ordner bleibt umgeleitete es sei denn, die folgende Einstellung in jeden Ordner Ordner Umleitung Einstellung konfiguriert ist: **der Ordner zurück, der lokalen umleiten Ort des Benutzerprofils nach dem Entfernen der Richtlinie**. Profile, die zuvor auf einem bestimmten Computer roaming wurden werden auf ähnliche Weise **Roaming** in den **Typ** Spalten angezeigt; Allerdings wird **die Statusspalte** **lokalen**angezeigt.

## Weitere Informationen

- [Bereitstellen von Ordnerumleitung, Offlinedateien](deploy-folder-redirection.md)
- [Bereitstellen von Roamingbenutzerprofilen](deploy-roaming-user-profiles.md)
- [Übersicht über die Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile](folder-redirection-rup-overview.md)
- [Tiefere Einblicke etwas in Windows 8 primären Computer](https://blogs.technet.com/b/askds/archive/2012/10/23/digging-a-little-deeper-into-windows-8-primary-computer.aspx)