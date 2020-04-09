---
title: biout admin GetPriority
description: Windows-Befehls Thema für **bigsadmin GetPriority**, das die Priorität des angegebenen Auftrags abruft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: b27829a0fb852abb88c88a65e61e8d7693ca2df2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850543"
---
# <a name="bitsadmin-getpriority"></a>biout admin GetPriority

Ruft die Priorität des angegebenen Auftrags ab.

## <a name="syntax"></a>Syntax

```
bitsadmin /getpriority <job>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| -------------- | -------------- |
| Auftrag | Der Anzeige Name oder GUID des Auftrags. |

## <a name="remarks"></a>Hinweise

Die Priorität für diesen Befehl kann wie folgt lauten:

- **Grundes**

- **Hochrangiger**

- **Normaler**

- **Preis**

- **Unbekannter**

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Im folgenden Beispiel wird die Priorität für den Auftrag mit dem Namen " *mydownloadjob*" abgerufen.

```
C:\>bitsadmin /getpriority myDownloadJob
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
