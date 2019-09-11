---
title: Verwenden von Robocopy zum Seeding für von Dateien für DFS-Replikation
description: Verwenden von "Robocopy. exe" zum vorab Seed von Dateien für DFS-Replikation.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 05/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4a0cad3c685c8609784c7096fe31d55294712c2e
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871980"
---
# <a name="use-robocopy-to-preseed-files-for-dfs-replication"></a>Verwenden von Robocopy zum Seeding für von Dateien für DFS-Replikation

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

In diesem Thema wird erläutert, wie Sie das Befehlszeilen Tool **Robocopy. exe**verwenden, um Dateien beim Einrichten der Replikation für die verteiltes Dateisystem (DFS)-Replikation (auch als DFSR oder DFS-R bezeichnet) in Windows Server zu Seeding für. Indem Sie Dateien vor dem Einrichten DFS-Replikation hinzufügen, einen neuen Replikations Partner hinzufügen oder einen Server ersetzen, können Sie die erst Synchronisierung beschleunigen und das Klonen der DFS-Replikation Datenbank in Windows Server 2012 R2 aktivieren. Die Robocopy-Methode ist eine von mehreren Preseeding-Methoden. eine Übersicht finden Sie unter [Step 1: Seeding für files for DFS-Replikation](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495046(v%3dws.11)>).

Das Befehlszeilenprogramm Robocopy (robustes Datei kopieren) ist in Windows Server enthalten. Das Hilfsprogramm bietet umfassende Optionen, darunter das Kopieren von Sicherheit, Backup-API-Unterstützung, Wiederholungs Funktionen und Protokollierung. Spätere Versionen umfassen Multithreading-und nicht gepufferte e/a-Unterstützung.

>[!IMPORTANT]
>Robocopy kopiert exklusiv gesperrte Dateien nicht. Wenn Benutzer in der Regel viele Dateien für lange Zeiträume auf den Dateiservern sperren, sollten Sie eine andere Preseeding-Methode verwenden. Für das präseeding ist keine perfekte Entsprechung zwischen Dateilisten auf den Quell-und Ziel Servern erforderlich, aber je mehr Dateien nicht vorhanden sind, wenn die erste Synchronisierung für DFS-Replikation ausgeführt wird, desto weniger effektiv ist das vorseeding. Um Sperr Konflikte zu minimieren, verwenden Sie Robocopy für Ihre Organisation außerhalb der Spitzenzeiten. Überprüfen Sie immer die Robocopy-Protokolle nach dem Preseeding, um sicherzustellen, dass Sie wissen, welche Dateien aufgrund exklusiver Sperren übersprungen wurden.

Führen Sie die folgenden Schritte aus, um Robocopy zum Seeding für von Dateien für DFS-Replikation zu verwenden:

1. [Laden Sie die neueste Version von Robocopy herunter, und installieren Sie Sie.](#step-1-download-and-install-the-latest-version-of-robocopy)
2. [Stabilisieren von Dateien, die repliziert werden.](#step-2-stabilize-files-that-will-be-replicated)
3. [Kopieren Sie die replizierten Dateien auf den Zielserver.](#step-3-copy-the-replicated-files-to-the-destination-server)

## <a name="prerequisites"></a>Erforderliche Komponenten

Da das präseeding nicht direkt DFS-Replikation einschließt, müssen Sie nur die Anforderungen zum Ausführen einer Dateikopie mit Robocopy erfüllen.

- Sie benötigen ein Konto, das Mitglied der lokalen Administratoren Gruppe auf dem Quell-und dem Zielserver ist.

- Installieren Sie die neueste Version von Robocopy auf dem Server, den Sie zum Kopieren der Dateien verwenden möchten – entweder den Quell Server oder den Zielserver; Sie müssen die neueste Version für die Betriebssystemversion installieren. Anweisungen finden [Sie unterschritt 2: Stabilisieren von Dateien, die repliziert](#step-2-stabilize-files-that-will-be-replicated)werden. Wenn Sie Dateien nicht von einem Server mit Windows Server 2003 R2 vorab bereitstellen, können Sie Robocopy entweder auf dem Quell-oder Zielserver ausführen. Der Zielserver, der in der Regel über die aktuellste Version des Betriebssystems verfügt, bietet Ihnen Zugriff auf die neueste Version von Robocopy.

- Stellen Sie sicher, dass auf dem Ziellaufwerk ausreichend Speicherplatz verfügbar ist. Erstellen Sie keinen Ordner auf dem Pfad, in den Sie kopieren möchten: Robocopy muss den Stamm Ordner erstellen.
    
    >[!NOTE]
    >Wenn Sie entscheiden, wie viel Speicherplatz für die vorab bereitgestellten Dateien belegt werden soll, sollten Sie die erwartete Daten Vergrößerung im Zeitverlauf und die Speicheranforderungen für DFS-Replikation in Erwägung gezogen Hilfe zur Planung finden Sie unter [Bearbeiten der Kontingent Größe des Stagingordners und des Konflikts und gelöschten Ordners](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754229(v=ws.11)) in [Verwalten von DFS-Replikation](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754771(v=ws.11)>).

- Installieren Sie auf dem Quell Server optional den Prozess Monitor oder den Prozess-Explorer, mit dem Sie nach Anwendungen suchen können, die Dateien sperren. Informationen zum Herunterladen finden Sie unter [Prozess Monitor](https://docs.microsoft.com/sysinternals/downloads/procmon) und [Prozess-Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer).

## <a name="step-1-download-and-install-the-latest-version-of-robocopy"></a>Schritt 1: Herunterladen und Installieren der neuesten Version von Robocopy

Bevor Sie Robocopy zum Seeding für von Dateien verwenden, sollten Sie die neueste Version von **Robocopy. exe**herunterladen und installieren. Dadurch wird sichergestellt, dass DFS-Replikation Dateien aufgrund von Problemen in den Liefer Versionen von Robocopy nicht überspringt.

Die Quelle für die neueste kompatible Robocopy-Version hängt von der Version von Windows Server ab, die auf dem Server ausgeführt wird. Informationen zum Herunterladen des Hotfixes mit der neuesten Version von Robocopy für Windows Server 2008 R2 oder Windows Server 2008 finden Sie [in der Liste der derzeit verfügbaren Hotfixes für verteiltes Dateisystem-Technologien (DFS) unter Windows Server 2008 und in. Windows Server 2008 R2](https://support.microsoft.com/help/968429/list-of-currently-available-hotfixes-for-distributed-file-system-dfs-t).

Alternativ dazu können Sie den neuesten Hotfix für ein Betriebssystem suchen und installieren, indem Sie die folgenden Schritte ausführen.

### <a name="locate-and-install-the-latest-version-of-robocopy-for-a-specific-version-of-windows-server"></a>Suchen und Installieren der neuesten Version von Robocopy für eine bestimmte Version von Windows Server

1. Öffnen [https://support.microsoft.com](https://support.microsoft.com/)Sie in einem Webbrowser.

2. Geben Sie in der **Suchunterstützung**die folgende Zeichenfolge `<operating system version>` ein, und ersetzen Sie dabei durch das entsprechende Betriebssystem. Drücken Sie dann die EINGABETASTE:
    
    ```robocopy.exe kbqfe "<operating system version>"```
    
    Geben Sie beispielsweise **Robocopy. exe kbqfe "Windows Server 2008 R2"** ein.

3. Suchen und laden Sie den Hotfix mit der höchsten ID (d. h. der neuesten Version) herunter.

4. Installieren Sie den Hotfix auf dem Server.

## <a name="step-2-stabilize-files-that-will-be-replicated"></a>Schritt 2: Dateien stabilisieren, die repliziert werden

Nachdem Sie die aktuelle Version von Robocopy auf dem-Server installiert haben, sollten Sie verhindern, dass gesperrte Dateien das Kopieren blockieren, indem Sie die Methoden verwenden, die in der folgenden Tabelle beschrieben sind. Bei den meisten Anwendungen werden Dateien nicht exklusiv gesperrt. Während des normalen Betriebs kann es jedoch vorkommen, dass ein kleiner Prozentsatz der Dateien auf Dateiservern gesperrt ist.

|Quelle der Sperre|Erläuterung|Abhilfemaßnahmen|
|---|---|---|
|Benutzer öffnen Dateien auf Freigaben Remote.|Mitarbeiter stellen eine Verbindung mit einem Standarddatei Server her und Bearbeiten Dokumente, Multimedia-Inhalte oder andere Dateien. Wird manchmal auch als herkömmlicher Basisordner oder freigegebene datenworkloads bezeichnet.|Führen Sie Robocopy-Vorgänge nur außerhalb der Spitzenzeiten außerhalb der Geschäftszeiten aus. Dadurch wird die Anzahl der Dateien minimiert, die Robocopy während des Preseeding überspringen muss.<br><br>Legen Sie den schreibgeschützten Zugriff auf die Dateifreigaben, die mithilfe der Windows PowerShell-Cmdlets " **Grant-smbshareaccess** " und " **Close-smbsession** " repliziert werden, vorübergehend fest. Wenn Sie Berechtigungen für eine gemeinsame Gruppe, z. b. für alle Benutzer oder authentifizierte Benutzer, festgelegt haben, können Standardbenutzer weniger wahrscheinlich Dateien mit exklusiven Sperren öffnen (wenn Ihre Anwendungen den schreibgeschützten Zugriff erkennen, wenn Dateien geöffnet werden).<br><br>Sie können auch eine temporäre Firewallregel für den eingehenden SMB-Port 445 auf diesen Server festlegen, um den Zugriff auf Dateien zu blockieren oder das Cmdlet " **Block-smbshareaccess** " zu verwenden. Allerdings wirken sich beide Methoden stark auf Benutzer Vorgänge aus.|
|Anwendungen öffnen lokale Dateien.|Anwendungsworkloads, die auf einem Dateiserver ausgeführt werden, Sperren manchmal Dateien.|Temporäres deaktivieren oder Deinstallieren der Anwendungen, die Dateien sperren. Sie können den Prozess Monitor oder den Prozess-Explorer verwenden, um zu bestimmen, welche Anwendungen Dateien sperren. Zum Herunterladen von Process Monitor oder Process Explorer besuchen Sie die Seite [Prozessmonitor](https://docs.microsoft.com/sysinternals/downloads/procmon) und [Prozess-Explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer) .|

## <a name="step-3-copy-the-replicated-files-to-the-destination-server"></a>Schritt 3: Kopieren der replizierten Dateien auf den Zielserver

Nachdem Sie die Sperren für die Dateien minimiert haben, die repliziert werden, können Sie die Dateien vom Quell Server auf den Zielserver vorab einschleusen.

>[!NOTE]
>Sie können Robocopy entweder auf dem Quellcomputer oder auf dem Zielcomputer ausführen. Im folgenden Verfahren wird die Ausführung von Robocopy auf dem Zielserver beschrieben, auf dem normalerweise ein aktuelleres Betriebssystem ausgeführt wird, um alle zusätzlichen Robocopy-Funktionen zu nutzen, die das aktuellere Betriebssystem möglicherweise bereitstellt.

### <a name="preseed-the-replicated-files-onto-the-destination-server-with-robocopy"></a>Präseed der replizierten Dateien auf dem Zielserver mit Robocopy

1. Melden Sie sich beim Zielserver mit einem Konto an, das Mitglied der lokalen Administratoren Gruppe auf dem Quell-und dem Zielserver ist.

2. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten.

3. Führen Sie den folgenden Befehl aus, um die Dateien von der Quell-zum Zielserver vorzuleiten, und ersetzen Sie dabei die Werte für die in Klammern stehenden Werte für Quelle, Ziel und Protokolldatei:
    
    ```PowerShell
    robocopy "<source replicated folder path>" "<destination replicated folder path>" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:<log file path> /v
    ```
    
    Dieser Befehl kopiert den gesamten Inhalt des Quell Ordners in den Zielordner mit den folgenden Parametern:
    
    |Parameter|Beschreibung|
    |---|---|
    |"\<replizierter Ordner Pfad\>für Quelle"|Gibt den Quellordner für den präseed auf dem Zielserver an.|
    |"\<Pfad\>des replizierten Ziel Ordners"|Gibt den Pfad zu dem Ordner an, in dem die Dateien mit dem präseeding gespeichert werden.<br><br>Der Zielordner darf nicht bereits auf dem Zielserver vorhanden sein. Um übereinstimmende Dateihashes zu erhalten, muss Robocopy den Stamm Ordner erstellen, wenn die Dateien vorab erstellt werden.|
    |/e|Kopiert Unterverzeichnisse und Ihre Dateien sowie leere Unterverzeichnisse.|
    |/b|Kopiert Dateien im Sicherungs Modus.|
    |/copyall|Kopiert alle Dateiinformationen, einschließlich Daten, Attribute, Zeitstempel, NTFS-Zugriffs Steuerungs Liste (Access Control List, ACL), Besitzer Informationen und Überwachungsinformationen.|
    |/r: 6|Wiederholt den Vorgang sechs Mal, wenn ein Fehler auftritt.|
    |/w: 5|Wartet 5 Sekunden zwischen den Wiederholungen.|
    |MT: 64|Kopiert 64-Dateien gleichzeitig.|
    |/xD DfsrPrivate|Schließt den DfsrPrivate-Ordner aus.|
    |/tee|Schreibt die Status Ausgabe in das Konsolenfenster sowie in die Protokolldatei.|
    |/log \<Protokolldatei Pfad >|Gibt die zu schreibende Protokolldatei an. Überschreibt den vorhandenen Inhalt der Datei. (Verwenden `/log+ <log file path>`Sie, um die Einträge an die vorhandene Protokolldatei anzufügen.)|
    |/v|Erzeugt eine ausführliche Ausgabe, die übersprungene Dateien einschließt.|
    
    Der folgende Befehl repliziert z. b. Dateien aus dem replizierten Quellordner "\\E: RF01" auf das Daten Laufwerk D auf dem Zielserver:
    
    ```PowerShell
    robocopy.exe "\\srv01\e$\rf01" "d:\rf01" /e /b /copyall /r:6 /w:5 /MT:64 /xd DfsrPrivate /tee /log:c:\temp\preseedsrv02.log
    ```
    
    >[!NOTE]
    >Es wird empfohlen, die oben beschriebenen Parameter zu verwenden, wenn Sie Robocopy verwenden, um Dateien für DFS-Replikation vorab zu verwenden. Sie können jedoch einige ihrer Werte ändern oder weitere Parameter hinzufügen. Beispielsweise können Sie testen, ob Sie über die Kapazität verfügen, einen höheren Wert (Thread Anzahl) für den */MT* -Parameter festzulegen. Wenn Sie in erster Linie größere Dateien replizieren, können Sie die Kopier Leistung möglicherweise erhöhen, indem Sie die **/j** -Option für nicht gepufferte e/a-Vorgänge hinzufügen. Weitere Informationen zu Robocopy-Parametern finden Sie in der [Robocopy](https://docs.microsoft.com/windows-server/administration/windows-commands/robocopy) -Befehlszeilen Referenz.

    >[!WARNING]
    >Um potenzielle Datenverluste zu vermeiden, wenn Sie Robocopy verwenden, um Dateien für DFS-Replikation zu Seeding für, nehmen Sie die folgenden Änderungen an den empfohlenen Parametern nicht vor:
    >- Verwenden Sie nicht den */mir* -Parameter (der eine Verzeichnisstruktur spiegelt) oder den */MOV* -Parameter (der die Dateien verschiebt und dann aus der Quelle löscht).
    >-  Entfernen Sie die Optionen **/e**, **/b**und **/COPYALL** nicht.

4. Nachdem der Kopiervorgang abgeschlossen ist, überprüfen Sie das Protokoll auf Fehler oder übersprungene Dateien. Verwenden Sie Robocopy, um ausgelassene Dateien einzeln zu kopieren, anstatt den gesamten Satz von Dateien neu zu verwenden. Wenn Dateien aufgrund exklusiver Sperren übersprungen wurden, versuchen Sie, einzelne Dateien später mit Robocopy zu kopieren, oder akzeptieren Sie, dass diese Dateien über die Netzwerk Replikation durch DFS-Replikation während der ersten Synchronisierung erforderlich sind.

## <a name="next-step"></a>Nächster Schritt

Nachdem Sie die erste Kopie fertiggestellt haben, und verwenden Sie Robocopy, um Probleme mit so vielen übersprungenen Dateien wie möglich zu beheben, verwenden Sie das **Get-dfsrfilehash** -Cmdlet in Windows PowerShell oder den **Dfsrdiag** -Befehl, um die vorab bereitgestellten Dateien zu überprüfen, indem Sie vergleichen. Dateihashes auf den Quell-und Ziel Servern. Ausführliche Anweisungen finden [Sie unterschritt 2: Überprüfen Sie Dateien, die dem](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn495042(v%3dws.11)>)DFS-Replikation vorangestehen sind.
