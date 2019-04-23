---
title: Festplatte auswählen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a0da614b-09d9-433b-b4eb-9127f84431cb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6e8352b45cf3a46f14828c9c6796e4ec73499d5a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858961"
---
# <a name="select-disk"></a>Festplatte auswählen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Wählt den angegebenen Datenträger und verlagert den Fokus auf sie.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
select disk={ <n> | <disk path> | system | next }  
```  
  
> [!NOTE]  
> Die **<disk path>**, **System**, und **Weiter** Parameter sind nur in Windows 7 und Windows Server 2008 R2 verfügbar.  
  
## <a name="parameters"></a>Parameter  
  
|Parameter|Beschreibung|  
|-------|--------|  
|<n>|Gibt die Anzahl des Datenträgers an, den Fokus erhalten. Sie können die Zahlen für alle Datenträger auf dem Computer anzeigen, indem Sie mit der **Liste Datenträger** in DiskPart den Befehl. **Hinweis**: Wenn Sie Systeme mit mehreren Datenträgern zu konfigurieren, verwenden Sie keine **select Disk\=0** den Systemdatenträger an. Wenn Sie neu starten, und andere Computer mit der gleichen Datenträgerkonfiguration können verschiedene Datenträgernummern hat, kann der Computer die Datenträgernummern neu zuweisen.|  
|<disk path>|Gibt den Speicherort des Datenträgers an, z. B. den Fokus erhalten **PCIROOT\(0\)\#PCI\(0F02\)\#AtA\(C00T00L00\)** . Wenn den Pfad zum Speicherort eines Datenträgers anzeigen möchten, wählen Sie ihn, und geben Sie dann **Detail Datenträger**.|  
|System|BIOS-Computer gibt an, dass es sich bei diesen Datenträger 0 den Fokus erhält. Auf EFI-Computern ist der Datenträger, auf der EFI-Systempartition \(ESP\) , der verwendet wird, für der aktuelle Startvorgang den Fokus erhält. Auf EFI-Computern wird der Befehl fehl, wenn es keine ASW, ist bei mehr als ein ESP oder den Computer, über Windows Preinstallation Environment gestartet wird \(Windows PE\).|  
|Weiter|Nachdem Sie ein Datenträger aktiviert ist, durchläuft dieser Befehl alle Datenträger in der Liste der Datenträger ab. Wenn Sie diesen Befehl ausführen, wird dem nächsten Datenträger gespeichert, in der Liste den Fokus erhalten.|  
  
## <a name="BKMK_examples"></a>Beispiele für  
Um den Fokus auf den Datenträger 1 verschieben möchten, geben Sie Folgendes ein:  
  
```  
select disk=1  
```  
  
Um einen Datenträger mit der Location-Path auszuwählen, geben Sie Folgendes ein:  
  
```  
select disk=PCIROOT(0)#PCI(0100)#atA(C00T00L01)  
```  
  
Geben Sie Folgendes ein, um den Systemdatenträger den Fokus zu verschieben:  
  
```  
select disk=system  
```  
  
Um den Fokus auf dem nächsten Datenträger auf dem Computer zu verschieben, geben Sie Folgendes ein:  
  
```  
select disk=next  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

