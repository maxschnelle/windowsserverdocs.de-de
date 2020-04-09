---
title: Hilfe
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75dbf94f-d79c-45b2-9463-c06648218f4a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 404cefe879e8f63678f2cba90516fad9c216eb23
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842313"
---
# <a name="help"></a>Hilfe

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine Liste der verfügbaren Befehle oder ausführliche Hilfe Informationen zu einem angegebenen Befehl an.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
help [<command>]  
```  
  
### <a name="parameters"></a>Parameter  
  
| Parameter |                              Beschreibung                              |
|-----------|-----------------------------------------------------------------------|
| <command> | Gibt den Befehl an, für den ausführliche Hilfe Informationen angezeigt werden sollen. |
  
## <a name="remarks"></a>Hinweise  
  
-   Wenn kein Befehl angegeben wird, werden in der **Hilfe** alle möglichen Befehle angezeigt.  
  
## <a name="examples"></a><a name=BKMK_examples></a>Beispiele  
Geben Sie Folgendes ein, um eine Liste aller in DiskPart verfügbaren Befehle anzuzeigen:  
  
```  
help  
```  
  
Geben Sie Folgendes ein, um ausführliche Hilfe Informationen zur Verwendung des Befehls **create partition primary** in DiskPart anzuzeigen:  
  
```  
help create partition primary  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

