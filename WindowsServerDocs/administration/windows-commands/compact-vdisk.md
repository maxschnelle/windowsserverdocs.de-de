---
title: Komprimieren Sie die virtuellen Datenträger
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: c4a95354bf041777e43a9eac5f16e693b02c185c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434304"
---
# <a name="compact-vdisk"></a>Komprimieren Sie die virtuellen Datenträger

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Reduziert die physische Größe einer dynamisch erweiterbaren virtuellen Festplatte (VHD)-Datei. Dieser Parameter ist hilfreich, da Sie dynamisch erweiterbare virtuelle Festplatten Anstieg der Größe, wie Sie Dateien hinzufügen, aber sie nicht automatisch verkleinert werden, werden Wenn Sie Dateien löschen.
> [!NOTE]
> Dieser Befehl gilt nur für Windows 7 und Windows Server 2008 R2 zur Verfügung.
> ## <a name="syntax"></a>Syntax
> ```
> compact vdisk
> ```
> ## <a name="remarks"></a>Hinweise
> - Eine dynamisch erweiterbare virtuellen Festplatte muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt werden. Verwenden der **wählen Vdisk** Befehl aus, um die virtuelle Festplatte auswählen, und verschiebt den Fokus auf sie.
> - Sie können nur komprimiert, dynamisch erweiterbare virtuelle Festplatten, die getrennt oder als schreibgeschützt angefügt werden.
>   ## <a name="BKMK_Examples"></a>Beispiele für
>   Um eine dynamisch erweiterbare virtuelle Festplatte komprimieren möchten, geben Sie Folgendes ein:
>   ```
>   compact vdisk
>   ```
>   ## <a name="additional-references"></a>Zusätzliche Referenzen
> - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
> - [attach vdisk](attach-vdisk.md)

-   [detail vdisk](detail-vdisk.md)
-   [Trennen Sie die virtuellen Datenträger](detach-vdisk.md)
-   [Erweitern Sie die virtuellen Datenträger](expand-vdisk.md)
-   [Zusammenführen von virtuellen Datenträger](merge-vdisk.md)
-   [select vdisk](select-vdisk.md)
-   [list_1](list_1.md)
