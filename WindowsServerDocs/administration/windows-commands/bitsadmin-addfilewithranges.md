---
title: bitsadmin addfilewithranges
description: 'Thema Windows-Befehle für **bigsadmin ADDFILEWITHRANGES** : Fügt eine Datei zum angegebenen Auftrag hinzu. Bits lädt die angegebenen Bereiche aus der Remote Datei herunter.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 557f19f6e106e5fb73b3a229090eecf0fc048758
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382017"
---
# <a name="bitsadmin-addfilewithranges"></a>bitsadmin addfilewithranges

Fügt dem angegebenen Auftrag eine Datei hinzu. Bits lädt die angegebenen Bereiche aus der Remote Datei herunter. Dieser Schalter ist nur für Download Aufträge gültig.

## <a name="syntax"></a>Syntax

```
bitsadmin /AddFileWithRanges <Job> <RemoteURL> <LocalName> <RangeList>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Auftrag|Der Anzeige Name oder GUID des Auftrags.|
|RemoteURL|*RemoteURL* ist die URL der Datei auf dem Server.|
|LocalName|*Localname* ist der Name der Datei auf dem lokalen Computer. " *Localname* " muss einen absoluten Pfad zur Datei enthalten.|
|Rangelist|*Rangelist* eine durch Trennzeichen getrennte Liste der Offset: length-Paare. Verwenden Sie einen Doppelpunkt, um den Offset Wert vom Längen Wert zu trennen. Beispielsweise weist der Wert `0:100,2000:100,5000:eof` Bits an, 100 Bytes von Offset 0, 100 Byte von Offset 2000 und den verbleibenden Bytes von Offset 5000 an das Ende der Datei zu übertragen.|

## <a name="more-information"></a>Weitere Informationen

-   Das Token **EOF** ist ein gültiger Längen Wert innerhalb der Offset-und Längen Paare in der *\<rangelist >* . Er weist den Dienst an, am Ende der angegebenen Datei zu lesen.
-   Beachten Sie, dass ADDFILEWITHRANGES mit dem Fehlercode 0x8020002c fehlschlägt, wenn ein Bereich der Länge 0 (null) zusammen mit einem anderen Bereich mit gleichem Offset angegeben wird, z. b.: C:\bits > BITSAdmin/ADDFILEWITHRANGES J2 http://bitsdc/dload/1k.zip c:\1k.zip 100:0100:5

    Fehlermeldung: Die Datei kann dem Auftrag "0x8020002c" nicht hinzugefügt werden. Die Liste der Byte Bereiche enthält einige überlappende Bereiche, die nicht unterstützt werden.

    Problem Umgehung: Geben Sie den Bereich mit der Länge Null nicht zuerst an. Beispiel: bizadmin/ADDFILEWITHRANGES J2 http://bitsdc/dload/1k.zip c:\1k.zip 100:5100:0.

## <a name="examples"></a>Beispiele

Im folgenden Beispiel wird Bits zum Übertragen von 100 Bytes von Offset 0, 100 Bytes von Offset 2000 und den verbleibenden Bytes von Offset 5000 an das Ende der Datei mitgeteilt.

```
C:\>bitsadmin /addfilewithranges http://downloadsrv/10mb.zip c:\10mb.zip "0:100,2000:100,5000:eof"
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)