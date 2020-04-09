---
title: bootcfg
description: Windows-Befehle-Thema für bootcfg, mit dem die Einstellungen der Boot. ini-Datei konfiguriert, abgefragt oder geändert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3deb354c-5717-4066-bc79-b9323d559e44
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a977b857242c030515a09a67eb0d284ade7a0beb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848383"
---
# <a name="bootcfg"></a>bootcfg

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht das Konfigurieren, Abfragen oder Ändern von Einstellungen in der Datei „Boot.ini“.

## <a name="syntax"></a>Syntax

```  
bootcfg <parameter> [arguments...]  
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|  
|-------|--------|  
|[bootcfg addsw](bootcfg-addsw.md)|Fügt Optionen für das Laden von Betriebssystemen für einen angegebenen Betriebssystem Eintrag hinzu.|  
|[bootcfg copy](bootcfg-copy.md)|Erstellt eine Kopie eines vorhandenen Start Eintrags, dem Sie Befehlszeilenoptionen hinzufügen können.|  
|[bootcfg dbg1394](bootcfg-dbg1394.md)|Konfiguriert 1394-Port Debugging für einen angegebenen Betriebssystem Eintrag.|  
|[bootcfg debug](bootcfg-debug.md)|Fügt die Debugeinstellungen für einen angegebenen Betriebssystem Eintrag hinzu oder ändert Sie.|  
|[bootcfg default](bootcfg-default.md)|Gibt den Betriebssystem Eintrag an, der als Standard festgelegt werden soll.|  
|[bootcfg delete](bootcfg-delete.md)|Löscht einen Betriebssystem Eintrag im Abschnitt **[Betriebssysteme]** der Datei "Boot. ini".|  
|[bootcfg ems](bootcfg-ems.md)|Ermöglicht es dem Benutzer, die Einstellungen für die Umleitung der Notfall Verwaltungsdienste-Konsole einem Remote Computer hinzuzufügen oder zu ändern.|  
|[bootcfg query](bootcfg-query.md)|Abfragen und Anzeigen der Abschnitts Einträge [Boot Loader] und **[Betriebssysteme]** aus der Datei "Boot. ini".|  
|[bootcfg raw](bootcfg-raw.md)|Fügt einem Betriebssystem Eintrag im Abschnitt **[Betriebssysteme]** der Datei "Boot. ini" die Optionen für das Betriebssystem laden hinzu, die als Zeichenfolge angegeben sind.|  
|[bootcfg rmsw](bootcfg-rmsw.md)|entfernt Optionen für das Laden von Betriebssystemen für einen angegebenen Betriebssystem Eintrag.|  
|[bootcfg timeout](bootcfg-timeout.md)|ändert den Timeout Wert des Betriebssystems.|  
