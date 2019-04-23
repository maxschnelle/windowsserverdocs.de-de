---
title: bitsadmin addfilewithranges
description: Windows-Befehle Thema **Bitsadmin Addfilewithranges** -Fügt eine Datei zum angegebenen Auftrag. BITS-downloads der angegebenen Bereiche aus der remote-Datei.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df0ce0bf-dff1-4a48-a16f-fd2f4d5f7189
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 69b402195f90977aa63299c1a2a550ba310a4513
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832341"
---
# <a name="bitsadmin-addfilewithranges"></a>bitsadmin addfilewithranges

Fügt eine Datei zum angegebenen Auftrag. BITS-downloads der angegebenen Bereiche aus der remote-Datei. Diese Option gilt nur für den Downloadaufträge zur Verfügung.

## <a name="syntax"></a>Syntax

```
bitsadmin /AddFileWithRanges <Job> <RemoteURL> <LocalName> <RangeList>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Anzeigenamen oder die GUID des Auftrags|
|RemoteURL|*RemoteURL* ist die URL der Datei auf dem Server.|
|LocalName|*LocalName* ist der Name der Datei auf dem lokalen Computer. *LocalName* muss einen absoluten Pfad zu der Datei enthalten.|
|RangeList|*RangeList* ist eine durch Trennzeichen getrennte Liste von Offset: Länge-Paaren. Verwenden Sie einen Doppelpunkt, um den Wert des Offsets vom Wert für die Länge zu trennen. Z. B. den Wert `0:100,2000:100,5000:eof` weist BITS, um 100 Bytes bei Offset 0, 100 Bytes bei Offset 2000 übertragen und die verbleibenden Bytes vom offset 5000 an das Ende der Datei.|

## <a name="more-information"></a>Weitere Informationen

-   Das Token **eof** ist ein gültige Länge-Wert in den Offset und Länge-Paaren, in der  *\<RangeList >*. Sie weist den Dienst bis zum Ende der angegebenen Datei gelesen.
-   Beachten Sie, dass mit dem Fehlercode 0x8020002c AddFileWithRanges ausgeführt wird, wenn z. B. ein Bereich mit der Länge Null zusammen mit einem anderen Bereich mit demselben Offset angegeben wird: C:\bits > Bitsadmin/ADDFILEWITHRANGES j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:0, 100:5

    Fehlermeldung: -Auftrags – 0x8020002c Datei hinzu. Die Liste mit bytebereichen enthält einige sich überschneidender Bereiche, die nicht unterstützt werden.

    Problemumgehung: Führen Sie nicht zuerst Geben Sie an, der Bereich der Länge 0 (null). Zum Beispiel: Bitsadmin/ADDFILEWITHRANGES j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:5, 100:0.

## <a name="BKMK_examples"></a>Beispiele für

Im folgende Beispiel wird BITS auf 100 Bytes vom Offset 0, 100 Bytes vom Offset 2000 übertragen, und die restlichen Bytes vom offset 5000 an das Ende der Datei.
```
C:\>bitsadmin /addfilewithranges http://downloadsrv/10mb.zip c:\10mb.zip "0:100,2000:100,5000:eof"
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)