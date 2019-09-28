---
title: nslookup ls
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f15f06fe-67e7-41a9-93b5-192ab14ab380
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ecc419a72599b661865af6283821129a7021938a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373089"
---
# <a name="nslookup-ls"></a>nslookup ls

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Listet Informationen für eine Domain Name System Domäne (DNS) auf.
## <a name="syntax"></a>Syntax
```
ls [<Option>] <DNSDomain> [{[>] <FileName>|[>>] <FileName>}]
```
## <a name="parameters"></a>Parameter

|    Parameter    |                                                                                                                                                                                                                                                                                                               Beschreibung                                                                                                                                                                                                                                                                                                                |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <Option>     | In der folgenden Tabelle sind die gültigen Optionen aufgeführt.<br /><br />--t: Listet alle Datensätze des angegebenen Typs auf. Eine Beschreibung <querytype> finden Sie unter **SetQueryType** in "Weitere Verweise".<br />--a: Listet die Aliase von Computern in der DNS-Domäne auf. Dieser Parameter ist ein Synonym für **-t CNAME** .<br />--d: Listet alle Datensätze für die DNS-Domäne auf. Dieser Parameter ist ein Synonym für " **-t any** ".<br />--h: Listet die CPU-und Betriebssysteminformationen für die DNS-Domäne auf. Dieser Parameter ist ein Synonym für **-t hinfo** .<br />--s: listet bekannte Dienste von Computern in der DNS-Domäne auf. Dieser Parameter ist ein Synonym für **-t-WGs**. |
|   <DNSDomain>   |                                                                                                                                                                                                                                                                                         Gibt die DNS-Domäne an, für die Sie Informationen wünschen.                                                                                                                                                                                                                                                                                         |
|   <FileName>    |                                                                                                                                                                                                                                 Gibt einen Dateinamen an, in dem die Ausgabe gespeichert werden soll. Sie können die Zeichen "größer als" (>) und "Double größer als" (> >) verwenden, um die Ausgabe auf die übliche Weise umzuleiten.                                                                                                                                                                                                                                  |
| {Help &#124; ?} |                                                                                                                                                                                                                                                                                          Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an.                                                                                                                                                                                                                                                                                           |

## <a name="remarks"></a>Hinweise
- Die Standardausgabe enthält Computernamen und Ihre IP-Adressen. Wenn die Ausgabe an eine Datei weitergeleitet wird, werden für alle vom Server empfangenen 50-Datensätze Hash Marken ausgegeben.
  ## <a name="additional-references"></a>Weitere Verweise
  [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup Set QueryType](nslookup-set-querytype.md)
