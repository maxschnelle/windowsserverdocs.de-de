---
Title: DiskPart-Befehle
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 3cc0667b54dba75d892795f6520664ce7a7a62a5
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192646"
---
# <a name="diskpart-commands"></a>DiskPart-Befehle

Gilt für: Windows 10, Windows 8.1, Windows 8, Windows 7, WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012 und Windows Server 2008 R2, WindowsServer 2008

DiskPart-Befehle helfen Ihnen beim Verwalten Ihrer PC Laufwerke (Datenträger, Partitionen, Volumes und virtuelle Festplatten). Bevor Sie den DiskPart-Befehle verwenden können, müssen Sie zuerst aufgeführt, und wählen Sie dann auf ein Objekt, das sie den Fokus erhält. Wenn ein Objekt den Fokus besitzt, werden alle DiskPart-Befehle, die Sie eingeben für dieses Objekt fungieren.

Sie können eine Liste der verfügbaren Objekte und bestimmen Sie mithilfe eines Objekts Anzahl oder die Laufwerkbuchstaben der **Datenträger der Liste "," Volume der Liste "," Liste Partition**, und **Vdisk Liste** Befehle. Die **Liste-Datenträger, Liste Vdisk** und **Liste Volume** Befehle zeigen alle Datenträger und Volumes auf dem Computer. Allerdings die **Liste Partition** Befehl werden nur Partitionen angezeigt, auf dem Datenträger, den Fokus besitzt. Bei Verwendung der **Liste** Befehle, ein Sternchen (\*) wird neben dem Objekt den Fokus besitzt.

Wenn Sie ein Objekt auswählen, bleibt der Fokus für das Objekt, bis Sie ein anderes Objekt auswählen. Z. B. verlagert der Fokus auf Datenträger 0 festgelegt ist, und Sie Volume 8 auf dem Datenträger 2 auswählen, den Fokus vom Datenträger 0 auf Datenträger 2, 8-Volume. Einige Befehle ändern den Fokus automatisch auf. Z. B. Wenn Sie eine neue Partition erstellen, wechselt der Fokus automatisch auf die neue Partition.

Sie können nur den Fokus auf eine Partition auf den ausgewählten Datenträger gewähren. Wenn eine Partition den Fokus besitzt, besitzt die im Zusammenhang mit dem (sofern vorhanden) auch den Fokus. Wenn ein Volume verfügt über den Fokus, die zugehörigen Datenträger und Partition, die auch den Fokus besitzen, wenn das Volume auf einer bestimmten Partition zugeordnet ist. Wenn dies nicht der Fall, den Fokus auf dem Datenträger ist und Partition gehen verloren.

## <a name="diskpart-commands"></a>DiskPart-Befehle

So starten Sie den DiskPart-Befehlsinterpreter, an der Eingabeaufforderung Folgendes:

`diskpart`

> [!IMPORTANT]
> Mitgliedschaft in der lokalen **Administratoren** oder einer gleichwertigen Gruppe, ist die mindestvoraussetzung zum Ausführen von DiskPart. 

Sie können die folgenden Befehle in der Diskpart-Befehlsinterpreter ausführen:

  - [Active](active.md)  
      
  - [Hinzufügen](add.md)  
      
  - [Weisen Sie](assign.md)  
      
  - [Fügen Sie die virtuellen Datenträger](attach-vdisk.md)  
      
  - [Attribute](attributes.md)  
      
  - [Automatische Bereitstellung](automount.md)  
      
  - [Break](break.md)  
      
  - [Bereinigen](clean.md)  
      
  - [Komprimieren Sie die virtuellen Datenträger](compact-vdisk.md)  
      
  - [Convert](convert.md)  
      
  - [Erstellen](create.md)  
      
  - [Löschen](delete.md)  
      
  - [Trennen Sie die virtuellen Datenträger](detach-vdisk.md)  
      
  - [Detail](detail.md)  
      
  - [Exit](exit.md)  
      
  - [Erweitern Sie die virtuellen Datenträger](expand-vdisk.md)  
      
  - [Erweitern](extend.md)  
      
  - [Dateisysteme](filesystems.md)  
      
  - [Format](format.md)  
      
  - [GPT](gpt.md)  
      
  - [Hilfe](help.md)  
      
  - [Importieren](import.md)  
      
  - [inaktiv](inactive.md)  
      
  - [Liste](list.md)  
      
  - [Zusammenführen von virtuellen Datenträger](merge-vdisk.md)  
      
  - [Offline](offline.md)  
      
  - [Online](online.md)  
      
  - [Wiederherstellen](recover.md)  
      
  - [Rem](rem.md)  
      
  - [Entfernen](remove.md)  
      
  - [Reparieren](repair.md)  
      
  - [Rescan](rescan.md)  
      
  - [Retain](retain.md)  
      
  - [San](san.md)  
      
  - [Auswahl](select.md)  
      
  - [Satz-id](set-id.md)  
      
  - [Shrink](shrink.md)  
      
  - [Uniqueid](uniqueid.md)  
      

## <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[Speicher-Cmdlets in Windows PowerShell](https://docs.microsoft.com/en-us/powershell/module/storage/)
