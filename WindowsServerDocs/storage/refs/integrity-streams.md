---
title: ReFS Integrity Streams
description: 
author: gawatu
ms.author: jgerend
manager: dmoss
ms.date: 11/14/2016
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.assetid: 1f1215cd-404f-42f2-b55f-3888294d8a1f
ms.openlocfilehash: d9e14e74591b341048316e9c2e69a312062c3304
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="refs-integrity-streams"></a>ReFS Integrity Streams
>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10

Integrität-Streams ist ein optionales Feature in ReFS, das die Datenintegrität mithilfe von Prüfsummen überprüft und verwaltet. Während ReFS immer Prüfsummen für Metadaten verwendet, erstellt oder überprüft ReFS standardmäßig keine Prüfsummen für Dateidaten. Integrity Streams ist ein optionales Feature, mit dem Benutzer die Verwendung von Prüfsummen für Dateidaten verwenden können. Wenn Integrity Streams aktiviert sind, können ReFS eindeutig bestimmen, ob Daten ungültig oder beschädigt ist. Darüber hinaus können ReFS und Speicherplätze gemeinsam automatisch beschädigte Metadaten und Daten korrigieren.

## <a name="how-it-works"></a>Funktionsweise 

Integrity Streams kann für einzelne Dateien, Verzeichnisse oder das gesamte Volume aktiviert werden, und die Integrity Stream-Einstellungen können jederzeit geändert werden. Darüber hinaus werden die Integrity Stream-Einstellungen für Dateien und Verzeichnisse von übergeordneten Verzeichnisse übernommen. 

Nachdem Integrity Streams aktiviert ist, erstellt und verwaltet ReFS eine Prüfsumme für die angegebenen Dateien in den Metadaten der Dateien. Diese Prüfsumme ermöglicht ReFS vor dem Zugriff die Integrität der Daten zu überprüfen. ReFS berechnet vor dem Zurückgeben von Daten, die Integrity Streams aktiviert haben, deren Prüfsumme:

<img src=media/compute-checksum.gif alt="Compute checksum for file data"/>

Anschließend wird die Prüfsumme mit den in der Datei enthaltenen Metadaten verglichen. Wenn die Prüfsummen übereinstimmen, werden die Daten als gültig markiert und an den Benutzer zurückgegebenen. Wenn die Prüfsummen nicht übereinstimmen, sind die Daten beschädigt. Die Volume-Resilienz entscheidet, wie ReFS auf Beschädigungen reagiert:

- Wenn ReFS ist auf einem nicht stabilen, einfachen Speicherplatz oder einem leeren Laufwerk bereitgestellt wird, gibt ReFS einen Fehler an den Benutzer zurück, ohne die beschädigten Daten zurückzugeben. 
- Wenn ReFS ist auf einem robusten Spiegelungs- oder Paritätsbereich bereitgestellt wird, versucht ReFS, das Problem zu beheben. 
    - Wenn der Versuch erfolgreich ist, schreibt ReFS eine Korrekturmaßnahme, um die Integrität der Daten wiederherzustellen und gibt die gültigen Daten an die Anwendung zurück. Die Anwendung ist von der Beschädigung nicht betroffen.
    - Wenn der Versuch fehlschlägt, gibt ReFS einen Fehler zurück. 

ReFS zeichnet alle Schäden im Systemereignisprotokoll auf. Das Protokoll spiegelt wieder, ob die Schäden behoben wurden. 

<img src=media/corrective-write.gif alt="Corrective write restores data integrity."/>

## <a name="performance"></a>Leistung 

Integrity Streams bietet eine verbesserte Datenintegrität für das System, es bringt jedoch auch Leistungseinbußen mit sich. Es gibt dafür mehrere verschiedene Gründe:
- Wenn Integrity Streams aktiviert ist, lösen alle Schreibvorgänge Zuordnungsmechanismus der Schreibvorgänge aus. Obwohl dadurch ein Engpass der Lese-, Änderungs- und Schreibvorgänge verhindert wird, da ReFS keine vorhandenen Daten lesen oder ändern muss, werden Daten häufig fragmentiert, was die Lesevorgänge verzögert. 
- Je nach Workload und dem zugrunde liegenden Speicher des Systems kann der Rechenaufwand für die Verarbeitung und Überprüfung der Daten der Prüfsumme die E/A-Latenz erhöhen. 

Da Integrity Streams die Leistung beeinträchtigten, wird empfohlen, Integrity Streams bei besonders leistungsabhängige Systemen zu deaktivieren. 

## <a name="integrity-scrubber"></a>Integrity-Bereiniger

Wie oben beschrieben, überprüft ReFS die Integrität der Daten automatisch, bevor darauf zugegriffen wird. ReFS verwendet auch einen Hintergrund-Bereiniger, womit ReFS selten genutzte Daten überprüft. Die Bereinigung durchsucht regelmäßig das Volume, erkennt dabei potenzielle Beschädigungen und löst dann proaktiv eine Reparatur jeglicher beschädigten Daten aus.

  >[!NOTE]
  >Die Datenintegritätsbereinigung kann nur Daten für Dateien überprüfen, für die Integrity Streams aktiviert ist.

Standardmäßig wird die Bereinigung alle vier Wochen ausgeführt, doch dieses Intervall kann im Taskplaner unter Microsoft\Windows\Datenintegrität konfiguriert werden. 

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

## <a name="see-also"></a>Weitere Informationen finden Sie unter

-   [ReFS – Übersicht](refs-overview.md)
-   [Block-Clone-Vorgänge auf ReFS](block-cloning.md)
-   [Direkte Speicherplätze – Übersicht](../storage-spaces/storage-spaces-direct-overview.md)
