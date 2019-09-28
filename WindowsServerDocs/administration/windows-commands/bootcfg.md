---
title: bootcfg
description: 'Windows-Befehle-Thema für **bootcfg** : konfiguriert, fragt oder ändert die Datei Einstellungen der Boot. ini-Datei.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3deb354c-5717-4066-bc79-b9323d559e44
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d66296327a2221093e5434f69e15e7c55df1f6b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379851"
---
# <a name="bootcfg"></a>bootcfg

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht das Konfigurieren, Abfragen oder Ändern von Einstellungen in der Datei „Boot.ini“.  
## <a name="syntax"></a>Syntax  
```  
bootcfg <parameter> [arguments...]  
```  
## <a name="parameters"></a>Parameter  
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
