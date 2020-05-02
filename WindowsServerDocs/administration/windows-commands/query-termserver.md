---
title: termserver Abfragen
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3b89d3b4-236f-4376-90b6-939a0ec4b288
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c8a0a4608a16df0336b90ea5df281278ae47a503
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722698"
---
# <a name="query-termserver"></a>termserver Abfragen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine Liste aller Remotedesktop-Sitzungshost Server (RD-Sitzungs Host Server) im Netzwerk an.

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.
> ## <a name="syntax"></a>Syntax
> ```
> query termserver [<ServerName>] [/domain:<Domain>] [/address] [/continue]
> ```
> ### <a name="parameters"></a>Parameter
> 
> |    Parameter     |                                                                        BESCHREIBUNG                                                                         |
> |------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
> |   <ServerName>   |                                               Gibt den Namen an, der den RD-Sitzungs Host Server identifiziert.                                               |
> | /Domain<Domain> | Gibt die Domäne an, die für Terminal Server abgefragt werden soll. Sie müssen keine Domäne angeben, wenn Sie die Domäne Abfragen, in der Sie gerade arbeiten. |
> |     /address     |                                                  Zeigt die Netzwerk-und Knoten Adressen für jeden Server an.                                                  |
> |    /Continue     |                                              Verhindert, dass angehalten wird, nachdem jeder Bildschirm mit Informationen angezeigt wird.                                               |
> |        /?        |                                                            Zeigt die Hilfe an der Eingabeaufforderung an.                                                            |
> 
> ## <a name="remarks"></a>Bemerkungen
> - **query termserver** durchsucht das Netzwerk nach allen angeschlossenen RD-Sitzungs Host Servern und gibt die folgenden Informationen zurück:
>   - Name des Servers
>   - Das Netzwerk (und die Knotenadresse, wenn die/Address-Option verwendet wird)
>     ## <a name="examples"></a>Beispiele
> - Geben Sie Folgendes ein, um Informationen über alle RD-Sitzungs Host Server im Netzwerk anzuzeigen:
>   ```
>   query termserver
>   ```
> - Geben Sie Folgendes ein, um Informationen zum Remote Desktop-Sitzungs Host Server mit dem Namen Server3 anzuzeigen:
>   ```
>   query termserver Server3
>   ```
> - Geben Sie Folgendes ein, um Informationen über alle RD-Sitzungs Host Server in der Domäne "ca" anzuzeigen:
>   ```
>   query termserver /domain:CONTOSO
>   ```
> - Geben Sie Folgendes ein, um die Netzwerk-und Knotenadresse für den RD-Sitzungs Host Server mit dem Namen Server3 anzuzeigen:
>   ```
>   query termserver Server3 /address
>   ```
>   ## <a name="additional-references"></a>Zusätzliche Referenzen
>   - [Befehlszeilen Syntax Key](command-line-syntax-key.md)
>   [Query](query.md)
>   [Remotedesktopdienste (Terminal Dienste) Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
