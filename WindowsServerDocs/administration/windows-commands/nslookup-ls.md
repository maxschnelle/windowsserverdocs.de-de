---
title: nslookup ls
description: Referenz Artikel für den Befehl nslookup ls, der DNS-Domänen Informationen auflistet.
ms.topic: reference
ms.assetid: f15f06fe-67e7-41a9-93b5-192ab14ab380
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 6910fa753ff394416f1cbf201db690647cebe9a0
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89635679"
---
# <a name="nslookup-ls"></a>nslookup ls

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Listet DNS-Domänen Informationen auf.

## <a name="syntax"></a>Syntax

```
ls [<option>] <DNSdomain> [{[>] <filename>|[>>] <filename>}]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<option>` | Folgende Optionen sind gültig:<ul><li>**-t:** Listet alle Datensätze des angegebenen Typs auf. Weitere Informationen finden Sie unter [nslookup Set QueryType](nslookup-set-querytype.md).</li><li>**-a:** Listet die Aliase von Computern in der DNS-Domäne auf. Dieser Parameter entspricht dem Wert **-t CNAME** .</li><li>**-d:** Listet alle Datensätze für die DNS-Domäne auf. Dieser Parameter entspricht dem Wert **-t any** .</li><li>**-h:** Listet die CPU-und Betriebssysteminformationen für die DNS-Domäne auf. Dieser Parameter ist identisch mit " **-t hinfo** ".</li><li>**-s:** Listet bekannte Dienste von Computern in der DNS-Domäne auf. Dieser Parameter entspricht dem **-t-Wi**. |
| `<DNSdomain>` | Gibt die DNS-Domäne an, für die Sie Informationen wünschen. |
| `<filename>` | Gibt einen Dateinamen an, der für die gespeicherte Ausgabe verwendet werden soll. Sie können die Zeichen "größer als" ( `>` ) und "Double größer als ()" verwenden `>>` , um die Ausgabe auf die übliche Weise umzuleiten. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Die Standardausgabe dieses Befehls enthält Computernamen und die zugehörigen IP-Adressen.

- Wenn die Ausgabe an eine Datei weitergeleitet wird, werden für alle vom Server empfangenen 50-Datensätze Hash Markierungen hinzugefügt.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [nslookup set querytype](nslookup-set-querytype.md)
