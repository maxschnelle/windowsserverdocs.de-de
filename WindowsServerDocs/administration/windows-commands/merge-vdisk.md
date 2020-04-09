---
title: Vdisk zusammenführen
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5865bb08-89a3-406c-8328-0ef8868d03e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1315b82510ae356f80d5b519c0676d0d156ab9fd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839623"
---
# <a name="merge-vdisk"></a>Vdisk zusammenführen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Führt eine differenzierende virtuelle Festplatte (VHD) mit der entsprechenden übergeordneten VHD zusammen. Die übergeordnete VHD wird so geändert, dass Sie die Änderungen der differenzierenden VHD einschließt.
> [!NOTE]
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2.
> ## <a name="syntax"></a>Syntax
> ```
> merge vdisk depth=<n>
> ```
> #### <a name="parameters"></a>Parameter
> 
> | Parameter |                                                                                    Beschreibung                                                                                    |
> |-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> | Tiefe =<n> | Gibt die Anzahl der übergeordneten VHD-Dateien an, die zusammengeführt werden sollen. " **Tiefe = 1** " gibt beispielsweise an, dass die differenzierende virtuelle Festplatte mit einer Ebene der differenzierenden Kette zusammengeführt wird. |
> 
> ## <a name="remarks"></a>Hinweise
> - Es muss eine VHD ausgewählt und getrennt werden, damit dieser Vorgang erfolgreich ausgeführt werden konnte. Wählen Sie mit dem Befehl **Vdisk auswählen** eine VHD aus, und verschieben Sie den Fokus darauf.
> - Mit diesem Parameter wird die übergeordnete VHD geändert. Folglich sind andere differenzierende VHDs, die vom übergeordneten Element abhängig sind, nicht mehr gültig.
>   ## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele
>   Geben Sie Folgendes ein, um eine differenzierende VHD mit der übergeordneten VHD zusammenzuführen:
>   ```
>   merge vdisk depth=1
>   ```
>   ## <a name="additional-references"></a>Weitere Verweise
> - - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
> - [Vdisk anfügen](attach-vdisk.md)
> - [Compact Vdisk](compact-vdisk.md)

-   [Detail-Vdisk](detail-vdisk.md)
-   [Vdisk trennen](detach-vdisk.md)
-   [Erweitern von Vdisk](expand-vdisk.md)
-   [Vdisk auswählen](select-vdisk.md)
-   [list_1](list_1.md)
