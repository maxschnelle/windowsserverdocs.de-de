---
title: pwlauncher
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0917bb7b-408a-40f7-a1c5-20e94c10d38b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0ddda3ab7831643c3c2c096ae87893d97f90155c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722750"
---
# <a name="pwlauncher"></a>pwlauncher



Aktiviert oder deaktiviert die Windows to go-Startoptionen (pwlauncher). Mit dem Befehlszeilen Tool " **pwlauncher** " können Sie den Computer so konfigurieren, dass er automatisch in einen Windows to go-Arbeitsbereich gestartet wird (sofern vorhanden), ohne dass Sie die Firmware eingeben oder die Startoptionen ändern müssen.



## <a name="syntax"></a>Syntax

```
Pwlauncher {/enable | /disable}
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/enable|Ermöglicht Windows to go-Startoptionen, damit der Computer automatisch von einem USB-Gerät gestartet wird, wenn es vorhanden ist.|
|/Disable|Deaktiviert die Windows to go-Startoptionen, sodass der Computer nicht von einem USB-Gerät gestartet werden kann, es sei denn, er ist manuell in der Firmware konfiguriert.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

Die größte Hürde für Benutzer, die Windows to go verwenden möchten, ist der Computer, der über USB gestartet werden soll. Dies erfolgt in der Regel, indem die Firmware eingegeben und verschiedene Konfigurationsoptionen ausprobiert werden, bis der Computer ordnungsgemäß konfiguriert ist. Dies ist für die meisten Benutzer kein einfaches Unterfangen und ist äußerst riskant, da die Firmware Optionen enthält, die ein System unbrauchbar machen können, wenn es falsch verwendet wird. Um dieses Problem zu beheben, beinhalten Windows 8 und spätere Betriebssysteme ein Feature namens Windows to go-Startoptionen, mit dem Benutzer Ihren Computer so konfigurieren können, dass er von Windows aus in Windows gestartet werden kann. Dies ist nicht der Fall, solange die Firmware das Starten von USB unterstützt. Das Aktivieren eines Systems für den immer ersten Start über USB hat Auswirkungen auf Sie. Beispielsweise könnte ein USB-Gerät, das Schadsoftware enthält, versehentlich gestartet werden, um das System zu kompromittieren, oder es können mehrere USB-Laufwerke angeschlossen werden, um einen Start Konflikt auszulösen. Aus diesem Grund werden die Windows to go-Startoptionen in der Standardkonfiguration standardmäßig deaktiviert. Außerdem sind Administratorrechte erforderlich, um die Windows to go-Startoptionen zu konfigurieren. Wenn Sie die Windows to go-Startoptionen mithilfe des Befehlszeilen Tools pwlauncher oder der APP **Windows to go Startup Options** aktivieren, versucht der Computer, von einem beliebigen USB-Gerät zu starten, das vor dem Start in den Computer eingefügt wurde.

## <a name="examples"></a>Beispiele

Zeigt, wie Sie den Befehl " **pwlauncher** " verwenden können, um den Start über USB zu aktivieren:
```
Pwlauncher /enable
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)