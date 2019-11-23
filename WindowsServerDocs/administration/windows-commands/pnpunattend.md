---
title: pnpunattend
description: Erfahren Sie, wie Sie die Gerätetreiber auf einem Computer überwachen und automatische Treiber Installationen durchführen.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4fa88932-cff0-4dfc-936c-98c0e3dfbeb8 britw
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 77a6ab1ea45322e3c53e8b095c412cf8838be60d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372269"
---
# <a name="pnpunattend"></a>pnpunattend

Überwacht einen Computer auf Gerätetreiber und führt unbeaufsichtigte Treiber Installationen durch oder sucht nach Treibern, ohne zu installieren und optional die Ergebnisse an die Befehlszeile zu melden. Verwenden Sie diesen Befehl, um die Installation bestimmter Treiber für bestimmte Hardware Geräte anzugeben. Siehe Anmerkungen.

## <a name="syntax"></a>Syntax

```
PnPUnattend.exe auditSystem [/help] [/?] [/h] [/s] [/L]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Durchgänge|Gibt die Online Treiberinstallation an.</br>Erforderlich, außer wenn **pnpunattend** entweder mit **/Help** oder **/?** ausgeführt wird Metern.|
|/s|Optional. Gibt an, dass Treiber ohne Installation von gesucht werden sollen.|
|/L|Optional. Gibt an, dass die Protokollinformationen für diesen Befehl an der Eingabeaufforderung angezeigt werden.|
|/?|Optional. Zeigt die Hilfe für diesen Befehl an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Vorläufige Vorbereitung ist erforderlich. Vor der Verwendung dieses Befehls müssen Sie die folgenden Aufgaben ausführen:

1. Erstellen Sie ein Verzeichnis für die Treiber, die Sie installieren möchten. Erstellen Sie z. b. einen Ordner unter **c:\drivers\video** für Grafikkartentreiber.
2. Laden Sie das Treiber Paket für Ihr Gerät herunter, und extrahieren Sie es. Kopieren Sie den Inhalt des unter Ordners, der die INF-Datei für Ihre Version des Betriebssystems enthält, und alle Unterordner in den von Ihnen erstellten Videoordner. Kopieren Sie z. b. die Videotreiber Dateien nach c:\drivers\video.
3. Fügen Sie dem Ordner, den Sie in Schritt 1 erstellt haben, eine System Umgebungs Pfad-Variable hinzu. Beispiel: **c:\drivers\video**.
4. Erstellen Sie den folgenden Registrierungsschlüssel, und legen Sie dann für den von Ihnen erstellten **DriverPath** -Schlüssel die **Wertdaten** auf **1**fest.
5. Navigieren Sie für Windows® 7 in den Registrierungs Pfad: **HKEY_LOCAL_Machine \SOFTWARE\Microsoft\Windows NT\CurrentVersion\\** , und erstellen Sie dann die Schlüssel: **unattendsettings\pnpunattend\driverpath\\**
6. Navigieren Sie für Windows Vista zum Registrierungs Pfad: **HK_LM \SOFTWARE\Microsoft\Windows NT\CurrentVersion\\** , und erstellen Sie dann die Schlüssel = **\unattendsettings\pnpunattend\driverpath**.

## <a name="examples"></a>Beispiele

Der folgende Beispiel Befehl zeigt, wie Sie die Datei " **pnpunattend. exe** " verwenden, um einen Computer auf mögliche Treiber Updates zu überwachen, und dann die Ergebnisse an die Eingabeaufforderung melden.

```
pnpunattend auditsystem /s /l 
```

## <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)