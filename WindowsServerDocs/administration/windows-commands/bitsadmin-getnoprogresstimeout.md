---
title: bitsadmin getnoprogresstimeout
description: Referenz Artikel für den bistiadmin getnoprogresstimeout-Befehl, der die Zeitspanne (in Sekunden) angibt, die der Dienst versucht, die Datei zu übertragen, nachdem ein vorübergehender Fehler auftritt.
ms.topic: article
ms.assetid: 9cd9b19b-cbb4-4352-8419-978080f016b6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b0bd85d93416e5e5718f5be830c99936a3080e24
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87894140"
---
# <a name="bitsadmin-getnoprogresstimeout"></a>bitsadmin getnoprogresstimeout

Ruft die Zeitdauer in Sekunden ab, die der Dienst versucht, die Datei zu übertragen, nachdem ein vorübergehender Fehler aufgetreten ist.

## <a name="syntax"></a>Syntax

```
bitsadmin /getnoprogresstimeout <job>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="examples"></a>Beispiele

So rufen Sie den Wert für den Status Timeout Wert für den Auftrag *mydownloadjob*ab:

```
bitsadmin /getnoprogresstimeout myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
