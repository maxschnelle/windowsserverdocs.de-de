---
title: bitsadmin setvalidationstate
description: Referenz Thema für den BITSAdmin setvalidationstate-Befehl, mit dem der Inhalts Überprüfungs Zustand der angegebenen Datei innerhalb des Auftrags festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e8fc8e8c-171c-4681-8057-6986b018e576
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e3f22dc09eb1f70ce3c1ebd80fd6ba721e864377
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720465"
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
| TRUE oder false | **True** schaltet die Inhalts Überprüfung für die angegebene Datei ein, während **false** Sie deaktiviert. |

## <a name="examples"></a>Beispiele

So legen Sie den Status der Inhalts Überprüfung von Datei 2 für den Auftrag *mydownloadjob*auf true fest:

```
bitsadmin /setvalidationstate myDownloadJob 2 TRUE
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
