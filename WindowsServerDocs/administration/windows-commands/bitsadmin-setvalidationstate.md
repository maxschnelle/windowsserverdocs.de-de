---
title: bitsadmin setvalidationstate
description: Referenz Artikel für den Befehl "BITSAdmin setvalidationstate", mit dem der Inhalts Überprüfungs Zustand der angegebenen Datei innerhalb des Auftrags festgelegt wird.
ms.topic: reference
ms.assetid: e8fc8e8c-171c-4681-8057-6986b018e576
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1f30807e392ede7710c4d7740416d2cdb34c1378
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89630615"
---
# <a name="bitsadmin-setvalidationstate"></a>bitsadmin setvalidationstate

Legt den Inhalts Überprüfungs Zustand der angegebenen Datei innerhalb des Auftrags fest.

## <a name="syntax"></a>Syntax

```
bitsadmin /setvalidationstate <job> <file_index> <TRUE|FALSE>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
