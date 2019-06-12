---
title: change logon
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 45c171a1b14cf69abf039d57697cad933a2dd87b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434570"
---
>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

# <a name="change-logon"></a>change logon
Aktiviert oder deaktiviert die Anmeldungen von Clientsitzungen, oder zeigt den aktuellen Status der Anmeldung.
Dieses Dienstprogramm ist hilfreich für Systemwartung.
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.
> ## <a name="syntax"></a>Syntax
> ```
> change logon {/query | /enable | /disable | /drain | /drainuntilrestart}
> ```
> ## <a name="parameters"></a>Parameter
> 
> |     Parameter      |                                                       Beschreibung                                                        |
> |--------------------|--------------------------------------------------------------------------------------------------------------------------|
> |       /query       |                             Zeigt den aktuellen Status für die Anmeldung an, ob aktiviert oder deaktiviert.                              |
> |      / Enable /       |                              Können Anmeldungen von Clientsitzungen, jedoch nicht aus der Konsole an.                              |
> |      / Disable      |  Deaktiviert Weitere Anmeldungen von Clientsitzungen, jedoch nicht aus der Konsole an. Derzeit angemeldete Benutzer hat keine Auswirkungen auf.   |
> |       /drain       |                 Anmeldungen von neuen Clientsitzungen deaktiviert, aber erneute Verbindungen zu vorhandenen Sitzungen können.                 |
> | /drainuntilrestart | Deaktiviert die Anmeldungen vom neuen Clientsitzungen, bis der Computer neu gestartet wird, jedoch ermöglicht die erneute Verbindungen zu vorhandenen Sitzungen. |
> |         /?         |                                           Zeigt die Hilfe an der Eingabeaufforderung an.                                           |
> 
> ## <a name="remarks"></a>Hinweise
> - Nur Administratoren können die **Anmeldung ändern** Befehl.
> - Anmeldungen werden erneut aktiviert, wenn Sie das System neu starten. Wenn Sie von einer Clientsitzung mit dem Remotedesktop-Sitzungshost (rd Session Host)-Server verbunden sind und Deaktivieren von Anmeldungen, und melden Sie sich vor der erneuten Aktivierung von Anmeldungen, werden Sie nicht eine Verbindung mit der Sitzung herstellen können. Melden Sie sich an der Konsole an, um Anmeldungen von Clientsitzungen erneut zu aktivieren.
>   ## <a name="BKMK_examples"></a>Beispiele für
> - Um den aktuellen Status der Anmeldung anzuzeigen, geben Sie Folgendes ein:
>   ```
>   change logon /query
>   ```
> - Geben Sie Folgendes ein, um Anmeldungen von Clientsitzungen zu aktivieren:
>   ```
>   change logon /enable
>   ```
> - Geben Sie Folgendes ein, um Clients zu deaktivieren:
>   ```
>   change logon /disable
>   ```
>   #### <a name="additional-references"></a>Zusätzliche Referenzen
>   [Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
>   [ändern](change.md)
>   [Remote Desktop Services &#40;"Terminal Services"&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
