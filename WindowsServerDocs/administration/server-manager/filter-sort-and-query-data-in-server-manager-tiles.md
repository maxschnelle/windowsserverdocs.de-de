---
title: Filtern, Sortieren und Abfragen von Daten in Server-Manager-Kacheln
description: Server-Manager
ms.topic: article
ms.assetid: 8786f791-73e5-4c75-8d12-46e88a196976
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0ddaaadbda28b5494ce5ab0a053b70abd5882591
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628303"
---
# <a name="filter-sort-and-query-data-in-server-manager-tiles"></a>Filtern, Sortieren und Abfragen von Daten in Server-Manager-Kacheln

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In Windows Server können Sie mit Kacheln in Server-Manager Daten filtern und sortieren sowie benutzerdefinierte Abfragen erstellen und speichern. Sie können in den Kacheln "Ereignisse", "Leistung", "Best Practices Analyzer", "Dienste", "Rollen" und "Features" in Server-Manager Kacheln zum Sortieren, verwenden von Schlüsselwort Filtern und Ausführen von Abfragen für Listeneinträge ausführen.

Dieses Thema enthält folgende Abschnitte:

-   [Filtern von Listeneinträgen in Kacheln](#BKMK_tiles)

-   [Sortieren von Listeneinträgen in Kacheln](#BKMK_sort)

-   [Erstellen und Ausführen benutzerdefinierter Abfragen für Kachel Daten](#BKMK_query)

## <a name="filter-list-entries-in-tiles"></a><a name=BKMK_tiles></a>Filtern von Listeneinträgen in Kacheln
Mit dem Textfeld **Filtern** können Sie die Liste der Einträge, die in einer Kachel angezeigt werden, schnell auf Einträge reduzieren, die eine bestimmte Zeichenfolge enthalten.

#### <a name="to-apply-a-filter-to-the-list-of-entries-in-a-tile"></a>So wenden Sie einen Filter auf die Listeneinträge in Kacheln an

1.  Öffnen Sie eine Rollen-oder Server Gruppenseite in Server-Manager.

2.  Geben Sie im Textfeld **Filter** auf der Kachel Ereignisse, Leistung, Best Practices Analyzer, Dienste oder Rollen und Features eine Zeichenfolge ein, nach der Sie filtern möchten.

    Wenn Sie z. b. nur Ereignisse mit der Ereignis-ID 1014 anzeigen möchten, geben Sie im **Filter** Textfeld **1014** ein. Alle gesammelten Ereignisse, in denen die Zeichenfolge **1014** in mindestens einem Feld enthalten ist, werden als Ergebnisse zurückgegeben.

3.  Hinweis: Der Filter ändert die Beschreibung unter dem Titel der Kachel. Anstelle von **Alle** steht nun **Gefilterte Ergebnisse**.

4.  Um den Filter zu löschen, löschen Sie die Zeichenfolge im Filterfeld, oder klicken Sie auf **X**.

## <a name="sort-list-entries-in-tiles"></a><a name=BKMK_sort></a>Sortieren von Listeneinträgen in Kacheln
Sortieren Sie die Listeneinträge in Server-Manager Kacheln durch Klicken auf Spaltenüberschriften. Durch einmaliges Klicken auf eine Spaltenüberschrift werden die Spaltenwerte in aufsteigender alphanumerischer Reihenfolge sortiert (Pfeil zeigt nach oben). Durch erneutes Klicken werden die Spaltenwerte in absteigender alphanumerischer Reihenfolge sortiert (Pfeil zeigt nach unten).

## <a name="create-and-run-custom-queries-on-tile-data"></a><a name=BKMK_query></a>Erstellen und Ausführen benutzerdefinierter Abfragen für Kachel Daten
In den Kacheln Ereignisse, Leistung, Best Practices Analyzer, Dienste oder Rollen und Features in Server-Manager können Sie benutzerdefinierte Abfragen erstellen. Der Bereich der Kachel Symbolleiste, in dem Sie Kriterien zum Erstellen einer benutzerdefinierten Abfrage auswählen, ist standardmäßig ausgeblendet. Klicken Sie auf **erweitern** (Chevron-Schaltfläche am rechten Rand der Kachel Symbolleiste), um die Abfrage Kriterien anzuzeigen.

#### <a name="to-create-a-custom-query-for-tile-data"></a>So erstellen Sie eine benutzerdefinierte Abfrage für Kacheldaten

1.  Öffnen Sie eine Rollen-oder Server Gruppenseite in Server-Manager.

2.  Erweitern Sie auf der Kachel Ereignisse, Leistung, Best Practices Analyzer, Dienste oder Rollen und Features den Bereich Abfrage-Building, indem Sie auf **erweitern**klicken.

3.  Klicken Sie auf **Kriterien hinzufügen** , um eine Liste mit Attributen (oder Feldern) zu öffnen, die auf die Einträge in der Kachel angewendet werden.

4.  Wählen Sie Kriterien zum Hinzufügen aus. Wenn Sie fertig sind, klicken Sie auf **Hinzufügen**. Die ausgewählten Kriterien werden dem Bereich zum Erstellen von Abfragen hinzugefügt.

5.  Klicken Sie auf den Hypertextoperator, um einen Operator auszuwählen. Der Standardoperator für numerische Kriterien bzw. datums- und uhrzeitbezogene Kriterien ist **Kleiner oder gleich**.

6.  Geben Sie akzeptable Werte für die Kriterien ein. Wenn Sie z. b. **Datum und Uhrzeit**ausgewählt haben, geben Sie ein Datum im Format *m/d/yyyy*an.

7.  Wiederholen Sie die Schritte ab Schritt 3, um der Abfrage weitere Kriterien hinzuzufügen.

    Sie können Kriterien, die bereits in der Abfrage vorhanden sind, duplizieren. Die Duplikate werden der Abfrage jedoch mit dem Operator **oder** hinzugefügt.

    Wenn Sie z. b. die Ereignis-IDs 1003 oder 1014 Abfragen möchten, fügen Sie zuerst die ID-Kriterien zu Ihrer Abfrage hinzu, legen Sie den Wert der ID auf **1003**fest, und fügen Sie dann der Abfrage ein zweites ID-Kriterium hinzu, wobei der Wert der zweiten ID **1014**entspricht. Sie erhalten die Abfrage **und ID gleich 1003 oder ID gleich 1014**.

8.  Klicken Sie nach dem Hinzufügen der Kriterien und der Angabe der Operatoren und Werte auf **Speichern**, um die Abfrage zu speichern.

9. Geben Sie einen Anzeigenamen für die Abfrage an. Beispielsweise können Sie die im zuvor beschriebenen Schritt erstellte Abfrage **Lizenzierungsereignisse** nennen.

10. Klicken Sie nach dem Anzeigen der Ergebnisse auf **Alle löschen**, um alle Filter und Abfragen zu löschen und alle Listeneinträge anzuzeigen

11. Um eine gespeicherte Abfrage auszuführen, klicken Sie auf **Gespeicherte Suchabfragen**, und klicken Sie auf den Namen der gespeicherten Abfragen, die Sie ausführen möchten.

12. Um eine gespeicherte Abfrage zu löschen, klicken Sie auf **Gespeicherte Suchabfragen**, und klicken Sie auf **X** neben dem Namen der gespeicherten Abfragen, die Sie löschen möchten.

## <a name="see-also"></a>Weitere Informationen
[Server-Manager](server-manager.md) 
 [Anzeigen und Konfigurieren von Leistungs-, Ereignis-und Dienst Daten](view-and-configure-performance-event-and-service-data.md)



