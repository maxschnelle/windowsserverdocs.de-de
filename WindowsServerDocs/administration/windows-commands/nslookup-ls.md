---
title: nslookup ls
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6a11867ff2ec69b1ef938149ac485ff8827b58de
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436922"
---
# <a name="nslookup-ls"></a>nslookup ls

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Listet Informationen für eine Domäne (DNS, Domain Name System).
## <a name="syntax"></a>Syntax
```
ls [<Option>] <DNSDomain> [{[>] <FileName>|[>>] <FileName>}]
```
## <a name="parameters"></a>Parameter

|    Parameter    |                                                                                                                                                                                                                                                                                                               Beschreibung                                                                                                                                                                                                                                                                                                                |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <Option>     | Die folgende Tabelle enthält die gültige Optionen.<br /><br />--t: Listet alle Datensätze des angegebenen Typs. Eine Beschreibung der <querytype>, finden Sie unter **Setquerytype** in zusätzliche Verweise.<br />--a: Listet die Aliase der Computer in der DNS-Domäne. Dieser Parameter ist ein Synonym für **- t CNAME-Eintrag**<br />-: "d:" listet alle Einträge für die DNS-Domäne. Dieser Parameter ist ein Synonym für **- t ANY**<br />--h: Listet Informationen zu CPU und Betriebssystem für die DNS-Domäne. Dieser Parameter ist ein Synonym für **- t HINFO**<br />--s: bekannten Dienste von Computern in der DNS-Domäne aufgelistet. Dieser Parameter ist ein Synonym für **-t "wks" beginnen**. |
|   <DNSDomain>   |                                                                                                                                                                                                                                                                                         Gibt die DNS-Domäne für die Sie Informationen möchten.                                                                                                                                                                                                                                                                                         |
|   <FileName>    |                                                                                                                                                                                                                                 Gibt einen Dateinamen in dem die Ausgabe zu speichern. Sie können es verwenden, der größer als (>) und doppeltes größer als (>>) Zeichen, die die Ausgabe umgeleitet, auf die übliche Weise.                                                                                                                                                                                                                                  |
| {help &#124; ?} |                                                                                                                                                                                                                                                                                          Zeigt eine kurze Zusammenfassung der **Nslookup** Unterbefehle.                                                                                                                                                                                                                                                                                           |

## <a name="remarks"></a>Hinweise
- Die Standardausgabe enthält, die Computernamen und die IP-Adressen. Bei der Ausgabe in eine Datei weitergeleitet wird, werden Nummernzeichen für alle 50 Datensätze, die vom Server empfangene gedruckt.
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  [Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
  [Nslookup festgelegt Querytype](nslookup-set-querytype.md)
