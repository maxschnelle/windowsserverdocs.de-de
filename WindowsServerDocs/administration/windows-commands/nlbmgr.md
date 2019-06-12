---
title: nlbmgr
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 757b218ad3a88cc10c4d1bcfed15a83bfd34cc74
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437033"
---
# <a name="nlbmgr"></a>nlbmgr

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Verwenden den Netzwerklastenausgleich-Manager, können Sie konfigurieren und verwalten Sie Ihre Netzwerklastenausgleich-Cluster und alle Hosts im Cluster von einem einzelnen Computer, und Sie können auch die Clusterkonfiguration zu anderen Hosts replizieren. Sie können den Netzwerklastenausgleich-Manager starten, über die Befehlszeile mithilfe des Befehls **nlbmgr.exe**, das installiert wird, der **systemroot\System32** Ordner.
## <a name="syntax"></a>Syntax
```
nlbmgr [/help] [/noping] [/hostlist <filename>] [/autorefresh <interval>]
```
### <a name="parameters"></a>Parameter

|        Parameter        |                                                                                                                                                                                                Beschreibung                                                                                                                                                                                                |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          /help          |                                                                                                                                                                                   Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                    |
|         / noping         | Verhindert, dass ein Netzwerklastenausgleich-Manager Pingen die Hosts vor dem Versuch, sie wenden Sie sich über die Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) an. Verwenden Sie diese Option, wenn Sie Internet Control Message Protocol (ICMP) auf alle verfügbaren Netzwerkadapter deaktiviert haben. Wenn Sie den Netzwerklastenausgleich-Manager versucht, einen Host zu kontaktieren, der nicht verfügbar ist, wird eine Verzögerung bei Verwendung dieser Option. |
|  /hostlist <filename>   |                                                                                                                                                                Lädt die Hosts in Netzwerklastenausgleich-Manager in Filename angegeben.                                                                                                                                                                 |
| / AutoRefresh <interval> |                                                                                                          Netzwerklastenausgleich-Manager die Host- und Clusterebene Informationen aktualisieren, führt dazu, dass jede <interval> Sekunden. Wenn kein Intervall angegeben wird, werden die Informationen alle 60 Sekunden aktualisiert.                                                                                                          |
|           /?            |                                                                                                                                                                                   Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                    |

## <a name="additional-references"></a>Zusätzliche Referenzen
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

