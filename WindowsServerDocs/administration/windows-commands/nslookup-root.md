---
title: nslookup root
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9c29edc3-ec49-43f2-bc49-86bf0612d816
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bdfbe40443cf8f2fec2f81608bb93603cd74937f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723690"
---
# <a name="nslookup-root"></a>nslookup root

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ändert den Standard Server für den Stamm Domain Name System des DNS-Domänen Namen-Speicherplatzes auf den Server.
## <a name="syntax"></a>Syntax
```
root 
```
### <a name="parameters"></a>Parameter

|    Parameter    |                      BESCHREIBUNG                      |
|-----------------|-------------------------------------------------------|
| {Help &#124;?} | Zeigt eine kurze Zusammenfassung der **nslookup** -Unterbefehle an. |

## <a name="remarks"></a>Bemerkungen
- Derzeit wird der NS.nic.DDN.mil Nameserver verwendet. Dieser Befehl ist ein Synonym für lserver NS.nic.DDN.mil. Sie können den Namen des Stamm Servers mit dem Befehl " **root festlegen** " ändern.
  ## <a name="additional-references"></a>Zusätzliche Referenzen
  - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [nslookup](nslookup-set-root.md) -Stammgruppe
