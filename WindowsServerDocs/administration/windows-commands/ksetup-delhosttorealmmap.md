---
title: 'Ksetup: Delta Host Report Map'
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3faee482-a96c-4614-86fd-aaa446643ec4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 85e9f6b4a9f1c9050ed843f3837a2bd87aaf6eae
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841733"
---
# <a name="ksetupdelhosttorealmmap"></a>Ksetup: Delta Host Report Map



Entfernt die Zuordnung eines Dienst Prinzipal namens (SPN) zwischen dem angegebenen Host und dem Bereich. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /delhosttorealmmap <HostName> <RealmName>
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Hostname >|Der Hostname ist der Computername, und er kann als voll qualifizierter Domänen Name des Computers angegeben werden.|
|\<Realmname >|Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com.|

## <a name="remarks"></a>Hinweise

Wenn eine Zuordnung zwischen Host und Bereich (oder mehreren Hosts zu Bereich) vorhanden ist, wird diese Zuordnung durch diesen Befehl entfernt.

Die Zuordnung wird in der Registrierung in **HKEY_LOCAL_MACHINE \system\currentcontolset\lsa\kerberos\hosttorealm**aufgezeichnet. Sie sollten die Zuordnung in der Registrierung überprüfen, nachdem Sie diesen Befehl verwendet haben.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Wenn Sie die Konfiguration des Bereichs "Configuration Manager" ändern, löschen Sie die Zuordnung des Host Computers IPops897 in den Bereich:
```
ksetup /delhosttorealmmap IPops897 CONTOSO
```
Nachdem Sie diesen Befehl ausgeführt haben, können Sie in der Registrierung überprüfen, ob die Zuordnung beabsichtigt ist.

## <a name="additional-references"></a>Weitere Verweise

-   [Ksetup:addhosttorealmmap](ksetup-addhosttorealmmap.md)
-   [Ksetup](ksetup.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)