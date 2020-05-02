---
title: change (Ändern)
description: Referenz Thema für den Change-Befehl, mit dem Remotedesktop-Sitzungshost Servereinstellungen für Anmeldungen, com-Port Zuordnungen und Installationsmodus geändert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90012116-0fb3-4f34-a819-cf4d4b4f8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a35bd558898b3991a9e6f847d415a67d70f0d01b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82715513"
---
# <a name="change"></a>change (Ändern)

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert Remotedesktop-Sitzungshost Servereinstellungen für Anmeldungen, com-Port Zuordnungen und Installationsmodus.

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11)).

## <a name="syntax"></a>Syntax

 ```
 change logon
 change port
 change user
 ```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| [Anmelde Befehl ändern](change-logon.md) | Aktiviert oder deaktiviert Anmeldungen von Client Sitzungen auf einem Remotedesktop-Sitzungshost Server oder zeigt den aktuellen Anmeldestatus an. |
| [Befehl "Port ändern"](change-port.md) | Listet die COM-Port Zuordnungen auf, die mit MS-DOS-Anwendungen kompatibel sind, oder ändert Sie. |
| [Benutzer Befehl ändern](change-user.md) | Ändert den Installationsmodus für den Remotedesktop-Sitzungshost-Server. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Remotedesktopdienste (Terminaldienste): Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
