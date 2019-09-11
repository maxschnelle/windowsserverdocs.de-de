---
title: msdt
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ead1b672-a120-4e16-94aa-a8e13602c1d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7bec16ab3f716148bb009dd56be475fcd058a897
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868896"
---
# <a name="msdt"></a>msdt



Ruft ein Problem Behandlungspaket in der Befehlszeile oder als Teil eines automatisierten Skripts auf und ermöglicht zusätzliche Optionen ohne Benutzereingaben.

## <a name="syntax"></a>Syntax

```
msdt </id <name> | /path <name> | /cab < name>> <</parameter> [options] … <parameter> [options]>>
```

## <a name="parameters"></a>Parameter

In der folgenden Tabelle sind die Parameter und Optionen enthalten, die von MSDT. exe unterstützt werden.


|      Parameter      |                                                                                            Beschreibung                                                                                             |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /ID \<Paketname > |        Gibt an, welches Diagnosepaket ausgeführt werden soll. Eine Liste der verfügbaren Pakete finden Sie in der Problem Behandlungspaket-ID im Abschnitt "verfügbare Problem Behandlungspakete" weiter unten in diesem Thema.         |
|  /Path \<Verzeichnis  |                                                                                           . diagpkg-Datei                                                                                            |
|   /DCI \<Passkey->   |                                        Füllt das Hauptschlüssel-Feld in MSDT vorab auf. Dieser Parameter wird nur verwendet, wenn ein Support Anbieter einen Passkey bereitgestellt hat.                                         |
|  /DT \<Verzeichnis >   | Zeigt den Verlauf der Problembehandlung im angegebenen Verzeichnis an. Diagnoseergebnisse werden in den Verzeichnissen " **%LocalAppData%\diagnostics** " oder " **%LocalAppData%\elevateddiagnostics** " des Benutzers gespeichert. |
| /AF \<Antwortdatei >  |                                               Gibt eine Antwortdatei im XML-Format an, die Antworten auf eine oder mehrere Diagnose Interaktionen enthält.                                               |

