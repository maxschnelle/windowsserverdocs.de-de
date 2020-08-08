---
title: Erstellen einer Dateiprüfung
description: In diesem Artikel wird beschrieben, wie ein Datei Bildschirm erstellt wird.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 4efa2add790e4284865a54eaedf3cbb7d9c0589c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971097"
---
# <a name="create-a-file-screen"></a>Erstellen einer Dateiprüfung

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Wenn Sie einen neuen Bildschirm erstellen, können Sie wählen, ob Sie eine Datei Bildschirm Vorlage speichern möchten, die auf den von Ihnen definierten benutzerdefinierten Datei Bildschirm Eigenschaften basiert. Der Vorteil besteht darin, dass ein Link zwischen Datei Bildschirmen und der Vorlage, mit der Sie erstellt werden, verwaltet wird, sodass Änderungen an der Vorlage in Zukunft auf alle Datei Bildschirme angewendet werden können, die davon abgeleitet sind. Dabei handelt es sich um ein Feature, das die Implementierung von Änderungen an der Speicher Richtlinie vereinfacht, indem ein zentraler Punkt bereitgestellt wird, an dem Sie alle Updates vornehmen

## <a name="to-create-a-file-screen-with-custom-properties"></a>So erstellen Sie einen Datei Bildschirm mit benutzerdefinierten Eigenschaften

1.  Klicken Sie unter **Datei-Überprüfungs Verwaltung**auf den Knoten **Datei Bildschirme** .

2.  Klicken Sie mit der rechten Maustaste auf **Datei Bildschirme,** und klicken Sie auf **Datei Bildschirm erstellen** (oder wählen Sie im **Aktions** Bereich **Datei erstellen** ) aus. Daraufhin wird das Dialogfeld **Datei Bildschirm erstellen** geöffnet.

3.  Geben Sie unter **Datei Bildschirm Pfad**den Namen ein, oder navigieren Sie zu dem Ordner, für den der Datei Bildschirm gilt. Der Bildschirm Datei wird auf den ausgewählten Ordner und alle zugehörigen Unterordner angewendet.

4.  Klicken Sie unter **wie möchten Sie die Eigenschaften des Datei Bildschirms konfigurieren?** auf **benutzerdefinierte Datei Bildschirm Eigenschaften definieren**, und klicken Sie dann auf **benutzerdefinierte Eigenschaften**. Dadurch wird das Dialogfeld **Eigenschaften des Datei Bildschirms** geöffnet.

5.  Wenn Sie die Eigenschaften einer vorhandenen Vorlage kopieren möchten, die als Basis für den Datei Bildschirm verwendet werden soll, wählen Sie eine Vorlage aus der Dropdown Liste **Eigenschaften aus Vorlage kopieren** aus. Klicken Sie dann auf **Kopieren**.

    Ändern oder legen Sie auf der Registerkarte "Einstellungen" **auf der Register** Karte " **Einstellungen** " die folgenden Werte fest:

6.  Klicken Sie unter **Screentyp**auf die Option **aktives Screening** oder **Passives Screening** . (Das aktive Screening verhindert, dass Benutzer Dateien speichern, die Mitglieder von blockierten Dateigruppen sind, und generiert Benachrichtigungen, wenn Benutzer versuchen, nicht autorisierte Dateien zu speichern. Passives Screening sendet konfigurierte Benachrichtigungen, verhindert jedoch nicht, dass Benutzer Dateien speichern.)

7.  Wählen Sie unter **Dateigruppen**die einzelnen Dateigruppen aus, die Sie in den Datei Bildschirm einschließen möchten. (Doppelklicken Sie auf die Dateigruppen Bezeichnung, um das Kontrollkästchen für die Datei Gruppe auszuwählen.)

    Wenn Sie die Dateitypen anzeigen möchten, die eine Datei Gruppe einschließt und ausschließt, klicken Sie auf die Dateigruppen Bezeichnung, und klicken Sie dann auf **Bearbeiten**. Zum Erstellen einer neuen Datei Gruppe klicken Sie auf **Erstellen**.

8.  Außerdem können Sie den **Datei Server Ressourcen-Manager** so konfigurieren, dass eine oder mehrere Benachrichtigungen generiert werden, indem Sie Optionen auf den Registerkarten **E-Mail**, **Ereignisprotokoll**, **Befehl**und **Bericht** festlegen. Weitere Informationen zu Datei Bildschirm-Benachrichtigungs Optionen finden Sie unter [Erstellen einer Datei Bildschirm Vorlage](create-file-screen-template.md).

9.  Nachdem Sie alle Datei Bildschirm Eigenschaften ausgewählt haben, die Sie verwenden möchten, klicken Sie auf **OK** , um das Dialogfeld **Eigenschaften des Datei Bildschirms** zu schließen.

10. Klicken Sie im Dialogfeld **Datei erstellen** auf **Erstellen** , um den Datei Bildschirm zu speichern. Dadurch wird das Dialogfeld **benutzerdefinierte Eigenschaften als Vorlage speichern** geöffnet.

11. Wählen Sie den Typ des benutzerdefinierten Datei Bildschirms aus, den Sie erstellen möchten:

    -   Zum Speichern einer Vorlage, die auf diesen angepassten Eigenschaften basiert (empfohlen), klicken Sie auf **benutzerdefinierte Eigenschaften als Vorlage speichern** , und geben Sie einen Namen für die Vorlage ein. Mit dieser Option wird die Vorlage auf den neuen Datei Bildschirm angewendet, und Sie können die Vorlage verwenden, um in Zukunft weitere Datei Bildschirme zu erstellen. Dadurch können Sie die Datei Bildschirme später automatisch aktualisieren, indem Sie die Vorlage aktualisieren.
    -   Wenn Sie beim Speichern der Datei auf dem Bildschirm keine Vorlage speichern möchten, klicken Sie auf **den Bildschirm benutzerdefinierte Datei speichern, ohne eine Vorlage zu erstellen**.

12. Klicken Sie auf **OK**.

## <a name="additional-references"></a>Weitere Verweise

-   [Datei Prüfungsverwaltung](file-screening-management.md)
-   [Definieren von Dateigruppen für die Prüfung](define-file-groups-for-screening.md)
-   [Erstellen einer Dateiprüfungsvorlage](create-file-screen-template.md)
-   [Bearbeiten der Eigenschaften der Dateiprüfungsvorlage](edit-file-screen-template-properties.md)


