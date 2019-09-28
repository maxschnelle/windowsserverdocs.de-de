---
title: pwlauncher
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0917bb7b-408a-40f7-a1c5-20e94c10d38b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4cf65643e0c5a4b28e06619a8156792b6e5456ea
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371968"
---
# <a name="pwlauncher"></a>pwlauncher



Aktiviert oder deaktiviert die Windows to go-Startoptionen (pwlauncher). Mit dem Befehlszeilen Tool " **pwlauncher** " können Sie den Computer so konfigurieren, dass er automatisch in einen Windows to go-Arbeitsbereich gestartet wird (sofern vorhanden), ohne dass Sie die Firmware eingeben oder die Startoptionen ändern müssen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Pwlauncher {/enable | /disable}
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/enable|Ermöglicht Windows to go-Startoptionen, damit der Computer automatisch von einem USB-Gerät gestartet wird, wenn es vorhanden ist.|
|/Disable|Deaktiviert die Windows to go-Startoptionen, sodass der Computer nicht von einem USB-Gerät gestartet werden kann, es sei denn, er ist manuell in der Firmware konfiguriert.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Die größte Hürde für Benutzer, die Windows to go verwenden möchten, ist der Computer, der über USB gestartet werden soll. Dies erfolgt in der Regel, indem die Firmware eingegeben und verschiedene Konfigurationsoptionen ausprobiert werden, bis der Computer ordnungsgemäß konfiguriert ist. Dies ist für die meisten Benutzer kein einfaches Unterfangen und ist äußerst riskant, da die Firmware Optionen enthält, die ein System unbrauchbar machen können, wenn es falsch verwendet wird. Um dieses Problem zu beheben, beinhalten Windows 8 und spätere Betriebssysteme eine Funktion mit dem Namen "Windows to go-Startoptionen", die es einem Benutzer ermöglicht, den Computer so zu konfigurieren, dass er von Windows aus in Windows gestartet werden kann. Firmware unterstützt das Starten von USB. Das Aktivieren eines Systems für den immer ersten Start über USB hat Auswirkungen auf Sie. Beispielsweise könnte ein USB-Gerät, das Schadsoftware enthält, versehentlich gestartet werden, um das System zu kompromittieren, oder es können mehrere USB-Laufwerke angeschlossen werden, um einen Start Konflikt auszulösen. Aus diesem Grund werden die Windows to go-Startoptionen in der Standardkonfiguration standardmäßig deaktiviert. Außerdem sind Administratorrechte erforderlich, um die Windows to go-Startoptionen zu konfigurieren. Wenn Sie die Windows to go-Startoptionen mithilfe des Befehlszeilen Tools pwlauncher oder der APP **Windows to go Startup Options** aktivieren, versucht der Computer, von einem beliebigen USB-Gerät zu starten, das vor dem Start in den Computer eingefügt wurde.

## <a name="BKMK_examples"></a>Beispiele

Im folgenden Beispiel wird gezeigt, wie Sie den Befehl **pwlauncher** verwenden können, um den Start über USB zu aktivieren:
```
Pwlauncher /enable
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)