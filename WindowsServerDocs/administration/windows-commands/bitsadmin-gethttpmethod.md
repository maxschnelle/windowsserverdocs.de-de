---
title: bitsadmin gethttpmethod
description: Referenz Thema für den bizadmin gethttpmethod-Befehl, mit dem das HTTP-Verb abgerufen wird, das mit dem Auftrag verwendet werden soll.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: a458322a5ace69df74df054a537a7365da9e7329
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717884"
---
# <a name="bitsadmin-gethttpmethod"></a>bitsadmin gethttpmethod

Ruft das HTTP-Verb ab, das mit dem Auftrag verwendet werden soll.

## <a name="syntax"></a>Syntax

```
bitsadmin /gethttpmethod <Job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie das HTTP-Verb für die Verwendung mit dem Auftrag *mydownloadjob*ab:

```
bitsadmin /gethttpmethod myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
