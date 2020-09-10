---
title: pnpunattend
description: Referenz Artikel für den pnpunattend-Befehl, mit dem die Gerätetreiber auf einem Computer überwacht werden und automatische Treiber Installationen durchführt werden.
ms.topic: reference
ms.assetid: 4fa88932-cff0-4dfc-936c-98c0e3dfbeb8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: 6e3e0f0dfd1b689a62bf59956d3934e5ea74d177
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89633675"
---
# <a name="pnpunattend"></a>pnpunattend

Überwacht einen Computer auf Gerätetreiber und führt unbeaufsichtigte Treiber Installationen durch oder sucht nach Treibern, ohne zu installieren und optional die Ergebnisse an die Befehlszeile zu melden. Verwenden Sie diesen Befehl, um die Installation bestimmter Treiber für bestimmte Hardware Geräte anzugeben.

## <a name="prerequisites"></a>Voraussetzungen

Eine vorläufige Vorbereitung ist für ältere Versionen des Windows-Betriebssystems erforderlich. Vor der Verwendung dieses Befehls müssen Sie die folgenden Aufgaben ausführen:

1. Erstellen Sie ein Verzeichnis für die Treiber, die Sie installieren möchten. Erstellen Sie z. b. einen Ordner unter **c:\drivers\video** für Grafikkartentreiber.

2. Laden Sie das Treiber Paket für Ihr Gerät herunter, und extrahieren Sie es. Kopieren Sie den Inhalt des unter Ordners, der die INF-Datei für Ihre Version des Betriebssystems enthält, und alle Unterordner in den von Ihnen erstellten Videoordner. Kopieren Sie z. b. die Videotreiber Dateien nach **c:\drivers\video**.

3. Fügen Sie dem Ordner, den Sie in Schritt 1 erstellt haben, eine System Umgebungs Pfad-Variable hinzu. Beispiel: **c:\drivers\video**.

4. Erstellen Sie den folgenden Registrierungsschlüssel, und legen Sie dann für den von Ihnen erstellten **DriverPath** -Schlüssel die **Wertdaten** auf **1**fest.

5. Navigieren Sie für Windows® 7 zum Registrierungs Pfad: **HKEY_LOCAL_Machine \SOFTWARE\Microsoft\Windows NT\CurrentVersion \\ **, und erstellen Sie dann die Schlüssel: **unattendsettings\pnpunattend\driverpath \\ ** .

## <a name="syntax"></a>Syntax

```
PnPUnattend.exe auditsystem [/help] [/?] [/h] [/s] [/l]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| Durchgänge | Gibt die Online Treiberinstallation an.<p>Erforderlich, es sei denn, dieser Befehl wird entweder mit **/help** dem/Help **-oder/?-** Befehl ausgeführt. Parameter auf. |
| /s | (Optional) Gibt an, dass Treiber ohne Installation von gesucht werden sollen. |
| /l | (Optional) Gibt an, dass die Protokollinformationen für diesen Befehl an der Eingabeaufforderung angezeigt werden. |
| `/? | /help` | (Optional) Zeigt die Hilfe für diesen Befehl an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

Der Befehl zeigt, wie Sie mithilfe der **PNPUnattend.exe** einen Computer auf mögliche Treiber Updates überwachen und die Ergebnisse an der Eingabeaufforderung melden, indem Sie Folgendes eingeben:

```
pnpunattend auditsystem /s /l
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
