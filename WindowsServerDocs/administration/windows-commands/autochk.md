---
title: autochk
description: 'Windows-Befehls Thema für **Autochk** : wird ausgeführt, wenn der Computer gestartet wird und vor Windows Server gestartet wurde, um die logische Integrität eines Dateisystems zu überprüfen.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8787e6a3-f023-4ea5-b2d1-61c6876d8aff
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 76e54d14879cefd4661a1ca7f1c3b8ee7ec58de2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382350"
---
# <a name="autochk"></a>autochk



Wird ausgeführt, wenn der Computer gestartet wird und bevor Windows Server® 2008 R2 mit der Überprüfung der logischen Integrität eines Dateisystems beginnt.

**Autochk. exe** ist eine Version von **chkdsk** , die nur auf NTFS-Datenträgern und erst vor dem Start von Windows Server 2008 R2 ausgeführt wird. **Autochk** kann nicht direkt über die Befehlszeile ausgeführt werden. **Autochk** wird stattdessen in den folgenden Situationen ausgeführt:
-   Wenn Sie versuchen, **chkdsk** auf dem Start Volume auszuführen.
-   Wenn **chkdsk** keine exklusive Verwendung des Volumes erzielen kann
-   Wenn das Volume als geändert gekennzeichnet ist

## <a name="remarks"></a>Hinweise

> -   [!WARNING]
>     Das Befehlszeilen Tool **Autochk** kann nicht direkt über die Befehlszeile ausgeführt werden. Verwenden Sie stattdessen das **chkntfs** -Befehlszeilen Tool, um die Art und Weise zu konfigurieren, in der **Autochk** beim Start ausgeführt werden soll.
> -   Sie können **chkntfs** mit dem **/x** -Parameter verwenden, um zu verhindern, dass **Autochk** auf einem bestimmten Volume oder mehreren Volumes ausgeführt wird.
> -   Verwenden Sie das Befehlszeilen Tool **Chkntfs. exe** mit dem **/t** -Parameter, um die Autochk-Verzögerung von 0 Sekunden in bis zu 3 Tage (259.200 Sekunden) zu ändern. Eine lange Verzögerung bedeutet jedoch, dass der Computer nicht gestartet wird, bis die Zeit abgelaufen ist, oder bis Sie eine Taste drücken, um das **Autochk**abzubrechen.

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

[CHKDSK](chkdsk.md)

[Chkntfs](chkntfs.md)

[Problembehandlung bei Datenträgern und Dateisystemen](https://go.microsoft.com/fwlink/?LinkId=4527)