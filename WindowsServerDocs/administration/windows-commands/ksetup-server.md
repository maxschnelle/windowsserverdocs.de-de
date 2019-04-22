---
title: ksetup:server
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3407111-ac92-457f-aa1f-a04fe9109d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f370d4dede278e1facdda829503ea3793502b9e6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814571"
---
# <a name="ksetupserver"></a>ksetup:server



Ermöglicht es Ihnen, geben Sie einen Namen für einen Computer, auf das Windows-Betriebssystem ausgeführt wird, so, dass die Änderungen mithilfe von **Ksetup** aktualisiert, dass den Zielcomputer. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /server <ServerName>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<ServerName>|Den vollständigen Computernamen an, an dem die Konfiguration bereitstellen, z. B. IPops897.corp.contoso.com sein soll.</br>Wenn eine unvollständige vollständig qualifizierte Domänennamen für die Computer angegeben ist, der Befehl schlägt fehl.|

## <a name="remarks"></a>Hinweise

Es gibt keine Möglichkeit, den Namen der Zielserver entfernen; Sie können nur sie zurück an den Namen des lokalen Computers ändern der Standard.

Der Name des Zielservers befindet sich in der Registrierung im **HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\LSA\Kerberos**. Es ist nicht mit gemeldet **Ksetup**.

## <a name="BKMK_Examples"></a>Beispiele für

Stellen Sie Ihre **Ksetup** Konfigurationen, die ab dem die IPops897-Computer, auf die Contoso-Domäne verbunden ist:
```
ksetup /server IPops897.corp.contoso.com
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup](ksetup.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)