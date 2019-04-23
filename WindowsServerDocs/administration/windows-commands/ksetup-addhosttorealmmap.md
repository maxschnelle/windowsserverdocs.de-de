---
title: ksetup:addhosttorealmmap
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 237742d5-fa68-466c-b97e-636f489248ea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 25cf258309c94f0efde980018dd5dcf3c7df4d60
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837501"
---
# <a name="ksetupaddhosttorealmmap"></a>ksetup:addhosttorealmmap



Fügt eine Dienst-Dienstprinzipalnamen (SPN)-Zuordnung zwischen dem angegebenen Host und dem Bereich hinzu. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /addhosttorealmmap <HostName> <RealmName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<HostName>|Der Hostname ist der Computername, und es kann als vollqualifizierten Domänennamen des Computers angegeben werden.|
|\<RealmName>|Der Bereichsname ist als Großbuchstaben DNS-Name, wie z. B. CORP. angegeben. "CONTOSO.COM".|

## <a name="remarks"></a>Hinweise

Mit diesem Befehl können Sie ordnen Sie einen Host oder mehrere Hosts, die das gleiche DNS-Suffix in den Bereich gemeinsam nutzen.

Die Zuordnung wird in der Registrierung aufgezeichnet **HKEY_LOCAL_MACHINE\SYSTEM\CurrentContolSet\Lsa\Kerberos\HostToRealm**.

## <a name="BKMK_Examples"></a>Beispiele für

Ordnen Sie den Hostcomputer IPops897 als Teil der Konfiguration von des CONTOSO-Bereichs in den Bereich:
```
ksetup /addhosttorealmmap IPops897 CONTOSO
```
In der Registrierung überprüfen, ob die Zuordnung ist wie vorgesehen.

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup:delhosttorealmmap](ksetup-delhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)