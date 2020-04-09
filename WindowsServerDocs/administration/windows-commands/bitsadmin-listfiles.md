---
title: bitsadmin listfiles
description: Windows-Befehls Thema für **bigsadmin-listFiles**, das die Dateien im angegebenen Auftrag auflistet.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ad0d1eaa-3bd8-45e5-8f72-4da7366f0d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1af11f7876a3d1cd36aa38c7ac26563c01e81ab5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850313"
---
# <a name="bitsadmin-listfiles"></a>bitsadmin listfiles

Listet die Dateien im angegebenen Auftrag auf.

## <a name="syntax"></a>Syntax

```
bitsadmin /listfiles <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Liste der Dateien für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /listfiles myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)