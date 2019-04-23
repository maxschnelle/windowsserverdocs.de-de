---
title: bootcfg
description: 'Windows-Befehle Thema **Bootcfg** : konfiguriert, Abfragen oder ändert die Einstellungen der Datei "Boot.ini".'
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 79a1c0e22a3b162ba9492c80d114b2d5b943c744
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867021"
---
# <a name="bootcfg"></a>bootcfg

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Ermöglicht das Konfigurieren, Abfragen oder Ändern von Einstellungen in der Datei „Boot.ini“.  
## <a name="syntax"></a>Syntax  
```  
bootcfg <parameter> [arguments...]  
```  
## <a name="parameters"></a>Parameter  
|Parameter|Beschreibung|  
|-------|--------|  
|[BOOTCFG addsw](bootcfg-addsw.md)|Fügt Betriebssystem Ladeoptionen für einen angegebenen Betriebssystem-Eintrag hinzu.|  
|[BOOTCFG kopieren](bootcfg-copy.md)|Erstellt eine Kopie eines vorhandenen Starteintrags, zu dem Sie Befehlszeilenoptionen hinzufügen können.|  
|[bootcfg dbg1394](bootcfg-dbg1394.md)|Konfiguriert die 1394 Port für einen bestimmten Betriebssystemeintrag Debuggen.|  
|[BOOTCFG Debuggen](bootcfg-debug.md)|Hinzufügen oder Ändern der Einstellungen zum Debuggen für einen bestimmten Betriebssystemeintrag.|  
|[BOOTCFG Standard](bootcfg-default.md)|Gibt den Betriebssystemeintrag als Standard festgelegt werden soll.|  
|[BOOTCFG löschen](bootcfg-delete.md)|Löscht einen Betriebssystem-Eintrag in der **[Betriebssysteme]** -Abschnitt der Datei "Boot.ini".|  
|[BOOTCFG ems](bootcfg-ems.md)|Ermöglicht es dem Benutzer hinzufügen oder ändern die Einstellungen für die Umleitung der Emergency Management Services-Konsole mit einem Remotecomputer aus.|  
|[bootcfg query](bootcfg-query.md)|Fragt ab und zeigt das [Startladeprogramm] und **[Betriebssysteme]** Abschnitt Einträge aus der Datei "Boot.ini".|  
|[unformatierte bootcfg](bootcfg-raw.md)|Fügt der Betriebssystem-Ladeoptionen angegeben werden, als eine Zeichenfolge, die ein Betriebssystem-Eintrag in der **[Betriebssysteme]** -Abschnitt der Datei "Boot.ini".|  
|[BOOTCFG rmsw](bootcfg-rmsw.md)|Optionen zum Laden von Betriebssystem für einen angegebenen Betriebssystem-Eintrag wird entfernt.|  
|[Bootcfg-timeout](bootcfg-timeout.md)|Ändert den Betriebssystem-Timeout-Wert.|  
