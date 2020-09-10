---
title: bitsadmin setdisplayname
description: Referenz Artikel für den Befehl "bitadmin setdisplayname", mit dem der Anzeige Name des angegebenen Auftrags festgelegt wird.
ms.topic: reference
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 57a72d198b7d262f3a7958920e5d54955f8b6270
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630935"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname

Legt den anzeigen Amen für den angegebenen Auftrag fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setdisplayname <job> <display_name>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| display_name | Text, der als angezeigter Name für den jeweiligen Auftrag verwendet wird. |

## <a name="examples"></a>Beispiele

So legen Sie den anzeigen Amen für den Auftrag auf *mydownloadjob*fest

```
bitsadmin /setdisplayname myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
