---
title: autochk
description: Windows-Befehls Thema für **Autochk**, das beim Starten des Computers und vor Windows Server ausgeführt wird, um die logische Integrität eines Dateisystems zu überprüfen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8787e6a3-f023-4ea5-b2d1-61c6876d8aff
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 30ccdbb6aad6e116988ae9c782e3ff359642453e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851123"
---
# <a name="autochk"></a>autochk

Wird ausgeführt, wenn der Computer gestartet wird und bevor Windows Server&reg; 2008 R2 mit der Überprüfung der logischen Integrität eines Dateisystems beginnt.

**Autochk. exe** ist eine Version von **chkdsk** , die nur auf NTFS-Datenträgern und erst vor dem Start von Windows Server 2008 R2 ausgeführt wird. **Autochk** kann nicht direkt über die Befehlszeile ausgeführt werden. **Autochk** wird stattdessen in den folgenden Situationen ausgeführt:

- Wenn Sie versuchen, **chkdsk** auf dem Start Volume auszuführen.

- , Wenn **chkdsk** keine exklusive Verwendung des Volumes erzielen kann.

- , Wenn das Volume als geändert gekennzeichnet ist.

## <a name="remarks"></a>Hinweise

> [!WARNING]
> Das Befehlszeilen Tool **Autochk** kann nicht direkt über die Befehlszeile ausgeführt werden. Verwenden Sie stattdessen das **chkntfs** -Befehlszeilen Tool, um die Art und Weise zu konfigurieren, in der **Autochk** beim Start ausgeführt werden soll.
> -  Sie können **chkntfs** mit dem **/x** -Parameter verwenden, um zu verhindern, dass **Autochk** auf einem bestimmten Volume oder mehreren Volumes ausgeführt wird.
>
> - Verwenden Sie das Befehlszeilen Tool **Chkntfs. exe** mit dem **/t** -Parameter, um die Autochk-Verzögerung von 0 Sekunden in bis zu 3 Tage (259.200 Sekunden) zu ändern. Eine lange Verzögerung bedeutet jedoch, dass der Computer nicht gestartet wird, bis die Zeit abgelaufen ist, oder bis Sie eine Taste drücken, um das **Autochk**abzubrechen.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [CHKDSK](chkdsk.md)

- [Chkntfs](chkntfs.md)

- [Problembehandlung bei Datenträgern und Dateisystemen](https://go.microsoft.com/fwlink/?LinkId=4527)