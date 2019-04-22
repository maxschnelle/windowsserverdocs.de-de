---
title: Abfrage termserver
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 5baab78f6a7222bad121773e686bacb01dc8872a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817231"
---
# <a name="query-termserver"></a>Abfrage termserver

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt eine Liste mit allen Remotedesktop-Sitzungshost (rd Session Host)-Servern im Netzwerk.
Beispiele für diesen Befehl verwenden, finden Sie unter [Beispiele](#BKMK_examples).
> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Neuerungen in der neuesten Version finden Sie unter [welche s New in Remote Desktop Services in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der technischen Bibliothek für Windows Server.
## <a name="syntax"></a>Syntax
```
query termserver [<ServerName>] [/domain:<Domain>] [/address] [/continue]
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|<ServerName>|Gibt den Namen, der den Remotedesktop-Sitzungshostserver identifiziert.|
|/ Domain:<Domain>|Gibt die Domäne, zum Abfragen von Terminalservern. Sie müssen sich nicht um eine Domäne angeben, wenn Sie die Domäne Abfragen sind, in der Sie gerade arbeiten.|
|/address|Zeigt die Netzwerk- und Knoten-Adressen für jeden Server.|
|"/ continue"|Verhindert, dass das Anhalten, nachdem jeder Bildschirm Informationen angezeigt wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|
## <a name="remarks"></a>Hinweise
-   **Abfragen von Termserver** durchsucht das Netzwerk aus, für alle Remotedesktop-Sitzungshostserver, und Sie die folgenden Informationen zurückgegeben:
    -   Der Name des Servers
    -   Das Netzwerk (und die Knotenadresse, wenn die Address-Option verwendet wird)
## <a name="BKMK_examples"></a>Beispiele für
-   Um Informationen über alle Remotedesktop-Sitzungshostserver im Netzwerk anzuzeigen, geben Sie Folgendes ein:
    ```
    query termserver
    ```
-   Um Informationen über den Remotedesktop-Sitzungshostserver mit dem Namen Server3 anzuzeigen, geben Sie Folgendes ein:
    ```
    query termserver Server3
    ```
-   Um Informationen über alle Remotedesktop-Sitzungshostserver in der Domäne CONTOSO anzuzeigen, geben Sie Folgendes ein:
    ```
    query termserver /domain:CONTOSO
    ```
-   Um das Netzwerk verwenden und Adresse für den Remotedesktop-Sitzungshostserver mit dem Namen Server3 anzuzeigen, geben Sie Folgendes ein:
    ```
    query termserver Server3 /address
    ```
#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[Abfrage](query.md)
[Remote Desktop Services &#40;"Terminal Services"&#41; -Befehlsreferenz](remote-desktop-services-terminal-services-command-reference.md)
