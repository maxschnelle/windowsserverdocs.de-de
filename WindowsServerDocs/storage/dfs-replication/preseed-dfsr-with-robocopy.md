---
title: Verwenden von Robocopy, um ein Vorab-Dateiseeding für die DFS-Replikation auszuführen
description: Informationen zur Verwendung von „Robocopy.exe“, um ein Vorab-Dateiseeding für die DFS-Replikation auszuführen.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8ff800fc2a0885cec39ca104607d7207f0bd8ce0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815603"
---
# <a name="use-robocopy-to-pre-seed-files-for-dfs-replication"></a>Verwenden von Robocopy, um ein Vorab-Dateiseeding für die DFS-Replikation auszuführen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

In diesem Thema wird erläutert, wie das Befehlszeilentool **Robocopy.exe** verwendet wird, um beim Einrichten der DFS-Replikation (auch als DFSR oder DFS-R bezeichnet) in Windows Server ein Vorab-Dateiseeding ausführen. Indem du vor dem Einrichten der DFS-Replikation (Distributed File System, verteiltes Dateisystem), dem Hinzufügen eines neuen Replikationspartners oder dem Austauschen eines Servers ein Vorab-Dateiseeding ausführst, kannst du die Erstsynchronisierung beschleunigen und das Klonen der DFS-Replikationsdatenbank in Windows Server 2012 R2 ermöglichen. Robocopy ist eine von mehreren Methoden für das Vorab-Seeding. Eine Übersicht findest du unter [Schritt 1: Ausführen eines Vorab-Dateiseedings für die DFS-Replikation](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495046(v%3dws.11)>).

Das Befehlszeilen-Hilfsprogramm Robocopy (Robust File Copy) ist in Windows Server enthalten. Das Hilfsprogramm bietet umfassende Optionen, beispielsweise das sichere Kopieren, Unterstützung der Sicherungs-API, Wiederholungsfunktionen und Protokollierung. Spätere Versionen umfassen Unterstützung für Multithreading und ungepufferte E/A.

>[!IMPORTANT]
>Robocopy kopiert keine exklusiv gesperrten Dateien. Wenn Benutzer auf den Dateiservern häufig viele Dateien für längere Zeit sperren, sollte eine andere Methode für das Vorab-Seeding verwendet werden. Für das Vorab-Seeding ist keine perfekte Übereinstimmung zwischen Dateilisten auf den Quell- und Zielservern erforderlich. Allerdings gilt: Je weniger Dateien bei der Erstsynchronisierung für die DFS-Replikation vorhanden sind, umso geringer ist die Effizienz des Vorab-Seedings. Um Sperrkonflikte zu minimieren, sollte Robocopy außerhalb der Spitzenzeiten in der Organisation verwendet werden. Nach dem Vorab-Seeding sollte anhand der Robocopy-Protokolle immer überprüft werden, welche Dateien aufgrund exklusiver Sperren übersprungen wurden.

Befolge diese Schritte, um mithilfe von Robocopy ein Vorab-Dateiseeding für die DFS-Replikation auszuführen:

1. [Herunterladen und Installieren der aktuellen Robocopy-Version](#step-1-download-and-install-the-latest-version-of-robocopy)
2. [Stabilisieren von Dateien, die repliziert werden](#step-2-stabilize-files-that-will-be-replicated)
3. [Kopieren der replizierten Dateien auf den Zielserver](#step-3-copy-the-replicated-files-to-the-destination-server)

## <a name="prerequisites"></a>Voraussetzungen

Da das Vorab-Seeding und die DFS-Replikation in keinem direkten Zusammenhang stehen, müssen nur die Anforderungen zum Kopieren von Dateien mit Robocopy erfüllt werden.

- Du benötigst ein Konto, das Mitglied der lokalen Administratorgruppe auf dem Quell- und dem Zielserver ist.

- Installiere die neueste Version von Robocopy auf dem Server, der zum Kopieren der Dateien verwendet wird – entweder auf dem Quellserver oder dem Zielserver. Es muss die neueste Version für die Betriebssystemversion installiert werden. Anweisungen findest du unter [Schritt 2: Stabilisieren von Dateien, die repliziert werden](#step-2-stabilize-files-that-will-be-replicated). Robocopy kann auf dem Quell- oder Zielserver ausgeführt werden, es sei denn, das Vorab-Dateiseeding erfolgt auf einem Server mit Windows Server 2003 R2. Der Zielserver, der in der Regel über die neuere Betriebssystemversion verfügt, bietet Zugriff auf die aktuelle Version von Robocopy.

- Auf dem Ziellaufwerk muss ausreichend Speicherplatz verfügbar sein. Es darf kein Ordner in dem Pfad erstellt werden, in den kopiert werden soll: Der Stammordner muss von Robocopy erstellt werden.
    
    >[!NOTE]
    >Bei der Entscheidung, wie viel Speicherplatz für die Dateien zugewiesen werden soll, für die ein Vorab-Seeding ausgeführt wurde, sollten der zukünftig erwartete Datenzuwachs und die Speicheranforderungen für die DFS-Replikation in Erwägung gezogen werden. Unterstützung bei der Planung findest du unter dem Thema zum [Bearbeiten der Kontingentgröße des Stagingordners und des Ordners „ConflictandDeleted“](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754229(v=ws.11)) unter [Verwalten der DFS-Replikation](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754771(v=ws.11)>).

- Installiere auf dem Quellserver optional den Prozessmonitor oder den Prozess-Explorer, mit dem du nach Anwendungen suchen kannst, durch die Dateien gesperrt werden. Informationen zum Download findest du unter [Prozessmonitor](https://docs.microsoft.com/sysinternals/downloads/procmon) und [Prozess-Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer).

## <a name="step-1-download-and-install-the-latest-version-of-robocopy"></a>Schritt 1: Herunterladen und Installieren der aktuellen Robocopy-Version

Bevor du Robocopy zum Vorab-Dateiseeding verwendest, solltest du die aktuelle Version von **Robocopy.exe** herunterladen und installieren. Dadurch wird verhindert, dass Dateien aufgrund von Problemen in den ausgelieferten Robocopy-Versionen von der DFS-Replikation übersprungen werden.

Die Quelle für die neueste kompatible Robocopy-Version hängt von der Windows Server-Version ab, die auf dem Server ausgeführt wird. Informationen zum Herunterladen des Hotfix mit der aktuellen Version von Robocopy für Windows Server 2008 R2 oder Windows Server 2008 findest du in der [Liste der derzeit verfügbaren Hotfixes für DFS-Technologien in Windows Server 2008 und in Windows Server 2008 R2](https://support.microsoft.com/help/968429/list-of-currently-available-hotfixes-for-distributed-file-system-dfs-t).

Mit den folgenden Schritten kannst du alternativ den aktuellen Hotfix für ein Betriebssystem suchen und installieren.

### <a name="locate-and-install-the-latest-version-of-robocopy-for-a-specific-version-of-windows-server"></a>Suchen und Installieren der aktuellen Version von Robocopy für eine bestimmte Windows Server-Version

1. Öffne in einem Webbrowser [https://support.microsoft.com](https://support.microsoft.com/).

2. Gib in **Support durchsuchen** die folgende Zeichenfolge ein, ersetze `<operating system version>` durch das entsprechende Betriebssystem, und drücke dann die EINGABETASTE:
    
    ```robocopy.exe kbqfe "<operating system version>"```
    
    Gib beispielsweise **robocopy.exe kbqfe „Windows Server 2008 R2“** ein.

3. Suche und lade den Hotfix mit der höchsten ID (d. h. die aktuelle Version) herunter.

4. Installiere den Hotfix auf dem Server.

## <a name="step-2-stabilize-files-that-will-be-replicated"></a>Schritt 2: Stabilisieren von Dateien, die repliziert werden

Nachdem du die aktuelle Version von Robocopy auf dem Server installiert hast, solltest du mithilfe der in der folgenden Tabelle beschriebenen Methoden verhindern, dass Kopiervorgänge durch gesperrte Dateien blockiert werden. Bei den meisten Anwendungen werden Dateien nicht exklusiv gesperrt. Während des normalen Betriebs kann es jedoch vorkommen, dass ein geringer Prozentsatz von Dateien auf Dateiservern gesperrt wird.

|Ursprung der Sperre|Erläuterung|Abhilfemaßnahmen|
|---|---|---|
|Benutzer öffnen Dateien im Remotemodus auf Freigaben.|Mitarbeiter stellen eine Verbindung mit einem Standarddateiserver her und bearbeiten Dokumente, Multimediainhalte oder andere Dateien. Werden zeitweise auch als herkömmlicher Basisordner oder als freigegebene Datenworkloads bezeichnet.|Robocopy-Vorgänge sollten nur außerhalb der Spitzen- und Geschäftszeiten ausgeführt werden. Dadurch wird die Anzahl der Dateien minimiert, die von Robocopy während des Vorab-Seedings übersprungen werden müssen.<br><br>Mit den Windows PowerShell-Cmdlets **Grant-SmbShareAccess** und **Close-SmbSession** kannst du für die zu replizierenden Dateifreigaben vorübergehend den schreibgeschützten Zugriff festlegen. Wenn du Berechtigungen für eine allgemeine Gruppe wie „Jeder“ oder „Authentifizierte Benutzer“ auf Lesezugriff festlegst, ist es weniger wahrscheinlich, dass Standardbenutzer Dateien mit exklusiven Sperren öffnen (wenn der Schreibschutz beim Öffnen der Dateien von ihren Anwendungen erkannt wird).<br><br>Du könntest auf dem jeweiligen Server auch eine temporäre Firewallregel für eingehende Daten an SMB-Port 445 festlegen, um den Zugriff auf die Dateien zu blockieren, oder das **Block-SmbShareAccess**-Cmdlet verwenden. Allerdings haben beide Methoden starke Auswirkungen auf die Benutzerfreundlichkeit.|
|Dateien werden von Anwendungen lokal geöffnet.|Dateien werden manchmal von Anwendungsworkloads gesperrt, die auf einem Dateiserver ausgeführt werden.|Die Anwendungen, durch die Dateien gesperrt werden, sollten vorübergehend deaktiviert oder deinstalliert werden. Um zu ermitteln, durch welche Anwendungen Dateien gesperrt werden, kannst du den Prozessmonitor oder Prozess-Explorer verwenden. Der Prozessmonitor kann von der Seite [Process Monitor](https://docs.microsoft.com/sysinternals/downloads/procmon) oder der Prozess-Explorer von der Seite [Process Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer) heruntergeladen werden.|

## <a name="step-3-copy-the-replicated-files-to-the-destination-server"></a>Schritt 3: Kopieren der replizierten Dateien auf den Zielserver

Nachdem du die Anzahl der Sperren für die zu replizierenden Dateien verringert hast, kannst du ein Vorab-Dateiseeding vom Quellserver auf den Zielserver durchführen.

>[!NOTE]
>Robocopy kann entweder auf dem Quellcomputer oder auf dem Zielcomputer ausgeführt werden. Im folgenden Verfahren wird die Ausführung von Robocopy auf dem Zielserver beschrieben, auf dem normalerweise ein aktuelleres Betriebssystem ausgeführt wird. So können alle zusätzlichen Robocopy-Funktionen genutzt werden, die das neuere Betriebssystem möglicherweise bereitstellt.

### <a name="pre-seed-the-replicated-files-onto-the-destination-server-with-robocopy"></a>Verwenden von Robocopy, um für die replizierten Dateien ein Vorab-Seeding auf den Zielserver auszuführen

1. Melde dich mit einem Konto beim Zielserver an, das Mitglied der lokalen Administratorgruppe auf dem Quell- und dem Zielserver ist.

2. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten.

3. Führe den folgenden Befehl aus, um ein Vorab-Dateiseeding vom Quell- auf den Zielserver auszuführen. Ersetze dabei die Werte in Klammern durch die Pfade für deinen eigenen Quell- und Zielserver und die Protokolldatei:
    
    ```PowerShell
    robocopy "<source replicated folder path>" "<destination replicated folder path>" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:<log file path> /v
    ```
    
    Mit diesem Befehl und den folgenden Parametern wird der gesamte Inhalt des Quellordners in den Zielordner kopiert:
    
    |Parameter|Beschreibung|
    |---|---|
    |„\<Pfad des replizierten Quellordners\>“|Gibt den Quellordner an, für den ein Vorab-Seeding auf den Zielserver ausgeführt wird.|
    |„\<Pfad des replizierten Zielordners\>“|Gibt den Pfad zu dem Ordner an, in dem die Dateien nach dem Vorab-Seeding gespeichert werden.<br><br>Der Zielordner darf noch nicht auf dem Zielserver vorhanden sein. Um übereinstimmende Dateihashes zu erhalten, muss der Stammordner von Robocopy erstellt werden, wenn das Vorab-Dateiseeding ausgeführt wird.|
    |/e|Kopiert Unterverzeichnisse und die enthaltenen Dateien sowie leere Unterverzeichnisse.|
    |/b|Kopiert Dateien im Sicherungsmodus.|
    |/copyall|Kopiert alle Dateiinformationen, einschließlich Daten, Attribute, Zeitstempel, NTFS-Zugriffssteuerungsliste sowie Informationen zum Besitzer und zur Überwachung.|
    |/r:6|Wiederholt den Vorgang sechsmal, wenn ein Fehler auftritt.|
    |/w:5|Wartet 5 Sekunden zwischen den Wiederholungen.|
    |MT:64|Kopiert 64 Dateien gleichzeitig.|
    |/xd DfsrPrivate|Schließt den Ordner „DfsrPrivate“ aus.|
    |/tee|Schreibt die Statusausgabe in das Konsolenfenster sowie in die Protokolldatei.|
    |/log \<Protokolldateipfad>|Gibt die zu schreibende Protokolldatei an. Überschreibt den vorhandenen Inhalt der Datei. (Verwende `/log+ <log file path>`, um Einträge an die vorhandene Protokolldatei anzufügen.)|
    |/v|Erzeugt eine ausführliche Ausgabe, die übersprungene Dateien einschließt.|
    
    Beispiel: Mit dem folgenden Befehl werden Dateien vom replizierten Quellordner „E:\\RF01“ auf das Datenlaufwerk „D“ auf dem Zielserver repliziert:
    
    ```PowerShell
    robocopy.exe "\\srv01\e$\rf01" "d:\rf01" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:c:\temp\pre-seedsrv02.log
    ```
    
    >[!NOTE]
    >Es wird empfohlen, die oben beschriebenen Parameter zu verwenden, wenn mit Robocopy ein Vorab-Dateiseeding für die DFS-Replikation ausgeführt wird. Allerdings können einige Parameterwerte geändert oder weitere Parameter hinzugefügt werden. Beispielsweise könnten Tests ergeben, dass genügend Kapazität vorhanden ist, um für den Parameter */MT* (Anzahl der Threads) einen höheren Wert festzulegen. Wenn in erster Linie größere Dateien repliziert werden, könnte die Kopierleistung verbessert werden, indem die Option **/j** für ungepufferte E/A hinzugefügt wird. Weitere Informationen zu Robocopy-Parametern findest du in der Befehlszeilenreferenz zu [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy).

    >[!WARNING]
    >Um potenzielle Datenverluste zu vermeiden, wenn Robocopy zum Vorab-Dateiseeding für die DFS-Replikation verwendet wird, sollten an den empfohlenen Parametern keine der folgenden Änderungen vorgenommen werden:
    >- Der Parameter */mir* (der eine Verzeichnisstruktur spiegelt) oder der Parameter */mov* (der die Dateien verschiebt und dann aus der Quelle löscht) sollte nicht verwendet werden.
    >-  Die Optionen **/e**, **/b** und **/copyall** dürfen nicht entfernt werden.

4. Nachdem der Kopiervorgang abgeschlossen ist, überprüfe das Protokoll auf Fehler oder übersprungene Dateien. Verwende Robocopy, um übersprungene Dateien einzeln zu kopieren, anstatt den gesamten Dateisatz erneut zu kopieren. Wenn Dateien aufgrund exklusiver Sperren übersprungen wurden, solltest du später versuchen, einzelne Dateien mit Robocopy zu kopieren, oder akzeptieren, dass diese Dateien während der Erstsynchronisierung per DFS-Replikation über das Netzwerk repliziert werden müssen.

## <a name="next-step"></a>Nächster Schritt

Nachdem die erste Kopie abgeschlossen ist und möglichst viele Probleme aufgrund übersprungener Dateien mithilfe von Robocopy behoben wurden, verwendest du das **Get-DfsrFileHash**-Cmdlet in Windows PowerShell oder den Befehl **Dfsrdiag**, um die Dateien, für die ein Vorab-Seeding ausgeführt wurde, zu überprüfen. Dazu vergleichst du Dateihashes auf dem Quellserver und dem Zielserver. Ausführliche Anweisungen findest du unter [Schritt 2: Überprüfen von Dateien, für die ein Vorab-Seeding ausgeführt wurde, für die DFS-Replikation](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495042(v%3dws.11)>).
