---
title: Import
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7bd78d76-0560-4d47-944c-fe960be2c10b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 07fdd03c73c454e92218a4c6983eac7f29b50883
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842173"
---
# <a name="import"></a>Import



Importiert eine austauschen-Schatten Kopie aus einer geladenen Metadatendatei in das System.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
import
```

## <a name="remarks"></a>Hinweise

-   Transportable-Schatten Kopien werden nicht sofort im System gespeichert. Die Details werden in einer XML-Datei des Sicherungs Komponenten Dokuments gespeichert, die von DiskShadow automatisch in einer CAB-Metadatendatei im Arbeitsverzeichnis angefordert und gespeichert wird. Sie können den Pfad und den Namen der Datei mit dem Befehl **Set Metadata (Metadaten festlegen** ) ändern.
-   Bevor Sie den **Import**verwenden können, müssen Sie mithilfe des Befehls " **Metadaten laden** " eine DiskShadow-Metadatendatei laden.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

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