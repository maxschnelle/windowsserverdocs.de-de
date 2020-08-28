---
title: bitsadmin getnoprogresstimeout
description: Referenz Artikel für den bistiadmin getnoprogresstimeout-Befehl, der die Zeitspanne (in Sekunden) angibt, die der Dienst versucht, die Datei zu übertragen, nachdem ein vorübergehender Fehler auftritt.
ms.topic: reference
ms.assetid: 9cd9b19b-cbb4-4352-8419-978080f016b6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 51a8327669bdadbebec28329e0c6b11cc32e672b
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89033518"
---
# <a name="bitsadmin-getnoprogresstimeout"></a>bitsadmin getnoprogresstimeout

Ruft die Zeitdauer in Sekunden ab, die der Dienst versucht, die Datei zu übertragen, nachdem ein vorübergehender Fehler aufgetreten ist.

## <a name="syntax"></a>Syntax

```
bitsadmin /getnoprogresstimeout <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
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
