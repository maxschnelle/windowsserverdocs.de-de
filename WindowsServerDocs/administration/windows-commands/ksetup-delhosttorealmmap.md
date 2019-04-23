---
title: ksetup:delhosttorealmmap
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3faee482-a96c-4614-86fd-aaa446643ec4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cf01edc4932fd5ec1cf98043de04286b3a100a34
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882341"
---
# <a name="ksetupdelhosttorealmmap"></a>ksetup:delhosttorealmmap



Entfernt eine Dienst-Dienstprinzipalnamen (SPN)-Zuordnung zwischen dem angegebenen Host und dem Bereich. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /delhosttorealmmap <HostName> <RealmName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<HostName>|Der Hostname ist der Computername, und es kann als vollqualifizierten Domänennamen des Computers angegeben werden.|
|\<RealmName>|Der Bereichsname ist als Großbuchstaben DNS-Name, wie z. B. CORP. angegeben. "CONTOSO.COM".|

## <a name="remarks"></a>Hinweise

Wenn ein Host-Bereich (oder mehrere Hosts und-Bereich) die Zuordnung vorhanden ist, wird der Befehl die Zuordnung entfernt.

Die Zuordnung wird in der Registrierung aufgezeichnet **HKEY_LOCAL_MACHINE\SYSTEM\CurrentContolSet\Lsa\Kerberos\HostToRealm**. Sie sollten überprüfen, ob die Zuordnung in der Registrierung nach dem mit dem folgenden Befehl.

## <a name="BKMK_Examples"></a>Beispiele für

Ändern die Konfiguration des CONTOSO-Bereichs, löschen Sie die Zuordnung des Hostcomputers IPops897 in den Bereich:
```
ksetup /delhosttorealmmap IPops897 CONTOSO
```
Nach der Ausführung dieses Befehls können Sie in der Registrierung überprüfen, ob die Zuordnung wie vorgesehen.

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)