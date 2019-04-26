---
title: pwlauncher
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 1aa2e22f74323bb6cabfc644ca67e17a7fcbd3fc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851021"
---
# <a name="pwlauncher"></a>pwlauncher



Aktiviert oder deaktiviert die Windows zu Go-Startoptionen (Pwlauncher). Die **Pwlauncher** -Befehlszeilentool können Sie den Computer in einen Windows To Go-Arbeitsbereich automatisch gestartet wird (sofern eine vorhanden ist), ohne dass Sie die Firmware eingeben oder ändern die Startoptionen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Pwlauncher {/enable | /disable}
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ Enable /|Ermöglicht Windows To Go-Startoptionen, sodass der Computer von einem USB-Gerät aus, wenn er automatisch gestartet wird|
|/ Disable|Deaktiviert die Windows To Go-Startoptionen, damit der Computer kann nicht von einem USB-Gerät gestartet werden, es sei denn, Sie manuell in der Firmware konfiguriert.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Die größte Hürde für einen Benutzer mit Windows To Go arbeiten möchte, erhält ihre Computer über USB gestartet. Dies erfolgt normalerweise durch Eingabe von der Firmware, und versuchen verschiedene Konfigurationsoptionen aus, bis der Computer ordnungsgemäß konfiguriert ist. Dies ist nicht für die meisten Benutzer eine einfache Angelegenheit, und ist sehr gefährlich, da die Firmware Optionen enthält, die ein System unbrauchbar, wenn Sie nicht ordnungsgemäß verwendet werden können. Dieses Problem, das Windows-8and andauernde enthalten höher ein Feature, mit dem Namen "Windows zu Go-Startoptionen? in dem einen Benutzer so konfigurieren Sie ihre Computer Starten von USB-Geräten aus, in Windows, ohne jemals Eingabe der Firmware, solange die Firmware unterstützt von USB-Geräten zu starten. Aktivieren ein System immer über USB gestartet wirkt sich zunächst, die Sie berücksichtigen sollten. Z. B. ein USB-Gerät mit Schadsoftware kann versehentlich gestartet werden, um das System gefährden oder mehrere USB-Laufwerke können dynamisch geladen werden, um einen Start-Konflikt verursachen. Aus diesem Grund ist die Standardkonfiguration der Windows zu Go-Startoptionen in der Standardeinstellung deaktiviert. Darüber hinaus sind Administratorrechte erforderlich, um Windows zu Go-Startoptionen zu konfigurieren. Wenn Sie die Windows To Go-Startoptionen, die mit dem Befehlszeilentool Pwlauncher aktivieren oder die **ändern Windows zu Go-Startoptionen** app, die der Computer, von einem beliebigen USB-Gerät zu starten, die an den Computer angeschlossen ist, bevor es wird versucht gestartet.

## <a name="BKMK_examples"></a>Beispiele für

Das folgende Beispiel zeigt Informationen zur Verwendung der **Pwlauncher** Befehl aus, um den Start über USB zu aktivieren:
```
Pwlauncher /enable
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)