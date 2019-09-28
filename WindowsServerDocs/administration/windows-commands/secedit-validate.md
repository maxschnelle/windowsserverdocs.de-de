---
title: 'secedit: Validate'
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: ece0a0324b77eb4226b679bc29f7bd599f15a120
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371101"
---
# <a name="seceditvalidate"></a>secedit: Validate



Überprüft die Sicherheitseinstellungen, die in einer Sicherheits Vorlage (INF-Datei) gespeichert sind. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
Secedit /validate <configuration file name>  

```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Name der Konfigurationsdatei|Erforderlich.</br>Gibt den Pfad und den Dateinamen für die Sicherheits Vorlage an, die überprüft wird.|

## <a name="remarks"></a>Hinweise

Das Überprüfen von Sicherheits Vorlagen kann Ihnen helfen, wenn eine beschädigte oder nicht ordnungsgemäß festgelegt ist.

Eine ungültige Sicherheits Vorlage wird nicht angewendet.

Die Protokolldatei wird nicht aktualisiert.

In Windows Server 2008 `Secedit /refreshpolicy` wurde durch `gpupdate`ersetzt. Weitere Informationen zum Aktualisieren von Sicherheitseinstellungen finden Sie unter [gpupdate](gpupdate.md).

## <a name="BKMK_Examples"></a>Beispiele

Nachdem ein Rollback für eine Sicherheits Vorlage ausgeführt wurde, sollten Sie überprüfen, ob die Rollback-INF-Datei "secrbkconfiguration. inf" gültig ist.
```
Secedit /validate secRBKcontoso.inf
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Secedit:generaterollback](secedit-generaterollback.md)
-   [Secedit](secedit.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)