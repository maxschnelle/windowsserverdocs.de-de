---
title: assign
description: Windows-Befehle Thema **weisen** -weist einen Laufwerkbuchstaben oder Bereitstellungspunkt auf dem Volume mit dem Fokus.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57912b73-622e-489b-b053-a369021ba8e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0d830f9b1ec894c1bc136a99e7beb5703f840dc4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889291"
---
# <a name="assign"></a>assign

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

weist einen Laufwerkbuchstaben oder Bereitstellungspunkt auf dem Volume mit dem Fokus.

## <a name="syntax"></a>Syntax
```
assign [{letter=<d> | mount=<path>}] [noerr]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|letter=<d>|Der Laufwerkbuchstabe, die Sie dem Volume zuweisen möchten.|
|mount=<path>|Der Pfad des Volumebereitstellungspunkts, die, den Sie dem Volume zuweisen möchten.<br /><br />Anweisungen dazu, wie Sie diesen Befehl verwenden, finden Sie unter [weisen Sie einen Pfad des Volumebereitstellungspunkts Ordner auf einem Laufwerk](https://go.microsoft.com/fwlink/?LinkId=207059) (https://go.microsoft.com/fwlink/?LinkId=207059).|
|Diskpart|nur für Skripts. Wenn ein Fehler gefunden wird, weiterhin DiskPart Befehle zu verarbeiten, als ob der Fehler nicht aufgetreten ist. Ohne diesen Parameter wird ein Fehler DiskPart mit dem Fehlercode zu beenden.|
## <a name="remarks"></a>Hinweise
-   Wenn kein Laufwerkbuchstabe oder Bereitstellungspunkt angegeben ist, wird die nächste verfügbare Laufwerkbuchstabe zugewiesen. Wenn der Laufwerkbuchstabe oder Bereitstellungspunkt bereits verwendet wird, wird ein Fehler generiert.
-   Mit der Assign-Befehl können Sie den Laufwerkbuchstaben, einen Wechseldatenträger zugeordneten ändern.
-   Sie können keine Laufwerkbuchstaben auf Systemvolumes, Startvolumes oder Volumes, die die Auslagerungsdatei enthalten. Darüber hinaus können nicht Sie einen Laufwerkbuchstaben einer Partition (Original Equipment Manufacturers) oder eine GUID-Partitionstabelle (Gpt) andere Partition als eine grundlegende Daten zur Partition zuweisen.
-   Ein Volume muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden. Verwenden der **wählen Volume** Befehl aus, wählen Sie ein Volume und verschiebt den Fokus auf sie.
## <a name="BKMK_examples"></a>Beispiele für
Um den Buchstaben E auf dem Volume in den Fokus zuzuweisen, geben Sie Folgendes ein:
```
assign letter=e
```

