---
title: Berichte nach Bedarf erstellen
description: Dieser Artikel beschreibt, wie Berichte nach Bedarf zum Analysieren der Datenträgerverwendung auf dem Server erstellt werden
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e91bfbc306d1d2712f7b35ec48114b3a8a84ec83
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890991"
---
# <a name="generate-reports-on-demand"></a>Berichte nach Bedarf erstellen

> Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

Während des täglichen Betriebs können Sie die Option **Berichte jetzt generieren** auswählen, um einen oder mehrere Berichte nach Bedarf zu erstellen. Mit diesen Berichten können Sie verschiedene Aspekte der aktuellen Datenträgerverwendung auf dem Server analysieren. Aktuelle Daten werden gesammelt, bevor die Berichte generiert werden.

Wenn Sie Berichte nach Bedarf erstellen, werden die Berichte an einem Standardspeicherort gespeichert, den Sie im Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** festlegen. Es wird allerdings keine Berichtsaufgabe zur späteren Verwendung erstellt. Sie können die Berichte sofort nach der Erstellung einsehen oder nachdem sie per E-Mail an eine Gruppe von Administratoren gesendet werden.

> [!Note]
> Wenn Sie die Berichte sofort öffnen möchten, müssen Sie warten, bis die Berichte generiert werden. Die Verarbeitungszeit variiert je nach den Arten von Berichten und Umfang der Daten.

## <a name="to-generate-reports-immediately"></a>So erstellen Sie Bericht sofort

1.  Klicken Sie auf den Knoten **Speicherberichtmanagement**.

2.  Klicken Sie mit der rechten Maustaste auf **Speicherberichtmanagement** und dann auf **Berichte jetzt generieren** (oder wählen Sie **Berichte jetzt generieren** im Bereich **Aktionen** aus). Das Dialogfeld **Speicherberichts-Aufgabeneigenschaften** wird geöffnet.

3.  So wählen Sie Volumes oder Ordner aus, in die Sie die Berichte erstellen:

    -   Klicken Sie unter **Umfang** auf **Hinzufügen**.
    -   Navigieren Sie zu dem Volume oder Ordner, auf den Sie die Berichte erstellen möchten und wählen Sie sie aus und klicken Sie dann auf **OK**, um den Pfad der Liste hinzuzufügen.
    -   Fügen Sie so viele Volumes oder Ordner aus, wie in den Berichten enthalten sein sollen. (Um ein Volume oder Ordner zu entfernen, klicken Sie auf den Pfad und dann auf **Entfernen**).

4.  So geben Sie die zu erstellenden Berichte an:

     -   Wählen Sie unter **Berichtsdaten** jeden Bericht aus, den Sie hinzufügen möchten.

    So bearbeiten Sie die Parameter eines Berichts:

    -   Klicken Sie auf die Bezeichnung des Berichts und dann auf **Parameter bearbeiten**.
    -   Bearbeiten Sie im Dialogfeld **Berichtsparameter** die Parameter nach Wunsch und klicken Sie dann auf **OK**.
    -  Um eine Liste der Parameter für alle ausgewählten Berichte anzuzeigen, klicken Sie auf **Ausgewählte Berichte überprüfen** und dann auf **Schließen**.
 
5.  So geben Sie das Speicherformat des Berichts an:

    -  Wählen Sie unter **Berichtsformate** ein oder mehrere Formate für die geplanten Berichte aus. Standardmäßig werden Berichte in Dynamic HTML (DHTML) generiert. Sie können auch HTML, XML, CSV und Text-Formate auswählen. Die Berichte werden im Standardspeicherort für bedarfsgesteuerte Berichte gespeichert.

6.  So übermitteln Sie Kopien der Berichte per E-Mail an Administratoren:

    -  Aktivieren Sie auf der Registerkarte **Übermittlung** das Kontrollkästchen die **Berichte an die folgenden Administratoren senden** aus und geben Sie die Namen der administrativen Konten, die die Berichte erhalten sollen. 
    - Verwenden Sie das Format *account@domain*, und verwenden Sie Semikolons zum Trennen mehrerer Konten.

7.  Klicken Sie auf **OK**, um die Daten zu sammeln und die Berichte zu erstellen. Das Dialogfeld **Speicherberichte generieren** wird geöffnet.

8.  Geben Sie an, wie Sie die bedarfsgesteuerten Berichte generieren möchten:

    -   Wenn Sie die Berichte sofort nach der Erstellung anzeigen möchten, klicken Sie auf **Auf zu generierende Berichte warten und sie dann anzeigen**. Jeder Bericht wird in seinem eigenen Fenster geöffnet.
    -   Wenn Sie die Berichte später anzeigen möchten, klicken Sie auf **Berichte im Hintergrund generieren**.

    Beide Optionen speichern die Berichte, und wenn Sie die Übermittlung per E-Mail aktiviert haben, werden die Berichte an die Administratoren in den Formaten gesendet, die Sie ausgewählt haben.

## <a name="see-also"></a>Siehe auch

-   [Speicherverwaltung für Berichte](storage-reports-management.md)
-   [Einstellung File Server Resource Manager-Optionen](setting-file-server-resource-manager-options.md)

