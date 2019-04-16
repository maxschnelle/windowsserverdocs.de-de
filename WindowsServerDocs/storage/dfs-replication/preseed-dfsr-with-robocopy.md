---
title: Verwenden Sie Robocopy, um die Dateien für die DFS-Replikation preseed
description: Wie Robocopy.exe verwenden, um die Dateien für die DFS-Replikation preseed.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: a7a14b1a1e0f91002b201869e4c68187ffaf3f8f
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082191"
---
# <a name="use-robocopy-to-preseed-files-for-dfs-replication"></a>Verwenden Sie Robocopy, um die Dateien für die DFS-Replikation preseed

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

In diesem Thema wird erläutert, wie Sie das Befehlszeilentool **Robocopy.exe**, um Dateien preseed beim Einrichten von Replikation (Distributed File System, DFS) Replikation (auch bekannt als DFSR oder DFS-R) in Windows Server. Durch preseeding Dateien vor dem Einrichten von DFS-Replikation, fügen Sie einen neuen Replikations-Partner oder Ersetzen Sie einen Server, können Sie erstsynchronisierung beschleunigen und Klonen der Datenbank DFS-Replikation in Windows Server 2012 R2 aktivieren. Die Robocopy-Methode ist einer der folgenden Methoden preseeding. eine Übersicht finden Sie unter [Schritt 1: preseed Dateien für die DFS-Replikation](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495046(v%3dws.11)>).

Das Befehlszeilenprogramm Robocopy (robuste Dateikopie) gehört zum Lieferumfang von Windows Server. Das Dienstprogramm bietet umfassende Optionen, die kopieren Sicherheit, backup-API-Unterstützung, "Wiederholen" Funktionen und Protokollierung enthalten. Höhere Versionen umfassen Multithreading und ungepuffert e/a-Unterstützung.

>[!IMPORTANT]
>Robocopy werden ausschließlich gesperrte Dateien nicht kopiert werden. Benutzer in der Regel viele Dateien für einen längeren Zeitraum auf Ihren Dateiservern zu sperren, sollten Sie eine andere preseeding-Methode verwenden. Preseeding ist kein identisches zwischen Dateilisten auf den Quell- und Ziel-Servern erforderlich, jedoch ist die weitere Dateien, die nicht vorhanden sind, wenn die anfängliche Synchronisierung für die DFS-Replikation, die weniger effektive preseeding ausgeführt wird. Um die Sperre Konflikte zu minimieren, verwenden Sie Robocopy Spitzenzeiten nicht für Ihre Organisation. Prüfen Sie die Protokolle Robocopy immer nach preseeding, um sicherzustellen, dass Sie wissen, welche Dateien aufgrund exklusive Sperren übersprungen wurden.

So verwenden Sie Robocopy preseed Dateien für die DFS-Replikation, gehen Sie folgendermaßen vor:

1. [Herunterladen und Installieren der neuesten Version von Robocopy.](#step-1:-download-and-install-the-latest-version-of-robocopy)
2. [Stabilisierung Dateien, die repliziert werden.](#step-2:-stabilize-files-that-will-be-replicated)
3. [Kopieren Sie die replizierten Dateien auf den Zielserver.](#step-3:-copy-the-replicated-files-to-the-destination-server)

## <a name="prerequisites"></a>Voraussetzungen

Da preseeding keine direkt DFS-Replikation, müssen Sie nur die Mindestanforderungen für die Ausführung einer Dateikopie mit Robocopy.

- Sie benötigen ein Konto, das Mitglied der lokalen Gruppe Administratoren auf dem Quell- und Ziel-Servern ist.

- Installieren Sie die aktuellste Version von Robocopy auf dem Server, die Sie zum Kopieren der Dateien verwenden – der Quellserver oder dem Zielserver; Sie benötigen, um die aktuellste Version für die Version des Betriebssystems zu installieren. Anweisungen finden Sie unter [Schritt2: Stabilisierung Dateien, die repliziert werden](#step-2:-stabilize-files-that-will-be-replicated). Es sei denn, Sie Dateien von einem Server mit Windows Server 2003 R2 preseeding, können Sie Robocopy auf Quelle oder Ziel-Server ausführen. Der Zielserver, der in der Regel die neuere Version des Betriebssystems hat, erhalten Sie Zugriff auf die neueste Version von Robocopy.

- Stellen Sie sicher, dass genügend freier Speicherplatz auf dem Ziellaufwerk verfügbar ist. Erstellen Sie einen Ordner nicht auf den Pfad, den Sie planen, zu kopieren: Robocopy muss im Stammordner erstellen.
    
    >[!NOTE]
    >Wenn Sie, wie viel Speicherplatz für die preseeded Dateien zugewiesen werden entscheiden, sollten Sie erwartete Datenwachstums über und Anforderungen für die DFS-Replikation. Planungshilfe, finden Sie unter [Verwalten von DFS](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754771(v=ws.11)>)-Replikation [Bearbeiten Sie die Größe der Staging-Ordner und Konflikt und Ordner gelöscht](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754229(v=ws.11)) .

- Installieren Sie auf dem Quellserver optional Process Monitor oder Explorer, dem Sie für Applikationen überprüfen können, die Sperren von Dateien. Informationen zum Herunterladen finden Sie unter [Process Monitor](https://docs.microsoft.com/sysinternals/downloads/procmon) und [Process Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer).

## <a name="step-1-download-and-install-the-latest-version-of-robocopy"></a>Schritt 1: Herunterladen und Installieren der neuesten Version von Robocopy

Bevor Sie Robocopy zum preseed Dateien verwenden, sollten Sie herunterladen und installieren die neueste Version von **Robocopy.exe**. Dadurch wird sichergestellt, dass die DFS-Replikation aufgrund des innerhalb Robocopys des Protokollversands Versionen Dateien überspringen nicht.

Die Quelle für die neueste Version der kompatibel Robocopy hängt von der Version von Windows Server, auf dem Server ausgeführt wird. Informationen zum Herunterladen des Hotfixes mit der neuesten Version von Robocopy für Windows Server 2008 R2 oder Windows Server 2008 finden Sie unter Liste der derzeit Hotfixes für verteilten Dateisystem (DFS)-Technologien in Windows Server 2008 und [ Windows Server 2008 R2](https://support.microsoft.com/help/968429/list-of-currently-available-hotfixes-for-distributed-file-system-dfs-t).

Alternativ können Sie suchen, und installieren die aktuelle Hotfixes für ein Betriebssystem durch Ausführen der folgenden Schritte.

### <a name="locate-and-install-the-latest-version-of-robocopy-for-a-specific-version-of-windows-server"></a>Suchen Sie und installieren Sie die neueste Version von Robocopy für eine bestimmte Version von Windows Server

1. Öffnen Sie in einem Webbrowser [https://support.microsoft.com](https://support.microsoft.com/).

2. Im **Search Support**, geben Sie folgende Zeichenfolge ersetzen `<operating system version>` mit dem entsprechenden Betriebssystem, und drücken Sie dann die EINGABETASTE:
    
    ```robocopy.exe kbqfe "<operating system version>"```
    
    Geben Sie beispielsweise **robocopy.exe based "Windows Server 2008 R2"**.

3. Suchen Sie und Laden Sie den Hotfix mit der höchsten ID-Nummer (d. h., die neueste Version).

4. Installieren Sie den Hotfix auf dem Server.

## <a name="step-2-stabilize-files-that-will-be-replicated"></a>Schritt 2: Stabilisierung Dateien, die repliziert werden

Nach der Installation der neuesten Version von Robocopy auf dem Server sollten Sie verhindern, dass gesperrte Dateien blockieren kopieren mithilfe der Methods in der folgenden Tabelle beschrieben. Die meisten Sperren Dateien nicht exklusiv. Während des normalen Betriebs möglicherweise ein kleiner Prozentsatz der Dateien auf dem Dateiserver gesperrt werden.

|Quelle der Sperre|Erläuterung|Abhilfemaßnahmen|
|---|---|---|
|Benutzer können Dateien auf Freigaben Remote öffnen.|Mitarbeiter Verbindung mit einer Serverfarm Standarddatei anzeigen und Bearbeiten von Dokumenten, multimedia-Inhalt oder andere Dateien. Auch bezeichnet als herkömmliche Basisordner oder freigegebene Daten Arbeitslasten.|Nur Operationen Robocopy während außerhalb der Spitzenzeiten, außerhalb der Geschäftszeiten. Dadurch wird die Anzahl von Dateien, die während preseeding Robocopy überspringen muss minimiert.<br><br>Sollten Sie vorübergehend festlegen schreibgeschützten Zugriff auf die Dateifreigaben, die mithilfe von Windows PowerShell **Grant-SmbShareAccess** und **Schließen SmbSession** -Cmdlets repliziert werden. Wenn Sie zum Lesen von Berechtigungen für eine gemeinsame Benutzergruppe wie jeder oder authentifizierte Benutzer festlegen, möglicherweise standard-Benutzer werden mit weitaus geringerer Wahrscheinlichkeit zum Öffnen von Dateien mit exklusiven Sperren (Wenn ihre Anwendung den schreibgeschützten Zugriff erkennen, wann Dateien geöffnet werden).<br><br>Sie sollten auch festlegen eine temporäre Firewallregel für SMB-Port 445 eingehend zu diesem Server So blockieren Sie den Zugriff auf Dateien oder verwenden Sie das Cmdlet **Block SmbShareAccess** . Diese beiden Methoden sind jedoch sehr störend auf Benutzeraktionen.|
|Clientanwendungen öffnen lokalen Dateien.|Ausführung auf einem Dateiserver manchmal Arbeitslasten Dateien sperren.|Vorübergehend deaktivieren Sie oder deinstallieren Sie die Anwendung, die Sperren von Dateien. Sie können Process Monitor oder Explorer verwenden, um zu bestimmen, welche Anwendungen Dateien sperren werden. Finden Sie Informationen zum Herunterladen von Process Monitor oder -Explorer auf den Seiten [Process Monitor](https://docs.microsoft.com/sysinternals/downloads/procmon) und [Process Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer) .|

## <a name="step-3-copy-the-replicated-files-to-the-destination-server"></a>Schritt 3: Kopieren Sie die replizierten Dateien auf den Zielserver

Nach dem Sperren der Dateien, die repliziert werden minimieren, können Sie die Dateien vom Quellserver auf den Zielserver preseed.

>[!NOTE]
>Sie können auf dem Quellcomputer oder dem Zielcomputer Robocopy ausführen. Das folgende Verfahren beschreibt das Ausführen von Robocopy auf dem Zielserver, der in der Regel ein neueren Betriebssystem ausgeführt wird, um alle zusätzlichen Robocopy-Funktionen nutzen, die möglicherweise das neuere Betriebssystem bereitstellt.

### <a name="preseed-the-replicated-files-onto-the-destination-server-with-robocopy"></a>Die replizierten Dateien auf dem Zielserver mit Robocopy preseed

1. Melden Sie sich mit einem Konto, das Mitglied der lokalen Gruppe Administratoren auf dem Quell- und Ziel-Servern ist auf den Zielserver.

2. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten.

3. Führen Sie den folgenden Befehl, ersetzen Ihre eigene Quelle, Ziel und Protokolldateipfade für die Werte in Klammern, um die Dateien aus der Quelle auf den Zielserver zu preseed:
    
    ```PowerShell
    robocopy "<source replicated folder path>" "<destination replicated folder path>" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:<log file path> /v
    ```
    
    Dieser Befehl kopiert alle Inhalte des Quellordners in den Zielordner, mit den folgenden Parametern:
    
    |Parameter|Beschreibung|
    |---|---|
    |"< source replizierten Ordner p > \"|Gibt an, die auf dem Zielserver preseed des Quellordners.|
    |"\ < Ziel repliziert Ordner p >"|Gibt den Pfad zu dem Ordner, in der die preseeded Dateien gespeichert werden.<br><br>Der Zielordner muss auf dem Zielserver noch nicht vorhanden. Um übereinstimmende Dateihashes erhalten möchten, muss Robocopy im Stammordner erstellen, wenn sie die Dateien preseeds.|
    |/ e|Kopiert Unterverzeichnisse und deren Dateien sowie die leeren Unterverzeichnisse.|
    |/ b|Kopiert Dateien in Backup-Modus.|
    |/ copyal|Kopiert alle Dateiinformationen, einschließlich Daten, Attribute, Zeitstempel, NTFS-Zugriffssteuerungsliste (ACL), Besitzerinformationen und Überwachung von Informationen.|
    |/r:6|Wiederholt den Vorgang sechs Mal, wenn ein Fehler auftritt.|
    |/w:5|5 Sekunden zwischen Wiederholungsversuchen wartet.|
    |MT:64|64-Dateien kopiert gleichzeitig.|
    |/ XD ConflictandDeletedManifest.Xml|Schließt den Ordner ConflictandDeletedManifest.Xml.|
    |/Tee|Schreibt Statusausgabe im Konsolenfenster sowie in die Protokolldatei.|
    |/ log \ < Protokolldateipfad >|Gibt die Protokolldatei geschrieben. Überschreibt die Datei vorhandenen Inhalt. (Verwenden, um die Einträge in die vorhandene Protokolldatei anzufügen `/log+ <log file path>`.)|
    |/v|Ausführlicher Ausgabe, der enthält Übersprungene Dateien.|
    
    Beispielsweise repliziert der folgende Befehl Dateien aus dem Quellordner repliziert, E:\\RF01, um Datenlaufwerk D auf dem Zielserver:
    
    ```PowerShell
    robocopy.exe "\\srv01\e$\rf01" "d:\rf01" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:c:\temp\preseedsrv02.log
    ```
    
    >[!NOTE]
    >Es wird empfohlen, wenn Sie Robocopy verwenden, um die Dateien für die DFS-Replikation preseed oben beschriebenen Parameter zu verwenden. Sie können jedoch einige der entsprechenden Werte ändern oder zusätzliche Parameter hinzufügen. Beispielsweise können Sie feststellen, über das Testen, ob Sie die Kapazität zum einen höheren Wert (Threadanzahl) für den *Parameter/MT* festgelegt haben. Auch, wenn größere Dateien in erster Linie repliziert werden, können Sie Kopie Leistung zu erhöhen, indem Sie die **Option/j** für ungepufferte e/a hinzufügen können. Weitere Informationen zu Parametern Robocopy finden Sie unter der [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy) Command-Line Reference.

    >[!WARNING]
    >Um potenziellen Datenverlust zu vermeiden, wenn Sie Robocopy verwenden, um die Dateien für die DFS-Replikation preseed, nehmen Sie die folgenden Änderungen nicht auf die empfohlene Parameter:
    >- Verwenden Sie nicht den *Parameter/mir* (, der eine Verzeichnisstruktur spiegelt) oder den Parameter */mov* (, der die Dateien verschoben, und löscht sie aus der Quelle).
    >-  Entfernen Sie die **Optionen/e**, **/ b**und **/copyall** nicht.

4. Kopieren Sie nach dem Abschluss untersuchen Sie das Ereignisprotokoll auf Fehler oder übersprungene Dateien. Verwenden Sie Robocopy übersprungenen Dateien einzeln anstelle den gesamten Satz von Dateien in diesem kopieren. Wenn Dateien aufgrund exklusive Sperren übersprungen wurden, versuchen Sie einzelne Dateien mit Robocopy später zu kopieren, oder akzeptieren Sie, dass diese Dateien über das Netzwerk Replikation von DFS-Replikation während der ersten Synchronisierung erforderlich ist.

## <a name="next-step"></a>Nächster Schritt

Nachdem Sie die erste Kopie abschließen und verwenden Sie Robocopy, um Probleme mit wie vielen Übersprungene Dateien wie möglich zu beheben, verwenden mit dem Cmdlet **Get-DfsrFileHash** in Windows PowerShell oder den Befehl **Dfsrdiag** Sie zum Überprüfen der preseeded Dateien durch Vergleichen Dateihashes auf den Quell- und Ziel-Servern. Weitere Informationen finden Sie unter [Schritt2: Überprüfen der Preseeded Dateien für die DFS-Replikation](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495042(v%3dws.11)>).