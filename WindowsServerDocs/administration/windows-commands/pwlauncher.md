---
title: pwlauncher
description: Referenz Artikel für den pwlauncher-Befehl, der die Windows to go-Startoptionen (pwlauncher) aktiviert oder deaktiviert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0917bb7b-408a-40f7-a1c5-20e94c10d38b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 29e7434731bc89dff9bddbaedb8a6179f266fa28
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936700"
---
# <a name="pwlauncher"></a>pwlauncher

Aktiviert oder deaktiviert die Windows to go-Startoptionen (pwlauncher). Mit dem Befehlszeilen Tool " **pwlauncher** " können Sie den Computer so konfigurieren, dass er automatisch in einen Windows to go-Arbeitsbereich gestartet wird (sofern vorhanden), ohne dass Sie die Firmware eingeben oder die Startoptionen ändern müssen.

Mithilfe von Windows to go-Startoptionen kann ein Benutzer Ihren Computer so konfigurieren, dass er von Windows aus in Windows gestartet wird, ohne jemals seine Firmware einzugeben, solange die Firmware das Starten von USB unterstützt. Das Aktivieren eines Systems für den immer ersten Start über USB hat Auswirkungen auf Sie. Beispielsweise könnte ein USB-Gerät, das Schadsoftware enthält, versehentlich gestartet werden, um das System zu kompromittieren, oder es können mehrere USB-Laufwerke angeschlossen werden, um einen Start Konflikt auszulösen. Aus diesem Grund werden die Windows to go-Startoptionen in der Standardkonfiguration standardmäßig deaktiviert. Außerdem sind Administratorrechte erforderlich, um die Windows to go-Startoptionen zu konfigurieren. Wenn Sie die Windows to go-Startoptionen mithilfe des Befehlszeilen Tools pwlauncher oder der APP **Windows to go Startup Options** aktivieren, versucht der Computer, von einem beliebigen USB-Gerät zu starten, das vor dem Start in den Computer eingefügt wurde.

## <a name="syntax"></a>Syntax

```
pwlauncher {/enable | /disable}
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| /enable | Aktiviert die Windows to go-Startoptionen, sodass der Computer automatisch von einem USB-Gerät gestartet wird, wenn es vorhanden ist. |
| /Disable | Deaktiviert die Windows to go-Startoptionen, sodass der Computer nicht von einem USB-Gerät gestartet werden kann, es sei denn, er ist manuell in der Firmware konfiguriert. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

So aktivieren Sie den Start über USB:

```
pwlauncher /enable
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
