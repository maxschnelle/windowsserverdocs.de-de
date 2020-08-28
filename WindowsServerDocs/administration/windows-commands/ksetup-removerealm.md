---
title: ksetup removerealm
description: Referenz Artikel für den Befehl "Ksetup removerealm", mit dem alle Informationen für den angegebenen Bereich aus der Registrierung gelöscht werden.
ms.topic: reference
ms.assetid: 39f0c6f0-4c50-4781-941e-0893495405e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 801ef79449cabed4718e417cac9aba9173dd07fb
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89025454"
---
# <a name="ksetup-removerealm"></a>ksetup removerealm

Löscht alle Informationen für den angegebenen Bereich aus der Registrierung.

Der Bereichs Name wird in der Registrierung unter `HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001` und gespeichert `\CurrentControlSet\Control\Lsa\Kerberos` . Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Sie können den Befehl " [Ksetup adressalmflags](ksetup-addrealmflags.md) " verwenden, um die Registrierung aufzufüllen.

> [!IMPORTANT]
> Der Standard Bereichs Name kann nicht vom Domänen Controller entfernt werden, da dadurch seine DNS-Informationen zurückgesetzt werden, und durch das Entfernen kann der Domänen Controller unbrauchbar werden.

## <a name="syntax"></a>Syntax

```
ksetup /removerealm <realmname>
```
### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<realmname>` | Gibt den Großbuchstaben-DNS-Namen an, z. b. Corp. CONTOSO.com, und wird als Standardbereich bzw. **Bereich** angezeigt, wenn **Ksetup** ausgeführt wird. |

### <a name="examples"></a>Beispiele

Zum Entfernen eines fehlerhaften Bereichs namens (. CON anstelle von. com) geben Sie auf dem lokalen Computer Folgendes ein:
```
ksetup /removerealm CORP.CONTOSO.CON
```

Zum Überprüfen des Entfernens können Sie den **Ksetup** -Befehl ausführen und die Ausgabe überprüfen.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup setrealm-Befehl](ksetup-setrealm.md)
