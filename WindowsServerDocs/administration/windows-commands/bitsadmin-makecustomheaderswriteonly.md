---
title: biout admin makecustomheadersschreiteonly
description: Windows-Befehls Thema für **bitionadmin makecustomheadersschreiteonly**, mit dem die benutzerdefinierten HTTP-Header eines Auftrags schreibgeschützt werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 9183b1b5de51020c5c6d2efad2c0a788d158a183
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850243"
---
# <a name="bitsadmin-makecustomheaderswriteonly"></a>biout admin makecustomheadersschreiteonly

Schreiben Sie die benutzerdefinierten HTTP-Header eines Auftrags als schreibgeschützt.

> [!Important]
> Diese Aktion kann nicht rückgängig gemacht werden.

## <a name="syntax"></a>Syntax

```
bitsadmin /makecustomheaderswriteonly <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel werden benutzerdefinierte HTTP-Header für den Auftrag mit dem Namen *mydownloadjob*schreibgeschützt.

```
C:\>bitsadmin /makecustomheaderswriteonly myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)