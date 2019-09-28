---
title: DiskPart-Skripts und-Beispiele
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 9c40ce79664795297af4369e35cbda7422617e6e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377853"
---
# <a name="diskpart-scripts-and-examples"></a>DiskPart-Skripts und-Beispiele

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verwenden Sie Diskpart `/s` zum Ausführen von Skripts, die Datenträger-@ no__t-1-bezogene Aufgaben automatisieren, z. b. das Erstellen von Volumes oder das Umstellen von Datenträgern Das Erstellen von Skripts für diese Aufgaben ist hilfreich, wenn Sie Windows mithilfe der unbeaufsichtigten Installation oder des sytinp-Tools bereitstellen, das das Erstellen von Volumes außer dem Start Volume nicht unterstützt.  
  
-   Erstellen Sie zum Erstellen eines DiskPart-Skripts eine Textdatei, die die Diskpart-Befehle enthält, die Sie ausführen möchten, mit einem Befehl pro Zeile und ohne leere Zeilen. Sie können eine Zeile mit `rem` starten, um die Zeile zu einem Kommentar zu machen.  
  
    Hier ist beispielsweise ein Skript, das einen Datenträger zurücksetzt und dann eine 300 MB-Partition für die Windows-Wiederherstellungs Umgebung erstellt:  
  
    ```  
    select disk 0  
    clean  
    convert gpt  
    create partition primary size=300  
    format quick fs=ntfs label="Windows RE tools"  
    assign letter="T"  
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
> Wenn Sie den **DiskPart** -Befehl als Teil eines Skripts verwenden, empfiehlt es sich, alle DiskPart-Vorgänge zusammen als Teil eines einzelnen DiskPart-Skripts abzuschließen. Sie können aufeinander folgende DiskPart-Skripts ausführen. Sie müssen jedoch mindestens 15 Sekunden zwischen den einzelnen Skripts für das vollständige Herunterfahren der vorherigen Ausführung zulassen, bevor Sie den **DiskPart** -Befehl erneut in aufeinander folgenden Skripts ausführen. Andernfalls können die nachfolgenden Skripts fehlschlagen. Sie können eine Pause zwischen aufeinander folgenden DiskPart-Skripts hinzufügen, indem Sie den Befehl "`timeout /t 15`" der Batchdatei zusammen mit den DiskPart-Skripts hinzufügen.  
  
Wenn Diskpart gestartet wird, werden die Diskpart-Version und der Computername an der Eingabeaufforderung angezeigt. Wenn Diskpart beim Versuch, eine Skript gesteuerte Aufgabe auszuführen, einen Fehler feststellt, stoppt DiskPart standardmäßig die Verarbeitung des Skripts und zeigt einen Fehlercode an \(, es sei denn, Sie haben den **Noerr** -Parameter @ no__t-2 angegeben. DiskPart gibt jedoch immer Fehler zurück, wenn Syntax Fehler auftreten, unabhängig davon, ob Sie den **Noerr** -Parameter verwendet haben. Mit dem **Noerr** -Parameter können Sie nützliche Aufgaben ausführen, z. b. die Verwendung eines einzelnen Skripts, um alle Partitionen auf allen Datenträgern unabhängig von der Gesamtzahl der Datenträger zu löschen.  
  
## <a name="see-also"></a>Siehe auch  
[Blutprobe Konfigurieren von UEFI @ no__t-0gpt @ no__t-1basierten Festplattenpartitionen mit Windows PE und DiskPart @ no__t-2  
[Blutprobe Konfigurieren von BIOS @ no__t-0mbr @ no__t-1basierte Festplattenpartitionen mithilfe von Windows PE und DiskPart @ no__t-2  
[Storage-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/hh848705.aspx)  
  

