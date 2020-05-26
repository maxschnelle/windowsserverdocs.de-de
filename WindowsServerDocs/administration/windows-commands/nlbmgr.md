---
title: nlbmgr
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 89cb8590-b7cf-4a27-89fa-0fa62ea1a1ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a055eb30984bd1832d84bce40607eb0722b175b2
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820850"
---
# <a name="nlbmgr"></a>nlbmgr

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mithilfe des Netzwerk Lastenausgleich-Managers können Sie die Netzwerk Lastenausgleichs-Cluster und alle Cluster Hosts von einem einzelnen Computer aus konfigurieren und verwalten. Außerdem können Sie die Cluster Konfiguration auf andere Hosts replizieren. Sie können den Netzwerk Lastenausgleich-Manager über die Befehlszeile starten, indem Sie den Befehl " **nlbmgr. exe**" verwenden, der im Ordner " **systemroot\system32** " installiert ist.
## <a name="syntax"></a>Syntax
```
nlbmgr [/help] [/noping] [/hostlist <filename>] [/autorefresh <interval>]
```
#### <a name="parameters"></a>Parameter

|        Parameter        |                                                                                                                                                                                                BESCHREIBUNG                                                                                                                                                                                                |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          /help          |                                                                                                                                                                                   Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                    |
|         /noping         | Verhindert, dass der Netzwerk Lastenausgleich-Manager die Hosts anheftet, bevor versucht wird, Sie über Windows-Verwaltungsinstrumentation (WMI) zu kontaktieren. Verwenden Sie diese Option, wenn Sie das Internet Control Message-Protokoll (ICMP) auf allen verfügbaren Netzwerkadaptern deaktiviert haben. Wenn der Netzwerk Lastenausgleich-Manager versucht, einen Host zu kontaktieren, der nicht verfügbar ist, tritt bei der Verwendung dieser Option eine Verzögerung auf. |
|  /hostlist<filename>   |                                                                                                                                                                Lädt die in filename angegebenen Hosts in den Netzwerk Lastenausgleich-Manager.                                                                                                                                                                 |
| /autorefresh<interval> |                                                                                                          Bewirkt, dass der Netzwerk Lastenausgleich-Manager die Host-und Cluster Informationen alle <interval> Sekunden aktualisiert. Wenn kein Intervall angegeben wird, werden die Informationen alle 60 Sekunden aktualisiert.                                                                                                          |
|           /?            |                                                                                                                                                                                   Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                    |

## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

