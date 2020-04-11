---
title: bitsadmin Beschreibung
description: Windows-Befehls Thema für **bitadmin setDescription**, mit dem die Beschreibung des angegebenen Auftrags festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1e46a5dd-4637-4a2e-b88f-d3f85b177db8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0b62e6b030c23c475418cd6f2c63f04edba1acff
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123019"
---
# <a name="bitsadmin-setdescription"></a>bitsadmin Beschreibung

Legt die Beschreibung für den angegebenen Auftrag fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setdescription <job> <description>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| description | Der Text, der zur Beschreibung des Auftrags verwendet wird. |

## <a name="examples"></a>Beispiele

Im folgenden Beispiel wird die Beschreibung für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /setdescription myDownloadJob music_downloads
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)