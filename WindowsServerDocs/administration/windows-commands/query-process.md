---
title: Abfrageprozess
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 36ce3ffc-0092-4eb1-a374-28e6616ca946
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 714a77c5fabf507b84090f37104203abd37a6f0f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371913"
---
# <a name="query-process"></a>Abfrageprozess

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu Prozessen an, die auf einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host) ausgeführt werden.
Mit diesem Befehl können Sie herausfinden, welche Programme von einem bestimmten Benutzer ausgeführt werden und welche Benutzer ein bestimmtes Programm ausführen.
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.
> ## <a name="syntax"></a>Syntax
> ```
> query process [* | <ProcessID> | <UserName> | <SessionName> | /id:<nn> | <ProgramName>] [/server:<ServerName>]
> ```
> ## <a name="parameters"></a>Parameter
> 
> |      Parameter       |                                                                 Beschreibung                                                                  |
> |----------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
> |          \*          |                                                    Listet die Prozesse für alle Sitzungen auf.                                                     |
> |     <ProcessID>      |                                   Gibt die numerische ID an, die den Prozess identifiziert, den Sie Abfragen möchten.                                   |
> |      <UserName>      |                                       Gibt den Namen des Benutzers an, dessen Prozesse Sie auflisten möchten.                                       |
> |    <SessionName>     |                                     Gibt den Namen der Sitzung an, deren Prozesse Sie auflisten möchten.                                      |
> |       /ID: <nn>       |                                      Gibt die ID der Sitzung an, deren Prozesse Sie auflisten möchten.                                       |
> |    <ProgramName>     |                     Gibt den Namen des Programms an, dessen Prozesse Sie Abfragen möchten. Die Erweiterung ". exe" ist erforderlich.                     |
> | /server:<ServerName> | Gibt den Remote Desktop-Sitzungs Host Server an, dessen Prozesse Sie auflisten möchten. Wenn keine Angabe erfolgt, wird der Server verwendet, auf dem Sie zurzeit angemeldet sind. |
> |          /?          |                                                     Zeigt die Hilfe an der Eingabeaufforderung an.                                                     |
> 
> ## <a name="remarks"></a>Hinweise
> - Administratoren haben Vollzugriff auf alle **Abfrageprozess** Funktionen.
> - Wenn Sie die Parameter <*username*>, <*Sessionname*>, **/ID:** <*NN*>, <*Program Name*> oder **\\** * nicht angeben, zeigt der **Abfrageprozess** nur die Prozesse an, die gehört zum aktuellen Benutzer.
> - Wenn eine Sitzung angegeben wird, muss eine aktive Sitzung identifiziert werden.
> - der **Abfrageprozess** gibt die folgenden Informationen zurück:
>   -   Der Benutzer, der den Prozess besitzt.
>   -   Die Sitzung, die den Prozess besitzt.
>   -   Die ID der Sitzung.
>   -   Der Name des Prozesses.
>   -   Die ID des Prozesses.
> - Wenn der **Abfrageprozess** Informationen zurückgibt, wird vor jedem Prozess, der zur aktuellen Sitzung gehört, ein größer-als-Symbol (>) angezeigt.
>   ## <a name="BKMK_examples"></a>Beispiele
> - Zum Anzeigen von Informationen zu den Prozessen, die von allen Sitzungen verwendet werden, geben Sie Folgendes ein:
>   ```
>   query process *
>   ```
> - Geben Sie Folgendes ein, um Informationen über die Prozesse anzuzeigen, die von der Sitzungs-ID 2 verwendet werden:
>   ```
>   query process /ID:2
>   ```
>   #### <a name="additional-references"></a>Weitere Verweise
>   [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
>   -[Abfrage](query.md)@no__t-[3 &#40;Remotedesktopdienste Befehls&#41; Referenz für Terminal Dienste](remote-desktop-services-terminal-services-command-reference.md)
