---
title: bitsadmin setvalidationstate
description: Referenz Artikel für den Befehl "BITSAdmin setvalidationstate", mit dem der Inhalts Überprüfungs Zustand der angegebenen Datei innerhalb des Auftrags festgelegt wird.
ms.topic: reference
ms.assetid: e8fc8e8c-171c-4681-8057-6986b018e576
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5885f0f43e7c33e55dc05182819a339d69519d84
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89034728"
---
# <a name="bitsadmin-setvalidationstate"></a>bitsadmin setvalidationstate

Legt den Inhalts Überprüfungs Zustand der angegebenen Datei innerhalb des Auftrags fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setvalidationstate <job> <file_index> <TRUE|FALSE>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ---------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| file_index | Beginnt bei 0. |
| TRUE oder FALSE | **True** schaltet die Inhalts Überprüfung für die angegebene Datei ein, während **false** Sie deaktiviert. |

## <a name="examples"></a>Beispiele

So legen Sie den Status der Inhalts Überprüfung von Datei 2 für den Auftrag *mydownloadjob*auf true fest:

```
bitsadmin /setvalidationstate myDownloadJob 2 TRUE
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
