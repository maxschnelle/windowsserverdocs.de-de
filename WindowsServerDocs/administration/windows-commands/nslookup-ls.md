---
title: nslookup ls
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f15f06fe-67e7-41a9-93b5-192ab14ab380
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dbaef500410d6427beb008109abcc2c339b8d65c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838733"
---
# <a name="nslookup-ls"></a>nslookup ls

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Listet Informationen für eine Domain Name System Domäne (DNS) auf.
## <a name="syntax"></a>Syntax
```
ls [<Option>] <DNSDomain> [{[>] <FileName>|[>>] <FileName>}]
```
### <a name="parameters"></a>Parameter

|    Parameter    |                                                                                                                                                                                                                                                                                                               Beschreibung                                                                                                                                                                                                                                                                                                                |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <Option>     | In der folgenden Tabelle sind die gültigen Optionen aufgeführt.<p>--t: Listet alle Datensätze des angegebenen Typs auf. Eine Beschreibung <querytype>finden Sie unter **SetQueryType** in "Weitere Verweise".<br />--a: Listet die Aliase von Computern in der DNS-Domäne auf. Dieser Parameter ist ein Synonym für **-t CNAME** .<br />--d: Listet alle Datensätze für die DNS-Domäne auf. Dieser Parameter ist ein Synonym für " **-t any** ".<br />--h: Listet die CPU-und Betriebssysteminformationen für die DNS-Domäne auf. Dieser Parameter ist ein Synonym für **-t hinfo** .<br />--s: listet bekannte Dienste von Computern in der DNS-Domäne auf. Dieser Parameter ist ein Synonym für **-t-WGs**. |
|   <DNSDomain>   |                                                                                                                                                                                                                                                                                         Gibt die DNS-Domäne an, für die Sie Informationen wünschen.                                                                                                                                                                                                                                                                                         |
|   <FileName>    |                                                                                                                                                                                                                                 Gibt einen Dateinamen an, in dem die Ausgabe gespeichert werden soll. Sie können die Zeichen "größer als" (>) und "Double größer als" (> >) verwenden, um die Ausgabe auf die übliche Weise umzuleiten.                                                                                                                                                                                                                                  |
| {Help &#124; ?} |                                                                                                                                                                                                                                                                                          Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.                                                                                                                                                                                                                                                                                           |

## <a name="remarks"></a>Hinweise
- Die Standardausgabe enthält Computernamen und Ihre IP-Adressen. Wenn die Ausgabe an eine Datei weitergeleitet wird, werden für alle vom Server empfangenen 50-Datensätze Hash Marken ausgegeben.
  ## <a name="additional-references"></a>Weitere Verweise
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup-Satz QueryType](nslookup-set-querytype.md)
