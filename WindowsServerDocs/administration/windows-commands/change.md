---
title: change
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90012116-0fb3-4f34-a819-cf4d4b4f8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eee52bbb24824ea01f9c55a4bfe6e3e60ad2ab58
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379552"
---
# <a name="change"></a>change

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

ändert Remotedesktop-Sitzungshost Servereinstellungen (RD-Sitzungs Host) für Anmeldungen, com-Port Zuordnungen und Installationsmodus.
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.
> ## <a name="syntax"></a>Syntax
> ```
> change logon
> change port
> change user
> ```
> ## <a name="parameters"></a>Parameter
> 
> |            Parameter            |                                                   Beschreibung                                                   |
> |---------------------------------|-----------------------------------------------------------------------------------------------------------------|
> | [change logon](change-logon.md) | Aktiviert oder deaktiviert Anmeldungen von Client Sitzungen auf einem Remote Desktop-Sitzungs Host Server oder zeigt den aktuellen Anmeldestatus an. |
> |  [change port](change-port.md)  |                Listet die COM-Port Zuordnungen auf, die mit MS-DOS-Anwendungen kompatibel sind, oder ändert Sie.                |
> |  [change user](change-user.md)  |                            ändert den Installationsmodus für den RD-Sitzungs Host Server.                             |
> 
> #### <a name="additional-references"></a>Weitere Verweise
> [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
> [Remotedesktopdienste &#40;Befehlsreferenz&#41; für Terminal Dienste](remote-desktop-services-terminal-services-command-reference.md)
