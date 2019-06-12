---
title: pnpunattend
description: Erfahren Sie, wie die Gerätetreiber auf einem Computer zu überwachen, als auch automatische Treiber Installationen.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 53b72459d497ac5d079336c2a00ba65634b2e3a6
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436336"
---
# <a name="pnpunattend"></a>pnpunattend

Überwacht, einen Computer für die Gerätetreiber, und führen Sie für die unbeaufsichtigte Installation, oder für Treiber suchen, ohne zu installieren und, optional die Ergebnisse an die Befehlszeile zu melden. Verwenden Sie diesen Befehl, um die Installation von bestimmten Treiber für bestimmte Hardwaregeräte anzugeben. Siehe Anmerkungen.

## <a name="syntax"></a>Syntax

```
PnPUnattend.exe auditSystem [/help] [/?] [/h] [/s] [/L]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|auditSystem|Gibt an, online-Treiber installieren.</br>Erforderlich, außer wenn **Pnpunattend** ausgeführt wird und entweder die **/Help** oder **/?** Parameter.|
|/s|Optional. Gibt an, nach Treibern suchen, ohne zu installieren.|
|/L|Optional. Gibt an, die die Protokollinformationen für diesen Befehl an der Eingabeaufforderung angezeigt.|
|/?|Optional. Zeigt die Hilfe für diesen Befehl an der Eingabeaufforderung.|

## <a name="remarks"></a>Hinweise

Vorbereitung ist erforderlich. Bevor Sie mit diesem Befehl müssen Sie die folgenden Aufgaben ausführen:

1. Erstellen Sie ein Verzeichnis für die Treiber, die Sie installieren möchten. Erstellen Sie z. B. einen Ordner auf **C:\Drivers\Video** für den Grafikkartentreiber.
2. Laden Sie und extrahieren Sie das Treiberpaket für Ihr Gerät. Kopieren Sie den Inhalt des Unterordners, der die INF-Datei für Ihre Version des Betriebssystems enthält sowie auf alle Unterordner, in den video-Ordner, den Sie erstellt haben. Kopieren Sie z. B. die Videotreiber-Dateien, um C:\Drivers\Video.
3. Systemumgebungsvariable Path hinzufügen, zu dem Ordner, die Sie in Schritt 1 z. B. erstellten **C:\Drivers\Video**.
4. Erstellen Sie den folgenden Registrierungsschlüssel, und klicken Sie dann für die **DriverPaths** Schlüssel, die Sie erstellt haben, legen die **Wertdaten** zu **1**.
5. Für Windows® 7 navigieren Sie im Registrierungspfad befinden: **HKEY_LOCAL_Machine\Software\Microsoft\Windows NT\CurrentVersion\\** , und klicken Sie dann die Schlüssel zu erstellen: **UnattendSettings\PnPUnattend\DriverPaths\\**
6. Navigieren Sie für Windows Vista zum Registrierungspfad: **HK_LM\Software\Microsoft\Windows NT\CurrentVersion\\** , und erstellen Sie dann auf die Schlüssel = **\UnattendSettings\PnPUnattend\DriverPaths**.

## <a name="examples"></a>Beispiele

Der Befehl im folgenden Beispiel veranschaulicht, wie die **PNPUnattend.exe** ein Computers für mögliche Treiberupdates überwachen und melden sich die Ergebnisse der Eingabeaufforderung.

```
pnpunattend auditsystem /s /l 
```

## <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)