---
title: bitadmin-setpeer-cachingflags
description: Windows-Befehls Thema für **BITSAdmin setpeercachingflags**, mit dem Flags festgelegt werden, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können und ob der Auftrag Inhalt von Peers herunterladen kann.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3f54a127-fb68-49a5-b843-664ec833df67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1b4a7807975fb46440301e30b1fdbd01784d7c85
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122774"
---
# <a name="bitsadmin-setpeercachingflags"></a>bitadmin-setpeer-cachingflags

Legt Flags fest, die bestimmen, ob die Dateien des Auftrags zwischengespeichert und für Peers bereitgestellt werden können und ob der Auftrag Inhalt von Peers herunterladen kann.

## <a name="syntax"></a>Syntax

```
bitsadmin /setpeercachingflags <job> <value>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |
| Wert | Eine Ganzzahl ohne Vorzeichen, einschließlich:<ul><li>**1.** der Auftrag kann Inhalt von Peers herunterladen.</li><li>**2.** die Dateien des Auftrags können zwischengespeichert und für Peers bereitgestellt werden.</li></ul> |

## <a name="examples"></a>Beispiele

Im folgenden Beispiel werden Flags für den Auftrag mit dem Namen *mydownloadjob*festgelegt, sodass Inhalt von Peers heruntergeladen werden kann.

```
C:\>bitsadmin /setpeercachingflags myDownloadJob 1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)