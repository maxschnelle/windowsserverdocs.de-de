---
title: secedit:validate
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9fb06354-f55a-4ca4-9fbc-9a872eb9b9cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cca64f6b2904ed11f6b45e316c8e4da0093c373e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877911"
---
# <a name="seceditvalidate"></a>secedit:validate



Überprüft die Sicherheitseinstellungen, die in eine Sicherheitsvorlage (INF-Datei) gespeichert. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
Secedit /validate <configuration file name>  

```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Konfigurationsdateiname|Erforderlich.</br>Gibt an, der Pfad und Dateiname für die Sicherheitsvorlage, die überprüft werden.|

## <a name="remarks"></a>Hinweise

Überprüfen von Sicherheitsvorlagen kann Ihnen helfen, beschädigt oder nicht ordnungsgemäß festgelegt ist.

Eine Ungültiger Sicherheitsvorlage wird nicht angewendet werden.

Die Protokolldatei wird nicht aktualisiert werden.

In Windows Server 2008 `Secedit /refreshpolicy` wurde durch ersetzt `gpupdate`. Informationen zum Aktualisieren von Sicherheitseinstellungen, finden Sie unter [Gpupdate](gpupdate.md).

## <a name="BKMK_Examples"></a>Beispiele für

Nachdem ein Rollback für eine Sicherheitsvorlage ausgeführt wird, möchten Sie überprüfen, ob die Rollback-inf-Datei, die secRBKcontoso.inf, gültig ist.
```
Secedit /validate secRBKcontoso.inf
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Secedit:generaterollback](secedit-generaterollback.md)
-   [Secedit](secedit.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)