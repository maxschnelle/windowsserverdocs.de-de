---
title: autochk
description: Referenz Artikel für den AUTOCHK-Befehl, der ausgeführt wird, wenn der Computer gestartet wird und vor Windows Server gestartet wurde, um die logische Integrität eines Dateisystems zu überprüfen.
ms.topic: article
ms.assetid: 8787e6a3-f023-4ea5-b2d1-61c6876d8aff
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91472aa7447c590aefcb4af58d1951e8e39225fe
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895284"
---
# <a name="autochk"></a>autochk

Wird ausgeführt, wenn der Computer gestartet wird und bevor Windows Server mit der Überprüfung der logischen Integrität eines Dateisystems beginnt.

**Autochk.exe** ist eine Version von **chkdsk** , die nur auf NTFS-Datenträgern und erst vor dem Starten von Windows Server ausgeführt wird. **Autochk** kann nicht direkt über die Befehlszeile ausgeführt werden. **Autochk** wird stattdessen in den folgenden Situationen ausgeführt:

- Wenn Sie versuchen, **chkdsk** auf dem Start Volume auszuführen.

- , Wenn **chkdsk** keine exklusive Verwendung des Volumes erzielen kann.

- , Wenn das Volume als geändert gekennzeichnet ist.

## <a name="remarks"></a>Bemerkungen

> [!WARNING]
> Das Befehlszeilen Tool **Autochk** kann nicht direkt über die Befehlszeile ausgeführt werden. Verwenden Sie stattdessen das **chkntfs** -Befehlszeilen Tool, um die Art und Weise zu konfigurieren, in der **Autochk** beim Start ausgeführt werden soll.
>
> - Sie können **chkntfs** mit dem **/x** -Parameter verwenden, um zu verhindern, dass **Autochk** auf einem bestimmten Volume oder mehreren Volumes ausgeführt wird.
>
> - Verwenden Sie das **chkntfs.exe** -Befehlszeilen Tool mit dem **/t** -Parameter, um die Autochk-Verzögerung von 0 Sekunden in bis zu 3 Tage (259.200 Sekunden) zu ändern. Eine lange Verzögerung bedeutet jedoch, dass der Computer nicht gestartet wird, bis die Zeit abgelaufen ist, oder bis Sie eine Taste drücken, um das **Autochk**abzubrechen.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [chkdsk-Befehl](chkdsk.md)

- [chkntfs-Befehl](chkntfs.md)
