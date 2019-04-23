---
title: hinzufügen
description: Windows-Befehle Thema **add_1** – Hinzufügen von Volumes auf den Satz von Volumes, die zu spiegelnde sind, oder fügt Aliase auf die Alias-Umgebung.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 549c8560774f004a60926ce568c850fd1b71c7f9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889951"
---
# <a name="add"></a>hinzufügen


Hinzufügen von Volumes auf den Satz von Volumes, die zu spiegelnde sind, oder fügt Aliase auf die Alias-Umgebung. Ohne Angabe von Unterbefehle, **hinzufügen** Listet die aktuellen Volumes und Aliase.

> [!NOTE]
> Aliase werden nicht auf die Alias-Umgebung hinzugefügt, bis die Schattenkopie erstellt wird. Aliase, die Sie sofort müssen hinzugefügt werden sollen, mithilfe von **alias hinzufügen**.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
add 
add volume <Volume> [provider <ProviderID>] 
add alias <AliasName> <AliasValue>
```

## <a name="add-subcommands"></a>Hinzufügen von Unterbefehle

|Unterbefehl|Beschreibung|
|----------|-----------|
|Volume|Fügt ein Volume der Schatten kopieren festgelegt wird, wird die Gruppe von Volumes Schattenkopien erstellt werden. Finden Sie unter [Volume hinzufügen](add-volume.md) für die Syntax und Parameter.|
|alias|Fügt dem angegebenen Namen und Wert der Alias-Umgebung an. Finden Sie unter [Add Alias](add-alias.md) für die Syntax und Parameter.|
|/?|Zeigt die Hilfe an der Befehlszeile eingeben.|

## <a name="BKMK_examples"></a>Beispiele für

Um die Volumes hinzugefügt und die Aliase, die derzeit in der Umgebung werden anzuzeigen, geben Sie Folgendes ein:
```
add
```
Die folgende Ausgabe zeigt, dass Laufwerk C festzulegende der Schatten Kopie hinzugefügt wurde:
```
Volume c: alias System1    GUID \\?\Volume{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}\
1 volume in Shadow Copy Set.
No Diskshadow aliases in the environment.
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)