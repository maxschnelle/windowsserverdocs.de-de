---
title: Benutzer Abfragen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a670fb78-c055-464a-b61d-3a85632c52c5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 65bf42281e6e1956331c061167aea23d1cd61a1d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384869"
---
# <a name="query-user"></a>Benutzer Abfragen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt Informationen zu Benutzersitzungen auf einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host) an.
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.
> ## <a name="syntax"></a>Syntax
> ```
> query user [<UserName> | <SessionName> | <SessionID>] [/server:<ServerName>]
> ```
> ## <a name="parameters"></a>Parameter
> 
> |      Parameter       |                                                     Beschreibung                                                     |
> |----------------------|---------------------------------------------------------------------------------------------------------------------|
> |      <UserName>      |                            Gibt den Anmelde Namen des Benutzers an, den Sie Abfragen möchten.                             |
> |    <SessionName>     |                              Gibt den Namen der Sitzung an, die Sie Abfragen möchten.                              |
> |     <SessionID>      |                               Gibt die ID der Sitzung an, die Sie Abfragen möchten.                               |
> | /server:<ServerName> | Gibt den Remote Desktop-Sitzungs Host Server an, den Sie Abfragen möchten. Andernfalls wird der aktuelle RD-Sitzungs Host Server verwendet. |
> |          /?          |                                        Zeigt die Hilfe an der Eingabeaufforderung an.                                         |
> 
> ## <a name="remarks"></a>Hinweise
> - Mit diesem Befehl können Sie herausfinden, ob ein bestimmter Benutzer an einem bestimmten Remote Desktop-Sitzungs Host Server angemeldet ist. der **Abfrage Benutzer** gibt die folgenden Informationen zurück:
>   -   Der Name des Benutzers.
>   -   Der Name der Sitzung auf dem RD-Sitzungs Host Server
>   -   Die Sitzungs-ID
>   -   Der Status der Sitzung (aktiv oder getrennt).
>   -   Die Leerlaufzeit (die Anzahl von Minuten seit der letzten Tastatureingabe oder Mausbewegung bei der Sitzung)
>   -   Das Datum und die Uhrzeit der Anmeldung des Benutzers.
> - Um den **Abfrage Benutzer**verwenden zu können, müssen Sie über die Berechtigung "Vollzugriff" oder "Abfrage Informationen" verfügen.
> - Wenn Sie die **Abfrage Benutzer** ohne Angabe <*username*>, <*Sessionname*> oder <*SessionID*> verwenden, wird eine Liste aller Benutzer zurückgegeben, die beim Server angemeldet sind. Alternativ können Sie auch die **Abfrage Sitzung** verwenden, um eine Liste aller Sitzungen auf einem Server anzuzeigen.
> - Wenn der **Abfrage Benutzer** Informationen zurückgibt, wird vor der aktuellen Sitzung ein größer-als-Symbol (>) angezeigt.
> - Der **/Server** -Parameter ist nur erforderlich, wenn Sie **Abfrage Benutzer** von einem Remote Server verwenden.
>   ## <a name="BKMK_examples"></a>Beispiele
> - Geben Sie Folgendes ein, um Informationen über alle Benutzer anzuzeigen, die auf dem System angemeldet sind:
>   ```
>   query user
>   ```
> - Geben Sie Folgendes ein, um Informationen zum Benutzer user1 auf Server SERver1 anzuzeigen:
>   ```
>   query user USER1 /server:SERver1
>   ```
>   #### <a name="additional-references"></a>Weitere Verweise
>   [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
>   [Abfrage](query.md)
>   [Remotedesktopdienste &#40;Befehlsreferenz&#41; für Terminal Dienste](remote-desktop-services-terminal-services-command-reference.md)
