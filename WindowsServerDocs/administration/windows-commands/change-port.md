---
title: change port
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3d772c90-e849-4e74-b9ec-b6cae1159336 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ced5b9f0198179ab8b388f56aaea848b7a966081
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434506"
---
# <a name="change-port"></a>change port

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Listet oder ändert die COM-Port-Zuordnungen mit MS-DOS-Anwendungen kompatibel ist.
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.
> ## <a name="syntax"></a>Syntax
> ```
> change port [<PortX>=<PortY> | /d <PortX> | /query]
> ```
> ## <a name="parameters"></a>Parameter
> 
> |    Parameter    |              Beschreibung               |
> |-----------------|----------------------------------------|
> | <PortX>=<PortY> |    Ordnet COM <*AnschlussX*>, <*dem AnschlussY*>.    |
> |   /d <PortX>    | Löscht die Zuordnung für COM <*AnschlussX*>. |
> |     /query      |  Zeigt die aktuellen portzuordnungen an.   |
> |       /?        |  Zeigt die Hilfe an der Eingabeaufforderung an.  |
> 
> ## <a name="remarks"></a>Hinweise
> - Die meisten MS-DOS-Anwendungen unterstützen nur COM1 bis COM4 serielle Anschlüsse. Die **Port ändern** Befehl ordnet einen seriellen Anschluss an eine andere Portnummer, ermöglicht es Anwendungen, die nicht höherwertigen COM unterstützen-Ports auf den seriellen Anschluss zugreifen. neuzuordnung funktioniert nur für die aktuelle Sitzung und wird nicht beibehalten, wenn Sie über eine Sitzung abmelden und dann erneut anmelden.
> - Verwendung **Port ändern** ohne Parameter aus, um die verfügbaren COM-Anschlüsse und ihre aktuellen Zuordnungen angezeigt.
>   ## <a name="BKMK_examples"></a>Beispiele für
> - Geben Sie Folgendes ein, um die COM12 COM1 für die Verwendung von einer MS-DOS-basierten Anwendung zuzuordnen:
>   ```
>   change port com12=com1
>   ```
> - Um die aktuellen portzuordnungen anzuzeigen, geben Sie Folgendes ein:
>   ```
>   change port /query
>   ```
>   #### <a name="additional-references"></a>Zusätzliche Referenzen
>   [Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
>   [ändern](change.md)
>   [Remote Desktop Services &#40;"Terminal Services"&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
