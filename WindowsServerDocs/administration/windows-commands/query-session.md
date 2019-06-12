---
title: abfragesitzung
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abc0ace8-0b74-4b6e-a937-a78bb4b61a1f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 25e2457d792b463ca861f0cba29f1c290684e7b0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442046"
---
# <a name="query-session"></a>abfragesitzung

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt Informationen zu Sitzungen auf einem Server Remote Desktop Session Host (rd Session Host).
Die Liste enthält Informationen, die nicht nur zu aktiven Sitzungen, sondern auch zu anderen Sitzungen, die der Server ausgeführt wird.
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.
> ## <a name="syntax"></a>Syntax
> ```
> query session [<SessionName> | <UserName> | <SessionID>] [/server:<ServerName>] [/mode] [/flow] [/connect] [/counter]
> ```
> ## <a name="parameters"></a>Parameter
> 
> |      Parameter       |                                                      Beschreibung                                                      |
> |----------------------|-----------------------------------------------------------------------------------------------------------------------|
> |    <SessionName>     |                               Gibt den Namen der Sitzung, die Sie abfragen möchten.                               |
> |      <UserName>      |                           Gibt den Namen des Benutzers, dessen Sitzungen Sie abfragen möchten.                            |
> |     <SessionID>      |                                Gibt die ID der Sitzung, die Sie abfragen möchten.                                |
> | /server:<ServerName> |                  Identifiziert den rd-Sitzungshostserver auf Abfrage. Der Standardwert ist der aktuelle Server.                   |
> |        / Mode         |                                            Zeigt die Einstellungen der aktuellen Zeile.                                            |
> |        /flow         |                                        Zeigt die aktuellen Einstellungen der flusssteuerung.                                        |
> |       /connect       |                                          Zeigt den aktuellen Verbindungseinstellungen.                                           |
> |       Sys       | Zeigt aktuelle Informationen zu Leistungsindikatoren, die Gesamtzahl der Sitzungen erstellt, einschließlich getrennt, sodass die Verbindung wiederhergestellt. |
> |          /?          |                                         Zeigt die Hilfe an der Eingabeaufforderung an.                                          |
> 
> ## <a name="remarks"></a>Hinweise
> - Benutzer können immer die Sitzung Abfragen, zu der der Benutzer zurzeit angemeldet ist. Um anderen Sitzungen abzufragen, muss der Benutzer Informationen beschränkten Zugriffsberechtigungen verfügen.
> - Wenn Sie eine Sitzung nicht mithilfe von angeben <*Sitzungsname*>, <*Benutzername*>, oder <*SessionID*>, **Abfragen Sitzung** Zeigt Informationen zu allen aktiven Sitzungen im System an.
> - Wenn **Abfragen Sitzung** gibt Informationen zurück, ein größer-als (>) ein wird vor der aktuellen Sitzung angezeigt. Es folgt die Ausgabe des Beispiels für **Abfragen Sitzung**:
>   ```
>   C:\>query session
>    SESSIONNAME    USERNAME       ID STATE  TYPE   DEVICE
>   console        Administrator1  0 active wdcon
>    rdp-tcp#1      User1           1 active wdtshare
>    rdp-tcp                        2 listen wdtshare
>                                   4 idle
>                                   5 idle
>   ```
>   Das größere als (>) Symbol gibt an, die aktuelle Sitzung. Sitzungsname Gibt den Namen der Sitzung an. Benutzername Gibt an, den Benutzernamen des Benutzers mit der Sitzung verbunden wird. Status bietet Informationen zu den aktuellen Status der Sitzung. Typ gibt an, den Sitzungstyp. Gerät, das nicht für die Konsole oder das Netzwerk verbundenen Sitzungen vorhanden ist, wird der Gerätename, die der Sitzung zugewiesen. Der Kommentar nach Informationen zur Sitzung wird aus dem Sitzungsprofil. Alle Sitzungen, in dem der anfängliche Zustand, als deaktiviert konfiguriert ist, werden nicht angezeigt, der **Abfragen Sitzung** auflisten, bis sie aktiviert sind.
>   ## <a name="BKMK_examples"></a>Beispiele für
> - Um Informationen zu allen aktiven Sitzungen auf SERver2-Server anzuzeigen, geben Sie Folgendes ein:
>   ```
>   query session /server:SERver2
>   ```
> - Um Informationen zu aktiven Sitzung modeM02 anzuzeigen, geben Sie Folgendes ein:
>   ```
>   query session modeM02
>   ```
>   #### <a name="additional-references"></a>Zusätzliche Referenzen
>   [Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
>   [Abfrage](query.md)
>   [Remote Desktop Services &#40;"Terminal Services"&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
