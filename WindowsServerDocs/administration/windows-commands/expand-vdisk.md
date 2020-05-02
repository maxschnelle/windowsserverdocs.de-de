---
title: Erweitern von Vdisk
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ae547b4-3813-4b86-bacd-bc273c028a2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c2380045de45397888777f58e3420c75bb6915ae
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725694"
---
# <a name="expand-vdisk"></a>Erweitern von Vdisk

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

erweitert eine virtuelle Festplatte (VHD) auf die Größe, die Sie angeben.
> [!NOTE]
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2.
> ## <a name="syntax"></a>Syntax
> ```
> expand vdisk maximum=<n>
> ```
> ### <a name="parameters"></a>Parameter
> 
> |  Parameter  |                      BESCHREIBUNG                      |
> |-------------|-------------------------------------------------------|
> | Maximum =<n> | Gibt die neue Größe für die VHD in Megabyte (MB) an. |
> 
> ## <a name="remarks"></a>Bemerkungen
> - Es muss eine VHD ausgewählt und getrennt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Vdisk auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.
>   ## <a name="examples"></a>Beispiele
>   Geben Sie Folgendes ein, um die ausgewählte VHD auf 20 GB zu erweitern:
>   ```
>   expand vdisk maximum=20000
>   ```
>   ## <a name="additional-references"></a>Zusätzliche Referenzen
> - - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
> - [attach vdisk](attach-vdisk.md)
> - [Compact Vdisk](compact-vdisk.md)

-   [Vdisk trennen](detach-vdisk.md)
-   [Detail-Vdisk](detail-vdisk.md)
-   [Vdisk zusammenführen](merge-vdisk.md)
-   [Vdisk auswählen](select-vdisk.md)
-   [list_1](list_1.md)
