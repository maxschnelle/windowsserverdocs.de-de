---
title: DiskPart-Skripts und-Beispiele
description: Referenz Thema für DiskPart-Skripts und Beispiele zum Automatisieren von Datenträger bezogenen Aufgaben, z. b. zum Erstellen von Volumes oder zum wandeln von Datenträgern in dynamische Datenträger.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 319c0795-11df-47c8-b203-eadb0577ee0d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 546f867b2cde199f54975a127b0faf11130996d2
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354670"
---
# <a name="diskpart-scripts-and-examples"></a>DiskPart-Skripts und-Beispiele

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verwenden `diskpart /s` Sie zum Ausführen von Skripts zum Automatisieren von Datenträger bezogenen Aufgaben, z. b. zum Erstellen von Volumes oder zum wandeln von Datenträgern in Das Erstellen von Skripts für diese Aufgaben ist hilfreich, wenn Sie Windows mithilfe der unbeaufsichtigten Installation oder des sytinp-Tools bereitstellen, das das Erstellen von Volumes außer dem Start Volume nicht unterstützt.

Erstellen Sie zum Erstellen eines DiskPart-Skripts eine Textdatei, die die Diskpart-Befehle enthält, die Sie ausführen möchten, mit einem Befehl pro Zeile und ohne leere Zeilen. Sie können eine Zeile mit starten `rem` , um die Zeile zu einem Kommentar zu machen. Hier ist beispielsweise ein Skript, das einen Datenträger zurücksetzt und dann eine 300 MB-Partition für die Windows-Wiederherstellungs Umgebung erstellt:

    ```
    select disk 0
    clean
    convert gpt
    create partition primary size=300
    format quick fs=ntfs label=Windows RE tools
    assign letter=T
    ```

## <a name="examples"></a>Beispiele

- Geben Sie zum Ausführen eines DiskPart-Skripts an der Eingabeaufforderung den folgenden Befehl ein, wobei *ScriptName* der Name der Textdatei ist, in der das Skript enthalten ist:

    ```
    diskpart /s scriptname.txt
    ```

- Zum Umleiten der Skript Ausgabe von DiskPart in eine Datei geben Sie den folgenden Befehl ein, wobei *Protokolldatei* der Name der Textdatei ist, in der DiskPart die Ausgabe schreibt:

    ```
    diskpart /s scriptname.txt > logfile.txt
    ```

### <a name="remarks"></a>Bemerkungen

- Wenn Sie den **DiskPart** -Befehl als Teil eines Skripts verwenden, empfiehlt es sich, alle DiskPart-Vorgänge zusammen als Teil eines einzelnen DiskPart-Skripts abzuschließen. Sie können aufeinander folgende DiskPart-Skripts ausführen. Sie müssen jedoch mindestens 15 Sekunden zwischen den einzelnen Skripts für das vollständige Herunterfahren der vorherigen Ausführung zulassen, bevor Sie den **DiskPart** -Befehl erneut in aufeinander folgenden Skripts ausführen. Andernfalls können die nachfolgenden Skripts fehlschlagen. Sie können eine Pause zwischen aufeinander folgenden DiskPart-Skripts hinzufügen, indem Sie den `timeout /t 15` Befehl der Batchdatei zusammen mit den DiskPart-Skripts hinzufügen.

- Wenn Diskpart gestartet wird, werden die Diskpart-Version und der Computername an der Eingabeaufforderung angezeigt. Wenn Diskpart beim Versuch, eine Skript gesteuerte Aufgabe auszuführen, einen Fehler feststellt, beendet DiskPart standardmäßig die Verarbeitung des Skripts und zeigt einen Fehlercode an (es sei denn, Sie haben den **Noerr** -Parameter angegeben). DiskPart gibt jedoch immer Fehler zurück, wenn Syntax Fehler auftreten, unabhängig davon, ob Sie den **Noerr** -Parameter verwendet haben. Mit dem **Noerr** -Parameter können Sie nützliche Aufgaben ausführen, z. b. die Verwendung eines einzelnen Skripts, um alle Partitionen auf allen Datenträgern unabhängig von der Gesamtzahl der Datenträger zu löschen.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Beispiel: Konfigurieren von UEFI/GPT-basierten Festplattenpartitionen mit Windows PE und DiskPart](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh825686(v=win.10))

- [Beispiel: Konfigurieren von BIOS/MBR-basierten Festplattenpartitionen mit Windows PE und DiskPart](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh825677(v=win.10))

- [Speicher-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/storage/?view=win10-ps)
