---
title: Erweitern von Vdisk
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3ae547b4-3813-4b86-bacd-bc273c028a2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8fb5d7b58b7aa4bc9557086c73020820cfa04284
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377292"
---
# <a name="expand-vdisk"></a>Erweitern von Vdisk

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

erweitert eine virtuelle Festplatte (VHD) auf die Größe, die Sie angeben.
> [!NOTE]
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2.
> ## <a name="syntax"></a>Syntax
> ```
> expand vdisk maximum=<n>
> ```
> ## <a name="parameters"></a>Parameter
> 
> |  Parameter  |                      Beschreibung                      |
> |-------------|-------------------------------------------------------|
> | Maximum = <n> | Gibt die neue Größe für die VHD in Megabyte (MB) an. |
> 
> ## <a name="remarks"></a>Hinweise
> - Es muss eine VHD ausgewählt und getrennt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Vdisk auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.
>   ## <a name="BKMK_Examples"></a>Beispiele
>   Geben Sie Folgendes ein, um die ausgewählte VHD auf 20 GB zu erweitern:
>   ```
>   expand vdisk maximum=20000
>   ```
>   ## <a name="additional-references"></a>Weitere Verweise
> - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
> - [Vdisk anfügen](attach-vdisk.md)
> - [Compact Vdisk](compact-vdisk.md)

-   [Vdisk trennen](detach-vdisk.md)
-   [Detail-Vdisk](detail-vdisk.md)
-   [Vdisk zusammenführen](merge-vdisk.md)
-   [Vdisk auswählen](select-vdisk.md)
-   [list_1](list_1.md)
