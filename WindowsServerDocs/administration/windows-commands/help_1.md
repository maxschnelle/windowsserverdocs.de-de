---
title: Hilfe
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75dbf94f-d79c-45b2-9463-c06648218f4a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c3d76a71ec287e5c874ae3e4dec34016c5c80336
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375579"
---
# <a name="help"></a>Hilfe

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine Liste der verfügbaren Befehle oder ausführliche Hilfe Informationen zu einem angegebenen Befehl an.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
help [<command>]  
```  
  
## <a name="parameters"></a>Parameter  
  
| Parameter |                              Beschreibung                              |
|-----------|-----------------------------------------------------------------------|
| <command> | Gibt den Befehl an, für den ausführliche Hilfe Informationen angezeigt werden sollen. |
  
## <a name="remarks"></a>Hinweise  
  
-   Wenn kein Befehl angegeben wird, werden in der **Hilfe** alle möglichen Befehle angezeigt.  
  
## <a name="BKMK_examples"></a>Beispiele  
Geben Sie Folgendes ein, um eine Liste aller in DiskPart verfügbaren Befehle anzuzeigen:  
  
```  
help  
```  
  
Geben Sie Folgendes ein, um ausführliche Hilfe Informationen zur Verwendung des Befehls **create partition primary** in DiskPart anzuzeigen:  
  
```  
help create partition primary  
```  
  
#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

