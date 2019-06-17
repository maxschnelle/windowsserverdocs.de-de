---
title: msdt
description: 'Windows-Befehle Thema ***- '
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
ms.openlocfilehash: ba411cf73026afe9990e5c32824e3dc277507891
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437232"
---
# <a name="msdt"></a>msdt



Ruft eine Problembehandlung Pack in der Befehlszeile oder als Teil eines automatisierten Skripts und zusätzliche Optionen ohne Benutzereingabe ermöglicht.

## <a name="syntax"></a>Syntax

```
msdt </id <name> | /path <name> | /cab < name>> <</parameter> [options] … <parameter> [options]>>
```

## <a name="parameters"></a>Parameter

Die folgende Tabelle enthält die Parameter und von msdt.exe unterstützten Optionen.


|      Parameter      |                                                                                            Beschreibung                                                                                             |
|---------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /ID \<Paketname > |        Gibt an, die Diagnose-Paket ausführen. Eine Liste der verfügbaren Pakete finden Sie unter der Problembehandlung Pack-ID im Feld "Verfügbare Problembehandlungspakete? weiter unten in diesem Thema.         |
|  / Path \<Verzeichnis  |                                                                                           .diagpkg-Datei                                                                                            |
|   /dci \<passkey>   |                                        Bereits das Hauptschlüssel Feld Msdt an. Dieser Parameter wird nur verwendet, wenn ein Anbieter für technischen Support einen Hauptschlüssel zur Verfügung gestellt.                                         |
|  /dt \<directory>   | Zeigt den Verlauf zur Problembehandlung im angegebenen Verzeichnis. Diagnoseergebnisse des Benutzers gespeichert sind **%LOCALAPPDATA%\Diagnostics** oder **%LOCALAPPDATA%\ElevatedDiagnostics** Verzeichnisse. |
| / AF \<Antwortdatei >  |                                               Gibt eine Antwortdatei im XML-Format, das Antworten auf eine oder mehrere diagnostische Interaktionen enthält.                                               |

