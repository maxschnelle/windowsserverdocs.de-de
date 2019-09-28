---
title: 'Ksetup: Delta Host Report Map'
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 70b54aaebc0b7b46c34c6f52e45f6583afd6c477
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375151"
---
# <a name="ksetupdelhosttorealmmap"></a>Ksetup: Delta Host Report Map



Entfernt die Zuordnung eines Dienst Prinzipal namens (SPN) zwischen dem angegebenen Host und dem Bereich. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /delhosttorealmmap <HostName> <RealmName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<hostname >|Der Hostname ist der Computername, und er kann als voll qualifizierter Domänen Name des Computers angegeben werden.|
|\<realmname >|Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com.|

## <a name="remarks"></a>Hinweise

Wenn eine Zuordnung zwischen Host und Bereich (oder mehreren Hosts zu Bereich) vorhanden ist, wird diese Zuordnung durch diesen Befehl entfernt.

Die Zuordnung wird in der Registrierung in **HKEY_LOCAL_MACHINE\SYSTEM\CurrentContolSet\Lsa\Kerberos\HostToRealm**aufgezeichnet. Sie sollten die Zuordnung in der Registrierung überprüfen, nachdem Sie diesen Befehl verwendet haben.

## <a name="BKMK_Examples"></a>Beispiele

Wenn Sie die Konfiguration des Bereichs "Configuration Manager" ändern, löschen Sie die Zuordnung des Host Computers IPops897 in den Bereich:
```
ksetup /delhosttorealmmap IPops897 CONTOSO
```
Nachdem Sie diesen Befehl ausgeführt haben, können Sie in der Registrierung überprüfen, ob die Zuordnung beabsichtigt ist.

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)