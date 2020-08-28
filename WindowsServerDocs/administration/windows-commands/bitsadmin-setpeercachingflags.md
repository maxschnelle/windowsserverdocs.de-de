---
title: bitsadmin setpeercachingflags
description: Referenz Artikel für den BITSAdmin setpeercachingflags-Befehl, mit dem Flags festgelegt werden, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können und ob der Auftrag Inhalt von Peers herunterladen kann.
ms.topic: reference
ms.assetid: 3f54a127-fb68-49a5-b843-664ec833df67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1305d8d865f51556f4b518c7972eaff4ca9ec3e5
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89026208"
---
# <a name="bitsadmin-setpeercachingflags"></a>bitsadmin setpeercachingflags

Legt Flags fest, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können und ob der Auftrag Inhalt von Peers herunterladen kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /setpeercachingflags <job> <value>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| value | Eine Ganzzahl ohne Vorzeichen, einschließlich:<ul><li>**1.** der Auftrag kann Inhalt von Peers herunterladen.</li><li>**2.** die Dateien des Auftrags können zwischengespeichert und für Peers bereitgestellt werden.</li></ul> |

## <a name="examples"></a>Beispiele

So lassen Sie zu, dass der Auftrag mit dem Namen *mydownloadjob* Inhalt von Peers herunterlädt:

```
bitsadmin /setpeercachingflags myDownloadJob 1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Bider admin-Befehl](bitsadmin.md)
