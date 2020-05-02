---
title: 'Ksetup: addhosttorealmmap'
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 237742d5-fa68-466c-b97e-636f489248ea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 732dccc868ca85b108ba443d912788a14dd0e107
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724773"
---
# <a name="ksetupaddhosttorealmmap"></a>Ksetup: addhosttorealmmap



Fügt eine Zuordnung des Dienst Prinzipal namens (SPN) zwischen dem angegebenen Host und dem Bereich hinzu.

## <a name="syntax"></a>Syntax

```
ksetup /addhosttorealmmap <HostName> <RealmName>
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Hostname>|Der Hostname ist der Computername, und er kann als voll qualifizierter Domänen Name des Computers angegeben werden.|
|\<Realmname->|Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com.|

## <a name="remarks"></a>Bemerkungen

Mit diesem Befehl können Sie einen Host oder mehrere Hosts, die das gleiche DNS-Suffix gemeinsam nutzen, dem Bereich zuordnen.

Die Zuordnung wird in der Registrierung in **HKEY_LOCAL_MACHINE \system\currentcontolset\lsa\kerberos\hosttorealm**aufgezeichnet.

## <a name="examples"></a>Beispiele

Ordnen Sie im Rahmen der Konfiguration des Bereichs "Configuration Manager" den Host Computer IPops897 dem Bereich zu:
```
ksetup /addhosttorealmmap IPops897 CONTOSO
```
Überprüfen Sie in der Registrierung, ob die Zuordnung beabsichtigt ist.

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Ksetup:delhosttorealmmap](ksetup-delhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)