---
title: DiskPart-Skripts und Beispiele
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 319c0795-11df-47c8-b203-eadb0577ee0d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a8bd0dfab98ca705cf64766d66285c69bd3d3129
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862791"
---
# <a name="diskpart-scripts-and-examples"></a>DiskPart-Skripts und Beispiele

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Verwenden Sie Diskpart `/s` zum Ausführen von Skripts, die Datenträger automatisieren\-bezogene Aufgaben wie das Erstellen von Volumes oder Datenträgern in dynamische Datenträger konvertieren. Skripting dieser Aufgaben ist nützlich, wenn Sie Windows bereitstellen mithilfe einer unbeaufsichtigten Installation oder dem Sysprep-Tool, die Erstellen von Volumes als das Startvolume nicht unterstützen.  
  
-   Um ein Diskpart-Skript zu erstellen, erstellen Sie eine Textdatei, die die Diskpart-Befehle enthält, die mit dem ein Befehl pro Zeile, und keine leeren Zeilen ausgeführt werden soll. Sie können am Anfang einer Zeile mit `rem` um der Zeile einen Kommentar zu machen.  
  
    beispielsweise hier s ein Skript, das Zurücksetzen von eines Datenträgers und erstellt dann eine 300 MB-Partition für die Windows-Wiederherstellung Umgebung:  
  
    ```  
    select disk 0  
    clean  
    convert gpt  
    create partition primary size=300  
    format quick fs=ntfs label="Windows RE tools"  
    assign letter="T"  
    ```  
  
-   Um ein DiskPart-Skript, an der Eingabeaufforderung auszuführen, geben Sie den folgenden Befehl ein, wobei *Skriptname* ist der Name der Textdatei mit dem Skript.  
  
    ```  
    diskpart /s scriptname.txt  
    ```  
  
-   Geben Sie den folgenden Befehl zum Umleiten DiskParts-Skript-Ausgabe in eine Datei, in denen *Logfile* ist der Name der Textdatei, in denen DiskPart dessen Ausgabe schreibt.  
  
    ```  
    diskpart /s scriptname.txt > logfile.txt  
    ```  
  
> [!IMPORTANT]  
> Bei Verwendung der **DiskPart** Befehl als Teil eines Skripts, es wird empfohlen, dass Sie alle Vorgänge DiskPart zusammen als Teil eines einzelnen DiskPart-Skripts ausführen. Sie können die aufeinander folgenden DiskPart-Skripts ausführen, jedoch müssen Sie mindestens 15 Sekunden zwischen den einzelnen Skripts für eine vollständige Herunterfahren der vorherigen Ausführung vor der Ausführung zulassen der **DiskPart** in nachfolgenden Skripts erneut den Befehl. Andernfalls können die nachfolgenden Skripts fehl. Sie können eine Pause zwischen aufeinander folgenden DiskPart-Skripts durch Hinzufügen von Hinzufügen der `timeout /t 15` Befehl an Ihrer Batchdatei zusammen mit Ihren DiskPart-Skripts.  
  
Wann DiskPart gestartet, die DiskPart-Version "und" Computer Namensanzeige an der Eingabeaufforderung. Standardmäßig, wenn DiskPart ein Fehler auftritt, bei dem Versuch, führen Sie einen Skripttask DiskPart beendet die Verarbeitung des Skripts und zeigt einen Fehlercode \(, wenn die Angabe der **DiskPart** Parameter\). Allerdings DiskPart immer gibt Fehler zurück, wenn es feststellt, dass Syntaxfehler, unabhängig davon, ob Sie verwendet die **DiskPart** Parameter. Die **DiskPart** Parameter können Sie nützliche Aufgaben, z. B. ein einzelnes Skript zum Löschen aller Partitionen auf allen Datenträgern, die unabhängig von der Gesamtzahl von Datenträgern ausführen.  
  
## <a name="see-also"></a>Siehe auch  
[Beispiel: Konfigurieren von UEFI\/Gpt\-basierend Hard Drive Partitionen durch Verwenden von Windows PE und DiskPart](https://technet.microsoft.com/library/hh825686.aspx)  
[Beispiel: Konfigurieren Sie BIOS\/MBR\-basierten Festplattenpartitionen mit Windows PE und DiskPart](https://technet.microsoft.com/library/hh825677.aspx)  
[Speicher-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/hh848705.aspx)  
  

