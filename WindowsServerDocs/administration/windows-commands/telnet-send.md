---
title: telnet send
description: Referenz Artikel für den Telnet-Befehl "Send", der Telnet-Befehle an den Telnet-Server sendet.
ms.topic: reference
ms.assetid: 7c217abc-1182-466e-914c-1ff16755021b
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: ab6c94f619ab28be7b850479a7e3d476e1394e09
ms.sourcegitcommit: 720455aad2bac78cf64997d196a13f35ea0acb73
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91717987"
---
# <a name="telnet-send"></a>Telnet: senden

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sendet Telnet-Befehle an den Telnet-Server.

## <a name="syntax"></a>Syntax

```
sen {ao | ayt | brk | esc | ip | synch | <string>} [?]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| OS | Sendet die Ausgabe des Telnet-Befehls **abgeb**Rochen. |
| AYT | Wird der Telnet-Befehl gesendet **?** |
| BRK | Sendet den Telnet-Befehl **BRK**. |
| ESC-TASTE | Sendet das aktuelle Telnet-Escapezeichen. |
| ip | Sendet den Telnet-Befehls **Unterbrechungs Prozess**. |
| synch | Sendet den Telnet-Befehl "Synch". |
| `<string>` | Sendet jede Zeichenfolge, die Sie an den Telnet-Server eingeben. |
| ? | Zeigt die diesem Befehl zugeordnete Hilfe an. |

## <a name="example"></a>Beispiel

Geben Sie Folgendes ein, um den Befehl Wenn Sie den Befehl **sind Sie** an den Telnet-Server zu senden:

```
sen ayt
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
