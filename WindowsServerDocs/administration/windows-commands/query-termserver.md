---
title: termserver Abfragen
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3b89d3b4-236f-4376-90b6-939a0ec4b288
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d63bd158dad74203aa7ee3fd4e43dffb97c4c873
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836923"
---
# <a name="query-termserver"></a>termserver Abfragen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine Liste aller Remotedesktop-Sitzungshost Server (RD-Sitzungs Host Server) im Netzwerk an.
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 wurde „Terminaldienste“ umbenannt in „Remotedesktopdienste“. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.
> ## <a name="syntax"></a>Syntax
> ```
> query termserver [<ServerName>] [/domain:<Domain>] [/address] [/continue]
> ```
> ### <a name="parameters"></a>Parameter
> 
> |    Parameter     |                                                                        Beschreibung                                                                         |
> |------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
> |   <ServerName>   |                                               Gibt den Namen an, der den RD-Sitzungs Host Server identifiziert.                                               |
> | /Domain:<Domain> | Gibt die Domäne an, die für Terminal Server abgefragt werden soll. Sie müssen keine Domäne angeben, wenn Sie die Domäne Abfragen, in der Sie gerade arbeiten. |
> |     /address     |                                                  Zeigt die Netzwerk-und Knoten Adressen für jeden Server an.                                                  |
> |    /Continue     |                                              Verhindert, dass angehalten wird, nachdem jeder Bildschirm mit Informationen angezeigt wird.                                               |
> |        /?        |                                                            Zeigt die Hilfe an der Eingabeaufforderung an.                                                            |
> 
> ## <a name="remarks"></a>Hinweise
> - **query termserver** durchsucht das Netzwerk nach allen angeschlossenen RD-Sitzungs Host Servern und gibt die folgenden Informationen zurück:
>   - Der Name des Servers.
>   - Das Netzwerk (und die Knotenadresse, wenn die/Address-Option verwendet wird)
>     ## <a name="examples"></a><a name=BKMK_examples></a>Beispiele
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
>   ## <a name="additional-references"></a>Weitere Verweise
>   - [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
>   [Abfrage](query.md)
>   [Remotedesktopdienste Befehls Verweis (Terminal Dienste)](remote-desktop-services-terminal-services-command-reference.md)
