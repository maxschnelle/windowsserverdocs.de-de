---
title: Anzeigen und Konfigurieren von Leistungsereignissen und Dienstdaten
description: Server-Manager
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-server-manager
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ccd59c35-4dbf-48e7-88a4-c519c00184d1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 727b81d1ba2cda32a7568e4e2f23065b1589e745
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861901"
---
# <a name="view-and-configure-performance-event-and-service-data"></a>Anzeigen und Konfigurieren von Leistungs-, Ereignis- und Dienstdaten

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Dieses Thema beschreibt das Anzeigen und konfigurieren die Ereignisprotokolleinträge, Leistungsindikatoren und dienstwarnungen, die für lokale und Remoteserver im Server-Manager angezeigt werden.  

Leistungs-, Dienst- und Ereignis-Log-Daten werden an zwei Stellen in der Server-Manager-Konsole in Windows Server angezeigt.  

-   Auf dem Dashboard, klicken Sie auf die **Ereignisse**, **Leistung**, und **Services** Zeilen Ereignisprotokolldaten zu konfigurieren, um Leistungs-, und Service-Protokolldaten, die Sie anzeigen möchten für Rollen, den gesamten Serverpool des Server-Manager-, Benutzer erstellte Servergruppen und den lokalen Server. Durch Klicken auf die **Detailansicht** Dialogfeldern, mit denen Sie die Daten angegeben, über die Sie im Dashboard informiert werden möchten. Nach dem Konfigurieren-Ereignis, Dienst und die leistungsprotokolldaten, die in den Dashboard-Miniaturansichten hervorgehoben werden sollen, finden Sie Protokolleinträge, die den Kriterien entsprechen, Sie haben angegeben, am unteren Rand der **Detailansicht** Dialogfelder.  

-   Die Kacheln **Ereignisse**, **Dienste** und **Leistung** sind Teil der Rollen- und Gruppen-Homepages. Mit den Befehlen im Menü **Aufgaben** dieser Kacheln können Sie die Daten angeben, die Sie von verwalteten Servern sammeln möchten. Die Kacheln enthalten Filter und Abfragen, mit denen die in der Kachel angezeigten Protokolleinträge weiter eingeschränkt werden können, sofern dies gewünscht wird.  

Dieses Thema enthält die folgenden Abschnitte:  

-   [Was sind Miniaturansichten?](#BKMK_thumb)  

-   [Anzeigen und Konfigurieren von Ereignissen](#BKMK_events)  

-   [Anzeigen und Konfigurieren von Leistungsindikatoren](#BKMK_perf)  

-   [Dienste verwalten und Konfigurieren von dienstbenachrichtigungen](#BKMK_services)  

-   [Anzeigen und kopieren-Ereignis und leistungseinträgen](#BKMK_copy)  

## <a name="BKMK_thumb"></a>Was sind Miniaturansichten?  
*Miniaturansichten* werden angezeigt, auf dem Server-Manager-Dashboard für jede Rolle (die Miniaturansicht einer Rolle enthält die gesammelten Daten zu allen Servern im Server-Manager-Pool, der die Rolle ausgeführt werden) für jede Servergruppe, für die **alle Server** Gruppe (alle Server im Server-Manager-Pool), und für den lokalen Server. Nachdem der Server-Manager Daten von verwalteten Servern erhält, werden für Rollen, die auf Servern im Serverpool ausgeführt werden, automatisch Miniaturansichten erstellt.  

Wenn die Server-Manager-Konsole auf einem Clientcomputer als Teil der Remoteserver-Verwaltungstools ausgeführt wird, besteht keine **lokalen Server** Miniaturansicht.  

Die Miniaturansicht zeigt eine kurze Übersicht über den Status und die Verwaltbarkeit von Rollen, Servern und Servergruppen. Farbe für die Zeile mit der Überschrift der Miniaturansicht ändert (und hervorgehobene Zahlen werden in den linken Rand angezeigt) Wenn Ereignisse, Leistungsindikatoren, Best Practices Analyzer-Ergebnisse, Dienste oder allgemeine verfügbarkeitsaspekte Kriterien, die Sie in der konfigurieren**Detailansicht** Dialogfeldern durch Klicken auf miniaturansichtzeilen geöffnet. In der folgenden Tabelle werden die in den Miniaturansichten angezeigten Daten erläutert.  

|Miniaturansichtszeile|Beschreibung|  
|---------|--------|  
|Verwaltbarkeit|Die Verwaltbarkeit eines Servers umfasst verschiedene Maßnahmen: Gibt an, ob der Server online oder offline ist, ob sie Daten zugegriffen werden kann und reporting Server-Manager ist, ob der Benutzer, der auf dem lokalen Computer angemeldet ist, auf ausreichende Benutzerrechte für zugreifen oder diese verwalten die Remoteserver, gibt an, ob der Remoteserver die Software ausgeführt wird, die erforderlich ist, um remote verwaltet werden, oder gibt an, ob der Server so konfiguriert ist, das diesem ermöglicht abgefragt und mithilfe von Server-Manager verwaltet werden. Nur verwaltbarkeitsdaten, die Server-Manager von einem Server erfassen können, auf denen Windows Server 2003 ausgeführt wird, ist, ob der Server online oder offline ist. Ausführliche Informationen zu Verwaltbarkeitsstatusfehlern und deren Behebung finden Sie im [Server Manager Troubleshooting Guide](https://social.technet.microsoft.com/wiki/contents/articles/13443.windows-server-2012-server-manager-troubleshooting-guide-part-i-overview.aspx).|  
|Ereignisse|Sie können die Zeile **Ereignisse** einer Miniaturansicht so konfigurieren, dass Benachrichtigungen angezeigt werden, wenn Ereignisse mit den von Ihnen angegebenen Schweregraden, Quellen, Zeiträumen, Servern oder Ereignis-IDs protokolliert werden. Details zu Ereignissen anzeigen und ändern Sie die anzuzeigenden Warnungen auf der **Ereignisse** Zeile aus, und Öffnen der **Detailansicht für Ereignisse** im Dialogfeld für die Rolle oder Servergruppe.|  
|Dienste|Sie können konfigurieren, die **Services** Zeile, um Warnungen anzuzeigen, wenn Dienste, in einer Rolle oder Gruppe, die entsprechen die Starttypen, Dienststatus, Dienstnamen und Servern, die Sie angeben gefunden werden, in der **Detailansicht der Dienste**  Dialogfeld.<br /><br />Nachdem ein Server dem-Serverpool Server-Manager hinzugefügt wurde, können dienstwarnungen zum Dienst Shellhardwareerkennung angezeigt werden, wenn keine Benutzer am verwalteten Server angemeldet sind. Dies geschieht, weil der Dienst für die Shellhardwareerkennung nur ausgeführt wird, wenn Benutzer am verwalteten Server angemeldet oder mit einer Remotedesktopsitzung auf dem verwalteten Server verbunden sind. Damit in diesem Fall keine Shellhardwareerkennung-Dienstwarnungen angezeigt werden, klicken Sie in den Miniaturansichten für Servergruppen, einschließlich der Gruppe **Alle Server** , auf **Dienste** . In der **Detailansicht der Dienste** Dialogfeld auf die **Services** Dropdown Liste deaktivieren das Kontrollkästchen für **Shellhardwareerkennung**, und klicken Sie dann auf **OK**.|  
|Leistung|Sie können konfigurieren, die **Leistung** Zeile, um Benachrichtigungen für eine Rolle oder Servergruppe angezeigt werden, wenn leistungsbenachrichtigungen, die mit übereinstimmen auftreten, Ressourcentypen, Servern oder Zeiträumen, die Sie, in angeben der **Leistungsdetails Ansicht** Dialogfeld.<br /><br />Leistungsindikatoren sind standardmäßig deaktiviert. Verwaltete Server werden, die Betriebssysteme neuer als die Windows Server 2003 ausgeführt werden soll, und für die Leistungsdaten Leistungsindikatoren nicht gestartet wurden, anzeigen in der Regel Verwaltbarkeit vom Typ **online - Leistungsindikatoren nicht gestartet** in der **Server** Kachel der Rollen- oder Gruppenseiten. Leistungsindikatoren für verwaltete Server deaktivieren auf der **alle Server** Seite der rechten Maustaste auf Einträge in der **Leistung** Kachel eine **Zählerstatus** Wert  **Off**, und klicken Sie dann auf **Leistungsindikatoren starten**. Sie können Leistungsindikatoren auch starten, mit der rechten Maustaste Einträge für Server in der **Server** Kachel der Rolle oder von Gruppenseiten und klicken Sie dann auf **Leistungsindikatoren starten**.|  
|BPA-Ergebnisse|Sie können konfigurieren, die **BPA-Ergebnisse** Zeile anzuzeigenden Warnungen für eine Rolle oder Servergruppe bei BPA-Scanergebnisse werden entsprechen finden Sie Schweregraden, Servern oder BPA-Kategorien aus, die Sie, in angeben der **BPA-Ergebnisse-Detailansicht** Dialogfeld.|  

## <a name="BKMK_events"></a>Anzeigen und Konfigurieren von Ereignissen  
In diesem Abschnitt erfahren Sie, wie Sie konfigurieren, welche Ereignisprotokolldaten von den Servern im Serverpool Server-Managers gesammelt werden, und welche Ereignisse sollen in den Miniaturansichten hervorheben.  

> [!NOTE]  
> Die Ereignisse, die über die Sie in den Miniaturansichten benachrichtigt werden, sind eine Teilmenge der gesamtereignisse, die Sie anweisen, die Server-Manager von verwalteten Servern gesammelt. Aber Ereigniskriterien in die **Ereignisdaten konfigurieren** im Dialogfeld **Ereignisse** Kacheln können die Anzahl der Warnungen auf dem Server-Manager-Dashboard, ändern die Ereigniskriterien in ändern Miniaturansichten hat keine Auswirkungen auf die Ereignisprotokolldaten, die von den verwalteten Servern gesammelt werden.  

#### <a name="to-configure-the-events-collected-from-managed-servers"></a>So konfigurieren Sie Ereignisse, die von verwalteten Servern gesammelt werden  

1.  Öffnen Sie eine beliebige Seite außer der Dashboardseite in der Server-Manager-Konsole. Sie können die Ereignisse, die Sie von den verwalteten Servern sammeln möchten, in der Kachel **Ereignisse** auf der Seite der entsprechenden Rolle, Servergruppe oder des lokalen Servers konfigurieren.  

2.  Klicken Sie in der Kachel **Ereignisse** im Menü **Aufgaben** auf **Ereignisdaten konfigurieren**.  

3.  Wählen Sie die Schweregrade für Ereignisse, die von den Servern in der ausgewählten Gruppe gesammelt werden sollen. Standardmäßig sind die Schweregrade **Kritisch**, **Fehler** und **Warnung** ausgewählt.  

4.  Geben Sie einen Zeitraum an, in dem die Ereignisse auftreten. Das Standardalter für Ereignisse beträgt 24 Stunden.  

5.  Wählen Sie die Ereignisprotokolldateien aus denen Ereignisse gesammelt werden soll. Die Standardwerte sind **Anwendung**, **Setup**und **System**.  

6.  Klicken Sie zum Speichern der Änderungen auf **OK** , um das Dialogfeld **Ereignisdaten konfigurieren** zu schließen. Ereignisdaten werden automatisch aktualisiert, wenn Ihre Änderungen gespeichert werden.  

#### <a name="to-configure-the-events-highlighted-in-thumbnails"></a>So konfigurieren Sie die Ereignisse, die in Miniaturansichten hervorgehoben werden  

1.  Wenn der Server-Manager bereits geöffnet ist, fahren Sie mit dem nächsten Schritt. Ist der Server-Manager noch nicht geöffnet, öffnen Sie ihn mit einer der folgenden Aktionen.  

    -   Starten Sie auf dem Windows-Desktop den Server-Manager, indem Sie in der Windows-Taskleiste auf **Server-Manager** klicken.  

    -   Klicken Sie auf der Windows-**Startseite** auf die Kachel Server-Manager.  

2.  Klicken Sie auf der Dashboardseite in der Kachel **Rollen und Servergruppen** in einer Miniaturansicht auf die Zeile **Ereignisse**.  

3.  In der **Detailansicht für Ereignisse** Dialogfeld fügen einen Schweregrad, der die gewünschten Ereignisse angezeigt. Standardmäßig werden in der Miniaturansicht nur Warnungen zu kritischen Ereignissen hervorgehoben. Beachten Sie, die die Anzahl der Ereignisse in angezeigt. die **Detailansicht** Dialogfeld erhöht, wenn Sie einen Schweregrad hinzufügen, über die Sie benachrichtigt werden möchten.  

4.  Wählen Sie im Feld **Ereignisquellen** die Ereignisquellen aus, über die Sie benachrichtigt werden möchten. Der Standardwert ist **All**.  

5.  Wenn diese Miniaturansicht für eine Rolle, die auf mehreren Servern oder auf eine Gruppe von mehreren Servern installiert ist ist, können Sie auswählen, dass der Server für die Sie ereigniswarnungen erhalten, in möchten der **Server** Dropdown-Liste.  

6.  In der **Zeitraum** an einem bestimmten Zeitraum nach oben zu 1440 Minuten, 24 Stunden bzw. 1 Tag.  

7.  Geben Sie im Feld **Ereignis-IDs** die Ereignis-IDs bestimmter Ereignisse an, über die Sie benachrichtigt werden möchten. Sie können einen Bereich von Ereignis-IDs getrennt durch einen Bindestrich (**-**) eingeben und Ereignis-IDs aus dem Bereich ausschließen, indem Sie den Bindestrich vor der Ereignis-ID oder dem Bereich von Ereignis-IDs eingeben, die Sie ausschließen möchten. Beispielsweise bedeutet der Wert **1,3,5-99,-76**, dass Warnungen für die Ereignis-IDs 1,3,5-99 und 76 und für alle Ereignisse-IDs zwischen 1 und 3 ausgelöst werden, mit Ausnahme von Ereignis-ID 5.  

8.  Wenn Sie die Kriterien dafür ändern, welche Warnungen angezeigt werden, ändert sich möglicherweise die Anzahl der Ereigniswarnungen, die im Ergebnisbereich unten im Dialogfeld angezeigt werden. Wählen Sie die Einträge in der Liste aus, und klicken Sie auf **Warnungen ausblenden** zu verhindern, dass sie Auswirkungen auf die Anzahl der Warnungen, die in der quellminiaturansicht angezeigt wird. Halten Sie bei der Auswahl der Warnungen die **STRG**-Taste gedrückt, um mehrere Warnungen gleichzeitig auszuwählen. Sie können Warnungen ausblenden, die Ihren Warnkriterien entsprechen, die Sie jedoch nicht anzeigen lassen möchten.  

9. Klicken Sie auf **Alle anzeigen** , um ausgeblendete Warnungen wieder in der Liste sichtbar zu machen.  

10. Klicken Sie auf **OK** um Ihre Änderungen zu speichern, schließen die **Detailansicht** (Dialogfeld), und sehen Sie sich den ereigniswarnungen in der quellminiaturansicht Änderungen.  

## <a name="BKMK_perf"></a>Anzeigen und Konfigurieren von leistungsprotokolldaten  
In diesem Abschnitt erfahren Sie, wie Sie konfigurieren, welche leistungsprotokolldaten von den Servern im Serverpool Server-Managers gesammelt werden, und welche leistungsindikatorwarnungen Sie in den Miniaturansichten hervorheben möchten.  

Leistungsindikatoren sind standardmäßig deaktiviert. Verwaltete Server werden, die Betriebssysteme neuer als die Windows Server 2003 ausgeführt werden soll, und für die Leistungsdaten Leistungsindikatoren nicht gestartet wurden, anzeigen in der Regel Verwaltbarkeit vom Typ **online - Leistungsindikatoren nicht gestartet** in der **Server** Kachel der Rollen- oder Gruppenseiten. Leistungsindikatoren für verwaltete Server deaktivieren auf der **alle Server** Seite der rechten Maustaste auf Einträge in der **Leistung** Kachel eine **Zählerstatus** Wert  **Off**, und klicken Sie dann auf **Leistungsindikatoren starten**. Sie können Leistungsindikatoren auch starten, mit der rechten Maustaste Einträge für Server in der **Server** Kachel der Rolle oder von Gruppenseiten und klicken Sie dann auf **Leistungsindikatoren starten**.  

> [!NOTE]  
> Die leistungswarnungen, die Sie in den Miniaturansichten anzeigen sind eine Teilmenge der gesamten Leistungsindikatordaten, die Sie anweisen, die Server-Manager von verwalteten Servern gesammelt. Aber Warnung Leistungskriterien im der **Leistungswarnungen konfigurieren** im Dialogfeld **Leistung** Kacheln können ändern, dass die Anzahl der Warnungen, die Sie sehen, auf dem Server-Manager-Dashboard ändern die Leistung Warnungskriterien in den Miniaturansichten hat keine Auswirkungen auf die leistungsprotokolldaten, die von den verwalteten Servern gesammelt werden.  
>   
> Aus diesem Grund kann das maximale Alter von Leistungsdaten, die Sie in den Miniaturansichten anzeigen können, nicht größer als der maximale Zeitraum der Diagrammanzeige sein, der im Dialogfeld **Leistungswarnungen konfigurieren** konfiguriert ist. Z. B. wenn die **Zeitraum der Diagrammanzeige** Wert **Leistungswarnungen konfigurieren** ist **1 Tag**, der maximale Wert für die **Zeitraum**Feld eine **Leistungsdetails Ansicht** Dialogfeld, das Sie im Server-Manager-Dashboard geöffnet haben, kann sein **1 Tag**, **rund um die**, oder **1.440 Minuten**.  

#### <a name="to-configure-the-performance-log-data-collected-from-managed-servers"></a>So konfigurieren Sie die Leistungsprotokolldaten, die von den verwalteten Servern gesammelt werden  

1.  Öffnen Sie eine beliebige Seite außer der Dashboardseite in der Server-Manager-Konsole. Sie können die Leistungsdaten, die Sie von den verwalteten Servern sammeln möchten, in der Kachel **Leistung** auf der Seite der entsprechenden Rolle, Servergruppe oder des lokalen Servers konfigurieren.  

2.  Um Leistungsprotokolldaten von verwalteten Servern sammeln zu können, müssen die Leistungsindikatoren aktiviert sein. Wenn Leistungsindikatoren deaktiviert sind, mit der rechten Maustaste eines Eintrags in der **Leistung** kachelliste aus, und klicken Sie dann auf **Leistungsindikatoren starten**. Das Sammeln von Leistungsindikatordaten kann einige Zeit in Anspruch nehmen, je nach der Anzahl der Server, von denen die Daten gesammelt werden, und der zur Verfügung stehenden Netzwerkbandbreite. Zeigen Sie den Status in der Spalte **Zählerstatus** an.  

3.  Klicken Sie im Menü **Aufgaben** der Kachel **Leistung** auf **Leistungswarnungen konfigurieren**.  

4.  für die Server in der ausgewählten Gruppe oder die ausgewählte Rolle ausgeführt werden, geben Sie an, ab welchem Prozentsatz der CPU-Auslastung von leistungsindikatorwarnungen vom Server-Manager gesammelt werden sollen. Der Standardwert liegt bei 85 %.  

5.  Geben Sie den verbleibenden verfügbaren Arbeitsspeicher in Megabyte an, den die Server haben sollen, bevor Leistungsindikatorwarnungen gesammelt werden. Der Standardwert ist 2 MB.  

6.  Geben Sie für die Ressourcen **CPU-Auslastung** und **Verfügbarer Arbeitsspeicher** in der Kachel **Leistung** einen Zeitraum, der in den Diagrammen widergespiegelt werden soll. Der Standardzeitraum ist ein Tag. Klicken Sie auf **Speichern**.  

    Beachten Sie, dass sich die Anzahl der Leistungswarnungen in der Kachel **Leistung** und die im Diagramm dargestellte Zuordnung der Warnungen im Zeitverlauf ändern können, nachdem Sie auf **Speichern**geklickt haben.  

    > [!NOTE]  
    > für virtuelle Computer mit [dynamischer Arbeitsspeicher](https://technet.microsoft.com/library/ff817651.aspx) aktiviert ist, kann die Anhebung des Schwellenwerts für Warnungen zu falsch positiven Warnungen.  

7.  Klicken Sie im Menü **Aufgaben** auf **Aktualisieren**, um die Liste der Leistungswarnungen zu aktualisieren, die von den Servern gesammelt werden.  

#### <a name="to-configure-the-performance-alerts-highlighted-in-thumbnails"></a>So konfigurieren Sie sie Leistungswarnungen, die in den Miniaturansichten hervorgehoben werden  

1.  Klicken Sie auf der Dashboardseite in der Kachel **Rollen und Servergruppen** in einer Miniaturansicht auf die Zeile **Leistung** .  

2.  In der **Leistungsdetails Ansicht** (Dialogfeld), aktivieren oder deaktivieren Sie die Kontrollkästchen für Schwellenwerte von ressourcenleistungen über die Sie benachrichtigt werden möchten die **Ressourcentyp** Feld. Beachten Sie, die die Anzahl der leistungswarnungen in angezeigt. die **Detailansicht** Dialogfeld steigt, wenn Sie eine Ressource Leistungsschwellenwert hinzufügen, über die Sie benachrichtigt werden möchten.  

3.  Wenn diese Miniaturansicht für eine Rolle, die auf mehreren Servern oder auf eine Gruppe von mehreren Servern installiert ist ist, können Sie auswählen, dass die Server für die Sie leistungswarnungen erhalten in möchten der **Server** Dropdown-Liste.  

4.  In der **Zeitraum** an einem bestimmten Zeitraum nach oben zu 1440 Minuten, 24 Stunden bzw. 1 Tag.  

5.  Wenn Sie die Kriterien dafür ändern, welche Warnungen angezeigt werden, ändert sich möglicherweise die Anzahl der Warnungen, die im Ergebnisbereich unten im Dialogfeld angezeigt werden. Klicken Sie auf **Warnungen ausblenden** , um alle Warnungen auszublenden, die sich nicht auf den aktuellen Zeitpunkt beziehen. Sie wirken sich dann nicht auf die Anzahl der Warnungen aus, die in der Quellminiaturansicht angezeigt wird.  

6.  Klicken Sie auf **Alle anzeigen** , um ausgeblendete Warnungen wieder in der Liste sichtbar zu machen.  

7.  Klicken Sie auf **OK** um Ihre Änderungen zu speichern, schließen die **Detailansicht** (Dialogfeld), und sehen Sie die Leistung in der quellminiaturansicht Änderungen.  

#### <a name="to-view-the-properties-of-performance-alerts"></a>So zeigen Sie die Eigenschaften der Leistungswarnungen an  

1.  Führen Sie eine der folgenden Aktionen aus.  

    -   Klicken Sie auf der Dashboardseite in der Kachel **Rollen und Servergruppen** in einer Miniaturansicht auf die Zeile **Leistung** .  

    -   Öffnen Sie die Homepage einer Rolle oder Gruppe, und suchen Sie nach der Kachel **Leistung** für die Rolle oder Gruppe.  

2.  Doppelklicken Sie auf eine Leistungswarnung in der Liste, um die dazugehörigen Eigenschaften anzuzeigen. Alternativ können Sie mit der rechten Maustaste auf eine Leistungswarnung klicken und dann **Eigenschaften anzeigen** auswählen.  

3.  Wählen Sie im Dialogfeld **Leistungsalarmeigenschaften** Protokolleinträge aus, um Informationen über die Prozesse anzuzeigen, die mit dem Eintrag im Bereich **Prozesse** verknüpft sind.  

4.  Wenn Sie die Leistungsalarmeigenschaften geprüft haben, schließen Sie das Dialogfeld.  

### <a name="analyze-performance-data-and-solve-problems"></a>Analyse von Leistungsdaten und Problembehebung  
Weitere Informationen zum Analysieren von Leistungsindikatordaten, die Sie in Server-Manager und zum Lösen von Leistungsproblemen auf verwalteten Servern angezeigt werden, finden Sie unter den folgenden Ressourcen.  

-   [Analysieren von Leistungsdaten](https://go.microsoft.com/fwlink/?LinkId=239829)  

-   [Beheben von Leistungsproblemen](https://go.microsoft.com/fwlink/?LinkId=239831)  

Weitere Informationen zu erweiterten Leistung Überwachung und Analyse verfügbaren Tools für Windows Server 2012 und spätere Versionen von Windows Server, einschließlich Server Performance Advisor 3.0, finden Sie unter [Leistung](https://msdn.microsoft.com/windows/hardware/gg463374.aspx) auf MSDN.  

## <a name="BKMK_services"></a>Dienste verwalten und Konfigurieren von dienstbenachrichtigungen  
In diesem Abschnitt erfahren Sie, wie starten, beenden, neu starten, Anhalten oder Fortsetzen von Diensten, die in angezeigt werden, die **Services** Kachel auf den Rollen- und servergruppenseiten in Server-Manager. Sie können die Dienste, die über die Sie benachrichtigt werden auch in den Miniaturansichten im Dashboard des Server-Manager konfigurieren.  

> [!NOTE]  
> Sie können den Starttyp für Dienste, dienstabhängigkeiten, Wiederherstellungsoptionen oder Diensteigenschaften in der Kachel "Services" im Server-Manager nicht ändern. Wenn Sie andere Diensteigenschaften als den Dienststatus ändern möchten, öffnen Sie das Snap-In **Dienste**. Eine Verknüpfung zum Öffnen der **Services** -Snap-in steht auf der **Tools** Menü im Server-Manager.  

#### <a name="to-start-stop-restart-pause-or-resume-a-service"></a>So können Sie Dienste starten, beenden, neu starten, anhalten und fortsetzen  

1.  Öffnen Sie eine beliebige Seite außer der Dashboardseite (also eine beliebige Rollen- oder gruppenhomepage), in der Server-Manager-Konsole.  

2.  Klicken Sie in der Kachel **Dienste** für die Rolle oder Gruppe mit der rechten Maustaste auf einen Dienst.  

3.  Klicken Sie im Kontextmenü auf die gewünschte Aktion, mit der dieser Dienst ausgeführt werden soll. Wurde der Dienst beendet, ist die einzige Aktion, die Sie ausführen können, den Dienst zu starten. Wird der Dienst angehalten, ist dementsprechend die einzige Aktion, die Sie ausführen können, den Dienst fortzusetzen.  

4.  Beachten Sie, dass sich der Wert der Spalte **Status** für den in der Kachel **Dienste** ausgewählten Dienst ändert, wenn Sie einen Dienst starten, stoppen, neu starten, anhalten oder fortsetzen.  

#### <a name="to-configure-service-alerts-highlighted-in-thumbnails"></a>So konfigurieren Sie die Dienstbenachrichtigungen, die in Miniaturansichten hervorgehoben werden  

1.  Klicken Sie auf der Dashboardseite in der Kachel **Rollen und Servergruppen** in einer Miniaturansicht auf die Zeile **Dienste**.  

2.  In der **Detailansicht der Dienste** wählen Sie im Dialogfeld die Starttypen für Dienste, die über die Sie benachrichtigt werden möchten. In der Standardeinstellung **automatisch (verzögerter Start)** und **automatische** ausgewählt sind.  

3.  Wählen Sie die Dienststatus, die über die Sie benachrichtigt werden möchten. Standardmäßig ist **Alle** ausgewählt.  

4.  Wählen Sie Dienste, die über die Sie benachrichtigt werden möchten. Standardmäßig ist **Alle** ausgewählt.  

5.  Wählen Sie die Server, der die Rolle oder Gruppe, die für die Sie dienstwarnungen erhalten möchten zugeordnet. Standardmäßig ist **Alle** ausgewählt.  

6.  Wenn Sie die Kriterien dafür ändern, welche Warnungen angezeigt werden, ändert sich möglicherweise die Anzahl der Warnungen, die im Ergebnisbereich unten im Dialogfeld angezeigt werden. Klicken Sie auf **Warnungen ausblenden** , um alle Warnungen auszublenden, die sich nicht auf den aktuellen Zeitpunkt beziehen. Sie wirken sich dann nicht auf die Anzahl der Warnungen aus, die in der Quellminiaturansicht angezeigt wird.  

7.  Klicken Sie auf **Alle anzeigen** , um ausgeblendete Warnungen wieder in der Liste sichtbar zu machen.  

8.  Klicken Sie auf **OK** um Ihre Änderungen zu speichern, schließen die **Detailansicht** (Dialogfeld), und sehen Sie den Dienst in der quellminiaturansicht Änderungen.  

## <a name="BKMK_copy"></a>Anzeigen und Kopieren von Ereignis-, Dienst- oder leistungseinträgen  
Sie können Eigenschaften für Ereignis-, Dienst- oder Leistung in beiden Kopieren der **Detailansicht** Dialogfelder und die **Ereignisse** und **Leistung** Kacheln für eine Rolle oder Gruppe. Mit der rechten Maustaste eines Ereignis- oder leistungseintrag, und klicken Sie dann auf **Kopie**.  

Über die Kachel **Ereignisse** können Sie auch in der unteren Hälfte der Kachel Ereigniseigenschaften in der Vorschau anzeigen, indem Sie in der Liste einen Eintrag auswählen. In der Vorschau angezeigten Eigenschaften kopieren, klicken Sie mit der rechten Maustaste auf das Vorschaufenster, und klicken Sie dann auf **Kopie**.  

## <a name="see-also"></a>Siehe auch  
[Server Manager](server-manager.md)  
[Filtern, Sortieren und Abfragen von Daten in Server-Manager-Kacheln](filter-sort-and-query-data-in-server-manager-tiles.md)  
