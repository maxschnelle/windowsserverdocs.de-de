---
title: change logon
description: Referenz Artikel zum Ändern des Anmelde Befehls, mit dem Anmeldungen von Client Sitzungen aktiviert oder deaktiviert werden oder der aktuelle Anmeldestatus angezeigt wird.
ms.topic: article
ms.assetid: 41466260-aee9-4333-bcb6-178112c22afd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f1196ec063ce6ab6d2ede64d58d22608e2e76c48
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880276"
---
# <a name="change-logon"></a>change logon

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Aktiviert oder deaktiviert Anmeldungen von Client Sitzungen oder zeigt den aktuellen Anmeldestatus an. Dieses Hilfsprogramm ist für die Systemwartung nützlich. Sie müssen ein Administrator sein, um diesen Befehl ausführen zu können.

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

```
change logon {/query | /enable | /disable | /drain | /drainuntilrestart}
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /Query "aus | Zeigt den aktuellen Anmeldestatus an, ob aktiviert oder deaktiviert. |
| /enable | Aktiviert Anmeldungen von Client Sitzungen, jedoch nicht über die-Konsole. |
| /Disable | Deaktiviert nachfolgende Anmeldungen von Client Sitzungen, jedoch nicht über die-Konsole. Wirkt sich nicht auf derzeit angemeldete Benutzer aus. |
| /drain | Deaktiviert Anmeldungen von neuen Client Sitzungen, ermöglicht aber das erneute Herstellen von Verbindungen mit vorhandenen Sitzungen. |
| /drainuntilrestart | Deaktiviert Anmeldungen von neuen Client Sitzungen, bis der Computer neu gestartet wird, ermöglicht aber das erneute Herstellen von Verbindungen mit vorhandenen Sitzungen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Anmeldungen werden erneut aktiviert, wenn Sie das System neu starten.

- Wenn Sie über eine Client Sitzung eine Verbindung mit dem Remotedesktop-Sitzungshost Server hergestellt haben und dann Anmeldungen deaktivieren und abmelden, bevor Sie Anmeldungen erneut aktivieren, können Sie keine Verbindung mit ihrer Sitzung wiederherstellen. Zum erneuten Aktivieren von Anmeldungen aus Client Sitzungen melden Sie sich an der Konsole an.

### <a name="examples"></a>Beispiele

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

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Befehl "ändern"](change.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
