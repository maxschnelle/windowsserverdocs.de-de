---
title: serverweroptin
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f3c0b0af-cafb-4f09-8b36-5a357ddf392d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 29545be99b14042d16a6f3a4118e0746f18b14ab
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869641"
---
# <a name="serverweroptin"></a>serverweroptin

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Können Sie die Fehlerberichterstattung zu aktivieren.
## <a name="syntax"></a>Syntax
```
serverweroptin [/query] [/detailed] [/summary]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/query|überprüft die aktuelle Einstellung an.|
|/detailed|Sendet ausführliche Berichte automatisch aus.|
|/summary|Zusammenfassende Berichte werden automatisch gesendet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="BKMK_Examples"></a>Beispiele für
Um die aktuelle Einstellung zu überprüfen, geben Sie Folgendes ein:
```
serverweroptin /query
```
Um automatisch ausführliche Berichte senden möchten, geben Sie Folgendes ein:
```
serverweroptin /detailed
```
Geben Sie zum automatischen Senden von Zusammenfassungsberichten
```
serverweroptin /summary
```
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Befehlszeilensyntax](command-line-syntax-key.md)

