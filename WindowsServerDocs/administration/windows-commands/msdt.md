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
ms.openlocfilehash: 781e83615d44a4adb20fd85fe5ce6ebc7c2d4966
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818831"
---
# <a name="msdt"></a>msdt



Ruft eine Problembehandlung Pack in der Befehlszeile oder als Teil eines automatisierten Skripts und zusätzliche Optionen ohne Benutzereingabe ermöglicht.

## <a name="syntax"></a>Syntax

```
msdt </id <name> | /path <name> | /cab < name>> <</parameter> [options] … <parameter> [options]>>
```

## <a name="parameters"></a>Parameter

Die folgende Tabelle enthält die Parameter und von msdt.exe unterstützten Optionen.

|Parameter|Beschreibung|
|---------|-----------|
|/ ID \<Paketname >|Gibt an, die Diagnose-Paket ausführen. Eine Liste der verfügbaren Pakete finden Sie unter der Problembehandlung Pack-ID im Feld "Verfügbare Problembehandlungspakete? weiter unten in diesem Thema.|
|/ Path \<Verzeichnis | .diagpkg-Datei | .diagcfg Datei >|Gibt den vollständigen Pfad zu einer Diagnose-Paket an. Wenn Sie ein Verzeichnis angeben, muss das Verzeichnis eine Diagnose-Paket enthalten. Sie können nicht den/Path-Parameter verwenden, in Verbindung mit der */ID*, */dci*, oder */cab* Parameter.|
|/dci \<passkey>|Bereits das Hauptschlüssel Feld Msdt an. Dieser Parameter wird nur verwendet, wenn ein Anbieter für technischen Support einen Hauptschlüssel zur Verfügung gestellt.|
|/dt \<directory>|Zeigt den Verlauf zur Problembehandlung im angegebenen Verzeichnis. Diagnoseergebnisse des Benutzers gespeichert sind **%LOCALAPPDATA%\Diagnostics** oder **%LOCALAPPDATA%\ElevatedDiagnostics** Verzeichnisse.|
|/ AF \<Antwortdatei >|Gibt eine Antwortdatei im XML-Format, das Antworten auf eine oder mehrere diagnostische Interaktionen enthält.|
