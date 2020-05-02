---
title: nslookup ls
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f15f06fe-67e7-41a9-93b5-192ab14ab380
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8357208406c0fca5d68da419baa2092d94fa9ec9
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723708"
---
# <a name="nslookup-ls"></a>nslookup ls

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Listet Informationen für eine Domain Name System Domäne (DNS) auf.
## <a name="syntax"></a>Syntax
```
ls [<Option>] <DNSDomain> [{[>] <FileName>|[>>] <FileName>}]
```
### <a name="parameters"></a>Parameter

|    Parameter    |                                                                                                                                                                                                                                                                                                               BESCHREIBUNG                                                                                                                                                                                                                                                                                                                |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <Option>     | In der folgenden Tabelle sind die gültigen Optionen aufgeführt.<p>--t: Listet alle Datensätze des angegebenen Typs auf. Eine Beschreibung von <querytype>finden Sie unter **SetQueryType** in "Weitere Verweise".<br />--a: Listet die Aliase von Computern in der DNS-Domäne auf. Dieser Parameter ist ein Synonym für **-t CNAME** .<br />--d: Listet alle Datensätze für die DNS-Domäne auf. Dieser Parameter ist ein Synonym für " **-t any** ".<br />--h: Listet die CPU-und Betriebssysteminformationen für die DNS-Domäne auf. Dieser Parameter ist ein Synonym für **-t hinfo** .<br />--s: listet bekannte Dienste von Computern in der DNS-Domäne auf. Dieser Parameter ist ein Synonym für **-t-WGs**. |
|   <DNSDomain>   |                                                                                                                                                                                                                                                                                         Gibt die DNS-Domäne an, für die Sie Informationen wünschen.                                                                                                                                                                                                                                                                                         |
|   <FileName>    |                                                                                                                                                                                                                                 Gibt einen Dateinamen an, in dem die Ausgabe gespeichert werden soll. Sie können die Zeichen "größer als" (>) und "Double größer als" (>>) verwenden, um die Ausgabe auf die übliche Weise umzuleiten.                                                                                                                                                                                                                                  |
| {Help &#124;?} |                                                                                                                                                                                                                                                                                          Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.                                                                                                                                                                                                                                                                                           |

## <a name="remarks"></a>Bemerkungen
- Die Standardausgabe enthält Computernamen und Ihre IP-Adressen. Wenn die Ausgabe an eine Datei weitergeleitet wird, werden für alle vom Server empfangenen 50-Datensätze Hash Marken ausgegeben.
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup Set QueryType](nslookup-set-querytype.md)
