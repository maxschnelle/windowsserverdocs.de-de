---
title: ksetup setcomputerpassword
description: Referenz Artikel für den Ksetup-Befehl setcomputerpassword, mit dem das Kennwort für den lokalen Computer festgelegt wird.
ms.topic: article
ms.assetid: e307d8f6-3b93-4c24-ac04-f31549f7dc7d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8d9dba34490616b07671ada16e0c76f0122c3d6a
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887776"
---
# <a name="ksetup-setcomputerpassword"></a>ksetup setcomputerpassword

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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)
