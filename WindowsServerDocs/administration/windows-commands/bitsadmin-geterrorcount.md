---
title: bitsadmin geterrorcount
description: Referenz Thema für den bizadmin GetErrorCount-Befehl, der die Anzahl der Male abruft, mit denen der angegebene Auftrag einen vorübergehenden Fehler generiert hat.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 516bd02ed296a2eba75e174c6f084926bde63e90
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718011"
---
# <a name="bitsadmin-geterrorcount"></a>bitsadmin geterrorcount

Ruft ab, wie oft der angegebene Auftrag einen vorübergehenden Fehler generiert hat.

## <a name="syntax"></a>Syntax

```
bitsadmin /geterrorcount <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie Fehler Anzahl Informationen für den Auftrag mit dem Namen *mydownloadjob*ab:

```
bitsadmin /geterrorcount myDownloadJob
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
