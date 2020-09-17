---
title: Exportieren und Importieren von virtuellen Computern
description: Zeigt, wie Sie virtuelle Computer mit dem Hyper-V-Manager oder Windows PowerShell exportieren und importieren.
ms.author: benarm
author: BenjaminArmstrong
ms.date: 12/13/2016
ms.topic: article
ms.assetid: 7fd996f5-1ea9-4b16-9776-85fb39a3aa34
ms.openlocfilehash: 8e5faf0b19a4452b4841eb75ced87f76bd58b117
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90746075"
---
# <a name="export-and-import-virtual-machines"></a>Exportieren und Importieren virtueller Computer

> Gilt für: Windows 10, Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

In diesem Artikel erfahren Sie, wie Sie einen virtuellen Computer exportieren und importieren. Dies ist eine schnelle Möglichkeit, Sie zu verschieben oder zu kopieren. In diesem Artikel werden auch einige der Optionen erläutert, die Sie beim Exportieren oder importieren treffen müssen.

## <a name="export-a-virtual-machine"></a>Exportieren eines virtuellen Computers

Bei einem Export werden alle erforderlichen Dateien in einer Einheit gesammelt: virtuelle Festplatten Dateien, Konfigurationsdateien für virtuelle Computer und alle Prüf Punkt Dateien. Dies können Sie auf einem virtuellen Computer durchführen, der sich im Zustand "gestartet" oder "beendet" befindet.

### <a name="using-hyper-v-manager"></a>Verwenden des Hyper-V-Managers

So erstellen Sie einen Export eines virtuellen Computers

1. In Hyper-V-Manager mit der rechten Maustaste in den virtuellen Computer, und wählen Sie **exportieren**.

2. Wählen Sie den Speicherort der exportierten Dateien aus, und klicken Sie auf **exportieren**.

Wenn der Export abgeschlossen ist, werden alle exportierten Dateien am Export Speicherort angezeigt.

### <a name="using-powershell"></a>PowerShell

Öffnen Sie eine Sitzung als Administrator, und führen Sie einen Befehl wie den folgenden aus, nachdem Sie und ersetzt haben \<vm name\> \<path\> :

```powershell
Export-VM -Name \<vm name\> -Path \<path\>
```

Weitere Informationen finden Sie unter [Export-VM](/powershell/module/hyper-v/export-vm).

## <a name="import-a-virtual-machine"></a>Importieren eines virtuellen Computers

Beim Importieren wird der virtuelle Computer beim Hyper-V-Host registriert. Sie können zurück in den Host oder einen neuen Host importieren. Wenn Sie auf denselben Host importieren, müssen Sie den virtuellen Computer nicht zuerst exportieren, da Hyper-V versucht, den virtuellen Computer aus den verfügbaren Dateien neu zu erstellen. Wenn Sie einen virtuellen Computer importieren, wird er registriert, damit er auf dem Hyper-V-Host verwendet werden kann.

Mit dem Assistenten zum Importieren virtueller Computer können Sie auch Inkompatibilitäten beheben, die beim Wechsel von einem Host zu einem anderen vorhanden sein können. Dies sind häufig Unterschiede bei physischer Hardware, z. b. Arbeitsspeicher, virtuelle Switches und virtuelle Prozessoren.

### <a name="import-using-hyper-v-manager"></a>Importieren mit dem Hyper-V-Manager

So importieren Sie einen virtuellen Computer:

1. Klicken Sie im Hyper-V-Manager im Menü **Aktionen** auf **virtuellen Computer importieren**.

2. Klicken Sie auf **Weiter**.

3. Wählen Sie den Ordner aus, der die exportierten Dateien enthält, und klicken Sie auf **weiter**.

4. Wählen Sie den zu importierenden virtuellen Computer aus.

5. Wählen Sie den Importtyp aus, und klicken Sie auf **weiter**. (Beschreibungen finden Sie unten unter [Importieren von Typen](#import-types).)

6. Klicken Sie auf **Fertig stellen**.

### <a name="import-using-powershell"></a>Importieren mithilfe von PowerShell

Verwenden Sie das Cmdlet **Import-VM** , und befolgen Sie dabei das Beispiel für den gewünschten Importtyp. Beschreibungen der Typen finden Sie unten unter [Importieren von Typen](#import-types).

#### <a name="register-in-place"></a>Direkt registrieren

Bei dieser Art von Import werden die Dateien verwendet, in denen Sie zum Zeitpunkt des Imports gespeichert sind, und die ID der virtuellen Maschine wird beibehalten. Der folgende Befehl zeigt ein Beispiel für eine Import Datei. Führen Sie einen ähnlichen Befehl mit ihren eigenen Werten aus.

```powershell
Import-VM -Path 'C:\<vm export path>\2B91FEB3-F1E0-4FFF-B8BE-29CED892A95A.vmcx'
```

#### <a name="restore"></a>Restore

Um den virtuellen Computer mit einem eigenen Pfad für die Dateien des virtuellen Computers zu importieren, führen Sie einen Befehl wie diesen aus, und ersetzen Sie die Beispiele durch ihre Werte:

```powershell
Import-VM -Path 'C:\<vm export path>\2B91FEB3-F1E0-4FFF-B8BE-29CED892A95A.vmcx' -Copy -VhdDestinationPath 'D:\Virtual Machines\WIN10DOC' -VirtualMachinePath 'D:\Virtual Machines\WIN10DOC'
```

#### <a name="import-as-a-copy"></a>Als Kopie importieren

Um einen Kopier Import abzuschließen und die Dateien des virtuellen Computers an den Hyper-V-Standard Speicherort zu verschieben, führen Sie einen Befehl wie diesen aus, und ersetzen Sie die Beispiele durch ihre Werte:

``` PowerShell
Import-VM -Path 'C:\<vm export path>\2B91FEB3-F1E0-4FFF-B8BE-29CED892A95A.vmcx' -Copy -GenerateNewId
```

Weitere Informationen finden Sie unter [Import-VM](/powershell/module/hyper-v/import-vm).

### <a name="import-types"></a>Typen importieren

Hyper-V bietet drei Import Typen:

- Direkt **registrieren** – bei diesem Typ wird davon ausgegangen, dass sich die Export Dateien an dem Speicherort befinden, an dem Sie den virtuellen Computer speichern und ausführen. Der importierte virtuelle Computer hat die gleiche ID wie beim Export. Wenn der virtuelle Computer bereits bei Hyper-V registriert ist, muss er daher gelöscht werden, bevor der Import Vorgang funktioniert. Wenn der Import abgeschlossen ist, werden die Export Dateien zu den Dateien mit dem Status "wird ausgeführt" und können nicht entfernt werden.

- **Wiederherstellen der virtuellen Maschine** – stellen Sie die virtuelle Maschine an einem von Ihnen ausgewählten Speicherort wieder her, oder verwenden Sie die Standardeinstellung für Hyper-V. Mit diesem Importtyp wird eine Kopie der exportierten Dateien erstellt und an den ausgewählten Speicherort verschoben. Nach dem Importieren hat der virtuelle Computer dieselbe ID wie zum Zeitpunkt des Exports. Wenn der virtuelle Computer bereits in Hyper-V ausgeführt wird, muss er daher gelöscht werden, bevor der Import abgeschlossen werden kann. Wenn der Import abgeschlossen ist, bleiben die exportierten Dateien intakt und können entfernt oder importiert werden.

- **Kopieren Sie den virtuellen Computer** – Dies ähnelt dem wiederherungstyp, in dem Sie einen Speicherort für die Dateien auswählen. Der Unterschied besteht darin, dass der importierte virtuelle Computer über eine neue eindeutige ID verfügt. Dies bedeutet, dass der virtuelle Computer mehrmals auf denselben Host importiert werden kann.