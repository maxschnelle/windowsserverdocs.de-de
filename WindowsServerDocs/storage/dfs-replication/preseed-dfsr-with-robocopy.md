---
title: Verwenden Sie Robocopy, um die Dateien für die DFS-Replikation Seeding
description: So Robocopy.exe verwenden, um die Dateien für die DFS-Replikation Seeding.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: eaec563157a77fd4e782842a81e5b59e49a5ea09
ms.sourcegitcommit: 7cb939320fa2613b7582163a19727d7b77debe4b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2019
ms.locfileid: "65621298"
---
# <a name="use-robocopy-to-preseed-files-for-dfs-replication"></a>Verwenden Sie Robocopy, um die Dateien für die DFS-Replikation Seeding

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

In diesem Thema wird erläutert, wie die Befehlszeilentools **Robocopy.exe**, um Dateien Seeding beim Einrichten der Replikation für die Replikation (Distributed File System, DFS), (auch bekannt als DFSR oder DFS-R) unter Windows Server. Durch preseeding-Dateien, bevor Sie die DFS-Replikation einrichten, Hinzufügen eines neuen Replikationspartners oder ein Servers ersetzen, können Sie beschleunigen der ersten Synchronisierung und das Klonen der Datenbank die DFS-Replikation unter Windows Server 2012 R2. Die Robocopy-Methode ist eine von mehreren preseeding Methoden. eine Übersicht finden Sie unter [Schritt 1: Seeding Dateien für die DFS-Replikation](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495046(v%3dws.11)>).

Das Befehlszeile-Hilfsprogramm von Robocopy (robuste Kopieren von Gastdateien), die mit Windows Server enthalten ist. Das Dienstprogramm bietet umfangreiche Optionen, die von Sicherheit, Sicherung-API-Unterstützung, Wiederholungsfunktionen und Protokollierung enthalten. Höhere Versionen enthalten die e/a-Unterstützung von Multithreading und nicht gepuffert.

>[!IMPORTANT]
>Robocopy werden ausschließlich gesperrte Dateien nicht kopiert werden. Wenn Benutzer tendenziell über viele Dateien über lange Zeiträume auf Ihren Dateiservern zu sperren, sollten erwägen Sie, eine andere preseeding Methode zu verwenden. Preseeding eine perfekte Übereinstimmung zwischen Dateilisten auf den Quell- und Ziel nicht erforderlich, jedoch wird die weitere Dateien, die nicht vorhanden sind, wenn die erste Synchronisierung für DFS-Replikation, die weniger effektiv preseeding durchgeführt wird. Um Sperrkonflikten zu minimieren, verwenden Sie Robocopy Zeiten außerhalb der Spitzenzeiten für Ihre Organisation ein. Prüfen Sie immer die Robocopy-Protokolle nach preseeding, um sicherzustellen, dass Sie verstehen, welche Dateien aufgrund von exklusiven Sperren übersprungen wurden.

So verwenden Robocopy, um Dateien für die DFS-Replikation Seeding, gehen Sie folgendermaßen vor:

1. [Herunterladen Sie und installieren Sie die neueste Version von Robocopy.](#step-1-download-and-install-the-latest-version-of-robocopy)
2. [Stabilisieren Sie Dateien, die repliziert werden.](#step-2-stabilize-files-that-will-be-replicated)
3. [Kopieren Sie die replizierte Dateien auf den Zielserver an.](#step-3-copy-the-replicated-files-to-the-destination-server)

## <a name="prerequisites"></a>Vorraussetzungen

Da preseeding keine direkt DFS-Replikation, müssen Sie nur die Anforderungen für die Durchführung eines Dateikopiervorgangs mit Robocopy erfüllen.

- Sie benötigen ein Konto, das ein Mitglied der lokalen Administratorengruppe auf den Quell-und Ziel ist.

- Installieren Sie die neueste Version von Robocopy, auf dem Server, die Sie zum Kopieren der Dateien verwenden – entweder auf dem Quellserver oder auf dem Zielserver; Sie benötigen, um die neueste Version für die Betriebssystemversion zu installieren. Anweisungen hierzu finden Sie unter [Schritt2: Stabilisieren Sie Dateien, die repliziert werden](#step-2-stabilize-files-that-will-be-replicated). Wenn Sie Dateien von einem Server unter Windows Server 2003 R2 preseeding sind, können Sie Robocopy auf die Quelle oder das Ziel-Server ausführen. Der Zielserver, der in der Regel die aktuellere Version des Betriebssystems verfügt, erhalten Sie Zugriff auf die neueste Version von Robocopy an.

- Stellen Sie sicher, dass genügend Speicherplatz auf dem Ziellaufwerk verfügbar ist. Erstellen Sie einen Ordner nicht auf dem Weg, dem Sie zum kopieren möchten: Robocopy muss im Stammordner erstellen.
    
    >[!NOTE]
    >Wie viel Speicherplatz für die preseeded Dateien zuweisen möchten, müssen, berücksichtigen Sie erwartete Wachstum über und speicheranforderungen für die DFS-Replikation. Planen die Hilfe, finden Sie unter [Bearbeiten der Kontingentgröße des Stagingordners und des Konfliktordners für gelöschte Ordner](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754229(v=ws.11)) in [Verwaltung von DFS-Replikation](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754771(v=ws.11)>).

- Installieren Sie auf dem Quellserver optional Process Monitor oder die Prozess-Explorer, die Sie verwenden können, überprüfen Sie für Anwendungen, die Dateien sperren. Informationen zum Herunterladen finden Sie unter [Process Monitor](https://docs.microsoft.com/sysinternals/downloads/procmon) und [Process Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer).

## <a name="step-1-download-and-install-the-latest-version-of-robocopy"></a>Schritt 1: Herunterladen Sie und installieren Sie die neueste Version von Robocopy

Bevor Sie Dateien Seeding Robocopy verwenden, sollten Sie diese herunterladen und installieren Sie die neueste Version von **Robocopy.exe**. Dadurch wird sichergestellt, dass die DFS-Replikation Dateien aufgrund von Problemen, die innerhalb Robocopys-Protokollversand-Versionen zu überspringen nicht.

Die Quelle für die neueste kompatible Robocopy-Version hängt von der Version von Windows Server, auf dem Server ausgeführt wird. Weitere Informationen zu den Hotfix an, mit der neuesten Version von Robocopy für Windows Server 2008 R2 oder Windows Server 2008 herunterladen, finden Sie unter [Liste der derzeit verfügbaren Hotfixes für Distributed File System (DFS)-Technologien in Windows Server 2008 und in Windows Server 2008 R2](https://support.microsoft.com/help/968429/list-of-currently-available-hotfixes-for-distributed-file-system-dfs-t).

Alternativ können Sie suchen und installieren den neuesten Hotfix für ein Betriebssystem installiert ist, indem Sie die folgenden Schritte aus.

### <a name="locate-and-install-the-latest-version-of-robocopy-for-a-specific-version-of-windows-server"></a>Suchen Sie und installieren Sie die neueste Version von Robocopy für eine bestimmte Version von Windows Server

1. Öffnen Sie in einem Webbrowser [ https://support.microsoft.com ](https://support.microsoft.com/).

2. In **Suchunterstützung**, geben Sie die folgende Zeichenfolge ist, und Ersetzen Sie dabei `<operating system version>` mit dem entsprechenden Betriebssystem, und drücken Sie dann die EINGABETASTE:
    
    ```robocopy.exe kbqfe "<operating system version>"```
    
    Geben Sie z. B. **robocopy.exe based "Windows Server 2008 R2-** .

3. Suchen Sie und Laden Sie den Hotfix an, mit der höchsten ID-Nummer (d. h. die neueste Version).

4. Installieren Sie den Hotfix auf dem Server.

## <a name="step-2-stabilize-files-that-will-be-replicated"></a>Schritt 2: Stabilisieren Sie Dateien, die repliziert werden

Nachdem Sie die neueste Version von Robocopy auf dem Server installiert haben, sollten Sie verhindern, dass gesperrte Dateien blockieren kopieren mithilfe der Methoden, die in der folgenden Tabelle beschrieben. Die meisten Anwendungen sind nicht exklusiv gesperrt werden Dateien. Während des normalen Betriebs, möglicherweise jedoch ein kleinen Prozentsatz der Dateien auf Dateiservern gesperrt werden.

|Quelle der Sperre|Erläuterung|Abhilfemaßnahmen|
|---|---|---|
|Benutzer öffnen Remote Dateien auf Dateifreigaben.|Mitarbeiter mit einem standard-Datei-Server verbinden und Bearbeiten von Dokumenten, multimedia-Inhalte oder andere Dateien. Mitunter als herkömmliche Ordner "home" oder freigegebenen Data-Workloads.|Nur Vorgänge Robocopy während außerhalb der Spitzenzeiten, außerhalb der Geschäftszeiten einrichten. Dies minimiert die Anzahl der Dateien, die während der preseeding Robocopy überspringen muss.<br><br>Empfiehlt es sich vorübergehend Lesezugriff auf die Dateifreigaben, die repliziert werden mithilfe des Windows PowerShell **Grant-SmbShareAccess** und **schließen-SmbSession** Cmdlets. Setzen Sie Berechtigungen für eine allgemeine Gruppe z. B. jeder oder authentifizierte Benutzer zu lesen, ist Standardbenutzer möglicherweise weniger wahrscheinlich zum Öffnen von Dateien mit exklusiven Sperren (Wenn ihre Anwendungen den schreibgeschützten Zugriff erkennen, wenn Dateien geöffnet werden).<br><br>Sie könnten auch erwägen, eine temporäre Firewallregel festlegen für SMB-Port 445 für diesen Server zum Blockieren des Zugriffs auf Dateien oder verwenden Sie eingehend die **Block-SmbShareAccess** Cmdlet. Beide Methoden sind jedoch sehr an Benutzervorgänge Unterbrechungen führen.|
|Anwendungen lokale Dateien zu öffnen.|Anwendungsworkloads, die auf einem Dateiserver ausgeführt wird, in einigen Fällen werden die Dateien sperren.|Vorübergehend deaktivieren oder Deinstallieren von Anwendungen, die Dateien sperren. Sie können Process Monitor oder die Prozess-Explorer verwenden, um zu bestimmen, welche Anwendungen Dateien sperren. Zum Herunterladen der Monitor "Prozess" oder die Prozess-Explorer finden Sie auf die [Process Monitor](https://docs.microsoft.com/sysinternals/downloads/procmon) und [Process Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer) Seiten.|

## <a name="step-3-copy-the-replicated-files-to-the-destination-server"></a>Schritt 3: Kopieren Sie die replizierte Dateien auf den Zielserver

Nachdem Sie Sperren für die Dateien, die repliziert werden minimieren, können Sie die Dateien vom Quellserver zum Zielserver Seeding.

>[!NOTE]
>Sie können die Robocopy auf dem Quellcomputer oder dem Zielcomputer ausführen. Das folgende Verfahren beschreibt das Ausführen von Robocopy auf dem Zielserver, der in der Regel ausgeführt wird ein neueres Betriebssystem, um keine zusätzlichen Robocopy-Funktionen nutzen, die das neuere Betriebssystem bereitstellen kann.

### <a name="preseed-the-replicated-files-onto-the-destination-server-with-robocopy"></a>Die replizierte Dateien auf den Zielserver mit Robocopy Seeding

1. Melden Sie sich auf den Zielserver mit einem Konto an, die ein Mitglied der lokalen Administratorengruppe auf den Quell-und Ziel ist.

2. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten.

3. Um die Dateien aus der Quelle zum Zielserver Seeding, führen Sie den folgenden Befehl aus, und Ersetzen Sie dabei Ihre eigenen Quelle, Ziel und Protokoll-Dateipfade für die in Klammern stehenden Werte ein:
    
    ```PowerShell
    robocopy "<source replicated folder path>" "<destination replicated folder path>" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:<log file path> /v
    ```
    
    Dieser Befehl kopiert alle Inhalte des Quellordners, in den Zielordner, mit den folgenden Parametern:
    
    |Parameter|Beschreibung|
    |---|---|
    |"\<Quelle repliziert Ordnerpfad\>"|Gibt an, der Quellordner, Seeding auf dem Zielserver.|
    |"\<Ziel repliziert Ordnerpfad\>"|Gibt den Pfad zu dem Ordner, in der die preseeded Dateien gespeichert werden.<br><br>Der Zielordner darf nicht bereits auf dem Zielserver vorhanden sein. Rufen Sie übereinstimmende Dateihashes muss Robocopy im Stammordner erstellen, wenn es sich um die Dateien preseeds.|
    |/ e|Kopiert, Unterverzeichnisse und ihre Dateien sowie die leeren Unterverzeichnisse.|
    |/b|Kopiert die Dateien im Sicherungsmodus bei protokollversandaufgaben.|
    |/copyall|Kopiert alle Dateiinformationen, einschließlich Daten, Attribute, Zeitstempel, der NTFS-Zugriffssteuerungsliste (ACL), Informationen über den sperrbesitzer und Überwachungsinformationen.|
    |/r:6|Wiederholt den Vorgang bis zu sechs Mal, wenn ein Fehler auftritt.|
    |/w:5|Wartet fünf Sekunden zwischen den Wiederholungen.|
    |MT:64|64 Dateien kopiert gleichzeitig.|
    |/xd DfsrPrivate|Schließt die Ordner DfsrPrivate.|
    |/Tee|Schreibt die Statusausgabe im Konsolenfenster sowie in die Protokolldatei.|
    |/ log \<Protokolldateipfad >|Gibt an, die Protokolldatei geschrieben. Wird der Inhalt der Datei vorhandenen überschrieben. (Verwenden, um die Einträge in die vorhandene Protokolldatei anzufügen `/log+ <log file path>`.)|
    |/v|Ausführliche Ausgabe erfolgt, die enthält ausgelassene Dateien.|
    
    Z. B. der folgende Befehl führt die Replikation vom repliziert Quellordner, "e:"\\RF01, auf Laufwerk D auf dem Zielserver:
    
    ```PowerShell
    robocopy.exe "\\srv01\e$\rf01" "d:\rf01" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:c:\temp\preseedsrv02.log
    ```
    
    >[!NOTE]
    >Es wird empfohlen, dass Sie die oben beschriebenen, bei der Verwendung von Robocopy, um die Dateien für die DFS-Replikation Seeding Parameter verwenden. Sie können jedoch einige der entsprechenden Werte ändern oder Hinzufügen von zusätzlichen Parametern. Angenommen, Sie möglicherweise feststellen, durch Tests, dass Sie die Kapazität für einen höheren Wert (Threadanzahl) festgelegt haben, für die *"/ MT"* Parameter. Auch wenn Sie in erster Linie größere Dateien replizieren müssen, Sie möglicherweise Kopie Leistungssteigerung durch Hinzufügen der **/j** Option für ungepufferte e/a. Weitere Informationen zu Robocopy-Parameter, finden Sie unter den [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy) Befehlszeilenreferenz.

    >[!WARNING]
    >Um potenzielle Datenverluste zu vermeiden, bei der Verwendung von Robocopy, um die Dateien für die DFS-Replikation Seeding, stellen Sie die folgenden Änderungen nicht auf die empfohlene Parameter:
    >- Verwenden Sie nicht die */mir* Parameter (die eine Verzeichnisstruktur spiegelt) oder die */mov* Parameter (das Verschieben der Dateien, und löscht sie aus der Quelle).
    >-  Entfernen Sie nicht die **/e**, **/b**, und **/copyall** Optionen.

4. Nachdem der Kopiervorgang abgeschlossen wurde, überprüfen Sie im Protokoll keine Fehler oder die übersprungene Dateien. Verwenden Sie Robocopy, um alle ausgelassenen Dateien einzeln, statt den gesamten Satz von Dateien bei einer zu kopieren. Wenn Dateien aufgrund von exklusiven Sperren übersprungen wurden, kopieren Sie einzelne Dateien mit Robocopy später noch Mal, oder akzeptieren Sie, dass diese Dateien die Over-the-Wire-Replikation mithilfe der DFS-Replikation bei der ersten Synchronisierung erforderlich sind.

## <a name="next-step"></a>Nächster Schritt

Nachdem Sie die erste Kopie abgeschlossen, und verwenden Sie Robocopy, um Probleme mit der Anzahl übersprungener Dateien wie möglich zu beheben, verwenden Sie die **Get-DfsrFileHash** Windows PowerShell-Cmdlet oder dem **Dfsrdiag** Befehl Überprüfen Sie die preseeded Dateien durch den Vergleich von Quell-und Ziel Dateihashes an. Ausführliche Anweisungen finden Sie unter [Schritt2: Überprüfen Sie die Preseeded Dateien für die DFS-Replikation](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495042(v%3dws.11)>).
