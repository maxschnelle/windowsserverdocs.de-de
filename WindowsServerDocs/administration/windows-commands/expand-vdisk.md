---
title: Erweitern von Vdisk
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3ae547b4-3813-4b86-bacd-bc273c028a2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 272714372a35f7f205b5a2e70cb2f2669b3a0634
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844893"
---
# <a name="expand-vdisk"></a>Erweitern von Vdisk

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

erweitert eine virtuelle Festplatte (VHD) auf die Größe, die Sie angeben.
> [!NOTE]
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2.
> ## <a name="syntax"></a>Syntax
> ```
> expand vdisk maximum=<n>
> ```
> ### <a name="parameters"></a>Parameter
> 
> |  Parameter  |                      Beschreibung                      |
> |-------------|-------------------------------------------------------|
> | Maximum =<n> | Gibt die neue Größe für die VHD in Megabyte (MB) an. |
> 
> ## <a name="remarks"></a>Hinweise
> - Es muss eine VHD ausgewählt und getrennt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Vdisk auswählen** ein Volume aus, und verschieben Sie den Fokus auf das Volume.
>   ## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele
>   Geben Sie Folgendes ein, um die ausgewählte VHD auf 20 GB zu erweitern:
>   ```
>   expand vdisk maximum=20000
>   ```
>   ## <a name="additional-references"></a>Weitere Verweise
> - - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
> - [Vdisk anfügen](attach-vdisk.md)
> - [Compact Vdisk](compact-vdisk.md)

-   [Vdisk trennen](detach-vdisk.md)
-   [Detail-Vdisk](detail-vdisk.md)
-   [Vdisk zusammenführen](merge-vdisk.md)
-   [Vdisk auswählen](select-vdisk.md)
-   [list_1](list_1.md)
