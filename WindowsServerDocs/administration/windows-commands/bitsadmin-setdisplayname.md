---
title: bitsadmin setdisplayname
description: Windows-Befehls Thema für **bizadmin setdisplayname**, mit dem der Anzeige Name des angegebenen Auftrags festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0b1086903dd130392800f325c451bb4750fbf8fa
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123006"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname

Legt den anzeigen Amen für den angegebenen Auftrag fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setdisplayname <job> <display_name>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| display_name | Text, der als angezeigter Name für den jeweiligen Auftrag verwendet wird. |

## <a name="examples"></a>Beispiele

Im folgenden Beispiel wird der Anzeige Name für den Auftrag auf *mydownloadjob*festgelegt.

```
C:\>bitsadmin /setdisplayname myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)