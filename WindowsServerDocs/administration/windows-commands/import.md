---
title: Importieren von DiskShadow
description: Referenz Artikel für den Import-Befehl, der eine austauschen-Schatten Kopie aus einer geladenen Metadatendatei in das System importiert.
ms.topic: reference
ms.assetid: 7bd78d76-0560-4d47-944c-fe960be2c10b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: bf86c069bf0f5de4d6fa773d319bdd75beeb93eb
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634528"
---
# <a name="import-diskshadow"></a>Importieren (DiskShadow)

Importiert eine austauschen-Schatten Kopie aus einer geladenen Metadatendatei in das System.

> Wichtig Bevor Sie diesen Befehl verwenden können, müssen Sie den [Befehl "Metadaten laden](load-metadata.md) " verwenden, um eine DiskShadow-Metadatendatei zu laden.

## <a name="syntax"></a>Syntax

```
import
```

#### <a name="remarks"></a>Hinweise

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