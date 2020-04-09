---
title: change logon
description: Windows-Befehls Artikel zum Ändern der Anmeldung, bei der Anmeldungen von Client Sitzungen aktiviert oder deaktiviert werden oder der aktuelle Anmeldestatus angezeigt wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 41466260-aee9-4333-bcb6-178112c22afd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6a101fc567981716536ecad8e754b81a43eb2c91
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848153"
---
# <a name="change-logon"></a>change logon

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktiviert oder deaktiviert Anmeldungen von Client Sitzungen oder zeigt den aktuellen Anmeldestatus an. Dieses Hilfsprogramm ist für die Systemwartung nützlich.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

> [!NOTE]
> In Windows Server 2008 R2 wurde „Terminaldienste“ umbenannt in „Remotedesktopdienste“. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
change logon {/query | /enable | /disable | /drain | /drainuntilrestart}
```
### <a name="parameters"></a>Parameter

|     Parameter      |                                                       Beschreibung                                                        |
|--------------------|--------------------------------------------------------------------------------------------------------------------------|
|       /Query "aus       |                             Zeigt den aktuellen Anmeldestatus an, ob aktiviert oder deaktiviert.                              |
|      /enable       |                              Aktiviert Anmeldungen von Client Sitzungen, jedoch nicht über die-Konsole.                              |
|      /Disable      |  Deaktiviert nachfolgende Anmeldungen von Client Sitzungen, jedoch nicht über die-Konsole. Wirkt sich nicht auf derzeit angemeldete Benutzer aus.   |
|       /drain       |                 Deaktiviert Anmeldungen von neuen Client Sitzungen, ermöglicht aber das erneute Herstellen von Verbindungen mit vorhandenen Sitzungen.                 |
| /drainuntilrestart | Deaktiviert Anmeldungen von neuen Client Sitzungen, bis der Computer neu gestartet wird, ermöglicht aber das erneute Herstellen von Verbindungen mit vorhandenen Sitzungen. |
|         /?         |                                           Zeigt die Hilfe an der Eingabeaufforderung an.                                           |

## <a name="remarks"></a>Hinweise
- Nur Administratoren können den Befehl zum **Ändern der Anmeldung** verwenden.
- Anmeldungen werden erneut aktiviert, wenn Sie das System neu starten. Wenn Sie eine Verbindung mit dem Remotedesktop-Sitzungshost-Server (RD-Sitzungs Host Server) aus einer Client Sitzung hergestellt haben und Anmeldungen deaktivieren und dann abmelden, bevor Sie Anmeldungen erneut aktivieren, können Sie keine erneute Verbindung mit ihrer Sitzung herstellen. Zum erneuten Aktivieren von Anmeldungen aus Client Sitzungen melden Sie sich an der Konsole an.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

- Geben Sie Folgendes ein, um den aktuellen Anmeldestatus anzuzeigen:
  ```
  change logon /query
  ```
- Geben Sie Folgendes ein, um Anmeldungen von Client Sitzungen zu aktivieren:
  ```
  change logon /enable
  ```
- Um Client Anmeldungen zu deaktivieren, geben Sie Folgendes ein:
  ```
  change logon /disable
  ```
  
## <a name="additional-references"></a>Weitere Verweise
- - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
- [change](change.md)
- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
