---
title: bitsadmin setpeercachingflags
description: Referenz Artikel für den BITSAdmin setpeercachingflags-Befehl, mit dem Flags festgelegt werden, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können und ob der Auftrag Inhalt von Peers herunterladen kann.
ms.topic: article
ms.assetid: 3f54a127-fb68-49a5-b843-664ec833df67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 73135ed6f08962cbe73aad4765dc4d3b4f7ff958
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87892980"
---
# <a name="bitsadmin-setpeercachingflags"></a>bitsadmin setpeercachingflags

Legt Flags fest, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können und ob der Auftrag Inhalt von Peers herunterladen kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /setpeercachingflags <job> <value>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
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
