---
title: nlbmgr
description: Referenz Thema für den Befehl "Nlbmgr", mit dem Sie Ihre Netzwerk Lastenausgleichs-Cluster und alle Cluster Hosts mithilfe des Netzwerk Lastenausgleich-Managers von einem einzelnen Computer aus konfigurieren und verwalten können.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 89cb8590-b7cf-4a27-89fa-0fa62ea1a1ca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2eb7f802944260f7274e7ace30b7b55e9c4b27ad
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721503"
---
# <a name="nlbmgr"></a>nlbmgr

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mit dem Netzwerk Lastenausgleich-Manager können Sie Ihre Netzwerk Lastenausgleichs-Cluster und alle Cluster Hosts von einem einzelnen Computer aus konfigurieren und verwalten. Sie können diesen Befehl auch verwenden, um die Cluster Konfiguration auf andere Hosts zu replizieren.

Sie können den Netzwerk Lastenausgleich-Manager über die Befehlszeile starten, indem Sie den Befehl **nlbmgr.exe**verwenden, der im Ordner **systemroot\system32** installiert ist.

## <a name="syntax"></a>Syntax

```
nlbmgr [/noping][/hostlist <filename>][/autorefresh <interval>][/help | /?]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| /noping | Verhindert, dass der Netzwerk Lastenausgleich-Manager die Hosts anheftet, bevor versucht wird, Sie über Windows-Verwaltungsinstrumentation (WMI) zu kontaktieren. Verwenden Sie diese Option, wenn Sie das Internet Control Message-Protokoll (ICMP) auf allen verfügbaren Netzwerkadaptern deaktiviert haben. Wenn der Netzwerk Lastenausgleich-Manager versucht, einen Host zu kontaktieren, der nicht verfügbar ist, tritt bei der Verwendung dieser Option eine Verzögerung auf. |
| /hostlist`<filename>` | Lädt die in filename angegebenen Hosts in den Netzwerk Lastenausgleich-Manager. |
| /autorefresh`<interval>` | Bewirkt, dass der Netzwerk Lastenausgleich-Manager die Host-und Cluster Informationen alle `<interval>` Sekunden aktualisiert. Wenn kein Intervall angegeben wird, werden die Informationen alle 60 Sekunden aktualisiert. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |
| /help | Zeigt die Hilfe an der Eingabeaufforderung an. |

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Referenz zu networkloadbalancingclusters-Cmdlets](https://docs.microsoft.com/powershell/module/networkloadbalancingclusters)
