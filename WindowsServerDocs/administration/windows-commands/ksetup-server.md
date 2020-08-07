---
title: ksetup server
description: Referenz Artikel für den Befehl "Ksetup Server", mit dem Sie einen Namen für einen Computer angeben können, auf dem das Windows-Betriebssystem ausgeführt wird, sodass die vom Ksetup-Befehl vorgenommenen Änderungen den Zielcomputer aktualisieren.
ms.topic: article
ms.assetid: e3407111-ac92-457f-aa1f-a04fe9109d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2bfa894468ee05b983d8c0122a1738982ef4d909
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887787"
---
# <a name="ksetup-server"></a>ksetup server

Mit dieser Option können Sie einen Namen für einen Computer angeben, auf dem das Windows-Betriebssystem ausgeführt wird, sodass vom **Ksetup** -Befehl vorgenommene Änderungen den Zielcomputer aktualisieren.

Der Name des Zielservers wird in der Registrierung unter gespeichert `HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\LSA\Kerberos` . Dieser Eintrag wird nicht gemeldet, wenn Sie den **Ksetup** -Befehl ausführen.

> [!IMPORTANT]
> Es gibt keine Möglichkeit, den Zielserver Namen zu entfernen. Stattdessen können Sie Sie wieder in den Namen des lokalen Computers ändern. Dies ist die Standardeinstellung.

## <a name="syntax"></a>Syntax

```
ksetup /server <servername>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<servername>` | Gibt den vollständigen Computernamen an, auf dem die Konfiguration wirksam wird, z. b. *IPops897.Corp.contoso.com*.<p>Wenn ein unvollständiger voll qualifizierter Domänen Computername angegeben wird, tritt bei dem Befehl ein Fehler auf. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die **Ksetup** -Konfigurationen auf dem *IPops897* -Computer, der in der Domäne "Configuration Manager" verbunden ist, effektiv zu gestalten:

```
ksetup /server IPops897.corp.contoso.com
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)
