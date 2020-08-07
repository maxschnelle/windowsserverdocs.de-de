---
title: Sc.exe löschen
description: Weitere Informationen zum Aufheben der Registrierung von Diensten mithilfe des sc.exe Hilfsprogramms
ms.topic: article
ms.assetid: 2fe94fb3-e4d1-47b5-b999-39995ecbb644
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5eb7bdd147d42c5b35106b65c512015526cb80cc
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883267"
---
# <a name="scexe-delete"></a>Sc.exe löschen

Löscht einen Dienst Unterschlüssel aus der Registrierung. Wenn der Dienst ausgeführt wird oder wenn ein anderer Prozess über ein geöffnetes Handle für den Dienst verfügt, wird der Dienst zum Löschen markiert.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
sc.exe [<ServerName>] delete [<ServiceName>]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<ServerName>|Gibt den Namen des Remote Servers an, auf dem sich der Dienst befindet. Der Name muss das Universal Naming Convention (UNC)-Format (z. b \\ \\ . MyServer) verwenden. Wenn Sie SC.exe lokal ausführen möchten, lassen Sie diesen Parameter Weg.|
|\<ServiceName>|Gibt den Dienstnamen an, der vom **getkeyname** -Vorgang zurückgegeben wird.|
|?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

Es wird nicht empfohlen, sc.exe zum Löschen integrierter Betriebssystem Dienste wie DHCP, DNS oder Internetinformationsdienste zu verwenden. Informationen zum Installieren, entfernen oder Neukonfigurieren von Betriebssystem Rollen,-Diensten und-Komponenten finden Sie unter [installieren oder Deinstallieren von Rollen, Rollen Diensten oder Features](/WindowsServerDocs/administration/server-manager/install-or-uninstall-roles-role-services-or-features.md) .

## <a name="examples"></a>Beispiele

Um den Dienst Unterschlüssel **newserv** aus der Registrierung auf dem lokalen Computer zu löschen, geben Sie Folgendes ein:
```
sc.exe delete newserv
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
