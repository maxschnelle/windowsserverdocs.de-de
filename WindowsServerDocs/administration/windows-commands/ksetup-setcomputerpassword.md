---
title: Ksetup setcomputerpassword
description: Referenz Thema für den Ksetup-Befehl "setcomputerpassword", mit dem das Kennwort für den lokalen Computer festgelegt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e307d8f6-3b93-4c24-ac04-f31549f7dc7d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1ec410cd85c13cb3a925c3fc65b8c9f86fba606a
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817430"
---
# <a name="ksetup-setcomputerpassword"></a>Ksetup setcomputerpassword

Legt das Kennwort für den lokalen Computer fest. Dieser Befehl wirkt sich nur auf das Computer Konto aus und erfordert einen Neustart, damit die Kenn Wort Änderung wirksam wird.

> [!IMPORTANT]
> Das Computer Konto Kennwort wird nicht in der Registrierung oder als Ausgabe des **Ksetup** -Befehls angezeigt.

## <a name="syntax"></a>Syntax

```
ksetup /setcomputerpassword <password>
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<password>` | Gibt das angegebene Kennwort an, mit dem das Computer Konto auf dem lokalen Computer festgelegt wird. Das Kennwort kann nur mit einem Konto mit Administrator Berechtigungen festgelegt werden, und das Kennwort muss zwischen 1 und 156 alphanumerische Zeichen oder Sonderzeichen enthalten. |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um das Computer Konto Kennwort auf dem lokalen Computer von *IPops897* auf *IPOP $897!* zu ändern:

```
ksetup /setcomputerpassword IPop$897!
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)
