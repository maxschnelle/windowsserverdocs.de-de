---
title: Benutzer, der Abfragen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: c6e0d936e03e14e134c7bfd450a878fda1a796c4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442002"
---
# <a name="query-user"></a>Benutzer, der Abfragen

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt Informationen über die Sitzung des Benutzers auf einem Server Remote Desktop Session Host (rd Session Host).
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.
> ## <a name="syntax"></a>Syntax
> ```
> query user [<UserName> | <SessionName> | <SessionID>] [/server:<ServerName>]
> ```
> ## <a name="parameters"></a>Parameter
> 
> |      Parameter       |                                                     Beschreibung                                                     |
> |----------------------|---------------------------------------------------------------------------------------------------------------------|
> |      <UserName>      |                            Gibt den Anmeldenamen des Benutzers, der abgefragt werden soll.                             |
> |    <SessionName>     |                              Gibt den Namen der Sitzung, die Sie abfragen möchten.                              |
> |     <SessionID>      |                               Gibt die ID der Sitzung, die Sie abfragen möchten.                               |
> | /server:<ServerName> | Gibt an, den rd-Sitzungshostserver, den Sie abfragen möchten. Andernfalls wird der aktuelle rd Session Host-Server verwendet. |
> |          /?          |                                        Zeigt die Hilfe an der Eingabeaufforderung an.                                         |
> 
> ## <a name="remarks"></a>Hinweise
> - Sie können diesen Befehl verwenden, um herauszufinden, ob ein bestimmter Benutzer eine bestimmte rd Session Host-Server angemeldet ist. **Benutzer, der Abfragen** die folgenden Informationen zurückgegeben:
>   -   Der Name des Benutzers
>   -   Der Name der Sitzung auf dem Remotedesktop-Sitzungshostserver
>   -   Die Sitzungs-ID
>   -   Der Status der Sitzung ("aktiv" oder "getrennt")
>   -   Die im Leerlauf Zeit (die Anzahl von Minuten seit der letzten Tastatureingabe oder der Bewegung der Maus in der Sitzung)
>   -   Datum und Uhrzeit, die der Benutzer angemeldet
> - Verwendung von **Abfrage**, müssen Sie eine Full Control-Berechtigung oder eine spezielle Berechtigung Informationen Abfragen.
> - Bei Verwendung von **Abfrage** ohne Angabe von <*Benutzername*>, <*Sitzungsname*>, oder <*SessionID*>, eine Liste mit allen Benutzer, die auf dem Server angemeldet sind, wird zurückgegeben. Alternativ können Sie auch verwenden **Abfragen Sitzung** um eine Liste aller Sitzungen auf einem Server anzuzeigen.
> - Wenn **Abfrage** gibt Informationen zurück, ein größer-als (>) ein wird vor der aktuellen Sitzung angezeigt.
> - Die **/Server** Parameter ist erforderlich, nur bei Verwendung von **Abfrage** von einem Remoteserver.
>   ## <a name="BKMK_examples"></a>Beispiele für
> - Um Informationen zu allen Benutzern, die protokolliert werden, auf dem System anzuzeigen, geben Sie Folgendes ein:
>   ```
>   query user
>   ```
> - Um Informationen über den Benutzer "user1" auf dem Server SERver1 anzuzeigen, geben Sie Folgendes ein:
>   ```
>   query user USER1 /server:SERver1
>   ```
>   #### <a name="additional-references"></a>Zusätzliche Referenzen
>   [Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
>   [Abfrage](query.md)
>   [Remote Desktop Services &#40;"Terminal Services"&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
