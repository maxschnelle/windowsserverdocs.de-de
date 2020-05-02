---
title: sichtbar
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9b0a21cf-3bef-4ade-b8f1-ac42f9203947
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 500dc5cfcd5e2bba4cfbc3cb5ef81a9065ea53cf
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725670"
---
# <a name="expose"></a>sichtbar



Macht eine persistente Schatten Kopie als Laufwerk Buchstaben, Freigabe oder Einfügepunkt verfügbar.



## <a name="syntax"></a>Syntax

```
expose <ShadowID> {<Drive:> | <Share> | <MountPoint>}
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|Shadowid|Gibt die Schatten-ID der Schatten Kopie an, die Sie verfügbar machen möchten.|
|\<Laufwerk: >|Macht die angegebene Schatten Kopie als Laufwerk Buchstaben (z. b. P:) verfügbar.|
|\<Freigabe>|Macht die angegebene Schatten Kopie in einer Freigabe verfügbar \\ \\(z. b. *MachineName*\)).|
|\<Bereitstellungspunkt->|Macht die angegebene Schatten Kopie für einen Einstellungspunkt verfügbar (z. b. "c:\shadowcopy\)".|

## <a name="remarks"></a>Bemerkungen

-   Anstelle von *shadowid*können Sie einen vorhandenen Alias oder eine Umgebungsvariable verwenden. Verwenden **Sie hinzufügen** ohne Parameter, um vorhandene Aliase anzuzeigen.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die dem VSS_SHADOW_1-Umgebungsvariable zugeordnete persistente Schatten Kopie als Laufwerk X verfügbar zu machen:
```
expose %vss_shadow_1% x:
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)