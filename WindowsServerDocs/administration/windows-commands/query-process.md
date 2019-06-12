---
title: Abfrageprozess
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 3248c2b1f476a1a9843f7e930b05a3dca812d694
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442122"
---
# <a name="query-process"></a>Abfrageprozess

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt Informationen zu Prozessen, die auf einem Remotedesktop-Sitzungshost (rd Session Host)-Server ausgeführt werden.
Sie können diesen Befehl verwenden, um herauszufinden, welche Programme, die ein bestimmten Benutzer ausgeführt wird, und auch die Benutzer ein bestimmtes Programm ausgeführt werden.
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.
> ## <a name="syntax"></a>Syntax
> ```
> query process [* | <ProcessID> | <UserName> | <SessionName> | /id:<nn> | <ProgramName>] [/server:<ServerName>]
> ```
> ## <a name="parameters"></a>Parameter
> 
> |      Parameter       |                                                                 Beschreibung                                                                  |
> |----------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
> |          \*          |                                                    Listet die Prozesse für alle Sitzungen an.                                                     |
> |     <ProcessID>      |                                   Gibt an, die numerische ID identifiziert den Prozess, den abgefragt werden soll.                                   |
> |      <UserName>      |                                       Gibt den Namen des Benutzers, dessen Prozesse, die Sie auflisten möchten.                                       |
> |    <SessionName>     |                                     Gibt den Namen der Sitzung, deren Prozesse, die Sie auflisten möchten.                                      |
> |       / ID:<nn>       |                                      Gibt die ID der Sitzung, deren Prozesse, die Sie auflisten möchten.                                       |
> |    <ProgramName>     |                     Gibt den Namen des Programms, deren Prozesse, die Sie abfragen möchten. Die ".exe"-Erweiterung ist erforderlich.                     |
> | /server:<ServerName> | Gibt an, den rd-Sitzungshostserver, deren Prozesse, die Sie auflisten möchten. Falls nicht angegeben, wird der Server, in dem Sie derzeit angemeldet sind, verwendet. |
> |          /?          |                                                     Zeigt die Hilfe an der Eingabeaufforderung an.                                                     |
> 
> ## <a name="remarks"></a>Hinweise
> - Administratoren haben vollen Zugriff auf alle **Abfragen Prozess** Funktionen.
> - Wenn Sie keinen angeben der <*Benutzername*>, <*Sitzungsname*>, **/ID:** <*Nn*>, <*ProgramName*>, oder **\\** * Parameter **Abfragen Prozess** zeigt nur die Prozesse, die für den aktuellen Benutzer gehören.
> - Wenn eine Sitzung angegeben wird, muss eine aktive Sitzung identifiziert werden.
> - **Abfragen von Prozess** die folgenden Informationen zurückgegeben:
>   -   Der Benutzer, der Besitzer des Prozesses ist
>   -   Die Sitzung, die Besitzer des Prozesses ist
>   -   Die ID der Sitzung
>   -   Der Name des Prozesses
>   -   Die ID des Prozesses
> - Wenn **Abfragen Prozess** gibt Informationen zurück, ein Symbol größer als (>) wird angezeigt, vor jedem Prozess, der mit der aktuellen Sitzung gehört.
>   ## <a name="BKMK_examples"></a>Beispiele für
> - Zum Anzeigen von Informationen zu den Prozessen, die von allen Sitzungen verwendet wird, geben Sie Folgendes ein:
>   ```
>   query process *
>   ```
> - Zum Anzeigen von Informationen zu den Prozessen, die von Sitzungs-ID 2 verwendet wird, geben Sie Folgendes ein:
>   ```
>   query process /ID:2
>   ```
>   #### <a name="additional-references"></a>Zusätzliche Referenzen
>   [Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
>   [Abfrage](query.md)
>   [Remote Desktop Services &#40;"Terminal Services"&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
