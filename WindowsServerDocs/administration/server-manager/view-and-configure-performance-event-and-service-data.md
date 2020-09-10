---
title: Anzeigen und Konfigurieren von Leistungs Ereignis-und Dienst Daten
description: Server-Manager
ms.topic: article
ms.assetid: ccd59c35-4dbf-48e7-88a4-c519c00184d1
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 8489c50c66bdba84078c7e5d75338af3eeeea56f
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627760"
---
# <a name="view-and-configure-performance-event-and-service-data"></a>Anzeigen und Konfigurieren von Leistungs-, Ereignis- und Dienstdaten

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird beschrieben, wie Sie die Ereignisprotokoll Einträge, Leistungsindikatoren und Dienst Warnungen anzeigen und konfigurieren, die für lokale und Remote Server in Server-Manager angezeigt werden.

Ereignis-, Dienst-und Leistungs Protokolldaten werden an zwei Stellen in der Server-Manager-Konsole in Windows Server angezeigt.

-   Auf dem Dashboard können Sie auf die Zeilen **Ereignisse**, **Leistung**und **Dienste** klicken, um die Ereignis-, Leistungs-und Dienst Protokolldaten zu konfigurieren, die Sie für Rollen, den gesamten Server-Manager Server Pool, vom Benutzer erstellte Server Gruppen und den lokalen Server anzeigen möchten. Durch Klicken auf die Textzeilen werden die Dialogfelder **Detailansicht** geöffnet, in denen Sie die Daten angeben können, über die Sie im Dashboard benachrichtigt werden möchten. Nachdem Sie die Ereignis-, Dienst-und Leistungs Protokolldaten konfiguriert haben, die in den Miniaturansichten des Dashboards hervorgehoben werden sollen, werden Protokolleinträge, die den angegebenen Kriterien entsprechen, unten in den Dialogfeldern **Detailansicht** aufgelistet.

-   Die Kacheln **Ereignisse**, **Dienste** und **Leistung** sind Teil der Rollen- und Gruppen-Homepages. Mit den Befehlen im Menü **Aufgaben** dieser Kacheln können Sie die Daten angeben, die Sie von verwalteten Servern sammeln möchten. Die Kacheln enthalten Filter und Abfragen, mit denen die in der Kachel angezeigten Protokolleinträge weiter eingeschränkt werden können, sofern dies gewünscht wird.

Dieses Thema enthält folgende Abschnitte:

-   [Was sind Miniaturansichten?](#BKMK_thumb)

-   [Anzeigen und Konfigurieren von Ereignissen](#BKMK_events)

-   [Anzeigen und Konfigurieren von Leistungsindikatoren](#BKMK_perf)

-   [Verwalten von Diensten und Konfigurieren von Dienstbenachrichtigungen](#BKMK_services)

-   [Anzeigen und Kopieren von Ereignis- und Leistungseinträgen](#BKMK_copy)

## <a name="what-are-thumbnails"></a><a name=BKMK_thumb></a>Was sind Miniaturansichten?
*Miniaturansichten* werden auf dem Server-Manager-Dashboard für jede Rolle angezeigt (die Miniaturansicht einer Rolle spiegelt die gesammelten Daten zu allen Servern im Server-Manager Pool wider, auf denen die Rolle ausgeführt wird), für jede Server Gruppe, für die Gruppe **alle** Server (alle Server im Server-Manager Pool) und für den lokalen Server. Nachdem Server-Manager Daten von verwalteten Servern abgerufen hat, werden für Rollen, die auf Servern im Server Pool ausgeführt werden, automatisch Miniaturansichten erstellt.

Wenn die Server-Manager-Konsole im Rahmen Remoteserver-Verwaltungstools auf einem Client Computer ausgeführt wird, gibt es keine Miniaturansicht für den **lokalen Server** .

Die Miniaturansicht zeigt eine kurze Übersicht über den Status und die Verwaltbarkeit von Rollen, Servern und Servergruppen. Die Farbe der Zeile für die Miniaturansicht-Überschrift ändert sich (und hervorgehobene Zahlen werden am linken Rand angezeigt), wenn Ereignisse, Leistungsindikatoren, Best Practices Analyzer Ergebnisse, Dienste oder allgemeine verwaltbarkeitsprobleme Kriterien erfüllen, die Sie in den durch Klicken auf Miniatur Ansichts Zeilen geöffneten Dialogfeldern der **Detailansicht** konfigurieren. In der folgenden Tabelle werden die in den Miniaturansichten angezeigten Daten erläutert.

|Miniaturansichtszeile|BESCHREIBUNG|
|---------|--------|
|Verwaltbarkeit|Die Verwaltbarkeit eines Servers umfasst mehrere Measures: ob der Server Online oder offline ist, ob auf ihn zugegriffen werden kann und welche Daten Server-Manager werden, ob der Benutzer, der am lokalen Computer angemeldet ist, über ausreichende Benutzerrechte für den Zugriff auf den Remote Server verfügt und ob auf dem Remote Server die gesamte für die Remote Verwaltung erforderliche Software verfügbar ist. oder, ob der Server so konfiguriert wurde, dass er mit Server-Manager abgefragt und verwaltet werden kann. Die einzigen verwaltbarkeitsdaten, die Server-Manager von einem Server, auf dem Windows Server 2003 ausgeführt wird, erfassen können, ist, ob der Server Online oder offline ist. Ausführliche Informationen zu verwaltbarkeitsstatusfehlern und deren Behebung finden Sie im [Server-Manager Forum](/answers/topics/windows-server-manager.html).|
|Events|Sie können die Zeile **Ereignisse** einer Miniaturansicht so konfigurieren, dass Benachrichtigungen angezeigt werden, wenn Ereignisse mit den von Ihnen angegebenen Schweregraden, Quellen, Zeiträumen, Servern oder Ereignis-IDs protokolliert werden. Zeigen Sie Details zu Ereignissen an, und ändern Sie die Warnungen, die Sie anzeigen möchten, indem Sie auf die Zeile **Ereignisse** klicken und das Dialogfeld **Detailansicht Ereignisse** für die Rolle oder Server Gruppe öffnen.|
|Dienste|Sie können die Zeile **Dienste** so konfigurieren, dass Warnungen angezeigt werden, wenn Dienste in einer Rolle oder Server Gruppe gefunden werden, die Start Typen, Dienststatus, Dienstnamen und Servern entsprechen, die Sie im Dialogfeld **Dienst Detailansicht** angeben.<p>Nachdem ein Server dem Server-Manager-Server Pool hinzugefügt wurde, können Dienst Warnungen zum Dienst für die Shellhardwareerkennung angezeigt werden, wenn keine Benutzer am verwalteten Server angemeldet sind. Dies geschieht, weil der Dienst für die Shellhardwareerkennung nur ausgeführt wird, wenn Benutzer am verwalteten Server angemeldet oder mit einer Remotedesktopsitzung auf dem verwalteten Server verbunden sind. Damit in diesem Fall keine Shellhardwareerkennung-Dienstwarnungen angezeigt werden, klicken Sie in den Miniaturansichten für Servergruppen, einschließlich der Gruppe **Alle Server**, auf **Dienste**. Deaktivieren Sie im Dialogfeld **Dienst Detailansicht** in der Dropdown Liste **Dienste** das Kontrollkästchen für **Shellhardwareerkennung**, und klicken Sie dann auf **OK**.|
|Leistung|Sie können die Zeile **Leistung** so konfigurieren, dass Warnungen für eine Rolle oder Server Gruppe angezeigt werden, wenn Leistungs Warnungen auftreten, die Ressourcentypen, Servern oder Zeiträumen entsprechen, die Sie im Dialogfeld **Leistungs Detailansicht** angeben.<p>Leistungsindikatoren sind standardmäßig deaktiviert. Verwaltete Server, auf denen Betriebssysteme ausgeführt werden, die neuer als Windows Server 2003 sind und für die keine Leistungsindikatoren gestartet wurden, zeigen normalerweise verwaltbarkeitsstatusfehler von **Online-Leistungsindikatoren** , die auf der Kachel **Server** der Rollen-oder Gruppen Seiten nicht gestartet sind, an. Um die Leistungsindikatoren für verwaltete Server zu aktivieren, klicken Sie auf der Seite **alle Server** mit der rechten Maustaste auf Einträge auf der Kachel **Leistung** , die den Indikator **Status** Wert **aus**anzeigt, und klicken Sie dann auf **Leistungsindikatoren starten**. Sie können Leistungsindikatoren auch starten, indem Sie in der Kachel **Server** der Rollen-oder Gruppen Seiten mit der rechten Maustaste auf Einträge für Server klicken und dann auf **Leistungsindikatoren starten**klicken.|
|BPA-Ergebnisse|Sie können die Zeile **BPA-Ergebnisse** so konfigurieren, dass Warnungen für eine Rolle oder Server Gruppe angezeigt werden, wenn BPA-Scanergebnisse gefunden werden, die Schweregraden, Servern oder BPA-Kategorien entsprechen, die Sie im Dialogfeld mit der **BPA-Ergebnis Detailansicht** angeben.|

## <a name="view-and-configure-events"></a><a name=BKMK_events></a>Anzeigen und Konfigurieren von Ereignissen
In diesem Abschnitt erfahren Sie, wie Sie konfigurieren können, welche Ereignisprotokoll Daten von den Servern im Server-Manager Server Pool gesammelt werden und welche Ereignisse Sie in den Miniaturansichten hervorheben möchten.

> [!NOTE]
> Die Ereignisse, über die Sie in den Miniaturansichten benachrichtigt werden, sind eine Teilmenge der Gesamt Ereignisse, die Sie anweisen, Server-Manager von verwalteten Servern zu erfassen. Obwohl das Ändern von Ereignis Kriterien im Dialogfeld **Ereignisdaten konfigurieren** in den Kacheln **Ereignisse** die Anzahl der Warnungen ändern kann, die auf dem Server-Manager-Dashboard angezeigt werden, wirkt sich das Ändern der Kriterien für Ereignis Warnungen in den Miniaturansichten nicht auf die Ereignisprotokoll Daten aus, die von den verwalteten Servern gesammelt werden.

#### <a name="to-configure-the-events-collected-from-managed-servers"></a>So konfigurieren Sie Ereignisse, die von verwalteten Servern gesammelt werden

1.  Öffnen Sie in der Server-Manager Konsole eine beliebige Seite außer dem Dashboard. Sie können die Ereignisse, die Sie von den verwalteten Servern sammeln möchten, in der Kachel **Ereignisse** auf der Seite der entsprechenden Rolle, Servergruppe oder des lokalen Servers konfigurieren.

2.  Klicken Sie in der Kachel **Ereignisse** im Menü **Aufgaben** auf **Ereignisdaten konfigurieren**.

3.  Wählen Sie die Ereignis Schweregrade aus, die von den Servern in der ausgewählten Gruppe gesammelt werden sollen. Standardmäßig sind die Schweregrade **Kritisch**, **Fehler** und **Warnung** ausgewählt.

4.  Geben Sie einen Zeitraum an, in dem die Ereignisse auftreten. Das Standardalter für Ereignisse beträgt 24 Stunden.

5.  Wählen Sie die Ereignisprotokoll Dateien aus, aus denen die Ereignisse gesammelt werden sollen. Die Standardwerte sind **Anwendung**, **Setup** und **System**.

6.  Klicken Sie zum Speichern der Änderungen auf **OK**, um das Dialogfeld **Ereignisdaten konfigurieren** zu schließen. Ereignisdaten werden automatisch aktualisiert, wenn Ihre Änderungen gespeichert werden.

#### <a name="to-configure-the-events-highlighted-in-thumbnails"></a>So konfigurieren Sie die Ereignisse, die in Miniaturansichten hervorgehoben werden

1.  Wenn Server-Manager bereits geöffnet ist, fahren Sie mit dem nächsten Schritt fort. Ist der Server-Manager noch nicht geöffnet, öffnen Sie ihn mit einer der folgenden Aktionen.

    -   Starten Sie auf dem Windows-Desktop den Server-Manager, indem Sie in der Windows-Taskleiste auf **Server-Manager** klicken.

    -   Klicken Sie auf dem Windows- **Start** Bildschirm auf die Kachel Server-Manager.

2.  Klicken Sie auf der Dashboardseite in der Kachel **Rollen und Servergruppen** in einer Miniaturansicht auf die Zeile **Ereignisse**.

3.  Fügen Sie im Dialogfeld **Ereignis Detailansicht** den Ereignissen, die Sie anzeigen möchten, einen Schweregrad hinzu. Standardmäßig werden in der Miniaturansicht nur Warnungen zu kritischen Ereignissen hervorgehoben. Beachten Sie, dass die Anzahl der im Dialogfeld **Detailansicht** angezeigten Ereignisse zunimmt, wenn Sie einen Schweregrad hinzufügen, über den Sie benachrichtigt werden möchten.

4.  Wählen Sie im Feld **Ereignisquellen** die Ereignisquellen aus, über die Sie benachrichtigt werden möchten. Die Standardeinstellung ist **Alle**.

5.  Wenn diese Miniaturansicht für eine Rolle gilt, die auf mehreren Servern oder einer Gruppe von mehreren Servern installiert ist, können Sie die Server, für die Sie Ereignis Warnungen erhalten möchten, in der Dropdown Liste **Server** auswählen.

6.  Geben Sie **im Feld Zeitraum** einen Zeitraum von bis zu 1440 Minuten, 24 Stunden oder 1 Tag an.

7.  Geben Sie im Feld **Ereignis-IDs** die Ereignis-IDs bestimmter Ereignisse an, über die Sie benachrichtigt werden möchten. Sie können einen Bereich von Ereignis-IDs getrennt durch einen Bindestrich ( **-** ) eingeben und Ereignis-IDs aus dem Bereich ausschließen, indem Sie den Bindestrich vor der Ereignis-ID oder dem Bereich von Ereignis-IDs eingeben, die Sie ausschließen möchten. Beispielsweise bedeutet der Wert **1,3,5-99,-76**, dass Warnungen für die Ereignis-IDs 1,3,5-99 und 76 und für alle Ereignisse-IDs zwischen 1 und 3 ausgelöst werden, mit Ausnahme von Ereignis-ID 5.

8.  Wenn Sie die Kriterien dafür ändern, welche Warnungen angezeigt werden, ändert sich möglicherweise die Anzahl der Ereigniswarnungen, die im Ergebnisbereich unten im Dialogfeld angezeigt werden. Wählen Sie Einträge in der Liste aus, und klicken Sie auf **Warnungen ausblenden** , um zu verhindern, dass die Anzahl der in der Quell Miniaturansicht angezeigten Warnungen beeinträchtigt wird. Halten Sie bei der Auswahl der Warnungen die **STRG**-Taste gedrückt, um mehrere Warnungen gleichzeitig auszuwählen. Sie können Warnungen ausblenden, die Ihren Warnkriterien entsprechen, die Sie jedoch nicht anzeigen lassen möchten.

9. Klicken Sie auf **Alle anzeigen**, um ausgeblendete Warnungen wieder in der Liste sichtbar zu machen.

10. Klicken Sie auf **OK** , um die Änderungen zu speichern, das Dialogfeld **Detailansicht** zu schließen und die Änderungen an den Ereignis Warnungen in der Quell Miniaturansicht anzuzeigen.

## <a name="view-and-configure-performance-log-data"></a><a name=BKMK_perf></a>Anzeigen und Konfigurieren von Leistungsprotokolldaten
In diesem Abschnitt erfahren Sie, wie Sie konfigurieren können, welche Leistungs Protokolldaten von den Servern im Server-Manager Server Pool gesammelt werden und welche Leistungs Warnungs Warnungen Sie in den Miniaturansichten hervorheben möchten.

Leistungsindikatoren sind standardmäßig deaktiviert. Verwaltete Server, auf denen Betriebssysteme ausgeführt werden, die neuer als Windows Server 2003 sind und für die keine Leistungsindikatoren gestartet wurden, zeigen normalerweise verwaltbarkeitsstatusfehler von **Online-Leistungsindikatoren** , die auf der Kachel **Server** der Rollen-oder Gruppen Seiten nicht gestartet sind, an. Um die Leistungsindikatoren für verwaltete Server zu aktivieren, klicken Sie auf der Seite **alle Server** mit der rechten Maustaste auf Einträge auf der Kachel **Leistung** , die den Indikator **Status** Wert **aus**anzeigt, und klicken Sie dann auf **Leistungsindikatoren starten**. Sie können Leistungsindikatoren auch starten, indem Sie in der Kachel **Server** der Rollen-oder Gruppen Seiten mit der rechten Maustaste auf Einträge für Server klicken und dann auf **Leistungsindikatoren starten**klicken.

> [!NOTE]
> Die Leistungs Warnungen, die Sie in den Miniaturansichten anzeigen, sind eine Teilmenge der gesamten Leistungsdaten, die Sie anweisen, Server-Manager von verwalteten Servern zu erfassen. Obwohl das Ändern der Kriterien für die Leistungs Warnung im Dialogfeld **Leistungs Warnungen konfigurieren** in den Kacheln **Leistung** die Anzahl der Warnungen ändern kann, die auf dem Server-Manager-Dashboard angezeigt werden, hat das Ändern der Kriterien für die Leistungs Warnung in den Miniaturansichten keine Auswirkung auf die Leistungs Protokolldaten, die von verwalteten Servern gesammelt werden.
>
> Aus diesem Grund kann das maximale Alter von Leistungsdaten, die Sie in den Miniaturansichten anzeigen können, nicht größer als der maximale Zeitraum der Diagrammanzeige sein, der im Dialogfeld **Leistungswarnungen konfigurieren** konfiguriert ist. Wenn der Wert des **Diagramms für die Diagramm Anzeige** in **Leistungs Warnungen konfigurieren** z. b. **1 Tag**ist, kann der Maximalwert für **das Feld Zeitraum** im Dialogfeld mit der **Leistungs Detailansicht** , das Sie über das Server-Manager Dashboard geöffnet haben, **1 Tag**, **24 Stunden**oder **1.440 Minuten**sein.

#### <a name="to-configure-the-performance-log-data-collected-from-managed-servers"></a>So konfigurieren Sie die Leistungsprotokolldaten, die von den verwalteten Servern gesammelt werden

1.  Öffnen Sie in der Server-Manager Konsole eine beliebige Seite außer dem Dashboard. Sie können die Leistungsdaten, die Sie von den verwalteten Servern sammeln möchten, in der Kachel **Leistung** auf der Seite der entsprechenden Rolle, Servergruppe oder des lokalen Servers konfigurieren.

2.  Um Leistungsprotokolldaten von verwalteten Servern sammeln zu können, müssen die Leistungsindikatoren aktiviert sein. Wenn die Leistungsindikatoren ausgeschaltet sind, klicken Sie mit der rechten Maustaste auf einen Eintrag in der Kachel **Leistung** , und klicken Sie dann auf **Leistungsindikatoren starten**. Das Sammeln von Leistungsindikatordaten kann einige Zeit in Anspruch nehmen, je nach der Anzahl der Server, von denen die Daten gesammelt werden, und der zur Verfügung stehenden Netzwerkbandbreite. Zeigen Sie den Status in der Spalte **Zählerstatus** an.

3.  Klicken Sie im Menü **Aufgaben** der Kachel **Leistung** auf **Leistungswarnungen konfigurieren**.

4.  Geben Sie für die Server in der ausgewählten Gruppe oder, auf denen die ausgewählte Rolle ausgeführt wird, an, in welchem Prozentsatz der CPU-Auslastung von Server-Manager Warnungen gesammelt werden sollen. Der Standardwert liegt bei 85 %.

5.  Geben Sie den verbleibenden verfügbaren Arbeitsspeicher in Megabyte an, den die Server haben sollen, bevor Leistungsindikatorwarnungen gesammelt werden. Der Standardwert ist 2 MB.

6.  Geben Sie für die Ressourcen **CPU-Auslastung** und **Verfügbarer Arbeitsspeicher** in der Kachel **Leistung** einen Zeitraum, der in den Diagrammen widergespiegelt werden soll. Der Standardzeitraum ist ein Tag. Klicken Sie auf **Speichern**.

    Beachten Sie, dass sich die Anzahl der Leistungswarnungen in der Kachel **Leistung** und die im Diagramm dargestellte Zuordnung der Warnungen im Zeitverlauf ändern können, nachdem Sie auf **Speichern** geklickt haben.

    > [!NOTE]
    > bei virtuellen Maschinen, für die [dynamischer Arbeitsspeicher](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff817651(v=ws.10)) aktiviert ist, kann das Erhöhen des Schwellenwerts für die Leistungs Warnungen zu falsch positiven Warnungen führen.

7.  Klicken Sie im Menü **Aufgaben** auf **Aktualisieren**, um die Liste der Leistungswarnungen zu aktualisieren, die von den Servern gesammelt werden.

#### <a name="to-configure-the-performance-alerts-highlighted-in-thumbnails"></a>So konfigurieren Sie sie Leistungswarnungen, die in den Miniaturansichten hervorgehoben werden

1.  Klicken Sie auf der Dashboardseite in der Kachel **Rollen und Servergruppen** in einer Miniaturansicht auf die Zeile **Leistung**.

2.  Aktivieren bzw. deaktivieren Sie im Dialogfeld **Leistungs Detailansicht** im Feld **Ressourcentyp** die Kontrollkästchen für Ressourcen Leistungs Schwellenwerte, über die Sie benachrichtigt werden möchten. Beachten Sie, dass sich die Anzahl der im Dialogfeld **Detailansicht** angezeigten Leistungs Warnungen erhöhen kann, wenn Sie einen Schwellenwert für die Ressourcen Leistung hinzufügen, über den Sie benachrichtigt werden möchten.

3.  Wenn diese Miniaturansicht für eine Rolle gilt, die auf mehreren Servern oder einer Gruppe von mehreren Servern installiert ist, können Sie die Server, für die Sie Leistungs Warnungen erhalten möchten, in der Dropdown Liste **Server** auswählen.

4.  Geben Sie **im Feld Zeitraum** einen Zeitraum von bis zu 1440 Minuten, 24 Stunden oder 1 Tag an.

5.  Wenn Sie die Kriterien dafür ändern, welche Warnungen angezeigt werden, ändert sich möglicherweise die Anzahl der Warnungen, die im Ergebnisbereich unten im Dialogfeld angezeigt werden. Klicken Sie auf **Warnungen ausblenden**, um alle Warnungen auszublenden, die sich nicht auf den aktuellen Zeitpunkt beziehen. Sie wirken sich dann nicht auf die Anzahl der Warnungen aus, die in der Quellminiaturansicht angezeigt wird.

6.  Klicken Sie auf **Alle anzeigen**, um ausgeblendete Warnungen wieder in der Liste sichtbar zu machen.

7.  Klicken Sie auf **OK** , um die Änderungen zu speichern. Schließen Sie das Dialogfeld **Detailansicht** , und zeigen Sie die Änderungen der Leistungs Warnung in der Quell Miniaturansicht an.

#### <a name="to-view-the-properties-of-performance-alerts"></a>So zeigen Sie die Eigenschaften der Leistungswarnungen an

1.  Führen Sie einen der folgenden Schritte aus:

    -   Klicken Sie auf der Dashboardseite in der Kachel **Rollen und Servergruppen** in einer Miniaturansicht auf die Zeile **Leistung**.

    -   Öffnen Sie die Homepage einer Rolle oder Gruppe, und suchen Sie nach der Kachel **Leistung** für die Rolle oder Gruppe.

2.  Doppelklicken Sie auf eine Leistungswarnung in der Liste, um die dazugehörigen Eigenschaften anzuzeigen. Alternativ können Sie mit der rechten Maustaste auf eine Leistungswarnung klicken und dann **Eigenschaften anzeigen** auswählen.

3.  Wählen Sie im Dialogfeld **Leistungsalarmeigenschaften** Protokolleinträge aus, um Informationen über die Prozesse anzuzeigen, die mit dem Eintrag im Bereich **Prozesse** verknüpft sind.

4.  Wenn Sie die Leistungsalarmeigenschaften geprüft haben, schließen Sie das Dialogfeld.

### <a name="analyze-performance-data-and-solve-problems"></a>Analyse von Leistungsdaten und Problembehebung
Weitere Informationen zum Analysieren von Leistungsdaten in Server-Manager und zur Behebung von Leistungsproblemen auf verwalteten Servern finden Sie in den folgenden Ressourcen.

-   [Analysieren von Leistungsdaten](https://go.microsoft.com/fwlink/?LinkId=239829)

-   [Behebung von Leistungsproblemen](https://go.microsoft.com/fwlink/?LinkId=239831)

Weitere Informationen zu erweiterten Tools für die Leistungsüberwachung und-Analyse, die für Windows Server 2012 und spätere Versionen von Windows Server verfügbar sind, einschließlich Server Performance Advisor 3,0, finden Sie unter Performance on MSDN ( [Leistung](/previous-versions/windows/hardware/design/dn614608(v=vs.85)) auf MSDN).

## <a name="manage-services-and-configure-service-alerts"></a><a name=BKMK_services></a>Verwalten von Diensten und Konfigurieren von Dienstbenachrichtigungen
In diesem Abschnitt erfahren Sie, wie Sie Dienste starten, anhalten, neu starten, anhalten oder fortsetzen, die auf den Rollen-und Server Gruppen Seiten in Server-Manager auf der Kachel **Dienste** angezeigt werden. Sie können auch die Dienste konfigurieren, über die Sie in den Miniaturansichten auf dem Server-Manager-Dashboard benachrichtigt werden.

> [!NOTE]
> Der Starttyp für Dienste, Dienst Abhängigkeiten, Wiederherstellungsoptionen oder andere Dienst Eigenschaften kann auf der Kachel Dienste in Server-Manager nicht geändert werden. Wenn Sie andere Diensteigenschaften als den Dienststatus ändern möchten, öffnen Sie das Snap-In **Dienste**. Eine Verknüpfung zum Öffnen des Snap-Ins " **Dienste** " ist im Menü " **Tools** " in Server-Manager verfügbar.

#### <a name="to-start-stop-restart-pause-or-resume-a-service"></a>So können Sie Dienste starten, beenden, neu starten, anhalten und fortsetzen

1.  Öffnen Sie in der Server-Manager Konsole eine beliebige Seite außer dem Dashboard (d. h. eine beliebige Rollen-oder Gruppen Startseite).

2.  Klicken Sie in der Kachel **Dienste** für die Rolle oder Gruppe mit der rechten Maustaste auf einen Dienst.

3.  Klicken Sie im Kontextmenü auf die gewünschte Aktion, mit der dieser Dienst ausgeführt werden soll. Wurde der Dienst beendet, ist die einzige Aktion, die Sie ausführen können, den Dienst zu starten. Wird der Dienst angehalten, ist dementsprechend die einzige Aktion, die Sie ausführen können, den Dienst fortzusetzen.

4.  Beachten Sie, dass sich der Wert der Spalte **Status** für den in der Kachel **Dienste** ausgewählten Dienst ändert, wenn Sie einen Dienst starten, stoppen, neu starten, anhalten oder fortsetzen.

#### <a name="to-configure-service-alerts-highlighted-in-thumbnails"></a>So konfigurieren Sie die Dienstbenachrichtigungen, die in Miniaturansichten hervorgehoben werden

1.  Klicken Sie auf der Dashboardseite in der Kachel **Rollen und Servergruppen** in einer Miniaturansicht auf die Zeile **Dienste**.

2.  Wählen Sie im Dialogfeld **Dienst Detailansicht** die Start Typen für Dienste aus, über die Sie benachrichtigt werden möchten. Standardmäßig sind **automatisch (verzögerter Start)** und **automatisch** ausgewählt.

3.  Wählen Sie die Dienststatus aus, über die Sie benachrichtigt werden möchten. Standardmäßig ist **Alle** ausgewählt.

4.  Wählen Sie Dienste aus, über die Sie benachrichtigt werden möchten. Standardmäßig ist **Alle** ausgewählt.

5.  Wählen Sie die Server aus, die der Rolle oder Gruppe zugeordnet sind, für die Sie Warnungen zu Diensten erhalten möchten. Standardmäßig ist **Alle** ausgewählt.

6.  Wenn Sie die Kriterien dafür ändern, welche Warnungen angezeigt werden, ändert sich möglicherweise die Anzahl der Warnungen, die im Ergebnisbereich unten im Dialogfeld angezeigt werden. Klicken Sie auf **Warnungen ausblenden**, um alle Warnungen auszublenden, die sich nicht auf den aktuellen Zeitpunkt beziehen. Sie wirken sich dann nicht auf die Anzahl der Warnungen aus, die in der Quellminiaturansicht angezeigt wird.

7.  Klicken Sie auf **Alle anzeigen**, um ausgeblendete Warnungen wieder in der Liste sichtbar zu machen.

8.  Klicken Sie auf **OK** , um die Änderungen zu speichern, das Dialogfeld **Detailansicht** zu schließen und die Änderungen an den Dienst Warnungen in der Quell Miniaturansicht anzuzeigen.

## <a name="view-and-copy-event-service-or-performance-entries"></a><a name=BKMK_copy></a>Anzeigen und Kopieren von Ereignis-, Dienst- oder Leistungseinträgen
Sie können in den Dialogfeldern **Detailansicht** und in den Kacheln **Ereignisse** und **Leistung** für eine Rolle oder eine Gruppe Eigenschaften für Ereignis-, Dienst-oder Leistungs Einträge kopieren. Klicken Sie mit der rechten Maustaste auf einen Ereignis-oder leistungseintrag, und klicken Sie auf **Kopieren**.

Über die Kachel **Ereignisse** können Sie auch in der unteren Hälfte der Kachel Ereigniseigenschaften in der Vorschau anzeigen, indem Sie in der Liste einen Eintrag auswählen. Zum Kopieren der in der Vorschau angezeigten Eigenschaften klicken Sie mit der rechten Maustaste auf den Vorschaubereich, und klicken Sie dann auf **Kopieren**.

## <a name="see-also"></a>Weitere Informationen
[Server-Manager](server-manager.md) 
 [Filtern, Sortieren und Abfragen von Daten in Server-Manager Kacheln](filter-sort-and-query-data-in-server-manager-tiles.md)