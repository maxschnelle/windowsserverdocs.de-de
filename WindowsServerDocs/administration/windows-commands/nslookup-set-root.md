---
title: nslookup set root
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ad5393c-d4fd-4594-8187-576b1dcde60a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38cd5a2e9878a8e43393befc5cbd4fc47c65ec53
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436602"
---
# <a name="nslookup-set-root"></a>nslookup set root

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ändert den Namen des Stammservers für Abfragen verwendet.
## <a name="syntax"></a>Syntax
```
set root=<RootServer>
```
## <a name="parameters"></a>Parameter

|    Parameter    |                                   Beschreibung                                    |
|-----------------|----------------------------------------------------------------------------------|
|  <RootServer>   | Gibt den neuen Namen für den Root-Server an. Der Standardwert ist "NS.NIC.ddn.mil". |
| {help &#124; ?} |              Zeigt eine kurze Zusammenfassung der **Nslookup** Unterbefehle.               |

## <a name="remarks"></a>Hinweise
- Die **Satz Stamm** Unterbefehl wirkt sich auf die **Stamm** Unterbefehl.
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  [Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
  [Nslookup-Stamm](nslookup-root.md)
