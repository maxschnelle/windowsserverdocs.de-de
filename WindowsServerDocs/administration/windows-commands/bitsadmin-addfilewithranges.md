---
title: bitsadmin addfilewithranges
description: Windows-Befehls Thema für **bigsadmin ADDFILEWITHRANGES**, mit dem dem angegebenen Auftrag eine Datei hinzugefügt wird. Bits lädt die angegebenen Bereiche aus der Remote Datei herunter.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: df0ce0bf-dff1-4a48-a16f-fd2f4d5f7189
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 60b448550473691bbbaf573f99f00609e14e0f42
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850953"
---
# <a name="bitsadmin-addfilewithranges"></a>bitsadmin addfilewithranges

Fügt dem angegebenen Auftrag eine Datei hinzu. Bits lädt die angegebenen Bereiche aus der Remote Datei herunter. Dieser Schalter ist nur für Download Aufträge gültig.

## <a name="syntax"></a>Syntax

```
bitsadmin /AddFileWithRanges <Job> <RemoteURL> <LocalName> <RangeList>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| RemoteURL | Die URL der Datei auf dem Server. |
| LocalName | Der Name der Datei auf dem lokalen Computer. Muss einen absoluten Pfad zur Datei enthalten. |
| Rangelist | Durch Trennzeichen getrennte Liste der Offset: length-Paare. Verwenden Sie einen Doppelpunkt, um den Offset Wert vom Längen Wert zu trennen. Beispielsweise weist der Wert `0:100,2000:100,5000:eof` Bits an, 100 Bytes von Offset 0, 100 Byte von Offset 2000 und den verbleibenden Bytes von Offset 5000 an das Ende der Datei zu übertragen. |

## <a name="remarks"></a>Hinweise

- Das Token **EOF** ist ein gültiger Längen Wert innerhalb der Offset-und Längen Paare in der *\<rangelist >* . Er weist den Dienst an, am Ende der angegebenen Datei zu lesen.

- ADDFILEWITHRANGES schlägt mit dem Fehlercode 0x8020002c fehl, wenn ein Bereich der Länge 0 (null) zusammen mit einem anderen Bereich mit gleichem Offset angegeben wird, z. b.:

    `C:\bits>bitsadmin /addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:0,100:5`

    **Fehlermeldung:** Die Datei kann dem Auftrag "0x8020002c" nicht hinzugefügt werden. Die Liste der Byte Bereiche enthält einige überlappende Bereiche, die nicht unterstützt werden.

    Problem **Umgehung:** Legen Sie den Bereich mit der Länge Null nicht zuerst fest. Verwenden Sie z. b.: 

    `bitsadmin /addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:5,100:0.`

## <a name="examples"></a>Beispiele

Im folgenden Beispiel wird Bits zum Übertragen von 100 Bytes von Offset 0, 100 Bytes von Offset 2000 und den verbleibenden Bytes von Offset 5000 an das Ende der Datei mitgeteilt.

```
C:\>bitsadmin /addfilewithranges http://downloadsrv/10mb.zip c:\10mb.zip 0:100,2000:100,5000:eof
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)