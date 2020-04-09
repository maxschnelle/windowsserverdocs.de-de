---
title: Änderung
description: Windows-Befehls Thema zu Änderungen, die Remotedesktop-Sitzungshost Servereinstellungen für Anmeldungen, com-Port Zuordnungen und Installationsmodus ändern.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90012116-0fb3-4f34-a819-cf4d4b4f8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d5d91f8d0941fc96e776c761b9c7037e58588df8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847953"
---
# <a name="change"></a>Änderung

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ändert Remotedesktop-Sitzungshost Servereinstellungen für Anmeldungen, com-Port Zuordnungen und Installationsmodus.

> [!NOTE]
> In Windows Server 2008 R2 wurde „Terminaldienste“ umbenannt in „Remotedesktopdienste“. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax

 ```
 change logon
 change port
 change user
 ```
 
 ### <a name="parameters"></a>Parameter
 
 |            Parameter            |                                                   Beschreibung                                                   |
 |---------------------------------|-----------------------------------------------------------------------------------------------------------------|
 | [change logon](change-logon.md) | Aktiviert oder deaktiviert Anmeldungen von Client Sitzungen auf einem Remote Desktop-Sitzungs Host Server oder zeigt den aktuellen Anmeldestatus an. |
 |  [change port](change-port.md)  |                Listet die COM-Port Zuordnungen auf, die mit MS-DOS-Anwendungen kompatibel sind, oder ändert Sie.                |
 |  [change user](change-user.md)  |                            ändert den Installationsmodus für den RD-Sitzungs Host Server.                             |
 
 ## <a name="additional-references"></a>Weitere Verweise
 - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
 [Remotedesktopdienste Befehlsreferenz (Terminal Dienste)](remote-desktop-services-terminal-services-command-reference.md)
