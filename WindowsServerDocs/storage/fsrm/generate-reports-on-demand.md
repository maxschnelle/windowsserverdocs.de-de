---
title: Berichte nach Bedarf erstellen
description: Dieser Artikel beschreibt, wie Berichte Bedarfs gesteuert generiert werden, um die Datenträger Verwendung auf dem Server zu analysieren.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: a44db85dee565bfa3c6032d52b4d752c61c09cc0
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961364"
---
# <a name="generate-reports-on-demand"></a>Berichte nach Bedarf erstellen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Bei täglichen Vorgängen können Sie die Option " **Berichte jetzt generieren** " verwenden, um einen oder mehrere Berichte bei Bedarf zu generieren. Mit diesen Berichten können Sie die verschiedenen Aspekte der aktuellen Datenträger Verwendung auf dem Server analysieren. Aktuelle Daten werden gesammelt, bevor die Berichte generiert werden.

Wenn Sie Berichte bei Bedarf generieren, werden die Berichte an einem Standard Speicherort gespeichert, den Sie im Dialogfeld **Datei Server Ressourcen-Manager Option** angeben, es wird jedoch keine Berichts Aufgabe für die spätere Verwendung erstellt. Sie können die Berichte sofort anzeigen, nachdem Sie generiert wurden, oder die Berichte per e-Mail an eine Gruppe von Administratoren senden.

> [!Note]
> Wenn Sie die Berichte sofort öffnen möchten, müssen Sie warten, während die Berichte generiert werden. Die Verarbeitungszeit variiert je nach Art der Berichte und dem Umfang der Daten.

## <a name="to-generate-reports-immediately"></a>So generieren Sie Berichte sofort

1. Klicken Sie auf den Knoten **Speicher Berichte-Verwaltung** .

2. Klicken Sie mit der rechten Maustaste auf **Speicher Berichte Verwaltung**, und klicken Sie dann auf **Berichte jetzt generieren** (oder klicken Sie im Bereich **Aktionen** auf **Berichte jetzt generieren** ). Dadurch wird das Dialogfeld Eigenschaften von " **Speicher Berichte** " geöffnet.

3. So wählen Sie Volumes oder Ordner aus, für die Berichte generiert werden sollen:

   -   Klicken Sie unter **Bereich**auf **Hinzufügen**.
   -   Navigieren Sie zu dem Volume oder Ordner, in dem Sie die Berichte generieren möchten, wählen Sie es aus, und klicken Sie dann auf **OK** , um den Pfad zur Liste hinzuzufügen.
   -   Fügen Sie beliebig viele Volumes oder Ordner hinzu, die Sie in die Berichte einschließen möchten. (Um ein Volume oder einen Ordner zu entfernen, klicken Sie auf den Pfad, und klicken Sie dann auf **Entfernen**.)

4. So geben Sie an, welche Berichte generiert werden sollen:

    -   Wählen Sie unter **Berichtsdaten**die einzelnen Berichte aus, die Sie einschließen möchten.

   So bearbeiten Sie die Parameter eines Berichts:

   -   Klicken Sie auf die Bezeichnung Bericht, und klicken Sie dann auf **Parameter bearbeiten**.
   -   Bearbeiten Sie im Dialogfeld **Berichts Parameter** die Parameter nach Bedarf, und klicken Sie dann auf **OK**.
   -  Wenn Sie eine Liste der Parameter für alle ausgewählten Berichte anzeigen möchten, klicken Sie auf **ausgewählte Berichte überprüfen** und dann auf **Schließen**.

5. So geben Sie die Formate zum Speichern der Berichte an:

   -  Wählen Sie unter **Berichtsformate**mindestens ein Format für die geplanten Berichte aus. Standardmäßig werden Berichte in Dynamic HTML (DHTML) generiert. Sie können auch HTML-, XML-, CSV-und Textformate auswählen. Die Berichte werden für Bedarfs gesteuerte Berichte am Standard Speicherort gespeichert.

6. So übermitteln Sie Kopien der Berichte per e-Mail an Administratoren:

   - Aktivieren Sie auf der Registerkarte **Übermittlung** das Kontrollkästchen **Berichte an folgende Administratoren senden** , und geben Sie dann die Namen der Administrator Konten ein, die Berichte erhalten sollen.
   - Verwenden Sie das Format <em>account@domain</em> , und verwenden Sie Semikolons zum Trennen mehrerer Konten.

7. Klicken Sie auf **OK**, um die Daten zu erfassen und die Berichte zu generieren. Dadurch wird das Dialogfeld **Speicher Berichte generieren** geöffnet.

8. Wählen Sie aus, wie die bedarfsgesteuerten Berichte generiert werden sollen:

   -   Wenn Sie die Berichte sofort nach ihrer Generierung anzeigen möchten, klicken Sie auf **warten, bis Berichte generiert werden, und zeigen Sie Sie**an. Jeder Bericht wird in einem eigenen Fenster geöffnet.
   -   Klicken Sie **im Hintergrund auf Berichte generieren**, um die Berichte später anzuzeigen.

   Mit beiden Optionen werden die Berichte gespeichert, und wenn Sie die Übermittlung per e-Mail aktiviert haben, senden Sie die Berichte in den von Ihnen ausgewählten Formaten an Administratoren.

## <a name="additional-references"></a>Weitere Verweise

-   [Speicherberichtmanagement](storage-reports-management.md)
-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)

