---
title: Erstellen einer Dateiprüfungsvorlage
description: In diesem Artikel wird beschrieben, wie Sie eine Datei Bildschirm Vorlage erstellen.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 87df941015b240fd34028e59b8aea489e9410834
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475627"
---
# <a name="create-a-file-screen-template"></a>Erstellen einer Dateiprüfungsvorlage

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Eine *Datei Bildschirm Vorlage* definiert einen Satz von Dateigruppen für den Bildschirm, den Typ der auszuführenden Überprüfung (aktiv oder passiv) und optional eine Reihe von Benachrichtigungen, die automatisch generiert werden, wenn ein Benutzer eine nicht autorisierte Datei speichert oder zu speichern versucht.

Datei Server Ressourcen-Manager können e-Mail-Nachrichten an Administratoren oder bestimmte Benutzer senden, ein Ereignis protokollieren, einen Befehl oder ein Skript ausführen oder Berichte generieren. Sie können mehr als einen Benachrichtigungstyp für ein Datei Bildschirm Ereignis konfigurieren.

Indem Sie Datei Bildschirme exklusiv aus Vorlagen erstellen, können Sie die Datei Bildschirme zentral verwalten, indem Sie die Vorlagen aktualisieren, anstatt die Änderungen auf den einzelnen Datei Bildschirmen zu replizieren. Dieses Feature vereinfacht die Implementierung von Änderungen an den Speicherrichtlinien, da alle Updates an einem zentralen Ort ausgeführt werden können.

> [!Important]
> Um e-Mail-Benachrichtigungen zu senden und die Speicher Berichte mit Parametern zu konfigurieren, die für Ihre Serverumgebung geeignet sind, müssen Sie zuerst die Optionen für allgemeine Dateiserver Ressourcen-Manager festlegen. Weitere Informationen finden Sie unter [Festlegen von Datei Server-Ressourcen-Manager Optionen](setting-file-server-resource-manager-options.md).

## <a name="to-create-a-file-screen-template"></a>So erstellen Sie eine Datei Bildschirm Vorlage

1.  Klicken Sie unter **Datei-Überprüfungs Verwaltung**auf den Knoten **Datei Bildschirm Vorlagen** .

2.  Klicken Sie mit der rechten Maustaste auf **Datei Bildschirm Vorlagen**, und klicken Sie dann auf **Datei Bildschirm Vorlage erstellen** (oder wählen Sie im **Aktions** Bereich **Datei Bildschirm Vorlage erstellen** ) aus. Daraufhin wird das Dialogfeld **Datei Bildschirm Vorlage erstellen** geöffnet.

3.  Wenn Sie die Eigenschaften einer vorhandenen Vorlage kopieren möchten, die als Basis für die neue Vorlage verwendet werden soll, wählen Sie in der Dropdown Liste **Eigenschaften aus Vorlage kopieren** eine Vorlage aus, und klicken Sie dann auf **Kopieren**.

    Wenn Sie die Eigenschaften einer vorhandenen Vorlage verwenden oder eine neue Vorlage erstellen möchten, ändern Sie auf der Registerkarte **Einstellungen** die folgenden Werte, bzw. legen Sie sie fest:

4.  Geben Sie im Textfeld **Vorlagen Name** einen Namen für die neue Vorlage ein.

5.  Klicken Sie unter **Screentyp**auf die Option **aktives Screening** oder **Passives Screening** . (Das aktive Screening verhindert, dass Benutzer Dateien speichern, die Mitglieder von blockierten Dateigruppen sind, und generiert Benachrichtigungen, wenn Benutzer versuchen, nicht autorisierte Dateien zu speichern. Passives Screening sendet konfigurierte Benachrichtigungen, verhindert jedoch nicht, dass Benutzer Dateien speichern.)

6.  So legen Sie fest, welche Dateigruppen angezeigt werden sollen:

    Wählen Sie unter **Dateigruppen**die einzelnen Dateigruppen aus, die Sie einschließen möchten. (Doppelklicken Sie auf die Dateigruppen Bezeichnung, um das Kontrollkästchen für die Datei Gruppe auszuwählen.)

    Wenn Sie die Dateitypen anzeigen möchten, die eine Datei Gruppe einschließt und ausschließt, klicken Sie auf die Dateigruppen Bezeichnung, und klicken Sie dann auf **Bearbeiten**. Zum Erstellen einer neuen Datei Gruppe klicken Sie auf **Erstellen**.

    Außerdem können Sie den Datei Server Ressourcen-Manager so konfigurieren, dass eine oder mehrere Benachrichtigungen generiert werden, indem Sie auf den Registerkarten **E-Mail**, **Ereignisprotokoll**, **Befehl**und **Bericht** die folgenden Optionen festlegen.

7.  So konfigurieren Sie e-Mail-Benachrichtigungen

    Legen Sie auf der Registerkarte **e-Mail-Nachricht** die folgenden Optionen fest:

    -   Um Administratoren zu benachrichtigen, wenn ein Benutzer oder eine Anwendung versucht, eine nicht autorisierte Datei zu speichern, aktivieren Sie das Kontrollkästchen **e-Mail an folgende Administratoren senden** , und geben Sie dann die Namen der Administrator Konten ein, die die Benachrichtigungen erhalten sollen. Verwenden Sie die Format *Konto* @ *Domäne*, und verwenden Sie Semikolons zum Trennen mehrerer Konten.
    -   Um eine e-Mail an den Benutzer zu senden, der versucht hat, die Datei zu speichern, aktivieren Sie das Kontrollkästchen **e-Mail an den Benutzer senden, der versucht hat, eine nicht autorisierte Datei zu speichern** .
    -   Um die Meldung zu konfigurieren, bearbeiten Sie die Standard Betreffzeile und den Nachrichtentext, die bereitgestellt werden. Der Text in Klammern fügt Variablen Informationen über das Datei Bildschirm Ereignis ein, das die Benachrichtigung verursacht hat. Beispielsweise fügt die \[ **Quell-IO-Besitzer** \] Variable den Namen des Benutzers ein, der versucht hat, eine nicht autorisierte Datei zu speichern. Um zusätzliche Variablen in den Text einzufügen, klicken Sie auf **Variable einfügen**.
    -   Um zusätzliche Header (einschließlich from, CC, BCC und Reply-to) zu konfigurieren, klicken Sie auf **zusätzliche e-Mail-Header**.

8.  So protokollieren Sie einen Fehler im Ereignisprotokoll, wenn ein Benutzer versucht, eine nicht autorisierte Datei zu speichern:

    Aktivieren Sie auf der Registerkarte **Ereignisprotokoll** das Kontrollkästchen **Warnung an Ereignisprotokoll senden** , und bearbeiten Sie den Standardprotokoll Eintrag.

9.  So führen Sie einen Befehl oder ein Skript aus, wenn ein Benutzer versucht, eine nicht autorisierte Datei zu speichern:

    Aktivieren Sie auf der Registerkarte **Befehl** das Kontrollkästchen **diesen Befehl oder Skript ausführen** . Geben Sie dann den Befehl ein, oder klicken Sie auf **Durchsuchen** , um den Speicherort des Skripts zu suchen. Sie können auch Befehlsargumente eingeben, ein Arbeitsverzeichnis für den Befehl oder das Skript auswählen oder die Einstellung für die Befehls Sicherheit ändern.

10. So generieren Sie einen oder mehrere Speicher Berichte, wenn ein Benutzer versucht, eine nicht autorisierte Datei zu speichern:

    Aktivieren Sie auf der Registerkarte **Bericht** das Kontrollkästchen **Berichte generieren** , und wählen Sie dann aus, welche Berichte generiert werden sollen. (Sie können einen oder mehrere e-Mail-Empfänger für den Bericht auswählen oder den Bericht an den Benutzer senden, der versucht hat, die Datei zu speichern.)

    Der Bericht wird am Standardort für Schadensberichte gespeichert. Dieser kann im Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** geändert werden.

11. Nachdem Sie alle Datei Vorlagen Eigenschaften ausgewählt haben, die Sie verwenden möchten, klicken Sie auf **OK** , um die Vorlage zu speichern.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Datei Prüfungsverwaltung](file-screening-management.md)
-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)
-   [Bearbeiten der Eigenschaften der Dateiprüfungsvorlage](edit-file-screen-template-properties.md)

