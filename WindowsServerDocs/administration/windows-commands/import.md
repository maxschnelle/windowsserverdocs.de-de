---
title: Importieren von DiskShadow
description: Referenz Artikel für den Import-Befehl, der eine austauschen-Schatten Kopie aus einer geladenen Metadatendatei in das System importiert.
ms.topic: article
ms.assetid: 7bd78d76-0560-4d47-944c-fe960be2c10b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d0d76c9565904d6e24c41f4c728bf43061f5040
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888367"
---
# <a name="import-diskshadow"></a>Importieren (DiskShadow)

Importiert eine austauschen-Schatten Kopie aus einer geladenen Metadatendatei in das System.

> Wichtig Bevor Sie diesen Befehl verwenden können, müssen Sie den [Befehl "Metadaten laden](load-metadata.md) " verwenden, um eine DiskShadow-Metadatendatei zu laden.

## <a name="syntax"></a>Syntax

```
import
```

#### <a name="remarks"></a>Bemerkungen

- Transportable-Schatten Kopien werden nicht sofort im System gespeichert. Die Details werden in einer XML-Datei des Sicherungs Komponenten Dokuments gespeichert, die von DiskShadow automatisch in einer CAB-Metadatendatei im Arbeitsverzeichnis angefordert und gespeichert wird. Verwenden Sie den [Befehl Set Metadata](set-metadata.md) , um den Pfad und den Namen dieser XML-Datei zu ändern.

## <a name="examples"></a>Beispiele

Im folgenden finden Sie ein Beispiel eines DiskShadow-Skripts, das die Verwendung des **Import** -Befehls veranschaulicht:

```
#Sample DiskShadow script demonstrating IMPORT
SET CONTEXT PERSISTENT
SET CONTEXT TRANSPORTABLE
SET METADATA transHWshadow_p.cab
#P: is the volume supported by the Hardware Shadow Copy provider
ADD VOLUME P:
CREATE
END BACKUP
#The (transportable) shadow copy is not in the system yet.
#You can reset or exit now if you wish.

LOAD METADATA transHWshadow_p.cab
IMPORT
#The shadow copy will now be loaded into the system.
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [DiskShadow-Befehl](diskshadow.md)