---
title: hinzufügen
description: 'Windows-Befehls Thema für **add_1** : fügt Volumes zu dem Satz von Volumes hinzu, die als Schatten kopiert werden sollen, oder fügt Aliase zur Alias Umgebung hinzu.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47efce7a-86d2-4872-ae31-baa108757afd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d1aaa211938d14a0019d29e64867f4df2475a877
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382783"
---
# <a name="add"></a>hinzufügen


Fügt Volumes zu dem Satz von Volumes hinzu, die als Schatten kopiert werden sollen, oder fügt der Alias Umgebung Aliase hinzu. Bei Verwendung ohne Unterbefehle listet **Add** die aktuellen Volumes und Aliase auf.

> [!NOTE]
> Aliase werden erst zur Alias Umgebung hinzugefügt, wenn die Schatten Kopie erstellt wird. Aliase, die Sie sofort benötigen, sollten mit **Add-Alias**hinzugefügt werden.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
add 
add volume <Volume> [provider <ProviderID>] 
add alias <AliasName> <AliasValue>
```

## <a name="add-subcommands"></a>Unterbefehle hinzufügen

|Unterbefehl|Beschreibung|
|----------|-----------|
|Volume|Fügt ein Volume zum Schattenkopiesatz hinzu. Dies ist der Satz von Volumes, auf die Schatten kopiert werden soll. Syntax und Parameter finden [Sie unter Volume hinzufügen](add-volume.md) .|
|alias|Fügt der Alias Umgebung den angegebenen Namen und Wert hinzu. Informationen finden [Sie unter Add-Alias](add-alias.md) für Syntax und Parameter.|
|/?|Zeigt die Hilfe in der Befehlszeile an.|

## <a name="BKMK_examples"></a>Beispiele

Zum Anzeigen der hinzugefügten Volumes und der Aliase, die sich derzeit in der Umgebung befinden, geben Sie Folgendes ein:
```
add
```
Die folgende Ausgabe zeigt, dass Laufwerk C dem Schattenkopiesatz hinzugefügt wurde:
```
Volume c: alias System1    GUID \\?\Volume{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}\
1 volume in Shadow Copy Set.
No Diskshadow aliases in the environment.
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)