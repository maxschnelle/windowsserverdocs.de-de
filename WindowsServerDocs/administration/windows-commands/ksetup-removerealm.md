---
title: Ksetup removerealm
description: Referenz Thema für den Befehl "Ksetup removerealm", mit dem alle Informationen für den angegebenen Bereich aus der Registrierung gelöscht werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 39f0c6f0-4c50-4781-941e-0893495405e8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5da1be77a3b585e566bfd3b051b2fb391b326f32
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817610"
---
# <a name="ksetup-removerealm"></a>Ksetup removerealm

Löscht alle Informationen für den angegebenen Bereich aus der Registrierung.

Der Bereichs Name wird in der Registrierung unter `HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001` und gespeichert `\CurrentControlSet\Control\Lsa\Kerberos` . Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Sie können den Befehl " [Ksetup adressalmflags](ksetup-addrealmflags.md) " verwenden, um die Registrierung aufzufüllen.

> [!IMPORTANT]
> Der Standard Bereichs Name kann nicht vom Domänen Controller entfernt werden, da dadurch seine DNS-Informationen zurückgesetzt werden, und durch das Entfernen kann der Domänen Controller unbrauchbar werden.

## <a name="syntax"></a>Syntax

```
ksetup /removerealm <realmname>
```
### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<realmname>` | Gibt den Großbuchstaben-DNS-Namen an, z. b. Corp. CONTOSO.com, und wird als Standardbereich bzw. **Bereich** angezeigt, wenn **Ksetup** ausgeführt wird. |

### <a name="examples"></a>Beispiele

Zum Entfernen eines fehlerhaften Bereichs namens (. CON anstelle von. com) geben Sie auf dem lokalen Computer Folgendes ein:
```
ksetup /removerealm CORP.CONTOSO.CON
```

Zum Überprüfen des Entfernens können Sie den **Ksetup** -Befehl ausführen und die Ausgabe überprüfen.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup setrealm-Befehl](ksetup-setrealm.md)
