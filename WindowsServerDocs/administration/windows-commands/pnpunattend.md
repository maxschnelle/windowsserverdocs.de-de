---
title: pnpunattend
description: Erfahren Sie, wie Sie die Gerätetreiber auf einem Computer überwachen und automatische Treiber Installationen durchführen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4fa88932-cff0-4dfc-936c-98c0e3dfbeb8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: e79dd4869a88dc48e579451bfdf2f8fecc55e4f9
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222030"
---
# <a name="pnpunattend"></a>pnpunattend

Überwacht einen Computer auf Gerätetreiber und führt unbeaufsichtigte Treiber Installationen durch oder sucht nach Treibern, ohne zu installieren und optional die Ergebnisse an die Befehlszeile zu melden. Verwenden Sie diesen Befehl, um die Installation bestimmter Treiber für bestimmte Hardware Geräte anzugeben. Siehe Hinweise.

## <a name="syntax"></a>Syntax

```
PnPUnattend.exe auditSystem [/help] [/?] [/h] [/s] [/L]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|auditSystem|Gibt die Online Treiberinstallation an.</br>Erforderlich, außer wenn **pnpunattend** entweder mit **/Help** oder **/?** ausgeführt wird Parameter auf.|
|/s|Dies ist optional. Gibt an, dass Treiber ohne Installation von gesucht werden sollen.|
|/L|Dies ist optional. Gibt an, dass die Protokollinformationen für diesen Befehl an der Eingabeaufforderung angezeigt werden.|
|/?|Dies ist optional. Zeigt die Hilfe für diesen Befehl an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

Vorläufige Vorbereitung ist erforderlich. Vor der Verwendung dieses Befehls müssen Sie die folgenden Aufgaben ausführen:

1. Erstellen Sie ein Verzeichnis für die Treiber, die Sie installieren möchten. Erstellen Sie z. b. einen Ordner unter **c:\drivers\video** für Grafikkartentreiber.
2. Laden Sie das Treiber Paket für Ihr Gerät herunter, und extrahieren Sie es. Kopieren Sie den Inhalt des unter Ordners, der die INF-Datei für Ihre Version des Betriebssystems enthält, und alle Unterordner in den von Ihnen erstellten Videoordner. Kopieren Sie z. b. die Videotreiber Dateien nach c:\drivers\video.
3. Fügen Sie dem Ordner, den Sie in Schritt 1 erstellt haben, eine System Umgebungs Pfad-Variable hinzu. Beispiel: **c:\drivers\video**.
4. Erstellen Sie den folgenden Registrierungsschlüssel, und legen Sie dann für den von Ihnen erstellten **DriverPath** -Schlüssel die **Wertdaten** auf **1**fest.
5. Navigieren Sie für Windows® 7 zum Registrierungs Pfad: **HKEY_LOCAL_Machine \SOFTWARE\Microsoft\Windows NT\CurrentVersion \\ **, und erstellen Sie dann die Schlüssel: **unattendsettings\pnpunattend\driverpath \\ ** .
6. Navigieren Sie für Windows Vista zum Registrierungs Pfad: **HK_LM \SOFTWARE\Microsoft\Windows NT\CurrentVersion \\ **, und erstellen Sie dann die Schlüssel = **\unattendsettings\pnpunattend\driverpath**.

## <a name="examples"></a>Beispiele

Der Befehl zeigt, wie Sie mit der Datei " **pnpunattend. exe** " einen Computer auf mögliche Treiber Updates überwachen und die Ergebnisse dann an die Eingabeaufforderung melden.

```
pnpunattend auditsystem /s /l
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)