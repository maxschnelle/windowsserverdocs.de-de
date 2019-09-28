---
title: Vdisk zusammenführen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5865bb08-89a3-406c-8328-0ef8868d03e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7023f2a6669ea6f6801e25cbfc87c950ab95a3bc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373732"
---
# <a name="merge-vdisk"></a>Vdisk zusammenführen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Führt eine differenzierende virtuelle Festplatte (VHD) mit der entsprechenden übergeordneten VHD zusammen. Die übergeordnete VHD wird so geändert, dass Sie die Änderungen der differenzierenden VHD einschließt.
> [!NOTE]
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2.
> ## <a name="syntax"></a>Syntax
> ```
> merge vdisk depth=<n>
> ```
> ### <a name="parameters"></a>Parameter
> 
> | Parameter |                                                                                    Beschreibung                                                                                    |
> |-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> | Tiefe = <n> | Gibt die Anzahl der übergeordneten VHD-Dateien an, die zusammengeführt werden sollen. " **Tiefe = 1** " gibt beispielsweise an, dass die differenzierende virtuelle Festplatte mit einer Ebene der differenzierenden Kette zusammengeführt wird. |
> 
> ## <a name="remarks"></a>Hinweise
> - Es muss eine VHD ausgewählt und getrennt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Vdisk auswählen** eine VHD aus, und verschieben Sie den Fokus darauf.
> - Mit diesem Parameter wird die übergeordnete VHD geändert. Folglich sind andere differenzierende VHDs, die vom übergeordneten Element abhängig sind, nicht mehr gültig.
>   ## <a name="BKMK_Examples"></a>Beispiele
>   Geben Sie Folgendes ein, um eine differenzierende VHD mit der übergeordneten VHD zusammenzuführen:
>   ```
>   merge vdisk depth=1
>   ```
>   ## <a name="additional-references"></a>Weitere Verweise
> - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
> - [Vdisk anfügen](attach-vdisk.md)
> - [Compact Vdisk](compact-vdisk.md)

-   [Detail-Vdisk](detail-vdisk.md)
-   [Vdisk trennen](detach-vdisk.md)
-   [Erweitern von Vdisk](expand-vdisk.md)
-   [Vdisk auswählen](select-vdisk.md)
-   [list_1](list_1.md)
