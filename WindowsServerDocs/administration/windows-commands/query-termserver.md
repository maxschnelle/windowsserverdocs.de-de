---
title: termserver Abfragen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3b89d3b4-236f-4376-90b6-939a0ec4b288
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 95a2e102a147bd7ebee24995d1e1fcd4147f8174
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371891"
---
# <a name="query-termserver"></a>termserver Abfragen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Zeigt eine Liste aller Remotedesktop-Sitzungshost Server (RD-Sitzungs Host Server) im Netzwerk an.
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.
> ## <a name="syntax"></a>Syntax
> ```
> query termserver [<ServerName>] [/domain:<Domain>] [/address] [/continue]
> ```
> ## <a name="parameters"></a>Parameter
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
>     ## <a name="BKMK_examples"></a>Beispiele
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
>   #### <a name="additional-references"></a>Weitere Verweise
>   [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
>   [Abfrage](query.md)
>   [Remotedesktopdienste &#40;Befehlsreferenz&#41; für Terminal Dienste](remote-desktop-services-terminal-services-command-reference.md)
