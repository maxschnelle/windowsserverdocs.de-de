---
title: query process
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 36ce3ffc-0092-4eb1-a374-28e6616ca946
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ac3e5a458d88d945e857cd1922783e5b0ff5cf0
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436285"
---
# <a name="query-process"></a>query process

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu Prozessen an, die auf einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host) ausgeführt werden.
Mit diesem Befehl können Sie herausfinden, welche Programme von einem bestimmten Benutzer ausgeführt werden und welche Benutzer ein bestimmtes Programm ausführen.

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.
> ## <a name="syntax"></a>Syntax
> ```
> query process [* | <ProcessID> | <UserName> | <SessionName> | /id:<nn> | <ProgramName>] [/server:<ServerName>]
> ```
> ### <a name="parameters"></a>Parameter
>
> |      Parameter       |                                                                 Beschreibung                                                                  |
> |----------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
> |          \*          |                                                    Listet die Prozesse für alle Sitzungen auf.                                                     |
> |     <ProcessID>      |                                   Gibt die numerische ID an, die den Prozess identifiziert, den Sie Abfragen möchten.                                   |
> |      <UserName>      |                                       Gibt den Namen des Benutzers an, dessen Prozesse Sie auflisten möchten.                                       |
> |    <SessionName>     |                                     Gibt den Namen der Sitzung an, deren Prozesse Sie auflisten möchten.                                      |
> |       /ID<nn>       |                                      Gibt die ID der Sitzung an, deren Prozesse Sie auflisten möchten.                                       |
> |    <ProgramName>     |                     Gibt den Namen des Programms an, dessen Prozesse Sie Abfragen möchten. Die Erweiterung ". exe" ist erforderlich.                     |
> | /server:<ServerName> | Gibt den Remote Desktop-Sitzungs Host Server an, dessen Prozesse Sie auflisten möchten. Wenn keine Angabe erfolgt, wird der Server verwendet, auf dem Sie zurzeit angemeldet sind. |
> |          /?          |                                                     Zeigt die Hilfe an der Eingabeaufforderung an.                                                     |
>
>#### <a name="remarks"></a>Hinweise
> - Administratoren haben Vollzugriff auf alle **Abfrageprozess** Funktionen.
> - Wenn Sie die <*username*>, <*Sessionname*>, **/ID:** < *NN*>, <*Programmname*> oder *-Parametern nicht angeben, **\\** zeigt der **Abfrageprozess** nur die Prozesse an, die zum aktuellen Benutzer gehören.
> - Wenn eine Sitzung angegeben wird, muss eine aktive Sitzung identifiziert werden.
> - der **Abfrageprozess** gibt die folgenden Informationen zurück:
>   -   Der Benutzer, der den Prozess besitzt.
>   -   Die Sitzung, die den Prozess besitzt.
>   -   Die ID der Sitzung.
>   -   Der Name des Prozesses.
>   -   Die ID des Prozesses.
> - Wenn der **Abfrageprozess** Informationen zurückgibt, wird vor jedem Prozess, der zur aktuellen Sitzung gehört, ein größer-als-Symbol (>) angezeigt.
>   ## <a name="examples"></a>Beispiele
> - Zum Anzeigen von Informationen zu den Prozessen, die von allen Sitzungen verwendet werden, geben Sie Folgendes ein:
>   ```
>   query process *
>   ```
> - Geben Sie Folgendes ein, um Informationen über die Prozesse anzuzeigen, die von der Sitzungs-ID 2 verwendet werden:
>   ```
>   query process /ID:2
>   ```
>   ## <a name="additional-references"></a>Zusätzliche Referenzen
>   - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md) 
>    [Abfrage](query.md) 
>    [Befehlsreferenz für Remotedesktopdienste (Terminal Dienste)](remote-desktop-services-terminal-services-command-reference.md)
