---
title: Verkleinern
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec87cc7c-9846-465e-a10d-4ee10db4f4e6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 071fa0cd92bcf93537bfb1ce602792266372e911
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845781"
---
# <a name="shrink"></a>Verkleinern

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Der Diskpart-Verkleinerungsbefehl reduziert die Größe des ausgewählten Volumes durch die Menge, die Sie angeben. Dieser Befehl stellt über den nicht verwendeten Speicherplatz am Ende des Volumes freier Speicherplatz zur Verfügung.

## <a name="syntax"></a>Syntax
```
shrink [desired=<n>] [minimum=<n>] [nowait] [noerr]
shrink querymax [noerr]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|desired=<n>|Gibt die gewünschte Menge des Speicherplatzes in Megabyte (MB), um die Größe des Volumes zu verringern.|
|minimum=<n>|Gibt die Mindestmenge an Speicherplatz in MB zum Verringern der Größe des Volumes durch.|
|querymax|Gibt den maximalen verfügbaren Speicherplatz in MB, die mit dem das Volume reduziert werden kann. Dieser Wert kann sich ändern, wenn Anwendungen gerade auf das Volume zugreifen.|
|NOWAIT|Erzwingt, dass der Befehl, um sofort während des verkleinerungsprozesses noch ausgeführt wird.|
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|
## <a name="remarks"></a>Hinweise
-   Sie können die Größe eines Volumes reduzieren, wenn es mit dem NTFS-Dateisystem formatiert ist oder sie nicht über ein Dateisystem verfügt.
-   Dieser Befehl kann auf einfache Volumes, und klicken Sie auf einfachen oder übergreifenden dynamischen Volumes.
-   Wenn Sie eine gewünschte Menge nicht angegeben ist, wird das Volume durch die Mindestmenge reduziert werden (falls angegeben).
-   Wenn Sie eine minimale Menge nicht angegeben ist, wird das Volume durch die gewünschte Menge reduziert werden (falls angegeben).
-   Wenn weder eine Mindestmenge noch eine gewünschte Menge angegeben wird, wird das Volume reduziert werden, von so weit wie möglich.
-   Wenn eine Mindestmenge angegeben ist, jedoch nicht genügend freier Speicherplatz verfügbar ist, wird der Befehl fehl.
-   Ein Volume muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden. Verwenden der **wählen Volume** Befehl aus, wählen Sie ein Volume und verschiebt den Fokus auf sie.
-   Dieser Befehl kann nicht auf Partitionen für Originalgerätehersteller (OEM), Extensible Firmware Interface (EFI) Systempartitionen oder Wiederherstellungspartitionen ausgeführt werden.
## <a name="BKMK_examples"></a>Beispiele für
Um die Größe des ausgewählten Volumes durch die größte mögliche Menge zwischen 250 bis 500 MB zu reduzieren, geben Sie Folgendes ein:
```
shrink desired=500 minimum=250
```
Um die maximale Anzahl von MB anzuzeigen, die durch das Volume reduziert werden kann, geben Sie Folgendes ein:
```
shrink querymax
```

[Ändern der Größe einer Partition](https://technet.microsoft.com/library/hh848680.aspx)
