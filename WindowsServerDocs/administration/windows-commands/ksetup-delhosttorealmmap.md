---
title: 'Ksetup: Delta Host Report Map'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3faee482-a96c-4614-86fd-aaa446643ec4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2b6b14785f254a63f0e16fcd16f1cd464a2d69c8
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724694"
---
# <a name="ksetupdelhosttorealmmap"></a>Ksetup: Delta Host Report Map



Entfernt die Zuordnung eines Dienst Prinzipal namens (SPN) zwischen dem angegebenen Host und dem Bereich.

## <a name="syntax"></a>Syntax

```
ksetup /delhosttorealmmap <HostName> <RealmName>
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Hostname>|Der Hostname ist der Computername, und er kann als voll qualifizierter Domänen Name des Computers angegeben werden.|
|\<Realmname->|Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com.|

## <a name="remarks"></a>Bemerkungen

Wenn eine Zuordnung zwischen Host und Bereich (oder mehreren Hosts zu Bereich) vorhanden ist, wird diese Zuordnung durch diesen Befehl entfernt.

Die Zuordnung wird in der Registrierung in **HKEY_LOCAL_MACHINE \system\currentcontolset\lsa\kerberos\hosttorealm**aufgezeichnet. Sie sollten die Zuordnung in der Registrierung überprüfen, nachdem Sie diesen Befehl verwendet haben.

## <a name="examples"></a>Beispiele

Wenn Sie die Konfiguration des Bereichs "Configuration Manager" ändern, löschen Sie die Zuordnung des Host Computers IPops897 in den Bereich:
```
ksetup /delhosttorealmmap IPops897 CONTOSO
```
Nachdem Sie diesen Befehl ausgeführt haben, können Sie in der Registrierung überprüfen, ob die Zuordnung beabsichtigt ist.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)