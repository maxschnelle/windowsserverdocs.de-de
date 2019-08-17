---
title: DiskPart-Befehle
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 7155dbf34f9986b3ebdd8b549b6a861cf7fcfe3a
ms.sourcegitcommit: 23a6e83b688119c9357262b6815c9402c2965472
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/16/2019
ms.locfileid: "69560432"
---
# <a name="diskpart-commands"></a>DiskPart-Befehle

Gilt für: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2, Windows Server 2008

DiskPart-Befehle helfen Ihnen beim Verwalten der Laufwerke Ihres PCs (Datenträger, Partitionen, Volumes oder virtuelle Festplatten). Bevor Sie Diskpart-Befehle verwenden können, müssen Sie zuerst auflisten und dann ein Objekt auswählen, um den Fokus zu erhalten. Wenn ein Objekt den Fokus besitzt, werden alle DiskPart-Befehle, die Sie eingeben, für dieses Objekt ausgeführt.

Sie können die verfügbaren Objekte auflisten und die Anzahl oder den Laufwerk Buchstaben eines Objekts mithilfe der Befehle **List Disk, List Volume, List Partition**und **List Vdisk** ermitteln. Auf den Befehlen Datenträger **auflisten, Vdisk auflisten** und **Volume auflisten** werden alle Datenträger und Volumes auf dem Computer angezeigt. Der Befehl " **Partition auflisten** " zeigt jedoch nur Partitionen auf dem Datenträger an, die den Fokus haben. Wenn Sie die **List** -Befehle verwenden, wird ein\*Sternchen () neben dem Objekt mit dem Fokus angezeigt.

Wenn Sie ein Objekt auswählen, bleibt der Fokus auf diesem Objekt, bis Sie ein anderes Objekt auswählen. Wenn beispielsweise der Fokus auf Datenträger 0 festgelegt ist und Sie Volume 8 auf Datenträger 2 auswählen, wechselt der Fokus von Datenträger 0 zu Datenträger 2, Volume 8. Einige Befehle ändern automatisch den Fokus. Wenn Sie z. b. eine neue Partition erstellen, wechselt der Fokus automatisch zur neuen Partition.

Sie können den Fokus nur auf eine Partition auf dem ausgewählten Datenträger legen. Wenn eine Partition den Fokus besitzt, hat das zugehörige Volume (sofern vorhanden) ebenfalls den Fokus. Wenn ein Volume den Fokus besitzt, haben der zugehörige Datenträger und die Partition ebenfalls den Fokus, wenn das Volume einer einzelnen bestimmten Partition zugeordnet wird. Wenn dies nicht der Fall ist, geht der Fokus auf den Datenträger und die Partition verloren.

## <a name="diskpart-commands"></a>DiskPart-Befehle

Geben Sie Folgendes an der Eingabeaufforderung ein, um den DiskPart-Befehls Interpreter zu starten:

`diskpart`

> [!IMPORTANT]
> Sie müssen mindestens Mitglied der lokalen Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um DiskPart ausführen zu können. 

Sie können die folgenden Befehle im DiskPart-Befehls Interpreter ausführen:

  - [Active](active.md)  
      
  - [Hinzufügen](add.md)  
      
  - [Assign](assign.md)  
      
  - [Vdisk anfügen](attach-vdisk.md)  
      
  - [Attribute](attributes.md)  
      
  - [Automatischen Bereitstellung](automount.md)  
      
  - [Umbruch](break.md)  
      
  - [Räumen](clean.md)  
      
  - [Compact Vdisk](compact-vdisk.md)  
      
  - [Umgebaut](convert.md)  
      
  - [Erstellen](create.md)  
      
  - [Löschen](delete.md)  
      
  - [Vdisk trennen](detach-vdisk.md)  
      
  - [Einzelnen](detail.md)  
      
  - [Exit](exit.md)  
      
  - [Erweitern von Vdisk](expand-vdisk.md)  
      
  - [Extend](extend.md)  
      
  - [Dateisysteme](filesystems.md)  
      
  - [Format](format.md)  
      
  - [GPT](gpt.md)  
      
  - [Hilfe](help.md)  
      
  - [Importieren](import.md)  
      
  - [VSTE](inactive.md)  
      
  - [Liste](list.md)  
      
  - [Vdisk zusammenführen](merge-vdisk.md)  
      
  - [Aufzu](offline.md)  
      
  - [Internet](online.md)  
      
  - [Wiederherstellen](recover.md)  
      
  - [REM](rem.md)  
      
  - [Entfernen](remove.md)  
      
  - [Reparatur](repair.md)  
      
  - [Neu einlesen](rescan.md)  
      
  - [Erhalten](retain.md)  
      
  - [Chen](san.md)  
      
  - [Auswahl](select.md)  
      
  - [ID festlegen](set-id.md)  
      
  - [Verkleinern](shrink.md)  
      
  - [UniqueId](uniqueid.md)  
      

## <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Storage-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/storage/)
