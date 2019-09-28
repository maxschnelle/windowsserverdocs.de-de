---
title: Compact Vdisk
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 40ca0820-67de-4160-b62a-e9bf63fe2790
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7efd40fa4b822636eda9f4082b5f561b452d3846
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379299"
---
# <a name="compact-vdisk"></a>Compact Vdisk

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verringert die physische Größe einer dynamisch erweiterbaren virtuellen Festplatten Datei (VHD). Dieser Parameter ist nützlich, da sich dynamisch erweiternde VHDs vergrößern, wenn Sie Dateien hinzufügen, aber Sie reduzieren beim Löschen von Dateien nicht automatisch die Größe.
> [!NOTE]
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2.
> ## <a name="syntax"></a>Syntax
> ```
> compact vdisk
> ```
> ## <a name="remarks"></a>Hinweise
> - Eine dynamisch erweiterbare virtuelle Festplatte muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Wählen Sie mit dem Befehl **Vdisk auswählen** eine VHD aus, und verschieben Sie den Fokus darauf.
> - Sie können dynamisch erweiterbare VHDs, die getrennt oder als schreibgeschützt angefügt sind, nur komprimieren.
>   ## <a name="BKMK_Examples"></a>Beispiele
>   Geben Sie Folgendes ein, um eine dynamisch erweiterbare VHD zu komprimieren:
>   ```
>   compact vdisk
>   ```
>   ## <a name="additional-references"></a>Weitere Verweise
> - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
> - [Vdisk anfügen](attach-vdisk.md)

-   [Detail-Vdisk](detail-vdisk.md)
-   [Vdisk trennen](detach-vdisk.md)
-   [Erweitern von Vdisk](expand-vdisk.md)
-   [Vdisk zusammenführen](merge-vdisk.md)
-   [Vdisk auswählen](select-vdisk.md)
-   [list_1](list_1.md)
