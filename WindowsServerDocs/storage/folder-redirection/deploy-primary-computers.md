---
title: Bereitstellen von primären Computern für Ordnerumleitung und Roamingbenutzerprofile
description: Aktivieren der Unterstützung primärer Computer und Festlegen primärer Computer für Benutzer mit Ordnerumleitung und Roamingbenutzerprofilen.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: 935d3ccf7de777a71d7c75179629b448dbb73a08
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966282"
---
# <a name="deploy-primary-computers-for-folder-redirection-and-roaming-user-profiles"></a>Bereitstellen von primären Computern für Ordnerumleitung und Roamingbenutzerprofile

>Gilt für: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2

In diesem Thema wird beschrieben, wie die Unterstützung primärer Computer aktiviert wird und wie primäre Computer für Benutzer festgelegt werden. Auf diese Weise können Sie steuern, auf welchen Computern Ordnerumleitung und Roamingbenutzerprofile verwendet werden.

> [!IMPORTANT]
> Wenn Sie Unterstützung primärer Computer für Roamingbenutzerprofile aktivieren, aktivieren Sie immer auch Unterstützung primärer Computer für Ordnerumleitung. Dadurch werden Dokumente und andere Benutzerdateien aus den Benutzerprofilen herausgehalten, sodass Profile klein und Anmeldezeiten schnell bleiben.

## <a name="prerequisites"></a>Voraussetzungen

## <a name="software-requirements"></a>Softwareanforderungen

Für die Unterstützung primärer Computer gelten die folgenden Anforderungen:

- Das AD DS-Schema (Active Directory Domain Services) muss so aktualisiert werden, dass es Schemaerweiterungen für Windows Server 2012 enthält (beim Installieren eines Windows Server 2012-Domänencontrollers wird das Schema automatisch aktualisiert). Weitere Informationen zum Aktualisieren des AD DS-Schemas finden Sie in den Themen zu [Adprep.exe-Integration](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh472161(v=ws.11)#adprepexe-integration>) und [Ausführen von „Adprep.exe“](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd464018(v=ws.10)>).
- Clientcomputer müssen Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausführen.

> [!TIP]
> Obwohl für die Unterstützung primärer Computer Ordnerumleitung und/oder Roamingbenutzerprofile erforderlich sind, ist es bei der erstmaligen Bereitstellung dieser Technologien am besten, die Unterstützung primärer Computer einzurichten, bevor Sie die Gruppenrichtlinienobjekte aktivieren, die Ordnerumleitung und Roamingbenutzerprofile konfigurieren. Dadurch wird verhindert, dass Benutzerdaten auf nicht primäre Computer kopiert werden, bevor die Unterstützung primärer Computer aktiviert ist. Konfigurationsinformationen finden Sie unter [Bereitstellen von Ordnerumleitung](deploy-folder-redirection.md) und [Bereitstellen von Roamingbenutzerprofilen](deploy-roaming-user-profiles.md).

## <a name="step-1-designate-primary-computers-for-users"></a>Schritt 1: Legen Sie die primären Computer für die Benutzer fest

Der erste Schritt beim Bereitstellen von Unterstützung für primäre Computern besteht darin, die primären Computer für jeden Benutzer festzulegen. Verwenden Sie hierzu das Active Directory-Verwaltungscenter, um den DN (Distinguished Name) der relevanten Computer abzurufen, und legen Sie dann das **msDs-PrimaryComputer**-Attribut fest.

> [!TIP]
> Weitere Informationen zur Verwendung von Windows PowerShell zum Arbeiten mit primären Computern finden Sie im Blogbeitrag [Digging a little deeper into Windows 8 Primary Computer](<https://blogs.technet.microsoft.com/askds/2012/10/23/digging-a-little-deeper-into-windows-8-primary-computer/>) (Tiefere Einblicke in primäre Windows 8-Computer).

Im Folgenden wird erläutert, wie Sie die primären Computer für Benutzer angeben:

1. Öffnen Sie den Server-Manager auf einem Computer, auf dem Active Directory-Verwaltungstools installiert sind.
2. Wählen Sie im Menü **Extras** die Option für das **Active Directory-Verwaltungscenter** aus. Das Active Directory-Verwaltungscenter wird angezeigt.
3. Navigieren Sie in der entsprechenden Domäne zum Container **Computer**.
4. Klicken Sie mit der rechten Maustaste auf einen Computer, den Sie als primären Computer festlegen möchten, und wählen Sie dann **Eigenschaften** aus.
5. Wählen Sie im Navigationsbereich die Option **Erweiterungen** aus.
6. Wählen Sie die Registerkarte **Attribut-Editor** aus, scrollen Sie zu **distinguishedName**, wählen Sie **Anzeigen** aus, klicken Sie mit der rechten Maustaste auf den aufgelisteten Wert, wählen Sie **Kopieren** aus, wählen Sie **OK** aus, und wählen Sie dann **Abbrechen** aus.
7. Navigieren Sie zum Container **Benutzer** in der entsprechenden Domäne, klicken Sie mit der rechten Maustaste auf den Benutzer, dem Sie den Computer zuweisen möchten, und klicken Sie dann auf **Eigenschaften**.
8. Wählen Sie im Navigationsbereich die Option **Erweiterungen** aus.
9. Wählen Sie die Registerkarte **Attribut-Editor** aus, wählen Sie **msDs-PrimaryComputer** aus, und wählen Sie dann **Bearbeiten** aus. Das Dialogfeld %%amp;quot;Editor für mehrwertige Zeichenfolgen%%amp;quot; wird angezeigt.
10. Klicken Sie mit der rechten Maustaste auf das Textfeld, wählen Sie **Einfügen** aus, klicken Sie auf **Hinzufügen**, wählen Sie **OK** aus, und wählen Sie **OK** dann erneut aus.

## <a name="step-2-optionally-enable-primary-computers-for-folder-redirection-in-group-policy"></a>Schritt 2: Aktivieren Sie optional primäre Computer für Ordnerumleitung in der Gruppenrichtlinie

Im nächsten Schritt konfigurieren Sie optional eine Gruppenrichtlinie, um Unterstützung primärer Computer für Ordnerumleitung zu aktivieren. Auf diese Weise können die Ordner eines Benutzers auf Computern umgeleitet werden, die als primäre Computer des Benutzers festgelegt sind, jedoch nicht auf anderen Computern. Sie können primäre Computer für Ordnerumleitung pro Computer oder pro Benutzer steuern.

So aktivieren Sie Unterstützung primärer Computer für Ordnerumleitung:

1. Klicken Sie in der Gruppenrichtlinienverwaltung mit der rechten Maustaste auf das Gruppenrichtlinienobjekt, das Sie bei der anfänglichen Konfiguration der Ordnerumleitung und/oder der Roamingbenutzerprofile erstellt haben (z. B. **Ordnerumleitungseinstellungen** oder **Roamingbenutzerprofil-Einstellungen**), und wählen Sie dann **Bearbeiten** aus.
2. Um Unterstützung primärer Computer mithilfe einer computerbasierten Gruppenrichtlinie zu aktivieren, navigieren Sie zu **Computerkonfiguration**. Navigieren Sie für eine benutzerbasierte Gruppenrichtlinie zu **Benutzerkonfiguration**.
    - Die computerbasierte Gruppenrichtlinie wendet die Verarbeitung des primären Computers auf alle Computer an, für die das Gruppenrichtlinienobjekt gilt. Dies wirkt sich auf alle Benutzer des Computers aus.
    - Die benutzerbasierte Gruppenrichtlinie wendet die Verarbeitung des primären Computers auf alle Benutzerkonten an, für die das Gruppenrichtlinienobjekt gilt. Dies wirkt sich auf alle Computer aus, bei denen sich der Benutzer anmeldet.
3. Navigieren Sie unter **Computerkonfiguration** oder **Benutzerkonfiguration** zu **Richtlinien**, **Administrative Vorlagen**, **System** und **Ordnerumleitung**.
4. Klicken Sie mit der rechten Maustaste auf **Ordner nur auf primären Computern umleiten**, und wählen Sie dann **Bearbeiten** aus.
5. Wählen Sie **Aktiviert** aus, und klicken Sie dann auf **OK**.

## <a name="step-3-optionally-enable-primary-computers-for-roaming-user-profiles-in-group-policy"></a>Schritt 3: Aktivieren Sie optional primäre Computer für Roamingbenutzerprofile in der Gruppenrichtlinie

Im nächsten Schritt konfigurieren Sie optional eine Gruppenrichtlinie, um Unterstützung primärer Computer für Roamingbenutzerprofile zu aktivieren. Auf diese Weise kann Roaming des Profils eines Benutzers auf Computer stattfinden, die als primäre Computer des Benutzers festgelegt sind, jedoch nicht auf andere Computer.

So aktivieren Sie primäre Computer für Roamingbenutzerprofile:

1. Aktivieren Sie Unterstützung primärer Computer für Ordnerumleitung, wenn dies noch nicht geschehen ist.<br>Dadurch werden Dokumente und andere Benutzerdateien aus den Benutzerprofilen herausgehalten, sodass Profile klein und Anmeldezeiten schnell bleiben.
2. Klicken Sie in der Gruppenrichtlinienverwaltung mit der rechten Maustaste auf das Gruppenrichtlinienobjekt, das Sie erstellt haben (z. B. **Ordnerumleitung und Roamingbenutzerprofil-Einstellungen**), und wählen Sie dann **Bearbeiten** aus.
3. Navigieren Sie zu **Computerkonfiguration**, **Richtlinien**, **Administrative Vorlagen**, **System** und dann zu **Benutzerprofile**.
4. Klicken Sie mit der rechten Maustaste auf **Roamingprofile nur auf primäre Computer herunterladen**, und wählen Sie dann **Bearbeiten** aus.
5. Wählen Sie **Aktiviert** aus, und klicken Sie dann auf **OK**.

## <a name="step-4-enable-the-gpo"></a>Schritt 4: Aktivieren Sie das Gruppenrichtlinienobjekt

Nachdem Sie die Konfiguration von Ordnerumleitung und Roamingbenutzerprofilen abgeschlossen haben, aktivieren Sie das Gruppenrichtlinienobjekt, falls dies noch nicht geschehen ist. Auf diese Weise kann es auf betroffene Benutzer und Computer angewendet werden.

So aktivieren Sie die Gruppenrichtlinienobjekte für Ordnerumleitung und/oder Roamingbenutzerprofile:

1. Öffnen Sie die Gruppenrichtlinienverwaltung.
2. Klicken Sie mit der rechten Maustaste auf die Gruppenrichtlinienobjekte, die Sie erstellt haben, und wählen Sie dann **Verknüpfung aktiviert** aus. Neben dem Menüelement sollte ein Kontrollkästchen angezeigt werden.

## <a name="step-5-test-primary-computer-function"></a>Schritt 5: Testen Sie die Funktion der primären Computer

Um die Unterstützung primärer Computer zu testen, melden Sie sich bei einem primären Computer an, bestätigen Sie, dass die Ordner und Profile umgeleitet werden, melden Sie sich dann an einem nicht-primären Computer an, und bestätigen Sie, dass die Ordner und Profile nicht umgeleitet werden.

So testen Sie die Funktionalität des primären Computers:

1. Melden Sie sich bei einem vorgesehenen primären Computer mit einem Benutzerkonto an, für das Sie Ordnerumleitung und/oder Roamingbenutzerprofile aktiviert haben.
2. Wenn sich das Benutzerkonto bereits beim Computer angemeldet hat, öffnen Sie eine Windows PowerShell-Sitzung oder ein Eingabeaufforderungsfenster als Administrator, geben Sie den folgenden Befehl ein, und melden Sie sich dann ab, wenn Sie dazu aufgefordert werden, um sicherzustellen, dass die neuesten Gruppenrichtlinieneinstellungen auf den Clientcomputer angewendet werden:

    ```PowerShell
    Gpupdate /force
    ```

3. Öffnen Sie den Datei-Explorer.
1. Klicken Sie mit der rechten Maustaste auf einen umgeleiteten Ordner (z. B. auf den Ordner „Eigene Dokumente“ in der Dokumentbibliothek), und wählen Sie dann **Eigenschaften** aus.
1. Wählen Sie die Registerkarte **Speicherort** aus, und vergewissern Sie sich, dass der Pfad die von Ihnen angegebene Dateifreigabe anstelle eines lokalen Pfads anzeigt. Um zu überprüfen, dass das Benutzerprofil gewechselt wird, öffnen Sie die **Systemsteuerung**, wählen Sie **System und Sicherheit**, **System**, **Erweiterte Systemeinstellungen** aus, wählen Sie dann im Abschnitt „Benutzerprofile“ die Option **Einstellungen** aus, und suchen Sie in der Spalte **Typ** nach **Roaming**.
1. Melden Sie sich mit demselben Benutzerkonto bei einem Computer an, der nicht als primärer Computer des Benutzers festgelegt ist.
1. Wiederholen Sie die Schritte 2 bis 5, und suchen Sie stattdessen nach lokalen Pfaden und einem Profiltyp **Lokal**.

> [!NOTE]
> Wenn Ordner auf einem Computer umgeleitet wurden, bevor Sie Unterstützung primärer Computer aktiviert haben, bleiben die Ordner umgeleitet, es sei denn, die folgende Einstellung wird in der Ordnerumleitungs-Richtlinieneinstellung jedes Ordners konfiguriert: **Ordner nach Entfernen der Richtlinie zurück an den Speicherort des lokalen Benutzerprofils umleiten**. Auf ähnliche Weise zeigen Profile, die zuvor auf einem bestimmten Computer als Roaming gekennzeichnet waren, in den Spalten **Typ** die Angabe **Roaming** an. In der Spalte **Status** wird jedoch **Lokal** angezeigt.

## <a name="more-information"></a>Weitere Informationen

- [Bereitstellen von Ordnerumleitung mit Offlinedateien](deploy-folder-redirection.md)
- [Bereitstellen von Roamingbenutzerprofilen](deploy-roaming-user-profiles.md)
- [Ordnerumleitung, Offlinedateien und Roamingbenutzerprofile – Übersicht](folder-redirection-rup-overview.md)
- [Digging a little deeper into Windows 8 Primary Computer (Tiefere Einblicke in primäre Windows 8-Computer)](/archive/blogs/askds/digging-a-little-deeper-into-windows-8-primary-computer)
