---
title: Compact Vdisk
description: Windows-Befehle Topic forcompact Vdisk, wodurch die physische Größe einer dynamisch erweiterbaren virtuellen Festplatten Datei (VHD) reduziert wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 40ca0820-67de-4160-b62a-e9bf63fe2790
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9691be21c188fbc2c3b2e782acde127270decf56
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847423"
---
# <a name="compact-vdisk"></a>Compact Vdisk

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verringert die physische Größe einer dynamisch erweiterbaren virtuellen Festplatten Datei (VHD). Dieser Parameter ist nützlich, da sich dynamisch erweiternde VHDs vergrößern, wenn Sie Dateien hinzufügen, aber Sie reduzieren beim Löschen von Dateien nicht automatisch die Größe.

> [!NOTE]
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2.

## <a name="syntax"></a>Syntax
```
compact vdisk
```

## <a name="remarks"></a>Hinweise

- Eine dynamisch erweiterbare virtuelle Festplatte muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl **Vdisk auswählen** eine VHD aus, und verschieben Sie den Fokus darauf.

- Sie können dynamisch erweiterbare VHDs, die getrennt oder als schreibgeschützt angefügt sind, nur komprimieren.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele
Geben Sie Folgendes ein, um eine dynamisch erweiterbare VHD zu komprimieren:
```
compact vdisk
```

## <a name="additional-references"></a>Weitere Verweise
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [Vdisk anfügen](attach-vdisk.md)
- [Detail-Vdisk](detail-vdisk.md)
- [Vdisk trennen](detach-vdisk.md)
- [Erweitern von Vdisk](expand-vdisk.md)
- [Vdisk zusammenführen](merge-vdisk.md)
- [Vdisk auswählen](select-vdisk.md)
- [list_1](list_1.md)
