---
title: Exportieren und Importieren von virtuellen Computern
description: Erfahren Sie, wie zum Exportieren und importieren virtueller Computer mit Hyper-V-Manager oder Windows PowerShell.
ms.prod: windows-server-threshold
author: KBDAzure
ms.author: kathydav
manager: dongill
ms.technology: compute-hyper-v
ms.date: 12/13/2016
ms.topic: article
ms.assetid: 7fd996f5-1ea9-4b16-9776-85fb39a3aa34
ms.openlocfilehash: b326fe8d7ff05ba73fc94225fa38921b42eb3fc6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844321"
---
>Gilt für: Windows 10, WindowsServer 2016, Microsoft Hyper-V Server 2016, WindowsServer 2019, Microsoft Hyper-V-Server 2019

# <a name="export-and-import-virtual-machines"></a>Exportieren und Importieren virtueller Computer

In diesem Artikel wird das Exportieren und importieren eine virtuelle Maschine, dies ist eine schnelle Möglichkeit zum Verschieben oder kopieren, veranschaulicht. Dieser Artikel beschreibt auch einige der Wahlmöglichkeiten machen, wenn Sie einen Export durchführen, oder importieren.

## <a name="export-a-virtual-machine"></a>Exportieren eines virtuellen Computers

Ein Export erfasst alle erforderliche Dateien in eine Einheit – virtuelle Festplattendateien, Konfigurationsdateien virtueller Computer und alle Prüfpunktdateien. Sie können auf einem virtuellen Computer dazu, die in einem gestarteten und beendeten Zustand befindet.

### <a name="using-hyper-v-manager"></a>Verwenden des Hyper-V-Managers

So erstellen Sie einen Export eines virtuellen Computers

1. In Hyper-V-Manager mit der rechten Maustaste in den virtuellen Computer, und wählen Sie **exportieren**.

2. Wählen Sie den Speicherort, um die exportierten Dateien aus, und klicken Sie auf **exportieren**.

Wenn der Export abgeschlossen ist, sehen Sie alle exportierte Dateien unter den Exportspeicherort.

### <a name="using-powershell"></a>Mithilfe der PowerShell

Öffnen einer Sitzung als Administrator, und führen Sie einen Befehl wie folgt aus, nach dem Ersetzen \<Name des virtuellen Computers\> und \<Pfad\>:

```powershell
Export-VM -Name \<vm name\> -Path \<path\>
```

Weitere Informationen finden Sie unter [Export-VM](https://docs.microsoft.com/powershell/module/hyper-v/export-vm).

## <a name="import-a-virtual-machine"></a>Importieren eines virtuellen Computers 

Beim Importieren wird der virtuelle Computer beim Hyper-V-Host registriert. Sie können der Host oder den neuen Host wieder importieren. Wenn Sie mit dem gleichen Host importieren, müssen Sie den virtuellen Computer zunächst exportieren, daran, dass Hyper-V versucht wird, um den virtuellen Computer aus der verfügbaren Dateien erneut zu erstellen. Importieren einer virtuellen Maschine registriert es, damit sie auf dem Hyper-V-Host verwendet werden kann.

Der Import-VM-Assistent unterstützt auch bei der Behebung von Inkompatibilitäten bietet, die beim Wechsel von einem Host zum anderen vorhanden sein können. Dies ist im Allgemeinen Unterschiede in der physischen Hardware, wie Arbeitsspeicher, virtuelle Switches und virtuelle Prozessoren.

### <a name="import-using-hyper-v-manager"></a>Importieren, die mit dem Hyper-V-Manager

Um einen virtuellen Computer zu importieren:

1. Von der **Aktionen** in Hyper-V-Manager, klicken Sie anschließend auf **importieren virtueller Computer**.

2. Klicken Sie auf **Weiter**.

3. Wählen Sie den Ordner, der die exportierten Dateien enthält, und klicken Sie auf **Weiter**.

4. Wählen Sie den virtuellen Computer importieren.

5. Wählen Sie den Import aus, und klicken Sie auf **Weiter**. (Beschreibungen, finden Sie unter [importieren Typen](#import-types)weiter unten.)

6. Klicken Sie auf **Fertig stellen**.

### <a name="import-using-powershell"></a>Importieren mithilfe von PowerShell

Verwenden der **Import-VM** Cmdlets, folgt das Beispiel für den Typ des Imports werden sollen. Beschreibungen der Kontotypen, finden Sie unter [importieren Typen](#import-types)weiter unten. 

#### <a name="register-in-place"></a>Direktes registrieren

Diese Art von importieren, werden die Dateien an, wo sie, zum Zeitpunkt des Imports gespeichert sind, verwendet, und behält die VM-ID an. Der folgende Befehl zeigt ein Beispiel für eine Datei importieren. Führen Sie einen ähnlichen Befehl durch Ihre eigenen Werte.

```powershell
Import-VM -Path 'C:\<vm export path>\2B91FEB3-F1E0-4FFF-B8BE-29CED892A95A.vmcx' 
```

#### <a name="restore"></a>Wiederherstellen

Um den virtuellen Computer, die Angabe Ihres eigenen Pfads für die Dateien der virtuellen Maschine zu importieren, führen Sie einen Befehl wie folgt, und Ersetzen Sie die Beispiele durch Ihre Werte ein:

```powershell
Import-VM -Path 'C:\<vm export path>\2B91FEB3-F1E0-4FFF-B8BE-29CED892A95A.vmcx' -Copy -VhdDestinationPath 'D:\Virtual Machines\WIN10DOC' -VirtualMachinePath 'D:\Virtual Machines\WIN10DOC'
```

#### <a name="import-as-a-copy"></a>Importieren Sie als eine Kopie

Führen einen Import kopieren und Verschieben von Dateien des virtuellen Computers auf den Hyper-V-Standardspeicherort, führen Sie einen Befehl wie folgt, und Ersetzen Sie die Beispiele durch Ihre Werte ein:

``` PowerShell
Import-VM -Path 'C:\<vm export path>\2B91FEB3-F1E0-4FFF-B8BE-29CED892A95A.vmcx' -Copy -GenerateNewId
```

Weitere Informationen finden Sie unter [Import-VM](https://docs.microsoft.com/powershell/module/hyper-v/import-vm).

### <a name="import-types"></a>Importtypen

Hyper-V bietet drei importtypen:

- **Direktes registrieren** – dieses Typs wird davon ausgegangen, Exportdateien werden in den Speicherort, wo Sie gespeichert und führen Sie den virtuellen Computer. Die importierte virtuelle Maschine hat dieselbe ID wie zuvor zum Zeitpunkt des Exports. Aus diesem Grund, wenn der virtuelle Computer bereits, mit Hyper-V registriert ist, muss er gelöscht werden, bevor der Import funktioniert. Wenn der Import abgeschlossen ist, werden die Exportdateien der ausgeführten Status der Dateien und kann nicht entfernt werden.

- **Wiederherstellen der virtuellen Maschine** : Wiederherstellen der virtuellen Maschine an einem Speicherort, die Sie auswählen, oder verwenden Sie die Standardeinstellung in Hyper-V. Dieser Importtyp wird eine Kopie der exportierten Dateien erstellt und sie in der ausgewählten Position verschoben werden. Nach dem Importieren hat der virtuelle Computer dieselbe ID wie zum Zeitpunkt des Exports. Wenn der virtuelle Computer bereits, in Hyper-V ausgeführt wird, muss er deshalb gelöscht werden soll, bevor der Import abgeschlossen werden kann. Wenn der Import abgeschlossen ist, können die exportierten Dateien bleiben erhalten und entfernt oder erneut importiert.

- **Kopieren Sie die virtuelle Maschine** – Dies ähnelt dem vorherigen Typ dahingehend, dass Sie einen Speicherort für die Dateien auswählen. Der Unterschied besteht darin, dass der importierte virtuelle Computer eine neue eindeutige ID verfügt, was bedeutet, dass Sie dem virtuellen Computer auf demselben Host mehrmals importieren können.

