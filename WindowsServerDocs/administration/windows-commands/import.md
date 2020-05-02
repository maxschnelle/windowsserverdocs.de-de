---
title: Import
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7bd78d76-0560-4d47-944c-fe960be2c10b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 72cbd6195de64a6a0a7f2c258e19b2d5eb1378b1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724854"
---
# <a name="import"></a>Import



Importiert eine austauschen-Schatten Kopie aus einer geladenen Metadatendatei in das System.



## <a name="syntax"></a>Syntax

```
import
```

## <a name="remarks"></a>Bemerkungen

-   Transportable-Schatten Kopien werden nicht sofort im System gespeichert. Die Details werden in einer XML-Datei des Sicherungs Komponenten Dokuments gespeichert, die von DiskShadow automatisch in einer CAB-Metadatendatei im Arbeitsverzeichnis angefordert und gespeichert wird. Sie können den Pfad und den Namen der Datei mit dem Befehl **Set Metadata (Metadaten festlegen** ) ändern.
-   Bevor Sie den **Import**verwenden können, müssen Sie mithilfe des Befehls " **Metadaten laden** " eine DiskShadow-Metadatendatei laden.

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)