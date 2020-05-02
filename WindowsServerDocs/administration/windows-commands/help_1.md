---
title: help
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75dbf94f-d79c-45b2-9463-c06648218f4a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6887edfd41895bb151c5aaebb88d8b72198f4dbf
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724900"
---
# <a name="help"></a>help

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine Liste der verfügbaren Befehle oder ausführliche Hilfe Informationen zu einem angegebenen Befehl an.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
help [<command>]  
```  
  
### <a name="parameters"></a>Parameter  
  
| Parameter |                              BESCHREIBUNG                              |
|-----------|-----------------------------------------------------------------------|
| <command> | Gibt den Befehl an, für den ausführliche Hilfe Informationen angezeigt werden sollen. |
  
## <a name="remarks"></a>Bemerkungen  
  
-   Wenn kein Befehl angegeben wird, werden in der **Hilfe** alle möglichen Befehle angezeigt.  
  
## <a name="examples"></a>Beispiele  
Geben Sie Folgendes ein, um eine Liste aller in DiskPart verfügbaren Befehle anzuzeigen:  
  
```  
help  
```  
  
Geben Sie Folgendes ein, um ausführliche Hilfe Informationen zur Verwendung des Befehls **create partition primary** in DiskPart anzuzeigen:  
  
```  
help create partition primary  
```  
  
## <a name="additional-references"></a>Zusätzliche Referenzen  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

