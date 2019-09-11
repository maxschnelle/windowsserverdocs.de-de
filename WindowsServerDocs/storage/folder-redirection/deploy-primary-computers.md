---
title: Primäre Computer für Ordner Umleitung und Roamingbenutzerprofile bereitstellen
description: Aktivieren der Unterstützung primärer Computer und festlegen primärer Computer für Benutzer mit Ordner Umleitung und Roamingbenutzerprofilen.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: fe026b97f15b4094303c8162c5363cc6205dedd1
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867280"
---
# <a name="deploy-primary-computers-for-folder-redirection-and-roaming-user-profiles"></a>Primäre Computer für Ordner Umleitung und Roamingbenutzerprofile bereitstellen

>Gilt für: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2

In diesem Thema wird beschrieben, wie die Unterstützung primärer Computer aktiviert und primäre Computer für Benutzer festgelegt werden. Auf diese Weise können Sie steuern, auf welchen Computern die Ordner Umleitung und Roamingbenutzerprofile verwendet werden.

> [!IMPORTANT]
> Wenn Sie die Unterstützung primärer Computer für Roamingbenutzerprofile aktivieren, aktivieren Sie die Unterstützung primärer Computer für die Ordner Umleitung Dadurch werden Dokumente und andere Benutzer Dateien aus den Benutzerprofilen heraus gehalten, sodass profile klein bleiben und die Anmeldezeiten schnell bleiben.

## <a name="prerequisites"></a>Erforderliche Komponenten

## <a name="software-requirements"></a>Softwareanforderungen

Für die Unterstützung primärer Computer gelten die folgenden Anforderungen:

- Das Active Directory Domain Services Schema (AD DS) muss aktualisiert werden, um Windows Server 2012-Schema Ergänzungen einschließen zu können (durch die Installation eines Windows Server 2012-Domänen Controllers wird das Schema automatisch aktualisiert). Weitere Informationen zum Aktualisieren des AD DS Schemas finden Sie unter [Integration von Adprep. exe](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh472161(v=ws.11)#adprepexe-integration>) und [Ausführen von Adprep. exe](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd464018(v=ws.10)>).
- Auf Client Computern muss Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt werden.

> [!TIP]
> Obwohl die Unterstützung für primäre Computer die Ordner Umleitung und/oder Roamingbenutzerprofile erfordert, ist es am besten, wenn Sie diese Technologien zum ersten Mal bereitstellen, die Unterstützung primärer Computer einzurichten, bevor die Gruppenrichtlinien Objekte zum Konfigurieren der Ordner Umleitung aktiviert werden. Roamingbenutzerprofile Dadurch wird verhindert, dass Benutzerdaten auf nicht primäre Computer kopiert werden, bevor die Unterstützung primärer Computer aktiviert ist. Informationen zur Konfiguration finden Sie unter Bereitstellen der [Ordner Umleitung](deploy-folder-redirection.md) und Bereitstellen von Server gespeicherten [Benutzerprofilen](deploy-roaming-user-profiles.md).

## <a name="step-1-designate-primary-computers-for-users"></a>Schritt 1: Legen Sie die primären Computer für die Benutzer fest

Der erste Schritt beim Bereitstellen der Unterstützung von primären Computern besteht darin, die primären Computer für jeden Benutzer festzulegen. Verwenden Sie hierzu Active Directory Verwaltungs Center, um den Distinguished Name der relevanten Computer abzurufen, und legen Sie dann das Attribut **msDS-primarycomputer** fest.

> [!TIP]
> Weitere Informationen zur Verwendung von Windows PowerShell für die Arbeit mit primären Computern finden Sie im Blogbeitrag, in dem Sie sich näher mit dem [primären Computer von Windows 8 befassen](<https://blogs.technet.microsoft.com/askds/2012/10/23/digging-a-little-deeper-into-windows-8-primary-computer/>).

Im folgenden wird erläutert, wie Sie die primären Computer für Benutzer angeben:

1. Öffnen Sie den Server-Manager auf einem Computer, auf dem Active Directory-Verwaltungstools installiert sind.
2. Wählen Sie **im Menü Extras** **Active Directory Verwaltungs Center**aus. Das Active Directory-Verwaltungscenter wird angezeigt.
3. Navigieren Sie in der entsprechenden Domäne zum Container **Computer** .
4. Klicken Sie mit der rechten Maustaste auf einen Computer, den Sie als primären Computer festlegen möchten, und wählen Sie dann **Eigenschaften**aus.
5. Wählen Sie im Navigationsbereich **Erweiterungen**aus.
6. Wählen Sie die Registerkarte Attribut- **Editor** aus, Scrollen Sie zu " **unterbrechername**", wählen Sie **Ansicht**aus, klicken Sie mit der rechten Maustasteauf den aufgelisteten Wert, wählen Sie **Kopieren**aus, und **Wählen Sie**
7. Navigieren Sie in der entsprechenden Domäne zum Container **Benutzer** , klicken Sie mit der rechten Maustaste auf den Benutzer, dem Sie den Computer zuweisen möchten, und wählen Sie dann **Eigenschaften**aus.
8. Wählen Sie im Navigationsbereich **Erweiterungen**aus.
9. Wählen Sie die Registerkarte **Attribut-Editor** aus, und wählen Sie **msDS-primarycomputer** und dann **Bearbeiten**aus. Das Dialogfeld %%amp;quot;Editor für mehrwertige Zeichenfolgen%%amp;quot; wird angezeigt.
10. Klicken Sie mit der rechten Maustaste auf das Textfeld, wählen Sie **Einfügen**aus, klicken Sie auf **Hinzufügen**, klicken Sie auf **OK**, **und wählen Sie**

## <a name="step-2-optionally-enable-primary-computers-for-folder-redirection-in-group-policy"></a>Schritt 2: Aktivieren Sie optional primäre Computer für die Ordner Umleitung in Gruppenrichtlinie

Im nächsten Schritt konfigurieren Sie optional Gruppenrichtlinie, um die Unterstützung primärer Computer für die Ordner Umleitung zu aktivieren. Auf diese Weise können die Ordner eines Benutzers auf Computern umgeleitet werden, die als primäre Computer des Benutzers festgelegt sind, jedoch nicht auf anderen Computern. Sie können primäre Computer für die Ordner Umleitung pro Computer oder pro Benutzer steuern.

So aktivieren Sie primäre Computer für die Ordner Umleitung:

1. Klicken Sie in Gruppenrichtlinie Verwaltung mit der rechten Maustaste auf das GPO, das Sie bei der Erstkonfiguration der Ordner Umleitung und/oder Roamingbenutzerprofile (z. b. Einstellungen für die **Ordner Umleitung** oder **Roamingbenutzerprofile**) erstellt haben. Wählen Sie **Bearbeiten**aus.
2. Um die Unterstützung primärer Computer mithilfe von computerbasierten Gruppenrichtlinie zu aktivieren, navigieren Sie zu **Computerkonfiguration**. Navigieren Sie für Benutzer basiertes Gruppenrichtlinie zu **Benutzerkonfiguration**.
    - Computer basierte Gruppenrichtlinie wendet die Verarbeitung des primären Computers auf alle Computer an, für die das Gruppenrichtlinien Objekt gilt. Dies wirkt sich auf alle Benutzer des Computers aus.
    - Benutzerbasierte Gruppenrichtlinie, die die Verarbeitung des primären Computers auf alle Benutzerkonten anwendet, für die das Gruppenrichtlinien Objekt gilt. Dies wirkt sich auf alle Computer aus, auf denen sich die Benutzer anmelden.
3. Navigieren Sie unter **Computer Konfiguration** oder **Benutzerkonfiguration**zu **Richtlinien**, **Administrative Vorlagen**und dann **System**, und klicken Sie dann auf **Ordner Umleitung**.
4. Klicken Sie **mit der rechten Maustaste auf nur auf primären Computern umleiten**, und wählen Sie dann **Bearbeiten**aus.
5. Wählen Sie **aktiviert**aus, und klicken Sie dann auf **OK**.

## <a name="step-3-optionally-enable-primary-computers-for-roaming-user-profiles-in-group-policy"></a>Schritt 3: Aktivieren Sie optional primäre Computer für Roamingbenutzerprofile in Gruppenrichtlinie

Im nächsten Schritt konfigurieren Sie optional Gruppenrichtlinie, um die Unterstützung primärer Computer für Roamingbenutzerprofile zu aktivieren. Dadurch kann das Profil eines Benutzers auf Computern, die als primäre Computer des Benutzers festgelegt sind, aber nicht auf anderen Computern gewechselt werden.

So aktivieren Sie primäre Computer für Roamingbenutzerprofile:

1. Aktivieren Sie die Unterstützung primärer Computer für die Ordner Umleitung, sofern nicht bereits geschehen.<br>Dadurch werden Dokumente und andere Benutzer Dateien aus den Benutzerprofilen heraus gehalten, sodass profile klein bleiben und die Anmeldezeiten schnell bleiben.
2. Klicken Sie in Gruppenrichtlinie Verwaltung mit der rechten Maustaste auf das von Ihnen erstellte GPO (z. b. **Einstellungen für Ordner Umleitung und Roamingbenutzerprofile**), und wählen Sie dann **Bearbeiten**
3. Navigieren Sie zu **Computer Konfiguration**, **Richtlinien**, **Administrative Vorlagen**, **System**und dann zu **Benutzerprofile**.
4. Klicken Sie **mit der rechten Maustaste auf Roamingprofile nur auf primären Computern herunterladen,** und wählen Sie dann **Bearbeiten**
5. Wählen Sie **aktiviert**aus, und klicken Sie dann auf **OK**.

## <a name="step-4-enable-the-gpo"></a>Schritt 4: Aktivieren des Gruppenrichtlinien Objekts

Nachdem Sie die Konfiguration der Ordner Umleitung und Roamingbenutzerprofile abgeschlossen haben, aktivieren Sie GPO, falls Sie dies noch nicht getan haben. Auf diese Weise kann die Anwendung auf betroffene Benutzer und Computer angewendet werden.

So aktivieren Sie die Gruppenrichtlinien Objekte für die Ordner Umleitung und/oder Roamingbenutzerprofile:

1. Öffnen der Gruppenrichtlinie Verwaltung
2. Klicken Sie mit der rechten Maustaste auf die von Ihnen erstellten Gruppenrichtlinien Objekte, und wählen Sie dann **Link aktiviert**aus. Neben dem Menü Element sollte ein Kontrollkästchen angezeigt werden.

## <a name="step-5-test-primary-computer-function"></a>Schritt 5: Test der primären Computer Funktion

Melden Sie sich zum Testen der Unterstützung des primären Computers bei einem primären Computer an, vergewissern Sie sich, dass die Ordner und Profile umgeleitet werden, melden Sie sich dann bei einem nicht primären Computer an, und vergewissern Sie sich, dass die Ordner und Profile nicht umgeleitet werden.

So testen Sie die Funktionalität des primären Computers:

1. Melden Sie sich bei einem vorgesehenen primären Computer mit einem Benutzerkonto an, für das Sie die Ordner Umleitung und/oder Roamingbenutzerprofile aktiviert haben.
2. Wenn sich das Benutzerkonto bereits am Computer angemeldet hat, öffnen Sie eine Windows PowerShell-Sitzung oder ein Eingabe Aufforderungs Fenster als Administrator, geben Sie den folgenden Befehl ein, und melden Sie sich dann an, wenn Sie dazu aufgefordert werden, sicherzustellen, dass die neuesten Gruppenrichtlinie Einstellungen auf das Client Computer:

    ```PowerShell
    Gpupdate /force
    ```

3. Öffnen Sie den Datei-Explorer.
1. Klicken Sie mit der rechten Maustaste auf einen umgeleiteten Ordner (z. b. auf den Ordner Eigene Dokumente in der Bibliothek Dokumente), und wählen Sie dann **Eigenschaften**aus.
1. Wählen Sie die Registerkarte **Speicherort** aus, und vergewissern Sie sich, dass der Pfad die angegebene Dateifreigabe anstelle eines lokalen Pfads anzeigt. Um zu bestätigen, dass das Benutzerprofil roamingbasiert, öffnen Sie die System **Steuerung**, wählen Sie **System und Sicherheit**, **System**, **Erweiterte System Einstellungen**aus, wählen Sie im Abschnitt Benutzerprofile die Option **Einstellungen** aus, und suchen Sie nach **. Roaming** in der **Type** -Spalte.
1. Melden Sie sich mit demselben Benutzerkonto bei einem Computer an, der nicht als primärer Computer des Benutzers festgelegt ist.
1. Wiederholen Sie die Schritte 2 – 5, und suchen Sie stattdessen nach lokalen Pfaden und einem **lokalen** Profiltyp.

> [!NOTE]
> Wenn Ordner auf einem Computer umgeleitet wurden, bevor Sie die Unterstützung primärer Computer aktiviert haben, bleiben die Ordner umgeleitet, es sei denn, die folgende Einstellung wird in der Ordner Umleitungs Richtlinien Einstellung jedes Ordners konfiguriert: **Leiten Sie den Ordner zurück an den lokalen Speicherort des Benutzerprofils, wenn die Richtlinie entfernt wird**. Auf ähnliche Weise wird für Profile, die zuvor auf einem bestimmten Computer **Roamingvorgang** verwendet haben, das Roaming in den **Typspalten** angezeigt in der Spalte **Status** wird jedoch **lokal**angezeigt.

## <a name="more-information"></a>Weitere Informationen

- [Bereitstellen der Ordner Umleitung mit Offlinedateien](deploy-folder-redirection.md)
- [Bereitstellen von Roamingbenutzerprofilen](deploy-roaming-user-profiles.md)
- [Übersicht über Ordner Umleitung, Offlinedateien und Roamingbenutzerprofile](folder-redirection-rup-overview.md)
- [Genauer Einblicken in den primären Windows 8-Computer](https://blogs.technet.com/b/askds/archive/2012/10/23/digging-a-little-deeper-into-windows-8-primary-computer.aspx)