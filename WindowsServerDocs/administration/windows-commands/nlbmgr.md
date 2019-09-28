---
title: nlbmgr
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 89cb8590-b7cf-4a27-89fa-0fa62ea1a1ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2843e303b296beca24132b62073b6776a343544b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373160"
---
# <a name="nlbmgr"></a>nlbmgr

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mithilfe des Netzwerk Lastenausgleich-Managers können Sie die Netzwerk Lastenausgleichs-Cluster und alle Cluster Hosts von einem einzelnen Computer aus konfigurieren und verwalten. Außerdem können Sie die Cluster Konfiguration auf andere Hosts replizieren. Sie können den Netzwerk Lastenausgleich-Manager über die Befehlszeile starten, indem Sie den Befehl " **nlbmgr. exe**" verwenden, der im Ordner " **systemroot\system32** " installiert ist.
## <a name="syntax"></a>Syntax
```
nlbmgr [/help] [/noping] [/hostlist <filename>] [/autorefresh <interval>]
```
### <a name="parameters"></a>Parameter

|        Parameter        |                                                                                                                                                                                                Beschreibung                                                                                                                                                                                                |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          /help          |                                                                                                                                                                                   Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                    |
|         /noping         | Verhindert, dass der Netzwerk Lastenausgleich-Manager die Hosts anheftet, bevor versucht wird, Sie über Windows-Verwaltungsinstrumentation (WMI) zu kontaktieren. Verwenden Sie diese Option, wenn Sie das Internet Control Message-Protokoll (ICMP) auf allen verfügbaren Netzwerkadaptern deaktiviert haben. Wenn der Netzwerk Lastenausgleich-Manager versucht, einen Host zu kontaktieren, der nicht verfügbar ist, tritt bei der Verwendung dieser Option eine Verzögerung auf. |
|  /hostlist <filename>   |                                                                                                                                                                Lädt die in filename angegebenen Hosts in den Netzwerk Lastenausgleich-Manager.                                                                                                                                                                 |
| /AutoRefresh <interval> |                                                                                                          Bewirkt, dass der Netzwerk Lastenausgleich-Manager die Host-und Cluster Informationen alle <interval> Sekunden aktualisiert. Wenn kein Intervall angegeben wird, werden die Informationen alle 60 Sekunden aktualisiert.                                                                                                          |
|           /?            |                                                                                                                                                                                   Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                    |

## <a name="additional-references"></a>Weitere Verweise
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

