---
title: Erstellen einer Dateiprüfungsvorlage
description: In diesem Artikel wird beschrieben, wie Sie eine Dateiprüfungsvorlage erstellen
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 63824f016180ce5a92d9a16b9ee0d26a46e5db72
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394208"
---
# <a name="create-a-file-screen-template"></a>Erstellen einer Dateiprüfungsvorlage

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Eine *Dateiprüfungsvorlage* definiert einen Satz von zu prüfenden Dateigruppen, den Typ der Prüfung (aktiv oder passiv) und optional eine Gruppe von Benachrichtigungen, die automatisch generiert wird, wenn ein Benutzer eine nicht autorisierte Datei speichert oder zu speichern versucht.

Der Ressourcen-Manager für Dateiserver kann E-Mail-Nachrichten an Administratoren oder bestimmte Benutzer senden, ein Ereignis protokollieren, einen Befehl oder ein Skript ausführen oder Berichte erstellen. Sie können mehr als eine Art der Benachrichtigung für ein Dateiprüfungsereignis konfigurieren.

Wenn Sie Dateiprüfungen ausschließlich auf der Grundlage von Vorlagen erstellen, können Sie die Dateiprüfungen zentral verwalten, indem Sie die Vorlagen aktualisieren, anstatt die Änderungen bei jeder einzelnen Dateiprüfungen zu replizieren. Dieses Feature vereinfacht die Implementierung von Änderungen an den Speicherrichtlinien, da alle Updates an einem zentralen Ort ausgeführt werden können.

> [!Important]
> Zum Senden von E-Mail-Benachrichtigungen und um Speicherberichte mit Parametern zu konfigurieren, die für die Serverumgebung geeignet sind, müssen Sie zuerst die allgemeinen Optionen des Ressourcen-Managers für Dateiserver festlegen. Weitere Informationen finden Sie unter [Festlegen der Einstellungen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md).

## <a name="to-create-a-file-screen-template"></a>So erstellen Sie eine Dateiprüfungsvorlage

1.  Klicken Sie unter **Dateiprüfungsverwaltung** auf den Knoten **Dateiprüfungsvorlage**.

2.  Klicken Sie mit der rechten Maustaste auf **Dateiprüfungsvorlage,** und dann auf **Dateiprüfungsvorlage erstellen** (oder wählen Sie **Dateiprüfungsvorlage erstellen** im Bereich **Aktionen** aus). Daraufhin wird das Dialogfeld **Dateiprüfungsvorlage erstellen** geöffnet.

3.  Wenn Sie die Eigenschaften einer vorhandenen Vorlage als Grundlage für eine neue Vorlage kopieren und verwenden möchten, wählen Sie in der Dropdownliste **Eigenschaften aus Vorlage kopieren** eine Vorlage aus, und klicken Sie anschließend in der Dropdownliste auf **Kopieren**.

    Wenn Sie die Eigenschaften einer vorhandenen Vorlage verwenden oder eine neue Vorlage erstellen möchten, ändern Sie auf der Registerkarte **Einstellungen** die folgenden Werte, bzw. legen Sie sie fest:

4.  Geben Sie im Textfeld **Vorlagenname** einen Namen für die neue Vorlage ein.

5.  Klicken Sie unter **Prüfungstyp** auf die Option **Aktives prüfen** oder **Passives prüfen**. (Aktives Prüfen verhindert, dass Benutzer Dateien speichern, die blockierten Dateigruppen angehören und Benachrichtigungen generieren, wenn Benutzer versuchen, nicht autorisierte Dateien zu speichern. Passives Prüfen sendet Konfigurationsbenachrichtigungen, aber es verhindert nicht, dass Benutzer Dateien speichern können).

6.  So geben Sie die zu prüfenden Dateigruppen an:

    Wählen Sie unter **Dateigruppen** jede Dateigruppe aus, die enthalten sein sollen. (Um das Kontrollkästchen für die Dateigruppe zu aktivieren, doppelklicken Sie auf die Bezeichnung der Dateigruppe.)

    Wenn Sie die Dateitypen anzeigen möchten, die eine Datei Gruppe einschließt und ausschließt, klicken Sie auf die Dateigruppen Bezeichnung, und klicken Sie dann auf **Bearbeiten**. Zum Erstellen einer neuen Datei Gruppe klicken Sie auf **Erstellen**.

    Darüber hinaus können Sie den Ressourcen-Manager für Dateiserver so konfigurieren, dass eine oder mehrere Benachrichtigungen erstellt werden. Dies geschieht durch das Festlegen der folgenden Optionen in den Registerkarten **E-Mail-Nachricht**, **Ereignisprotokoll**, **Befehl**, und **Bericht**.

7.  So konfigurieren Sie E-Mail-Benachrichtigungen:

    Legen Sie auf der Registerkarte **E-Mail-Nachricht** folgende Optionen fest:

    -   Um Administratoren zu benachrichtigen, wenn ein Benutzer oder eine Anwendung versucht, nicht autorisierte Dateien zu speichern, aktivieren Sie das Kontrollkästchen **E-Mail an die folgenden Administratoren senden** und geben Sie die Namen der administrativen Konten ein, die die Benachrichtigungen erhalten sollen. Verwenden Sie das Format *account*@*domain*, und verwenden Sie Semikolons zum Trennen mehrerer Konten.
    -   Aktivieren Sie zum Senden einer E-Mail an den Benutzer, der versucht hat, um die Datei zu speichern, das Kontrollkästchen **E-Mail an den Benutzer senden, der nicht autorisierte Datei zu speichern versucht**.
    -   Um die Nachricht zu konfigurieren, ändern Sie den vorgegebenen standardmäßigen Betreff und Textkörper. Der Text in Klammern fügt die Variableninformationen über das Dateiprüfungsereignis ein, das die Benachrichtigung verursacht hat. Beispielsweise wird der Name des Benutzers, der versucht hat, eine nicht autorisierte Datei zu speichern, vom \[-**Quell-IO-Besitzer**\]-Variablen eingefügt. Um zusätzliche Variablen in den Text einzufügen, klicken Sie auf **Variable einfügen**.
    -   Wenn Sie weitere Header konfigurieren möchten (einschließlich Von, Cc, Bcc und Antwort an), klicken Sie auf **Weitere E-Mail-Kopfzeilen**.

8.  So protokollieren Sie einen Fehler im Ereignisprotokoll, wenn ein Benutzer versucht, eine nicht autorisierte Datei zu speichern:

    Klicken Sie auf die Registerkarte **Ereignisprotokoll** und wählen Sie das Kontrollkästchen **Warnung an Ereignisprotokoll senden**. Bearbeiten Sie anschließend den Standard-Protokolleintrag.

9.  So führen Sie einen Befehl oder Skript aus, wenn ein Benutzer versucht, eine nicht autorisierte Datei zu speichern:

    Aktivieren Sie auf der Registerkarte **Befehl** das Kontrollkästchen **Diesen Befehl oder dieses Skript ausführen** . Geben Sie anschließend den Befehl ein oder klicken Sie auf **Durchsuchen**, um den Speicherort zu suchen, in dem das Skript gespeichert ist. Sie können ebenfalls Befehlsargumente eingeben, ein Arbeitsverzeichnis für den Befehl oder ein Skript auswählen oder die Sicherheitsstufeneinstellungen für den Befehl ändern.

10. So generieren Sie einen oder mehrere Speicherberichte, wenn ein Benutzer versucht, eine nicht autorisierte Datei zu speichern:

    Aktivieren Sie auf der Registerkarte **Bericht** das Kontrollkästchen **Berichte** und wählen Sie dann aus, welche Berichte erstellt werden sollen. (Sie können einen oder mehrere Administratoren als E-Mail-Empfänger für den Bericht auswählen oder den Bericht per E-Mail an den Benutzer senden, der versucht hat, die Datei zu speichern.)

    Der Bericht wird am Standardort für Schadensberichte gespeichert. Dieser kann im Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** geändert werden.

11. Wählen Sie zunächst alle Dateivorlageneigenschaften aus, die verwendet werden sollen, und klicken Sie anschließend zum Speichern der Vorlage auf **OK**.

## <a name="see-also"></a>Siehe auch

-   [Datei Prüfungsverwaltung](file-screening-management.md)
-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)
-   [Bearbeiten der Eigenschaften der Dateiprüfungsvorlage](edit-file-screen-template-properties.md)

