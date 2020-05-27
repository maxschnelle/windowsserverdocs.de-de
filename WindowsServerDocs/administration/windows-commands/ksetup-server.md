---
title: Ksetup-Server
description: Referenz Thema für den Befehl "Ksetup Server", mit dem Sie einen Namen für einen Computer angeben können, auf dem das Windows-Betriebssystem ausgeführt wird, sodass die vom Ksetup-Befehl vorgenommenen Änderungen den Zielcomputer aktualisieren.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e3407111-ac92-457f-aa1f-a04fe9109d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e39a3fbef4b99848d2a90c81007c526597c77275
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817520"
---
# <a name="ksetup-server"></a>Ksetup-Server

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)
