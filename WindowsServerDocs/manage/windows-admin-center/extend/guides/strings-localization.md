---
title: Zeichenfolgen und Lokalisierung in Windows Admin Center
description: Erfahren Sie mehr über die Vorbereitung von Zeichenfolgen für die Lokalisierung in Windows Admin Center-SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: fb328f86c98141a5a2a1c4fd05ec1d4c96a7bc5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845401"
---
# <a name="strings-and-localization-in-windows-admin-center"></a>Zeichenfolgen und Lokalisierung in Windows Admin Center #

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Ich ausführlichere in das Windows Admin Center-Extensions-SDK und sprechen über Zeichenfolgen und Lokalisierung.

Zum Aktivieren der Lokalisierung aller Zeichenfolgen, die auf der Darstellungsebene, nutzen Sie die Datei strings.resjson unter /src/resources/strings - gerendert werden ist es sich bereits eingerichtet. Wenn Sie eine neue Zeichenfolge zu Ihrer Erweiterung hinzufügen möchten, fügen sie als einen neuen Eintrag zu dieser Resjson-Datei hinzu. Die vorhandene Struktur weist das folgende Format:

``` ts
"<YourExtensionName>_<Component>_<Accessor>": "Your string value goes here.",
```

Sie können jedes gewünschte Format für Zeichenfolgen verwenden, aber beachten Sie, dass der Generierungsprozess (der Prozess, die von der Resjson verwendet und gibt die verwendbare TypeScript-Klasse), Unterstrich (_), Punkte (.) konvertiert werden.

Angenommen, dieser Eintrag:
``` ts
"HelloWorld_cim_title": "CIM Component",
```
Wird die folgende Struktur für den Accessor generiert:
``` ts
MsftSme.resourcesStrings<Strings>().HelloWorld.cim.title;
```
