---
title: Planen eines Satzes von Berichten
description: "Dieser Artikel beschreibt, wie ein Satz von Berichten in regelmäßigen Abständen generiert wird"
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 15b69e723af3a30375beae73782ab122c68f8880
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="schedule-a-set-of-reports"></a>Planen eines Satzes von Berichten

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Um einen Satz von Berichten in regelmäßigen Abständen zu generieren, planen Sie eine *Berichtsaufgabe.* Die Berichtsaufgabe gibt an, welche Berichte generiert und welche Parameter verwendet werden sollen; in welche Volumes und Ordner diese Berichte erstellt werden sollen; wie oft die Berichte generiert werden sollen und in welchem Dateiformaten sie gespeichert werden sollen.

Geplante Berichte werden in einem Standardort gespeichert. Dieser kann im Dialogfeld **Optionen für den Ressourcen-Manager für Dateiserver** festgelegt werden. Sie haben auch die Möglichkeit, die Berichte per E-Mail an einer Gruppe von Administratoren zu übermitteln.

> [!Note]
> Um die Auswirkungen der Berichtverarbeitung auf die Leistung zu minimieren, generieren Sie mehrere Berichte nach demselben Zeitplan, damit die Daten nur einmal gesammelt werden. Zum schnellen Hinzufügen von Berichten zu bestehenden Berichtsaufgaben können Sie die Aktion **Berichte für eine Berichtaufgabe hinzufügen oder entfernen** verwenden. Dadurch können Berichte aus mehreren Berichtsaufgaben hinzugefügt oder entfernt und die Berichtsparameter wie gewünscht bearbeitet werden. Um Zeitpläne oder Lieferadressen zu ändern, müssen Sie einzelne Berichtsaufgaben bearbeiten.

## <a name="to-schedule-a-report-task"></a>Planen einer Berichtsaufgabe

1.  Klicken Sie auf den Knoten **Speicherberichtmanagement**.

2.  Klicken Sie mit der rechten Maustaste auf **Speicherberichte verwalten** und dann auf **Neue Berichtsaufgabe planen** (oder wählen Sie **Neue Berichtsaufgabe planen** aus dem Bereich **Aktionen** aus). Das Dialogfeld **Speicherberichts-Aufgabeneigenschaften** wird geöffnet.

3.  So wählen Sie Volumes oder Ordner aus, in die Sie die Berichte erstellen:

    -   Klicken Sie unter **Umfang** auf **Hinzufügen**.
    -   Navigieren Sie zu dem Volume oder Ordner, auf den Sie die Berichte erstellen möchten und wählen Sie sie aus und klicken Sie dann auf **OK**, um den Pfad der Liste hinzuzufügen.
    -   Fügen Sie so viele Volumes oder Ordner aus, wie in den Berichten enthalten sein sollen. (Um ein Volume oder Ordner zu entfernen, klicken Sie auf den Pfad und dann auf **Entfernen**).

4.  So geben Sie die zu erstellenden Berichte an:

    -  Wählen Sie unter **Berichtsdaten** jeden Bericht aus, den Sie hinzufügen möchten. Standardmäßig werden alle Berichte für eine geplante Berichtsaufgabe generiert.

    So bearbeiten Sie die Parameter eines Berichts:

    -   Klicken Sie auf die Bezeichnung des Berichts und dann auf **Parameter bearbeiten**.
    -   Bearbeiten Sie im Dialogfeld **Berichtsparameter** die Parameter nach Wunsch und klicken Sie dann auf **OK**.

    -   Um eine Liste mit den Standardparametern für alle ausgewählten Berichte anzuzeigen, klicken Sie auf **Ausgewählte Berichte überprüfen**. Klicken Sie anschließend auf **Schließen**.

5.  So geben Sie das Speicherformat des Berichts an:

    -  Wählen Sie unter **Berichtsformate** ein oder mehrere Formate für die geplanten Berichte aus. Standardmäßig werden Berichte in Dynamic HTML (DHTML) generiert. Sie können auch HTML, XML, CSV und Text-Formate auswählen. Die Berichte werden im Standardspeicherort für geplante Berichte gespeichert.

6.  So übermitteln Sie Kopien der Berichte per E-Mail an Administratoren:

    - Aktivieren Sie auf der Registerkarte **Übermittlung** das Kontrollkästchen die **Berichte an die folgenden Administratoren senden** aus und geben Sie die Namen der administrativen Konten, die die Berichte erhalten sollen. 
    - Verwenden Sie das Format *account@domain*, und verwenden Sie Semikolons zum Trennen mehrerer Konten.

7.  So planen Sie die Berichte:

    Klicken Sie auf der Registerkarte **Zeitplan** auf **Zeitplan erstellen** und dann im Dialogfeld **Zeitplan** auf **Neu**. Die zeigt den Standardzeitplan für 9:00 Uhr täglich an, Sie können allerdings den Standardzeitplan ändern.

    -   Wählen Sie für die Frequenz der Berichtserstellung einen Intervall aus der Dropdownliste **Planungsaufgabe** aus.
        Sie können täglich, wöchentlich oder monatlich Berichte planen oder die Berichte nur einmal ausführen. Sie können die Berichte ebenfalls bei der Anmeldung oder beim Systemstart erstellen, oder wenn sich der Computer für eine bestimmte Zeit im Leerlauf befunden hat.
    -   Um weitere Planungsinformationen für das ausgewählte Zeitintervall bereitzustellen, ändern Sie oder legen Sie die Werte in der Option **Planungsaufgabe** fest.
        Diese Optionen ändern sich je nach dem von Ihnen ausgewählten Intervall. Beispielsweise können Sie die Anzahl der Wochen zwischen Berichten und die Tage der Woche für das Erstellen der Berichten für einen wöchentlichen Bericht angeben.
    -   Um die Uhrzeit anzugeben, wann Sie den Bericht erstellen möchten, geben Sie diese ein oder wählen Sie den Wert im Feld **Startzeit** aus.
    -   Klicken Sie für zusätzliche Planungsoptionen (einschließlich ein Start- und Enddatum für die Aufgabe) auf **Erweitert**.
    -   Klicken Sie auf **OK**, um den Zeitplan zu speichern.
    -  Klicken Sie zum Erstellen eines weiteren Zeitplans für eine Aufgabe (oder zum Ändern eines vorhandenen Zeitplans) in der Registerkarte **Zeitplan** auf **Zeitplan bearbeiten**.

8.  Klicken Sie auf **OK**, um den Bericht zu speichern.

Die Berichtsaufgabe wird dem **Speicherberichtmanagement**-Knoten hinzugefügt. Aufgaben werden erkannt über die Berichte, die generiert werden, den Namespace, auf den sie gemeldet werden und den Zeitplan des Berichts.

Darüber hinaus können Sie den aktuellen Status des Berichts einsehen (gibt an, ob der Bericht ausgeführt wird oder nicht), die letzte Laufzeit und das Ergebnis dieser Ausführung sowie die nächste geplante Laufzeit.

## <a name="see-also"></a>Weitere Informationen:

-   [Speicherberichtmanagement](storage-reports-management.md)
-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)


