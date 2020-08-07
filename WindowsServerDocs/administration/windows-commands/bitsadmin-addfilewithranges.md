---
title: bitsadmin addfilewithranges
description: Referenz Artikel für den Befehl bizadmin ADDFILEWITHRANGES, mit dem dem angegebenen Auftrag eine Datei hinzugefügt wird. Bits lädt die angegebenen Bereiche aus der Remote Datei herunter.
ms.topic: article
ms.assetid: df0ce0bf-dff1-4a48-a16f-fd2f4d5f7189
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c19c6dfec23cf012f42ab7d10b1d3df90ca957ff
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894876"
---
# <a name="bitsadmin-addfilewithranges"></a>bitsadmin addfilewithranges

Fügt dem angegebenen Auftrag eine Datei hinzu. Bits lädt die angegebenen Bereiche aus der Remote Datei herunter. Dieser Schalter ist nur für Download Aufträge gültig.

## <a name="syntax"></a>Syntax

```
bitsadmin /addfilewithranges <job> <remoteURL> <localname> <rangelist>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| RemoteURL | Die URL der Datei auf dem Server. |
| localname | Der Name der Datei auf dem lokalen Computer. Muss einen absoluten Pfad zur Datei enthalten. |
| rangelist | Durch Trennzeichen getrennte Liste der Offset: length-Paare. Verwenden Sie einen Doppelpunkt, um den Offset Wert vom Längen Wert zu trennen. Beispielsweise weist der Wert von `0:100,2000:100,5000:eof` Bits an, 100 Bytes von Offset 0, 100 Byte von Offset 2000 und den verbleibenden Bytes von Offset 5000 an das Ende der Datei zu übertragen. |

## <a name="remarks"></a>Bemerkungen

- Das Token **EOF** ist ein gültiger Längen Wert innerhalb der Offset-und Längen Paare im `<rangelist>` . Er weist den Dienst an, am Ende der angegebenen Datei zu lesen.

- Der `addfilewithranges` Befehl schlägt mit dem Fehlercode 0x8020002c fehl, wenn ein Bereich der Länge 0 (null) zusammen mit einem anderen Bereich mit dem gleichen Offset angegeben wird, z. b.:

    `c:\bits>bitsadmin /addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:0,100:5`

    **Fehlermeldung:** Die Datei kann dem Auftrag "0x8020002c" nicht hinzugefügt werden. Die Liste der Byte Bereiche enthält einige überlappende Bereiche, die nicht unterstützt werden.

    Problem **Umgehung:** Legen Sie den Bereich mit der Länge Null nicht zuerst fest. Verwenden Sie beispielsweise `bitsadmin /addfilewithranges j2 http://bitsdc/dload/1k.zip c:\1k.zip 100:5,100:0`.

## <a name="examples"></a>Beispiele

Zum Übertragen von 100 Bytes von Offset 0, 100 Bytes von Offset 2000 und den verbleibenden Bytes von Offset 5000 an das Ende der Datei:

```
bitsadmin /addfilewithranges http://downloadsrv/10mb.zip c:\10mb.zip 0:100,2000:100,5000:eof
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
