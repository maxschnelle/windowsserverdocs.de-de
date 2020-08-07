---
title: ReFS Integrity Streams
author: gawatu
ms.author: jgerend
manager: dmoss
ms.date: 10/16/2018
ms.topic: article
ms.assetid: 1f1215cd-404f-42f2-b55f-3888294d8a1f
ms.openlocfilehash: 15c4b7942be949af33e70d2a5f299af426040e7b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950504"
---
# <a name="refs-integrity-streams"></a>ReFS Integrity Streams
>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server (halbjährlicher Kanal), Windows 10

Integrität-Streams ist ein optionales Feature in ReFS, das die Datenintegrität mithilfe von Prüfsummen überprüft und verwaltet. Obwohl Refs immer Prüfsummen für Metadaten verwendet, werden Prüfsummen für Datei Daten von refs nicht standardmäßig generiert oder überprüft. Integritäts Datenströme sind ein optionales Feature, mit dem Benutzer Prüfsummen für Datei Daten verwenden können. Wenn Integritäts Datenströme aktiviert sind, können Refs eindeutig ermitteln, ob die Daten gültig oder beschädigt sind. Darüber hinaus können ReFS und Speicherplätze gemeinsam automatisch beschädigte Metadaten und Daten korrigieren.

## <a name="how-it-works"></a>Funktionsweise

Integrity Streams kann für einzelne Dateien, Verzeichnisse oder das gesamte Volume aktiviert werden, und die Integrity Stream-Einstellungen können jederzeit geändert werden. Darüber hinaus werden die Integrity Stream-Einstellungen für Dateien und Verzeichnisse von übergeordneten Verzeichnisse übernommen.

Nachdem Integrity Streams aktiviert ist, erstellt und verwaltet ReFS eine Prüfsumme für die angegebenen Dateien in den Metadaten der Dateien. Diese Prüfsumme ermöglicht ReFS vor dem Zugriff die Integrität der Daten zu überprüfen. ReFS berechnet vor dem Zurückgeben von Daten, die Integrity Streams aktiviert haben, deren Prüfsumme:

![Compute-Prüfsumme für Datei Daten](media/compute-checksum.gif)

Anschließend wird die Prüfsumme mit den in der Datei enthaltenen Metadaten verglichen. Wenn die Prüfsummen übereinstimmen, werden die Daten als gültig markiert und an den Benutzer zurückgegebenen. Wenn die Prüfsummen nicht stimmen, sind die Daten beschädigt. Die Volume-Resilienz entscheidet, wie ReFS auf Beschädigungen reagiert:

- Wenn ReFS ist auf einem nicht stabilen, einfachen Speicherplatz oder einem leeren Laufwerk bereitgestellt wird, gibt ReFS einen Fehler an den Benutzer zurück, ohne die beschädigten Daten zurückzugeben.
- Wenn ReFS ist auf einem robusten Spiegelungs- oder Paritätsbereich bereitgestellt wird, versucht ReFS, das Problem zu beheben.
    - Wenn der Versuch erfolgreich ist, schreibt ReFS eine Korrekturmaßnahme, um die Integrität der Daten wiederherzustellen und gibt die gültigen Daten an die Anwendung zurück. Die Anwendung ist von der Beschädigung nicht betroffen.
    - Wenn der Versuch fehlschlägt, gibt ReFS einen Fehler zurück.

ReFS zeichnet alle Schäden im Systemereignisprotokoll auf. Das Protokoll spiegelt wieder, ob die Schäden behoben wurden.

![Korrektur der Datenintegrität](media/corrective-write.gif)

## <a name="performance"></a>Leistung

Integrity Streams bietet eine verbesserte Datenintegrität für das System, es bringt jedoch auch Leistungseinbußen mit sich. Es gibt dafür mehrere verschiedene Gründe:
- Wenn Integrity Streams aktiviert ist, lösen alle Schreibvorgänge Zuordnungsmechanismus der Schreibvorgänge aus. Dies vermeidet zwar alle Lese-und Schreibvorgänge, da Refs keine vorhandenen Daten lesen oder ändern muss, aber häufig werden die Datei Daten fragmentiert, was zu Verzögerungen bei Lesevorgängen führt.
- Je nach Workload und dem zugrunde liegenden Speicher des Systems kann der Rechenaufwand für die Verarbeitung und Überprüfung der Daten der Prüfsumme die E/A-Latenz erhöhen.

Da Integritäts Datenströme Leistungseinbußen verursachen, empfiehlt es sich, Integritäts Datenströme auf Leistungs sensiblen Systemen zu deaktivieren.

## <a name="integrity-scrubber"></a>Integrität Scrubber

Wie oben beschrieben, werden die Datenintegrität von refs automatisch überprüft, bevor auf Daten zugegriffen wird. Refs verwendet auch einen Hintergrund-Scrubber, mit dem Refs Daten, auf die selten zugegriffen wird, überprüfen kann. Dieser Scrubber scannt regelmäßig das Volume, identifiziert latente Beschädigungen und löst proaktiv eine Reparatur von beschädigten Daten aus.

  >[!NOTE]
  >Die Datenintegritäts-Scrubber kann nur Datei Daten für Dateien validieren, in denen Integritäts Datenströme aktiviert sind.

Standardmäßig wird Scrubber alle vier Wochen ausgeführt. dieses Intervall kann jedoch in Taskplaner unter microsoft\windows\data Integrity Scan konfiguriert werden.

## <a name="examples"></a>Beispiele
Um die Integritätseinstellungen der Dateidaten zu überwachen und zu ändern, verwendet ReFS die Cmdlets **Get-FileIntegrity**- und **Set-FileInInttegrity**.

### <a name="get-fileintegrity"></a>Get-FileIntegrity
Um festzustellen, ob Integrity Streams für Dateidaten aktiviert ist, führen Sie das Sie Cmdlet **Get-FileIntegrity** aus.

```PowerShell
PS C:\> Get-FileIntegrity -FileName 'C:\Docs\TextDocument.txt'
```

Sie können auch das Cmdlet **Get-Element** ausführen, um die Integrity Stream-Einstellungen für alle Dateien in einem bestimmten Verzeichnis abzurufen.

```PowerShell
PS C:\> Get-Item -Path 'C:\Docs\*' | Get-FileIntegrity
```

### <a name="set-fileintegrity"></a>Set-FileIntegrity
Verwenden Sie zum Aktivieren/Deaktivieren von Integrity Stream für Dateidaten das Cmdlet **Set-FileIntegrity**.

```PowerShell
PS C:\> Set-FileIntegrity -FileName 'H:\Docs\TextDocument.txt' -Enable $True
```

Sie können auch das Cmdlet **Get-Element** ausführen, um die Integrity Stream-Einstellungen für alle Dateien in einem bestimmten Verzeichnis festzulegen.

```PowerShell
PS C:\> Get-Item -Path 'H\Docs\*' | Set-FileIntegrity -Enable $True
```

Das Cmdlet **Set-FileIntegrity** kann auch direkt auf Volumes und Verzeichnisse angewandt werden.

```PowerShell
PS C:\> Set-FileIntegrity H:\ -Enable $True
PS C:\> Set-FileIntegrity H:\Docs -Enable $True
```

## <a name="additional-references"></a>Weitere Verweise

-   [ReFS – Übersicht](refs-overview.md)
-   [Block-Clone-Vorgänge auf ReFS](block-cloning.md)
-   [Direkte Speicherplätze – Übersicht](../storage-spaces/storage-spaces-direct-overview.md)
