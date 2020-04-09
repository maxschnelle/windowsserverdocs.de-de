---
title: nlbmgr
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 89cb8590-b7cf-4a27-89fa-0fa62ea1a1ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dab1a2eff2c0c2e039e67e9c3271a967b802ac7c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838873"
---
# <a name="nlbmgr"></a>nlbmgr

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mithilfe des Netzwerk Lastenausgleich-Managers können Sie die Netzwerk Lastenausgleichs-Cluster und alle Cluster Hosts von einem einzelnen Computer aus konfigurieren und verwalten. Außerdem können Sie die Cluster Konfiguration auf andere Hosts replizieren. Sie können den Netzwerk Lastenausgleich-Manager über die Befehlszeile starten, indem Sie den Befehl " **nlbmgr. exe**" verwenden, der im Ordner " **systemroot\system32** " installiert ist.
## <a name="syntax"></a>Syntax
```
nlbmgr [/help] [/noping] [/hostlist <filename>] [/autorefresh <interval>]
```
#### <a name="parameters"></a>Parameter

|        Parameter        |                                                                                                                                                                                                Beschreibung                                                                                                                                                                                                |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          /help          |                                                                                                                                                                                   Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                    |
|         /noping         | Verhindert, dass der Netzwerk Lastenausgleich-Manager die Hosts anheftet, bevor versucht wird, Sie über Windows-Verwaltungsinstrumentation (WMI) zu kontaktieren. Verwenden Sie diese Option, wenn Sie das Internet Control Message-Protokoll (ICMP) auf allen verfügbaren Netzwerkadaptern deaktiviert haben. Wenn der Netzwerk Lastenausgleich-Manager versucht, einen Host zu kontaktieren, der nicht verfügbar ist, tritt bei der Verwendung dieser Option eine Verzögerung auf. |
|  /hostlist <filename>   |                                                                                                                                                                Lädt die in filename angegebenen Hosts in den Netzwerk Lastenausgleich-Manager.                                                                                                                                                                 |
| /AutoRefresh <interval> |                                                                                                          Bewirkt, dass der Netzwerk Lastenausgleich-Manager die Host-und Cluster Informationen alle <interval> Sekunden aktualisiert. Wenn kein Intervall angegeben wird, werden die Informationen alle 60 Sekunden aktualisiert.                                                                                                          |
|           /?            |                                                                                                                                                                                   Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                    |

## <a name="additional-references"></a>Weitere Verweise
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

