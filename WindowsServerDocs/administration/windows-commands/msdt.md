---
title: msdt
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ead1b672-a120-4e16-94aa-a8e13602c1d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 87c1e4e8cd6d9de036b47de590867a6531d0335a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839253"
---
# <a name="msdt"></a>msdt



Ruft ein Problem Behandlungspaket in der Befehlszeile oder als Teil eines automatisierten Skripts auf und ermöglicht zusätzliche Optionen ohne Benutzereingaben.

## <a name="syntax"></a>Syntax

```
msdt </id <name> | /path <name> | /cab < name>> <</parameter> [options] … <parameter> [options]>>
```

### <a name="parameters"></a>Parameter

In der folgenden Tabelle sind die Parameter und Optionen enthalten, die von MSDT. exe unterstützt werden.


|      Parameter      |                                                                                            Beschreibung                                                                                             |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /ID \<Paketname > |        Gibt an, welches Diagnosepaket ausgeführt werden soll. Eine Liste der verfügbaren Pakete finden Sie in der Problem Behandlungspaket-ID im Abschnitt Verfügbare Problem Behandlungspakete weiter unten in diesem Thema.         |
|  /Path \<Verzeichnis  |                                                                                           . diagpkg-Datei                                                                                            |
|   /DCI \<>   |                                        Füllt das Hauptschlüssel-Feld in MSDT vorab auf. Dieser Parameter wird nur verwendet, wenn ein Support Anbieter einen Passkey bereitgestellt hat.                                         |
|  /DT \<Verzeichnis >   | Zeigt den Verlauf der Problembehandlung im angegebenen Verzeichnis an. Diagnoseergebnisse werden in den Verzeichnissen " **%LocalAppData%\diagnostics** " oder " **%LocalAppData%\elevateddiagnostics** " des Benutzers gespeichert. |
| /AF \<Antwortdatei >  |                                               Gibt eine Antwortdatei im XML-Format an, die Antworten auf eine oder mehrere Diagnose Interaktionen enthält.                                               |

