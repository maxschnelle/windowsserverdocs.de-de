---
title: bootcfg
description: Referenz Artikel für den bootcfg-Befehl, mit dem Boot.ini Datei Einstellungen konfiguriert, abgefragt oder geändert werden.
ms.topic: article
ms.assetid: 3deb354c-5717-4066-bc79-b9323d559e44
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: edab8bc0b4e63544282e53f0a7b6e1fc255a4be7
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880525"
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
| [bootcfg delete](bootcfg-delete.md) | Löscht einen Betriebssystem Eintrag im Abschnitt [Betriebssysteme] der Boot.ini Datei. |
| [bootcfg ems](bootcfg-ems.md) | Ermöglicht es dem Benutzer, die Einstellungen für die Umleitung der Notfall Verwaltungsdienste-Konsole einem Remote Computer hinzuzufügen oder zu ändern. |
| [bootcfg query](bootcfg-query.md) | Hiermit werden die Abschnitts Einträge [Boot Loader] und [Betriebssysteme] aus Boot.ini abgefragt und angezeigt. |
| [bootcfg raw](bootcfg-raw.md) | Fügt einem Betriebssystem Eintrag im Abschnitt [Betriebssysteme] der Boot.ini Datei die als Zeichenfolge angegebenen Betriebssystem-Lade Optionen hinzu. |
| [bootcfg rmsw](bootcfg-rmsw.md) | Entfernt Optionen für das Laden von Betriebssystemen für einen angegebenen Betriebssystem Eintrag. |
| [bootcfg timeout](bootcfg-timeout.md) | Ändert den Timeout Wert des Betriebssystems. |
