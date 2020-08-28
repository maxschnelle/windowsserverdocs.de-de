---
title: bitsadmin setnoprogresstimeout
description: Referenz Artikel für den bistiadmin setnoprogresstimeout-Befehl, der die Zeitspanne (in Sekunden) angibt, die der Dienst versucht, die Datei zu übertragen, nachdem ein vorübergehender Fehler aufgetreten ist.
ms.topic: reference
ms.assetid: 7fac50d9-cc6b-46a4-a96f-fab751ee1756
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dc2559a963900234fd3111edb1a32e3f13b27e40
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89027798"
---
# <a name="bitsadmin-setnoprogresstimeout"></a>bitsadmin setnoprogresstimeout

Legt die Zeitspanne (in Sekunden) fest, die Bits versucht, die Datei zu übertragen, nachdem der erste vorübergehende Fehler aufgetreten ist.

## <a name="syntax"></a>Syntax

```
bitsadmin /setnoprogresstimeout <job> <timeoutvalue>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| TimeOutValue | Die Zeitdauer, die Bits auf die Übertragung einer Datei nach dem ersten Fehler (in Sekunden) wartet. |

### <a name="remarks"></a>Bemerkungen

- Das Timeout Intervall "kein Fortschritt" beginnt, wenn der Auftrag seinen ersten vorübergehenden Fehler feststellt.

- Das Timeout Intervall wird beendet oder zurückgesetzt, wenn ein Byte mit Daten erfolgreich übertragen wird.

- Wenn das Timeout Intervall "kein Status" den Timeout *Wert*überschreitet, wird der Auftrag in einen schwerwiegenden Fehlerzustand versetzt.

## <a name="examples"></a>Beispiele

Legen Sie für den Auftrag *mydownloadjob*Folgendes fest, um den Timeout Wert "kein Fortschritt" auf 20 Sekunden festzulegen:

```
bitsadmin /setnoprogresstimeout myDownloadJob 20
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
