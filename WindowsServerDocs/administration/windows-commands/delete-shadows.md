---
title: Löschen Sie Schatten
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b0d5414cb5b60face5245d7ea22d66c8629bfcb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873731"
---
# <a name="delete-shadows"></a>Löschen Sie Schatten



Löscht die Schattenkopien.

## <a name="syntax"></a>Syntax

```
delete shadows [all | volume <Volume> | oldest <Volume> | set <SetID> | id <ShadowID> | exposed {<Drive> | <MountPoint>}]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|all|Löscht alle Schattenkopien.|
|Volume \<Volume >|Löscht alle Schattenkopien auf dem angegebenen Volume.|
|älteste \<Volume >|Löscht die älteste Schattenkopie des angegebenen Volumes an.|
|Legen Sie \<SetID >|Löscht die Schattenkopien in die Schatten-kopieren-Satz von der angegebenen ID Sie können einen Alias angeben, indem die **%** symbol, wenn der Alias in der aktuellen Umgebung vorhanden ist.|
|ID \<ShadowID >|Löscht eine Schattenkopie von der angegebenen ID Sie können einen Alias angeben, indem die **%** symbol, wenn der Alias in der aktuellen Umgebung vorhanden ist.|
|verfügbar gemachten {\<Drive > | <MountPoint>}|Löscht die Schattenkopie verfügbar gemacht werden, die zum Zeitpunkt angegebene Laufwerk Laufwerkbuchstabe oder Bereitstellungspunkt an. Geben Sie als c:\mountPoint oder durch den Laufwerksbuchstaben, z. B. p: Bereitstellungspunkten.|

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)