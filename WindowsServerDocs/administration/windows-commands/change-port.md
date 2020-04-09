---
title: change port
description: Windows-Befehls Thema für den änderungsport, der die COM-Port Zuordnungen auflistet oder ändert, die mit MS-DOS-Anwendungen kompatibel sind.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3d772c90-e849-4e74-b9ec-b6cae1159336 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 39273382038edb7709f2d99baea8090d71df3a57
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848073"
---
# <a name="change-port"></a>change port

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Listet die COM-Port Zuordnungen auf, die mit MS-DOS-Anwendungen kompatibel sind, oder ändert Sie.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

> [!NOTE]
> In Windows Server 2008 R2 wurde „Terminaldienste“ umbenannt in „Remotedesktopdienste“. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax

```
change port [<PortX>=<PortY| /d <PortX| /query]
```

### <a name="parameters"></a>Parameter


|    Parameter    |              Beschreibung               |
|-----------------|----------------------------------------|
| <PortX>=<PortY> | Ordnet com-<*Portx*-> <*Porty* zu> |
|   /d <PortX>    | Löscht die Zuordnung für com <*Portx*> |
|     /Query "aus      | Zeigt die aktuellen Port Zuordnungen an. |
|       /?        | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="remarks"></a>Hinweise

- Die meisten MS-DOS-Anwendungen unterstützen nur die seriellen Anschlüsse COM1 bis COM4. Der Befehl **Port ändern** ordnet einen seriellen Anschluss einer anderen Portnummer zu, sodass Anwendungen, die High-nummerierte com-Ports nicht unterstützen, auf den seriellen Anschluss zugreifen können. die Neuzuordnung funktioniert nur für die aktuelle Sitzung und wird nicht beibehalten, wenn Sie sich von einer Sitzung abmelden und dann wieder anmelden.

- Verwenden Sie den **änderungsport** ohne Parameter, um die verfügbaren com-Anschlüsse und ihre aktuellen Zuordnungen anzuzeigen.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

- Wenn Sie COM12 COM1 für die Verwendung durch eine MS-DOS-basierte Anwendung zuordnen möchten, geben Sie Folgendes ein:
  ```
  change port com12=com1
  ```
- Geben Sie Folgendes ein, um die aktuellen Port Zuordnungen anzuzeigen:
  ```
  change port /query
  ```

### <a name="additional-references"></a>Weitere Verweise
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [change](change.md)
- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
