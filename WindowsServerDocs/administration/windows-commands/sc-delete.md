---
title: sc.exe löschen
description: Referenz Artikel für den sc.exe DELETE-Befehl, mit dem ein Dienst Unterschlüssel aus der Registrierung gelöscht wird.
ms.topic: reference
ms.assetid: 2fe94fb3-e4d1-47b5-b999-39995ecbb644
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 12c09bd72259a8e4b58f134ca19f1fc825f2f1bb
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388461"
---
# <a name="scexe-delete"></a>sc.exe löschen

Löscht einen Dienst Unterschlüssel aus der Registrierung. Wenn der Dienst ausgeführt wird oder wenn ein anderer Prozess über ein geöffnetes Handle für den Dienst verfügt, wird der Dienst zum Löschen markiert.

> [!NOTE]
> Es wird nicht empfohlen, diesen Befehl zu verwenden, um integrierte Betriebssystem Dienste wie DHCP, DNS oder Internetinformationsdienste zu löschen. Informationen zum Installieren, entfernen oder Neukonfigurieren von Betriebssystem Rollen,-Diensten und-Komponenten finden Sie unter [installieren oder Deinstallieren von Rollen, Rollen Diensten oder Features](/WindowsServerDocs/administration/server-manager/install-or-uninstall-roles-role-services-or-features.md) .

## <a name="syntax"></a>Syntax

```
sc.exe [<servername>] delete [<servicename>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<servername>` | Gibt den Namen des Remote Servers an, auf dem sich der Dienst befindet. Der Name muss das Universal Naming Convention (UNC)-Format (z. b \\ . MyServer) verwenden. Verwenden Sie diesen Parameter nicht, um SC.exe lokal auszuführen. |
| `<servicename>` | Gibt den Dienstnamen an, der vom **getkeyname** -Vorgang zurückgegeben wird. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="examples"></a>Beispiele

Um den Dienst Unterschlüssel **newserv** aus der Registrierung auf dem lokalen Computer zu löschen, geben Sie Folgendes ein:

```
sc.exe delete NewServ
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
