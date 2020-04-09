---
title: DiskPart-Skripts und-Beispiele
description: Windows-Befehle Thema für DiskPart-Skripts und Beispiele zum Automatisieren von Datenträger bezogenen Aufgaben, z. b. zum Erstellen von Volumes oder zum wandeln von Datenträgern in dynamische Datenträger.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 319c0795-11df-47c8-b203-eadb0577ee0d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bdfa35e8597479f32bc9bd854549cb3f74e4c0d3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845493"
---
# <a name="diskpart-scripts-and-examples"></a>DiskPart-Skripts und-Beispiele

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verwenden Sie Diskpart `/s` zum Ausführen von Skripts, mit denen Datenträger bezogene Aufgaben automatisiert werden, z. b. das Erstellen von Volumes oder das Umstellen von Datenträgern Das Erstellen von Skripts für diese Aufgaben ist hilfreich, wenn Sie Windows mithilfe der unbeaufsichtigten Installation oder des sytinp-Tools bereitstellen, das das Erstellen von Volumes außer dem Start Volume nicht unterstützt.  
  
-   Erstellen Sie zum Erstellen eines DiskPart-Skripts eine Textdatei, die die Diskpart-Befehle enthält, die Sie ausführen möchten, mit einem Befehl pro Zeile und ohne leere Zeilen. Sie können eine Zeile mit `rem` starten, um die Zeile zu einem Kommentar zu machen.  
  
    Hier ist beispielsweise ein Skript, das einen Datenträger zurücksetzt und dann eine 300 MB-Partition für die Windows-Wiederherstellungs Umgebung erstellt:  
  
    ```  
    select disk 0  
    clean  
    convert gpt  
    create partition primary size=300  
    format quick fs=ntfs label=Windows RE tools  
    assign letter=T  
    ```  
  
-   Geben Sie zum Ausführen eines DiskPart-Skripts an der Eingabeaufforderung den folgenden Befehl ein, wobei *ScriptName* der Name der Textdatei ist, in der das Skript enthalten ist.  
  
    ```  
    diskpart /s scriptname.txt  
    ```  
  
-   Zum Umleiten der Skript Ausgabe von DiskPart in eine Datei geben Sie den folgenden Befehl ein, wobei *Protokolldatei* der Name der Textdatei ist, in die Diskpart die Ausgabe schreibt.  
  
    ```  
    diskpart /s scriptname.txt > logfile.txt  
    ```  
  
> [!IMPORTANT]  
> Wenn Sie den **DiskPart** -Befehl als Teil eines Skripts verwenden, empfiehlt es sich, alle DiskPart-Vorgänge zusammen als Teil eines einzelnen DiskPart-Skripts abzuschließen. Sie können aufeinander folgende DiskPart-Skripts ausführen. Sie müssen jedoch mindestens 15 Sekunden zwischen den einzelnen Skripts für das vollständige Herunterfahren der vorherigen Ausführung zulassen, bevor Sie den **DiskPart** -Befehl erneut in aufeinander folgenden Skripts ausführen. Andernfalls können die nachfolgenden Skripts fehlschlagen. Sie können eine Pause zwischen aufeinander folgenden DiskPart-Skripts hinzufügen, indem Sie den `timeout /t 15`-Befehl der Batchdatei zusammen mit den DiskPart-Skripts hinzufügen.  
  
Wenn Diskpart gestartet wird, werden die Diskpart-Version und der Computername an der Eingabeaufforderung angezeigt. Wenn Diskpart beim Versuch, eine Skript gesteuerte Aufgabe auszuführen, einen Fehler feststellt, stoppt DiskPart standardmäßig die Verarbeitung des Skripts und zeigt einen Fehlercode \(an, es sei denn, Sie haben den **Noerr** -Parameter\)angegeben. DiskPart gibt jedoch immer Fehler zurück, wenn Syntax Fehler auftreten, unabhängig davon, ob Sie den **Noerr** -Parameter verwendet haben. Mit dem **Noerr** -Parameter können Sie nützliche Aufgaben ausführen, z. b. die Verwendung eines einzelnen Skripts, um alle Partitionen auf allen Datenträgern unabhängig von der Gesamtzahl der Datenträger zu löschen.  
  
## <a name="additional-references"></a>Weitere Verweise
  
- [Beispiel: Konfigurieren von UEFI-\/GPT\-basierten Festplattenpartitionen mithilfe von Windows PE und DiskPart](https://technet.microsoft.com/library/hh825686.aspx)  
- [Beispiel: Konfigurieren von BIOS-\/MBR\-basierten Festplattenpartitionen mithilfe von Windows PE und DiskPart](https://technet.microsoft.com/library/hh825677.aspx)  
- [Storage-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/hh848705.aspx)  
  

