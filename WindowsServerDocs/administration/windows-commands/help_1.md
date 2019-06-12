---
title: Hilfe
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 078c779e7813d2aa7499e515d9729edf92452237
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438201"
---
# <a name="help"></a>Hilfe

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt eine Liste der verfügbaren Befehle oder ausführliche Hilfeinformationen für einen angegebenen Befehl.  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
help [<command>]  
```  
  
## <a name="parameters"></a>Parameter  
  
| Parameter |                              Beschreibung                              |
|-----------|-----------------------------------------------------------------------|
| <command> | Gibt den Startbefehl für die ausführliche Hilfeinformationen anzuzeigen. |
  
## <a name="remarks"></a>Hinweise  
  
-   Wenn kein Befehl angegeben wird, **Hilfe** werden alle möglichen Befehle angezeigt.  
  
## <a name="BKMK_examples"></a>Beispiele für  
Geben Sie zum Anzeigen einer Liste aller Befehle in DiskPart verfügbar:  
  
```  
help  
```  
  
Zum Anzeigen von ausführlichen Hilfeinformationen zur Verwendung der **erstellen Sie eine primäre Partition** Befehl DiskPart, Typ:  
  
```  
help create partition primary  
```  
  
#### <a name="additional-references"></a>Zusätzliche Referenzen  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

