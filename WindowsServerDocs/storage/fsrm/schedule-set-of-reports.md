---
title: Planen eines Satzes von Berichten
description: In diesem Artikel wird beschrieben, wie Sie einen Satz von Berichten in regelmäßigen Abständen generieren.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 4b8b0c66bc4f6e5445635deead1f79f7cc11309d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950464"
---
# <a name="schedule-a-set-of-reports"></a>Planen eines Satzes von Berichten

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Zum Erstellen eines Satzes von Berichten in regelmäßigen Abständen planen Sie einen *Berichts Task.* Die Berichts Aufgabe gibt an, welche Berichte generiert und welche Parameter verwendet werden sollen. welche Volumes und Ordner sollen berichtet werden? Gibt an, wie oft die Berichte generiert werden und in welchen Dateiformaten sie gespeichert werden sollen.

Geplante Berichte werden an einem Standard Speicherort gespeichert, den Sie im Dialogfeld **Datei Server Ressourcen-Manager Optionen** angeben können. Sie haben auch die Möglichkeit, die Berichte per e-Mail an eine Gruppe von Administratoren zu übermittelt.

> [!Note]
> Um die Auswirkungen der Berichts Verarbeitung auf die Leistung zu minimieren, generieren Sie mehrere Berichte nach demselben Zeitplan, sodass die Daten nur einmal gesammelt werden. Zum schnellen Hinzufügen von Berichten zu vorhandenen Berichtsaufgaben können Sie die Aktion **Berichte für einen Berichts Task hinzufügen oder entfernen** verwenden. Dies ermöglicht es Ihnen, Berichte aus mehreren Berichtsaufgaben hinzuzufügen oder daraus zu entfernen und die Berichts Parameter zu bearbeiten. Zum Ändern von Zeitplänen oder Übermittlungs Adressen müssen Sie einzelne Berichtsaufgaben bearbeiten.

## <a name="to-schedule-a-report-task"></a>So planen Sie eine Berichts Aufgabe

1. Klicken Sie auf den Knoten **Speicher Berichte-Verwaltung** .

2. Klicken Sie mit der rechten Maustaste auf **Speicher Berichte-Verwaltung**, und klicken Sie dann auf **Task ' neuen Bericht planen** ' (oder wählen Sie im **Aktions** Bereich **eine neue Berichts Aufgabe planen** ) aus. Dadurch wird das Dialogfeld Eigenschaften von " **Speicher Berichte** " geöffnet.

3. So wählen Sie Volumes oder Ordner aus, für die Berichte generiert werden sollen:

   -   Klicken Sie unter **Bereich**auf **Hinzufügen**.
   -   Navigieren Sie zu dem Volume oder Ordner, in dem Sie die Berichte generieren möchten, wählen Sie es aus, und klicken Sie dann auf **OK** , um den Pfad zur Liste hinzuzufügen.
   -   Fügen Sie beliebig viele Volumes oder Ordner hinzu, die Sie in die Berichte einschließen möchten. (Um ein Volume oder einen Ordner zu entfernen, klicken Sie auf den Pfad, und klicken Sie dann auf **Entfernen**.)

4. So geben Sie an, welche Berichte generiert werden sollen:

   -  Wählen Sie unter **Berichtsdaten**die einzelnen Berichte aus, die Sie einschließen möchten. Standardmäßig werden alle Berichte für eine geplante Berichts Aufgabe generiert.

   So bearbeiten Sie die Parameter eines Berichts:

   -   Klicken Sie auf die Bezeichnung Bericht, und klicken Sie dann auf **Parameter bearbeiten**.
   -   Bearbeiten Sie im Dialogfeld **Berichts Parameter** die Parameter nach Bedarf, und klicken Sie dann auf **OK**.

   -   Klicken Sie auf **ausgewählte Berichte überprüfen**, um eine Liste der Parameter für alle ausgewählten Berichte anzuzeigen. Klicken Sie anschließend auf **Schließen**.

5. So geben Sie die Formate zum Speichern der Berichte an:

   -  Wählen Sie unter **Berichtsformate**mindestens ein Format für die geplanten Berichte aus. Standardmäßig werden Berichte in Dynamic HTML (DHTML) generiert. Sie können auch HTML-, XML-, CSV-und Textformate auswählen. Die Berichte werden am Standard Speicherort für geplante Berichte gespeichert.

6. So übermitteln Sie Kopien der Berichte per e-Mail an Administratoren:

   - Aktivieren Sie auf der Registerkarte **Übermittlung** das Kontrollkästchen **Berichte an folgende Administratoren senden** , und geben Sie dann die Namen der Administrator Konten ein, die Berichte erhalten sollen.
   - Verwenden Sie das Format <em>account@domain</em> , und verwenden Sie Semikolons zum Trennen mehrerer Konten.

7. So planen Sie die Berichte

   Klicken Sie auf der Registerkarte **Zeitplan** auf **Zeitplan erstellen**, und klicken Sie dann im Dialogfeld **Zeitplan** auf **neu**. Hiermit wird ein Standard Zeitplan für 9:00 Uhr angezeigt. täglich, Sie können den Standard Zeitplan jedoch ändern.

   -   Wählen Sie in der Dropdown Liste Zeit **Plan Aufgabe** ein Intervall aus, um eine Häufigkeit für das Erstellen von Berichten anzugeben.
       Sie können tägliche, wöchentliche oder monatliche Berichte planen oder die Berichte nur einmal generieren. Sie können beim Systemstart oder bei der Anmeldung auch Berichte generieren, oder wenn sich der Computer für einen bestimmten Zeitraum im Leerlauf befunden hat.
   -   Zum Bereitstellen zusätzlicher Zeit Planungsinformationen für das ausgewählte Intervall müssen Sie die Werte in den Optionen für Zeit **Plan Aufgaben** ändern oder festlegen.
       Diese Optionen werden basierend auf dem Intervall geändert, das Sie auswählen. Beispielsweise können Sie für einen wöchentlichen Bericht die Anzahl der Wochen Zwischenberichten und die Wochentage angeben, an denen Berichte generiert werden sollen.
   -   Zum Angeben der Tageszeit, zu der der Bericht generiert werden soll, geben Sie den Wert in das Feld **Start Zeit** ein, oder wählen Sie ihn aus.
   -   Klicken Sie auf **erweitert**, um auf zusätzliche Planungsoptionen (einschließlich Start-und Enddatum für die Aufgabe) zuzugreifen.
   -   Klicken Sie auf **OK**, um den Zeitplan zu speichern.
   -  Zum Erstellen eines zusätzlichen Zeitplans für eine Aufgabe (oder zum Ändern eines vorhandenen Zeitplans) klicken Sie auf der Registerkarte **Zeitplan** auf **Zeitplan bearbeiten**.

8. Klicken Sie auf **OK**, um den Bericht zu speichern.

Die Berichts Aufgabe wird dem Knoten **Speicher Berichte-Verwaltung** hinzugefügt. Tasks werden durch die zu generierenden Berichte, den Namespace, für den berichtet werden soll, und den Berichts Zeitplan identifiziert.

Außerdem können Sie den aktuellen Status des Berichts (unabhängig davon, ob der Bericht ausgeführt wird), die letzte Laufzeit und das Ergebnis der Ausführung sowie die nächste geplante Laufzeit anzeigen.

## <a name="additional-references"></a>Weitere Verweise

-   [Speicherberichtmanagement](storage-reports-management.md)
-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)


