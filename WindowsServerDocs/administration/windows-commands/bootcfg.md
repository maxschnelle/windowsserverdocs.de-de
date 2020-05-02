---
title: bootcfg
description: Referenz Thema für den bootcfg-Befehl, mit dem die Einstellungen der Boot. ini-Datei konfiguriert, abgefragt oder geändert werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3deb354c-5717-4066-bc79-b9323d559e44
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: aca24cfbf47586ae1d7d4262c232be47a056f7ae
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82708865"
---
# <a name="bootcfg"></a>bootcfg

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ermöglicht das Konfigurieren, Abfragen oder Ändern von Einstellungen in der Datei „Boot.ini“.

## <a name="syntax"></a>Syntax

```  
bootcfg <parameter> [arguments...]  
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| [bootcfg addsw](bootcfg-addsw.md) | Fügt Optionen für das Laden von Betriebssystemen für einen angegebenen Betriebssystem Eintrag hinzu. |
| [bootcfg copy](bootcfg-copy.md) | Erstellt eine Kopie eines vorhandenen Start Eintrags, dem Sie Befehlszeilenoptionen hinzufügen können. |
| [bootcfg dbg1394](bootcfg-dbg1394.md) | Konfiguriert 1394-Port Debugging für einen angegebenen Betriebssystem Eintrag. |
| [bootcfg debug](bootcfg-debug.md) | Fügt die Debugeinstellungen für einen angegebenen Betriebssystem Eintrag hinzu oder ändert Sie. |
| [bootcfg default](bootcfg-default.md) | Gibt den Betriebssystem Eintrag an, der als Standard festgelegt werden soll. |
| [bootcfg delete](bootcfg-delete.md) | Löscht einen Betriebssystem Eintrag im Abschnitt [Betriebssysteme] der Datei "Boot. ini". |
| [bootcfg ems](bootcfg-ems.md) | Ermöglicht es dem Benutzer, die Einstellungen für die Umleitung der Notfall Verwaltungsdienste-Konsole einem Remote Computer hinzuzufügen oder zu ändern. |
| [bootcfg query](bootcfg-query.md) | Abfragen und Anzeigen der Abschnitts Einträge [Boot Loader] und [Betriebssysteme] aus der Datei "Boot. ini". |
| [bootcfg raw](bootcfg-raw.md) | Fügt einem Betriebssystem Eintrag im Abschnitt [Betriebssysteme] der Datei "Boot. ini" die Optionen für das Betriebssystem laden hinzu, die als Zeichenfolge angegeben sind. |
| [bootcfg rmsw](bootcfg-rmsw.md) | Entfernt Optionen für das Laden von Betriebssystemen für einen angegebenen Betriebssystem Eintrag. |
| [bootcfg timeout](bootcfg-timeout.md) | Ändert den Timeout Wert des Betriebssystems. |
