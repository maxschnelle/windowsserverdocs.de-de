---
title: Zeichenfolgen und Lokalisierung in Windows Admin Center
description: Erfahren Sie mehr über das Vorbereiten der Zeichenfolgen für die Lokalisierung in Windows Admin Center SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: f0671160bd790d80e35f6d6c1586a07969939070
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296732"
---
# Zeichenfolgen und Lokalisierung in Windows Admin Center #

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

In Windows Admin Center-Erweiterungen SDK gehen Sie wir ausführlicheren und Zeichenfolgen und Lokalisierung beschäftigen.

Zum Aktivieren der Lokalisierung aller Zeichenfolgen, die auf die Darstellungsschicht, profitieren Sie von der strings.resjson-Datei unter /src/resources/strings - gerendert werden ist bereits einrichten. Wenn Sie eine neue Zeichenfolge zur Erweiterung hinzufügen müssen, fügen sie für diese Resjson-Datei als einen neuen Eintrag hinzu. Die vorhandene Struktur gilt Folgendes Format:

``` ts
"<YourExtensionName>_<Component>_<Accessor>": "Your string value goes here.",
```

Sie können ein beliebiges Format aus, den Sie für die Zeichenfolgen verwenden, aber beachten Sie, dass der Generation Prozess (der Prozess, der bildinhaltpipeline werden die Resjson und die verwendbare TypeScript-Klasse) Unterstrich (_), Punkte (.) konvertiert.

Beispielsweise wird dieser Eintrag:
``` ts
"HelloWorld_cim_title": "CIM Component",
```
Wird die folgende Accessor-Struktur:
``` ts
MsftSme.resourcesStrings<Strings>().HelloWorld.cim.title;
```

## Weitere Sprachen für die Lokalisierung hinzufügen ## 

Für die Lokalisierung für andere Sprachen muss eine strings.resjson-Datei für jede Sprache erstellt werden. Diese Dateien müssen stellen in ```\loc\output\{!ExtensionName}\{!LanguageFolder}\strings.resjson```. Die verfügbaren Sprachen mit entsprechenden Ordnern sind:

| Sprache      | Ordner      |
| ------------- |-------------|
| Čeština | cs-CZ |
| Deutsch | de-DE |
| Englisch | en-US |
| Spanisch | es-ES |
| Français | fr-FR | 
| Magyar | hu-HU | 
| Italiano | it-IT |
| 日本語 | ja-JP | 
| 한국어 | ko-KR | 
| Niederlande | nl-NL |
| Polski | pl-PL |
| Português (Brasil) | pt-BR |
| Português (Portugal) | pt-PT |
| РУССКИЙ | ru-RU |
| Svenska | sv-SE |
| Türkçe    | tr-TR |
| 中文(简体) | zh-CN |
| 中文(繁體) | zh-TW |
> [!NOTE]
> Wenn Ihre Datei Struktur Anforderungen unterschiedliche innerhalb der Loc-Ausgabe sind, müssen Sie die LocaleOffset für die schlucken dienen Aufgabe "generieren Resjson-Json-lokalisierten" anpassen, die in der gulpfile.js ist. Dieser Offset ist wie tief in den Loc-Ordner, die Suche nach strings.resjson Dateien gestartet werden soll.

Jede Datei strings.resjson wird auf die gleiche Weise wie bereits erwähnt, am Anfang dieses Handbuchs formatiert sein. 

Eine Lokalisierung für Spanisch enthalten z. B. enthalten diesen Eintrag in ```\loc\output\HelloWorld\es-ES\strings.resjson```: 
```json
"HelloWorld_cim_title": "CIM Componente",
```
Anytime, dass Sie die lokalisierte Zeichenfolgen hinzugefügt, schlucken dienen generieren muss erneut ausgeführt werden, um diese angezeigt werden. Führen Sie Folgendes aus:
``` cmd
gulp generate 
```

Um sicherzustellen, dass Ihre Zeichenfolgen generiert wurden navigieren Sie zu ```\src\app\assets\strings\{!LanguageFolder}\strings.resjson```. Die neu hinzugefügte Eintrag wird in dieser Datei angezeigt.
Nun, wenn Sie die Option "Sprache" im Windows Admin Center wechseln, werden Sie die lokalisierten Zeichenfolgen in der Erweiterung zu sehen sein. 
