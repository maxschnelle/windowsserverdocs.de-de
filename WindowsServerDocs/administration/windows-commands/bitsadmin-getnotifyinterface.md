---
title: bitsadmin getnotifyinterface
description: Windows-Befehls Thema für **bigsadmin getnotifyinterface**, das bestimmt, ob ein anderes Programm eine com-Rückruf Schnittstelle für den angegebenen Auftrag registriert hat.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 40bf9dd8-b167-406a-80a6-a5a6f1b8cf7f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5eb5aee42446c70f16fd6785a3645f42c1987e4d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850573"
---
# <a name="bitsadmin-getnotifyinterface"></a>bitsadmin getnotifyinterface

Bestimmt, ob ein anderes Programm eine com-Rückruf Schnittstelle (die Benachrichtigungs Schnittstelle) für den angegebenen Auftrag registriert hat.

## <a name="syntax"></a>Syntax

```
bitsadmin /getnotifyinterface <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

#### <a name="output"></a>Ausgabe

Mit der Ausgabe für diesen Befehl wird entweder, **registriert** oder **nicht registriert**angezeigt.

> [!NOTE]
> Das Programm, das die Rückruf Schnittstelle registriert hat, kann nicht bestimmt werden.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Benachrichtigungs Schnittstelle für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getnotifyinterface myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)