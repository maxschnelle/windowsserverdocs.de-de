---
title: change logon
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 41466260-aee9-4333-bcb6-178112c22afd Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c04eaffe366dce079aed53351589c1b5026954e3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379644"
---
>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="change-logon"></a>change logon
Aktiviert oder deaktiviert Anmeldungen von Client Sitzungen oder zeigt den aktuellen Anmeldestatus an.
Dieses Hilfsprogramm ist für die Systemwartung nützlich.
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.
> ## <a name="syntax"></a>Syntax
> ```
> change logon {/query | /enable | /disable | /drain | /drainuntilrestart}
> ```
> ## <a name="parameters"></a>Parameter
> 
> |     Parameter      |                                                       Beschreibung                                                        |
> |--------------------|--------------------------------------------------------------------------------------------------------------------------|
> |       /Query "aus       |                             Zeigt den aktuellen Anmeldestatus an, ob aktiviert oder deaktiviert.                              |
> |      /enable       |                              Aktiviert Anmeldungen von Client Sitzungen, jedoch nicht über die-Konsole.                              |
> |      /Disable      |  Deaktiviert nachfolgende Anmeldungen von Client Sitzungen, jedoch nicht über die-Konsole. Wirkt sich nicht auf derzeit angemeldete Benutzer aus.   |
> |       /drain       |                 Deaktiviert Anmeldungen von neuen Client Sitzungen, ermöglicht aber das erneute Herstellen von Verbindungen mit vorhandenen Sitzungen.                 |
> | /drainuntilrestart | Deaktiviert Anmeldungen von neuen Client Sitzungen, bis der Computer neu gestartet wird, ermöglicht aber das erneute Herstellen von Verbindungen mit vorhandenen Sitzungen. |
> |         /?         |                                           Zeigt die Hilfe an der Eingabeaufforderung an.                                           |
> 
> ## <a name="remarks"></a>Hinweise
> - Nur Administratoren können den Befehl zum **Ändern der Anmeldung** verwenden.
> - Anmeldungen werden erneut aktiviert, wenn Sie das System neu starten. Wenn Sie eine Verbindung mit dem Remotedesktop-Sitzungshost-Server (RD-Sitzungs Host Server) aus einer Client Sitzung hergestellt haben und Anmeldungen deaktivieren und dann abmelden, bevor Sie Anmeldungen erneut aktivieren, können Sie keine erneute Verbindung mit ihrer Sitzung herstellen. Zum erneuten Aktivieren von Anmeldungen aus Client Sitzungen melden Sie sich an der Konsole an.
>   ## <a name="BKMK_examples"></a>Beispiele
> - Geben Sie Folgendes ein, um den aktuellen Anmeldestatus anzuzeigen:
>   ```
>   change logon /query
>   ```
> - Geben Sie Folgendes ein, um Anmeldungen von Client Sitzungen zu aktivieren:
>   ```
>   change logon /enable
>   ```
> - Um Client Anmeldungen zu deaktivieren, geben Sie Folgendes ein:
>   ```
>   change logon /disable
>   ```
>   #### <a name="additional-references"></a>Weitere Verweise
>   [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
>   -[Änderung](change.md)@no__t-[3 &#40;Remotedesktopdienste Befehls&#41; Referenz für Terminal Dienste](remote-desktop-services-terminal-services-command-reference.md)
