---
title: autochk
description: Windows-Befehle Thema **Autochk** – ausgeführt wird, wenn der Computer gestartet wird und vor dem Windows Server zu starten, um zu überprüfen, ob die logische Integrität eines Dateisystems.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 023bd81b93106a091fb9f26d97cf7eda75f0f633
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888461"
---
# <a name="autochk"></a>autochk



Wird ausgeführt, wenn der Computer gestartet wird und vor Windows Server® 2008 R2 wird gestartet. Überprüfen Sie, ob die logische Integrität eines Dateisystems.

**Autochk.exe** ist eine Version von **Chkdsk** , die nur auf NTFS-Datenträgern und nur vor dem Starten von Windows Server 2008 R2 ausgeführt wird. **Autochk** kann nicht direkt über die Befehlszeile ausgeführt werden. Stattdessen **Autochk** wird in den folgenden Situationen ausgeführt:
-   Wenn Sie versuchen, führen Sie **Chkdsk** auf dem Startvolume
-   Wenn **Chkdsk** nicht exklusive Verwendung des Volumes zugreifen
-   Wenn das Volume als geändert gekennzeichnet ist

## <a name="remarks"></a>Hinweise

> -   [!WARNING]
>     Die **Autochk** Befehlszeilentool kann nicht direkt über die Befehlszeile ausgeführt werden. Verwenden Sie stattdessen die **Chkntfs** Befehlszeilentool, mit der gewünscht konfigurieren sollen **Autochk** beim Start ausgeführt.
-   Sie können **Chkntfs** mit der **/x** Parameter, um zu verhindern, dass **Autochk** ausgeführt wird, ein bestimmtes Volume oder mehrere Volumes.
-   Verwenden der **Chkntfs.exe** Befehlszeilentool mit der **/t /** Parameter, um die Autochk Verzögerung von 0 Sekunden auf bis zu 3 Tage (259.200 Sekunden) zu ändern. Eine lange Verzögerung bedeutet jedoch, dass der Computer nicht gestartet wird, bis die Zeit abgelaufen ist oder Sie eine Abbrechen-Taste auf **Autochk**.

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)

[Chkdsk](chkdsk.md)

[Chkntfs](chkntfs.md)

[Problembehandlung bei Datenträgern und Dateisystemen](https://go.microsoft.com/fwlink/?LinkId=4527)