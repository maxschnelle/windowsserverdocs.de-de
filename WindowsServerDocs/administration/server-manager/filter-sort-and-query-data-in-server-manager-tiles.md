---
title: Filtern, Sortieren und Abfragen von Daten in Server-Manager-Kacheln
description: Server-Manager
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8786f791-73e5-4c75-8d12-46e88a196976
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 51c0e1f3af727c4e7ddf18024fab9a95808d2338
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868911"
---
# <a name="filter-sort-and-query-data-in-server-manager-tiles"></a>Filtern, Sortieren und Abfragen von Daten in Server-Manager-Kacheln

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

In Windows Server-Kacheln in Server-Manager können Sie filtern und Sortieren von Daten, und erstellen und Speichern von benutzerdefinierten Abfragen. Sie können zu sortieren, Schlüsselwörtern filtern und Ausführen von Abfragen für Listeneinträge in den Kacheln für Ereignisse, Leistung, Best Practices Analyzer, Services, sowie Rollen und Features auf Server Rollen- oder Gruppenseiten in Server-Manager.  
  
Dieses Thema enthält die folgenden Abschnitte:  
  
-   [Filtern von Listeneinträgen in Kacheln](#BKMK_tiles)  
  
-   [Sortieren von Listeneinträgen in Kacheln](#BKMK_sort)  
  
-   [Erstellen Sie und führen Sie benutzerdefinierter Abfragen für Kacheldaten aus](#BKMK_query)  
  
## <a name="BKMK_tiles"></a>Filtern von Listeneinträgen in Kacheln  
Mit dem Textfeld **Filtern** können Sie die Liste der Einträge, die in einer Kachel angezeigt werden, schnell auf Einträge reduzieren, die eine bestimmte Zeichenfolge enthalten.  
  
#### <a name="to-apply-a-filter-to-the-list-of-entries-in-a-tile"></a>So wenden Sie einen Filter auf die Listeneinträge in Kacheln an  
  
1.  Öffnen Sie eine Rollen- oder Gruppenseite im Server-Manager.  
  
2.  In der **Filter** Geben Sie im Textfeld, einer Kachel Ereignisse, Leistung, Best Practices Analyzer, Dienste oder Rollen und Features, eine Zeichenfolge, die auf dem Sie filtern möchten.  
  
    Geben Sie beispielsweise, wenn Sie nur Ereignisse mit der Ereignis-ID 1014 anzeigen möchten, **1014** in die **Filter** Textfeld. Alle gesammelten Ereignisse, in denen die Zeichenfolge **1014** in mindestens einem Feld enthalten ist, werden als Ergebnisse zurückgegeben.  
  
3.  Hinweis: Der Filter ändert die Beschreibung unter dem Titel der Kachel. Anstelle von **Alle** steht nun **Gefilterte Ergebnisse**.  
  
4.  Um den Filter zu löschen, löschen Sie die Zeichenfolge im Filterfeld, oder klicken Sie auf **X**.  
  
## <a name="BKMK_sort"></a>Sortieren von Listeneinträgen in Kacheln  
Sortieren von Listeneinträgen in Kacheln von Server-Manager durch Klicken auf Spaltenüberschriften. Durch einmaliges Klicken auf eine Spaltenüberschrift werden die Spaltenwerte in aufsteigender alphanumerischer Reihenfolge sortiert (Pfeil zeigt nach oben). Durch erneutes Klicken werden die Spaltenwerte in absteigender alphanumerischer Reihenfolge sortiert (Pfeil zeigt nach unten).  
  
## <a name="BKMK_query"></a>Erstellen Sie und führen Sie benutzerdefinierter Abfragen für Kacheldaten aus  
Sie können benutzerdefinierte Abfragen erstellen, in den Kacheln für Ereignisse, Leistung, Best Practices Analyzer, Dienste oder Rollen und Features im Server-Manager. Standardmäßig ist der Bereich der kachelleiste, in dem Sie die Kriterien zum Erstellen einer benutzerdefinierten Abfrage auswählen, ausgeblendet. Klicken Sie auf **erweitern** (Chevron-Schaltfläche am rechten Rand der kachelleiste), die die Abfragekriterien anzuzeigen.  
  
#### <a name="to-create-a-custom-query-for-tile-data"></a>So erstellen Sie eine benutzerdefinierte Abfrage für Kacheldaten  
  
1.  Öffnen Sie eine Rollen- oder Gruppenseite im Server-Manager.  
  
2.  Erweitern Sie den Bereich zum Erstellen von Abfragen in einer Kachel, Ereignisse, Leistung, Best Practices Analyzer, Dienste oder Rollen und Features, durch Klicken auf **erweitern**.  
  
3.  Klicken Sie auf **Kriterien hinzufügen** , öffnen Sie eine Liste mit Attributen (oder Feldern), die auf die Einträge in der Kachel zutreffen.  
  
4.  die wählen Sie Kriterien zum Hinzufügen aus. Wenn Sie fertig sind, klicken Sie auf **hinzufügen**. Die ausgewählten Kriterien werden dem Bereich zum Erstellen von Abfragen hinzugefügt.  
  
5.  Klicken Sie auf den Hypertextoperator, um einen Operator auszuwählen. Der Standardoperator für numerische Kriterien bzw. datums- und uhrzeitbezogene Kriterien ist **Kleiner oder gleich**.  
  
6.  Geben Sie akzeptable Werte für die Kriterien ein. Bei Auswahl von beispielsweise **Datums- /**, geben Sie ein Datum im Format *dd.mm.yyyy*.  
  
7.  Wiederholen Sie die Schritte ab Schritt 3, um der Abfrage weitere Kriterien hinzuzufügen.  
  
    Sie können Kriterien, die bereits in der Abfrage vorhanden sind, duplizieren. Die Duplikate werden der Abfrage jedoch mit dem Operator **oder** hinzugefügt.  
  
    z. B. für die Abfrage nach den Ereignis-IDs 1003 oder 1014 Sie zuerst die ID-Kriterium zur Abfrage hinzufügen, stellen Sie den Wert der ID gleich **1003**, und klicken Sie dann ein zweites ID-Kriterium hinzufügen, um Ihrer Abfrage, die den Wert der zweiten ID gleich  **1014**. Sie erhalten die Abfrage **und ID gleich 1003 oder ID gleich 1014**.  
  
8.  Klicken Sie nach dem Hinzufügen der Kriterien und der Angabe der Operatoren und Werte auf **Speichern** , um die Abfrage zu speichern.  
  
9. Geben Sie einen Anzeigenamen für die Abfrage an. Beispielsweise können Sie die im zuvor beschriebenen Schritt erstellte Abfrage **Lizenzierungsereignisse** nennen.  
  
10. Klicken Sie nach dem Anzeigen der Ergebnisse auf **Alle löschen** , um alle Filter und Abfragen zu löschen und alle Listeneinträge anzuzeigen  
  
11. Um eine gespeicherte Abfrage auszuführen, klicken Sie auf **Gespeicherte Suchabfragen**, und klicken Sie auf den Namen der gespeicherten Abfragen, die Sie ausführen möchten.  
  
12. Um eine gespeicherte Abfrage zu löschen, klicken Sie auf **Gespeicherte Suchabfragen**, und klicken Sie auf **X** neben dem Namen der gespeicherten Abfragen, die Sie löschen möchten.  
  
## <a name="see-also"></a>Siehe auch  
[Server Manager](server-manager.md)  
[Anzeigen und Konfigurieren von Leistungs-, Ereignis- und Dienstdaten](view-and-configure-performance-event-and-service-data.md)  
  


