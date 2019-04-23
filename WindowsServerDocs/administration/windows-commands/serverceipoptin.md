---
title: serverceipoptin
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3d7d7fa7-0689-4797-b802-36fe260d21a0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fca2497af308faf298e1df03d8b07c68bf9e8b98
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840561"
---
# <a name="serverceipoptin"></a>serverceipoptin

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Können Sie in der Gruppenrichtlinien-Verwaltungskonsole (Customer Experience Improvement Program, CEIP) teilnehmen.
## <a name="syntax"></a>Syntax
```
serverceipoptin [/query] [/enable] [/disable]
```
### <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|/query|überprüft die aktuelle Einstellung an.|
|/ Enable /|Ermöglicht die Teilnahme.|
|/ Disable|Deaktiviert die Teilnahme.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="BKMK_Examples"></a>Beispiele für
Um die aktuellen Einstellungen zu überprüfen, geben Sie Folgendes ein:
```
serverceipoptin /query
```
Um die Teilnahme zu aktivieren, geben Sie Folgendes ein:
```
serverceipoptin /enable
```
Um die Teilnahme zu deaktivieren, geben Sie Folgendes ein:
```
serverceipoptin /disable
```
## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Befehlszeilensyntax](command-line-syntax-key.md)

