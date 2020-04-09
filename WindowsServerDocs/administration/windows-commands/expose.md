---
title: sichtbar
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9b0a21cf-3bef-4ade-b8f1-ac42f9203947
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55cc7a292b81977a346f3f078a3b5623243ea46c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80844803"
---
# <a name="expose"></a>sichtbar



macht eine persistente Schatten Kopie als Laufwerk Buchstaben, Freigabe oder Einfügepunkt verfügbar.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
expose <ShadowID> {<Drive:> | <Share> | <MountPoint>}
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Shadowid|Gibt die Schatten-ID der Schatten Kopie an, die Sie verfügbar machen möchten.|
|\<Laufwerk: >|Macht die angegebene Schatten Kopie als Laufwerk Buchstaben (z. b. P:) verfügbar.|
|\<Freigabe >|Macht die angegebene Schatten Kopie in einer Freigabe verfügbar (z. b. \\\\*MachineName*\).|
|\<Mountpoint >|Macht die angegebene Schatten Kopie für einen Einstellungspunkt verfügbar (z. b. c:\shadowcopy\).|

## <a name="remarks"></a>Hinweise

-   Anstelle von *shadowid*können Sie einen vorhandenen Alias oder eine Umgebungsvariable verwenden. Verwenden **Sie hinzufügen** ohne Parameter, um vorhandene Aliase anzuzeigen.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um die dem VSS_SHADOW_1-Umgebungsvariable zugeordnete persistente Schatten Kopie als Laufwerk X verfügbar zu machen:
```
expose %vss_shadow_1% x:
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)