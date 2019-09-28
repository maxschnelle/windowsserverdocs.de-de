---
title: 'Ksetup: addhosttorealmmap'
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: e6a28c6001707fac245de7136b5fb5bd38495027
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375647"
---
# <a name="ksetupaddhosttorealmmap"></a>Ksetup: addhosttorealmmap



Fügt eine Zuordnung des Dienst Prinzipal namens (SPN) zwischen dem angegebenen Host und dem Bereich hinzu. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /addhosttorealmmap <HostName> <RealmName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<hostname >|Der Hostname ist der Computername, und er kann als voll qualifizierter Domänen Name des Computers angegeben werden.|
|\<realmname >|Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com.|

## <a name="remarks"></a>Hinweise

Mit diesem Befehl können Sie einen Host oder mehrere Hosts, die das gleiche DNS-Suffix gemeinsam nutzen, dem Bereich zuordnen.

Die Zuordnung wird in der Registrierung in **HKEY_LOCAL_MACHINE\SYSTEM\CurrentContolSet\Lsa\Kerberos\HostToRealm**aufgezeichnet.

## <a name="BKMK_Examples"></a>Beispiele

Ordnen Sie im Rahmen der Konfiguration des Bereichs "Configuration Manager" den Host Computer IPops897 dem Bereich zu:
```
ksetup /addhosttorealmmap IPops897 CONTOSO
```
Überprüfen Sie in der Registrierung, ob die Zuordnung beabsichtigt ist.

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup:delhosttorealmmap](ksetup-delhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)