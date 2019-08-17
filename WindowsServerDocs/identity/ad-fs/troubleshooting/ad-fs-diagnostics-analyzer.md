---
title: AD FS-Hilfe Diagnose Analyzer
description: In diesem Dokument wird AD FS Help Diagnostics Analyzer beschrieben und erläutert, wie die grundlegenden Prüfungen mithilfe AD FS Diagnose-PowerShell-Moduls durchgeführt werden können.
author: billmath
ms.author: billmath
manager: mtillman
ms.reviewer: anandyadavMSFT
ms.date: 03/29/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6b6b7563aaa1f3c7d706cfdd172faf18417623e5
ms.sourcegitcommit: 0467b8e69de66e3184a42440dd55cccca584ba95
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546581"
---
# <a name="ad-fs-help-diagnostics-analyzer"></a>AD FS-Hilfe Diagnose Analyzer

AD FS verfügt über zahlreiche Einstellungen, die die Vielzahl der Funktionen unterstützen, die für die Authentifizierung und Anwendungsentwicklung zur Verfügung stehen. Bei der Problembehandlung wird empfohlen, sicherzustellen, dass alle AD FS Einstellungen ordnungsgemäß konfiguriert sind. Eine manuelle Überprüfung dieser Einstellungen kann mitunter zeitaufwändig sein. AD FS Help Diagnostics Analyzer kann bei der Durchführung der grundlegenden Prüfungen mithilfe des PowerShell-Moduls "adfstoolbox" helfen. Nachdem Sie die Überprüfungen durchgeführt haben, stellt AD FS Hilfe den [Diagnose Analyse](https://aka.ms/adfsdiagnosticsanalyzer) Tool bereit, mit dem Sie die Ergebnisse leicht visualisieren und Korrekturmaßnahmen anbieten können.

Der Vorgang "Complete" erfordert drei einfache Schritte:

1. Einrichten des adfstoolbox-Moduls auf dem primären AD FS Server oder WAP-Server
2. Ausführen der Diagnose und Hochladen der Datei in AD FS Hilfe
3. Anzeigen der Diagnose Analyse und Beheben von Problemen

Wechseln Sie zu [AD FS Help Diagnostics Analyzer https://aka.ms/adfsdiagnosticsanalyzer) (](https://aka.ms/adfsdiagnosticsanalyzer) um die Problembehandlung zu beginnen.

![AD FS Diagnostics Analyzer-Tool auf AD FS Hilfe](media/ad-fs-diagonostics-analyzer/home.png)

## <a name="step-1-setup-the-adfstoolbox-module-on-ad-fs-server"></a>Schritt 1: Einrichten des adfstoolbox-Moduls auf AD FS Server

Zum Ausführen der [Diagnose Analyse](https://aka.ms/adfsdiagnosticsanalyzer)müssen Sie das adfstoolbox-PowerShell-Modul installieren. Wenn der AD FS Server über eine Internetverbindung verfügt, können Sie das Modul adfstoolbox direkt aus dem PowerShell-Katalog installieren. Wenn keine Internetverbindung besteht, können Sie diese manuell installieren. 

[!WARNING]
Wenn Sie AD FS 2,1 oder niedriger verwenden, müssen Sie die Version 1.0.13 von adfstoolbox installieren. Adfstoolbox unterstützt nicht mehr AD FS 2,1 oder niedriger in den neuesten Versionen.

![AD FS Diagnostics Analyzer-Setup](media/ad-fs-diagonostics-analyzer/step1_v2.png)

### <a name="setup-using-powershell-gallery"></a>Einrichten mithilfe des PowerShell-Katalogs

Wenn der AD FS Server über eine Internetverbindung verfügt, empfiehlt es sich, das adfstoolbox-Modul direkt aus dem PowerShell-Katalog zu installieren, indem Sie die unten angegebenen PowerShell-Befehle verwenden.

   ```powershell
    Install-Module -Name ADFSToolbox -force
    Import-Module ADFSToolbox -force
   ```

### <a name="setup-manually"></a>Manuelles Setup

Das Modul adfstoolbox muss manuell auf die AD FS-oder WAP-Server kopiert werden. Befolgen Sie die Anweisungen unten.

1. Starten Sie ein PowerShell-Fenster mit erhöhten Rechten auf einem Computer mit Internet Zugriff.
2. Installieren Sie das AD FS Toolbox-Modul.

    ```powershell
    Install-Module -Name ADFSToolbox -Force
    ```
3. Kopieren Sie den Ordner "adfstoolbox", der sich auf dem lokalen Computer befindet `%SYSTEMDRIVE%\Program Files\WindowsPowerShell\Modules\` , an denselben Speicherort auf dem AD FS-oder WAP-Computer.

4. Starten Sie auf dem AD FS Computer ein PowerShell-Fenster mit erhöhten Rechten, und führen Sie das folgende Cmdlet aus, um das Modul zu importieren

    ```powershell
    Import-Module ADFSToolbox -Force
    ```

## <a name="step-2-execute-the-diagnostics-cmdlet"></a>Schritt 2: Ausführen des Diagnose-Cmdlets

![AD FS Diagnostics Analyzer-Tool-Ergebnisse ausführen und hochladen](media/ad-fs-diagonostics-analyzer/step2_v2.png)

Ein einziger Befehl kann verwendet werden, um die Diagnosetests auf allen AD FS Servern in der Farm zu testen. Das PowerShell-Modul verwendet Remote-PS-Sitzungen, um die Diagnosetests auf verschiedenen Servern in der Farm auszuführen.

```powershell
    Export-AdfsDiagnosticsFile [-ServerNames <list of servers>]
```

Auf einem Server 2016 oder höher AD FS Farm liest der Befehl die Liste der AD FS Server aus AD FS Konfiguration. Anschließend wird versucht, die Diagnosetests für jeden Server in der Liste auszuführen. Wenn die Liste der AD FS Server nicht verfügbar ist (Beispiel 2012r2), werden die Tests auf dem lokalen Computer ausgeführt. Zum Angeben einer Liste von Servern, für die die Tests ausgeführt werden sollen, verwenden Sie das Argument " **servernames** ", um eine Liste mit Servern bereitzustellen. Unten ist ein Beispiel angegeben.

```powershell
    Export-AdfsDiagnosticsFile -ServerNames @("adfs1.contoso.com", "adfs2.contoso.com")
```

Das Ergebnis ist eine JSON-Datei, die in demselben Verzeichnis erstellt wird, in dem der Befehl ausgeführt wurde. Der Name der Datei lautet adfsdiagnosticsfile-\<Zeitstempel.\> Ein Beispiel Dateiname lautet adfsdiagnosticsfile-07312019-184201. JSON.

## <a name="step-3-upload-the-diagnostics-file"></a>Schritt 3: Diagnose Datei hochladen

Wählen Sie in Schritt [https://aka.ms/adfsdiagnosticsanalyzer](https://aka.ms/adfsdiagnosticsanalyzer) 3 unter Verwenden des Datei Browsers aus, um die hoch zuladende Ergebnisdatei auszuwählen.

Klicken Sie auf **hochladen** , um den Upload abzuschließen.

Wenn Sie sich mit einem Microsoft-Konto anmelden, können die Diagnoseergebnisse zu einem späteren Zeitpunkt gespeichert werden und können an den Microsoft-Support gesendet werden. Wenn Sie zu einem beliebigen Zeitpunkt einen Supportfall öffnen, kann Microsoft die Diagnose Analyseergebnisse anzeigen und das Problem schneller beheben.

![AD FS Diagnostics Analyzer-Tool-anmelden](media/ad-fs-diagonostics-analyzer/sign_in_step.png)

## <a name="step-4-view-diagnostics-analysis-and-resolve-any-issues"></a>Schritt 4: Anzeigen der Diagnose Analyse und Beheben von Problemen

Es gibt fünf Abschnitte der Testergebnisse:

1. Fehlgeschlagen: Dieser Abschnitt enthält eine Liste der fehlgeschlagenen Tests. Jedes Ergebnis umfasst Folgendes:
2. Warnung: Dieser Abschnitt enthält eine Liste der Tests, die zu einer Warnung geführt haben. Diese Probleme führen nicht wahrscheinlich zu Problemen bei der Authentifizierung auf einer umfassenderen Skala, sollten aber frühestens behandelt werden.
3. Vor Dieser Abschnitt enthält die Liste der Tests, die bestanden wurden und für die kein Aktions Element für den Benutzer vorhanden ist.
4. Nicht ausgeführt: Dieser Abschnitt enthält die Liste der Tests, die aufgrund fehlender Informationen nicht ausgeführt werden konnten.
5. Nicht zutreffend: Dieser Abschnitt enthält die Liste der Tests, die nicht ausgeführt wurden, weil Sie nicht für den jeweiligen Server anwendbar waren, auf dem der Befehl ausgeführt wurde.

![AD FS Diagnostics Analyzer Tool-Testergebnis Liste](media/ad-fs-diagonostics-analyzer/step3a_v3.png) jedes Testergebnis wird mit Details angezeigt, die den Test beschreiben, und die Auflösung der Schritte:

1. Testname: Der Name des Tests, der ausgeführt wurde.
2. Beschreibung: Eine Beschreibung des Tests.
3. Details: Die Beschreibung des gesamten Vorgangs, der während des Tests durchgeführt wurde.
4. Schritte zur Lösung: Die vorgeschlagenen Schritte zum Beheben des Problems, das durch den Test hervorgehoben wird.

![AD FS Diagnostics Analyzer Tool-Fehlerbehebung](media/ad-fs-diagonostics-analyzer/step3b_v3.png)

## <a name="next"></a>Nächste

- [Hilfe zur Behandlung von Problemen mit AD FS Hilfe](https://aka.ms/adfshelp/troubleshooting )
- [Behandeln von AD FS-Problemen](ad-fs-tshoot-overview.md)
