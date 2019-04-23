---
title: AD FS-Hilfe Diagnose Analyzer
description: In diesem Dokument wird beschrieben, AD FS-Hilfe Diagnose Analyzer aus, und wie sie die grundlegende ausführen kann überprüft mit AD FS-Diagnose-PowerShell-Modul.
author: billmath
ms.author: billmath
manager: mtillman
ms.reviewer: anandyadavMSFT
ms.date: 02/13/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a5b5f895a0575094f8f1af950bde82e1d56325b2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829121"
---
# <a name="ad-fs-help-diagnostics-analyzer"></a>AD FS-Hilfe Diagnose Analyzer

AD FS hat zahlreiche Einstellungen, die Vielzahl von Funktionen zu unterstützen, die für die Authentifizierung und Anwendungskonfiguration Entwicklung bietet. Während der Problembehandlung wird empfohlen, sicherzustellen, dass alle von der AD FS-Einstellungen ordnungsgemäß konfiguriert sind. Diese Einstellungen eine manuelle Überprüfung ausführen kann manchmal zeitaufwändig sein. AD FS-Hilfe Diagnose Analyzer können, führen Sie die grundlegenden Prüfungen, die mithilfe des ADFSToolbox PowerShell-Moduls. Nach der Durchführung von Überprüfungen, die AD FS-Hilfe enthält die [Diagnose Analyzer](https://aka.ms/adfsdiagnosticsanalyzer) können Sie problemlos die Ergebnisse zu visualisieren und Lösungsschritten bieten.

Der vollständige Vorgang akzeptiert 3 einfache Schritten:

1. Einrichten der ADFSToolbox-Modul auf dem primären AD FS-Server oder die WAP-server
2. Führen Sie die Diagnose und zum Hochladen der Datei in AD FS-Hilfe
3. Anzeigen der Analyse von Diagnosen und Beheben von Problemen

Wechseln Sie zu [Analyzer für AD FS-Hilfe-Diagnose (https://aka.ms/adfsdiagnosticsanalyzer) ](https://aka.ms/adfsdiagnosticsanalyzer) zu Beginn der Problembehandlung.

![AD FS-Diagnose-Analyzer-Tool auf AD FS-Hilfe](media/ad-fs-diagonostics-analyzer/home.png)

## <a name="step-1-setup-the-adfstoolbox-module-on-ad-fs-server"></a>Schritt 1: Das Modul ADFSToolbox auf AD FS-Server einrichten

Zum Ausführen der [Diagnose Analyzer](https://aka.ms/adfsdiagnosticsanalyzer), Sie müssen das ADFSToolbox-PowerShell-Modul installieren. Wenn AD FS-Server die Verbindung mit dem Internet verfügt, können Sie das Modul ADFSToolbox direkt aus dem PowerShell-Katalog installieren. Falls keine Verbindung mit dem Internet Klonen Sie das GitHub-Repository für die manuelle Installation. 

![Analyzer für AD FS-Diagnose - Setup](media/ad-fs-diagonostics-analyzer/step1.png)

### <a name="setup-using-powershell-gallery"></a>Setup unter Verwendung von PowerShell-Katalog

Wenn AD FS-Server dem Internet verbunden ist, wird empfohlen, das Modul ADFSToolbox direkt aus dem PowerShell-Katalog mithilfe der unten angegebenen PowerShell-Befehle zu installieren.
 
   ```powershell 
    Install-Module -Name ADFSToolbox -force
    Import-Module ADFSToolbox -force
   ```
### <a name="setup-manually-by-cloning-the-repository"></a>Richten Sie manuell, indem Sie das Repository Klonen

Das Modul ADFSToolbox kann manuell direkt aus GitHub installiert werden. Befolgen Sie die Anweisungen unten für das Klonen des Repositorys, und installieren das Modul ADFSToolbox auf dem AD FS-Server aus.

1. Herunterladen der [Repository](https://github.com/Microsoft/adfsToolbox/archive/master.zip)
2. Entzippen Sie die heruntergeladene Datei und kopieren Sie den AdfsToolbox-Master-Ordner in %SystemDrive%\\Programmdateien\\WindowsPowerShell\\Module\\.
3. Importieren Sie das PowerShell-Modul. Führen Sie in einer PowerShell-Fenster mit erhöhten Rechten Folgendes ein:
 
   ```powershell 
    Import-Module ADFSToolbox -Force
   ```

## <a name="step-2-execute-the-diagnostics-and-upload-the-file-to-ad-fs-help"></a>Schritt 2: Führen Sie die Diagnose und zum Hochladen der Datei in AD FS-Hilfe

Ein einzelnen Befehl kann verwendet werden, um die Diagnosetests bequem auf allen AD FS-Servern in der Farm auszuführen. PS-Remotesitzungen verwendet das PowerShell-Modul zur Ausführung der Diagnosetests auf verschiedenen Servern in der Farm.

```powershell
    Export-AdfsDiagnosticsFile [-adfsServers <list of servers>]
```

In einer Server 2016 AD FS-Farm wird der Befehl die Liste der AD FS-Server von AD FS-Konfiguration gelesen. Die Diagnosetests werden für jeden Server in der Liste dann versucht. Wenn die Liste der AD FS-Server nicht verfügbar ist (Beispiel 2012r2).), und klicken Sie dann die Tests für den lokalen Computer ausgeführt werden. Verwenden Sie zum Angeben einer Liste von Servern für die die Tests ausgeführt werden, die ausgeführt werden die **AdfsServers** Argument, um eine Liste mit Servern bereitzustellen. Ein Beispiel ist unten angegeben.

```powershell
    Export-AdfsDiagnosticsFile -adfsServers @("sts1.contoso.com", "sts2.contoso.com", "sts3.contoso.com")
```

Das Ergebnis ist eine JSON-Datei, die im gleichen Verzeichnis erstellt wird, in dem der Befehl ausgeführt wurde. Der Name der Datei ist ADFSDiagnosticsFile\<Zeitstempel\>. Ein Beispiel-Dateiname ist ADFSDiagnosticsFile-20180716124030.

In Schritt 2 auf [ https://aka.ms/adfsdiagnosticsanalyzer ](https://aka.ms/adfsdiagnosticsanalyzer) des Dateibrowsers verwenden, um die Ergebnisdatei zum Hochladen auszuwählen.

![AD FS-Diagnose-Analyzer-Tool – ausführen und Ergebnisse hochladen](media/ad-fs-diagonostics-analyzer/step2.png)

Klicken Sie auf **hochladen** den Upload abgeschlossen, und mit dem nächsten Schritt fortfahren.

## <a name="step-3-view-diagnostics-analysis-and-resolve-any-issues"></a>Schritt 3: Anzeigen der Analyse von Diagnosen und Beheben von Problemen

Es gibt vier Abschnitte der Testergebnisse:

1. Fehlgeschlagen: Dieser Abschnitt enthält die Liste der fehlgeschlagenen Tests. Jedes Ergebnis besteht aus:
2. Warnung: Dieser Abschnitt enthält eine Liste der Tests, die eine Warnung geführt hat. Diese Probleme nicht sehr wahrscheinlich Probleme rund um die Authentifizierung in größerem Umfang werden jedoch bald wie möglich behandelt werden sollte.
3. Nicht zutreffend: Dieser Abschnitt enthält die Liste der Tests, die nicht ausgeführt wurden, da sie nicht für den bestimmten Server zutreffend waren, auf denen der Befehl ausgeführt wurde.
4. Übergeben: Dieser Abschnitt enthält die Liste der Tests, die übergeben und kein Aktionselement, für den Benutzer.

Jedes Testergebnisses wird mit den Details angezeigt, die den Test und die Lösung beschreiben die Schritte aus:

1. Testname: Name des Tests, die ausgeführt wurde
2. Details: Beschreibung des gesamten Vorgangs, die während der Test ausgeführt wurde
3. Schritte zur Lösung: Die vorgeschlagenen Schritte zur Behebung des Problems, die vom Test hervorgehoben

![AD FS-Diagnose-Analyzer-Tool - Test-Ergebnisliste](media/ad-fs-diagonostics-analyzer/step3a.png)

![AD FS-Diagnose Analyzer-Tool - Fehlerbehebung](media/ad-fs-diagonostics-analyzer/step3b.png)

## <a name="next"></a>Nächste

- [Verwenden Sie AD FS-Hilfe Troublehshooting Leitfäden](https://aka.ms/adfshelp/troubleshooting )
- [AD FS-Problembehandlung](ad-fs-tshoot-overview.md)

 
