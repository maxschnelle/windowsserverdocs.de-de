---
title: Importieren
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: ddef3958bc431519e3cb89b658a58d1f4dba6938
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835261"
---
# <a name="import"></a>Importieren



importiert eine übertragbarer Schattenkopien aus einer geladenen Metadaten-Datei in das System an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
import
```

## <a name="remarks"></a>Hinweise

-   Übertragbarer Schattenkopien werden nicht sofort auf dem System gespeichert werden. Ihre Details werden in einer XML-Dokument von Backup-Komponenten-Datei gespeichert DiskShadow automatisch angefordert und in einer CAB-Metadatendatei in das Verzeichnis speichert. Sie können ändern, den Pfad und Namen, der diese Datei mit den **resultsetmetadaten** Befehl.
-   Vor der Verwendung **importieren**, müssen Sie eine Datei mit DiskShadow Metadaten laden die **Laden von Metadaten** Befehl.

## <a name="BKMK_examples"></a>Beispiele für

Im folgenden finden Sie ein Beispiel DiskShadow-Skript, das die Verwendung von veranschaulicht die **importieren** Befehl:
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

[Befehlszeilensyntax](command-line-syntax-key.md)