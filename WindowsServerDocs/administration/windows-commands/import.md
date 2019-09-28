---
title: Importieren
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7bd78d76-0560-4d47-944c-fe960be2c10b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 50a095c323806dd523994c36c5b427d4ecedf8ef
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375501"
---
# <a name="import"></a>Importieren



importiert eine austauschen-Schatten Kopie aus einer geladenen Metadatendatei in das System.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
import
```

## <a name="remarks"></a>Hinweise

-   Transportable-Schatten Kopien werden nicht sofort im System gespeichert. Die Details werden in einer XML-Datei des Sicherungs Komponenten Dokuments gespeichert, die von DiskShadow automatisch in einer CAB-Metadatendatei im Arbeitsverzeichnis angefordert und gespeichert wird. Sie können den Pfad und den Namen der Datei mit dem Befehl **Set Metadata (Metadaten festlegen** ) ändern.
-   Bevor Sie den **Import**verwenden können, müssen Sie mithilfe des Befehls " **Metadaten laden** " eine DiskShadow-Metadatendatei laden.

## <a name="BKMK_examples"></a>Beispiele

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

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)