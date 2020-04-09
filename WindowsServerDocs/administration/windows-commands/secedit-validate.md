---
title: 'secedit: Validate'
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9fb06354-f55a-4ca4-9fbc-9a872eb9b9cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b9425f7a1fb821f4ecbaa7c1689c3baabbff6223
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834873"
---
# <a name="seceditvalidate"></a>secedit: Validate



Überprüft die Sicherheitseinstellungen, die in einer Sicherheits Vorlage (INF-Datei) gespeichert sind. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
Secedit /validate <configuration file name>  

```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Name der Konfigurationsdatei|Erforderlich</br>Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die überprüft wird.|

## <a name="remarks"></a>Hinweise

Das Überprüfen von Sicherheits Vorlagen kann Ihnen helfen, wenn eine beschädigte oder nicht ordnungsgemäß festgelegt ist.

Eine ungültige Sicherheits Vorlage wird nicht angewendet.

Die Protokolldatei wird nicht aktualisiert.

In Windows Server 2008 wurde `Secedit /refreshpolicy` durch `gpupdate`ersetzt. Weitere Informationen zum Aktualisieren von Sicherheitseinstellungen finden Sie unter [gpupdate](gpupdate.md).

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Nachdem ein Rollback für eine Sicherheits Vorlage ausgeführt wurde, sollten Sie überprüfen, ob die Rollback-INF-Datei "secrbkconfiguration. inf" gültig ist.
```
Secedit /validate secRBKcontoso.inf
```

## <a name="additional-references"></a>Weitere Verweise

-   [Secedit:generaterollback](secedit-generaterollback.md)
-   [Secedit](secedit.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)