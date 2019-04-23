---
title: Eine andere Version des Windows Admin Center-SDK
description: Eine andere Version des Windows Admin Center-SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 47ae669e517f963762ee6267594e18f3413a72ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833621"
---
# <a name="target-a-different-version-of-the-windows-admin-center-sdk"></a>Eine andere Version des Windows Admin Center-SDK

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Halten die Erweiterung auf dem neuesten Stand mit SDK-Änderungen und Plattform ist einfach.  Wir verwenden [NPM-Tags](https://www.npmjs.com/package/@microsoft/windows-admin-center-sdk) , die Veröffentlichung neuer Features in der SDK-Versionen zu organisieren.

Es gibt drei SDK-Versionen, die, denen Sie auswählen können:

* ```latest``` – Dieses SDK-Paket ausgerichtet, mit der aktuellen GA-Version von Windows Admin Center
* ```insider``` – Dieses SDK-Paket ausgerichtet, mit der aktuellen Preview-Version von Windows Admin Center (verfügbar unter Windows Server Insider Preview)
* ```next``` – Dieses SDK-Paket enthält die neueste Funktionen

> [!NOTE]
> Erfahren Sie mehr über die verschiedenen [Versionen](https://aka.ms/WACDownloadPage) von Windows Admin Center, die zum Herunterladen verfügbar sind.

## <a name="targeting-sdk-version-on-a-new-project"></a>SDK-Zielversion an einem neuen Projekt

Wenn Sie eine neue Erweiterung erstellen zu können, zählen Sie die ```--version``` Parameter, um eine andere Version des SDK verwendet:

```
wac create --company "{!Company Name}" --tool "{!Tool Name}" --version {!version}
```

| Wert | Erläuterung | Beispiel |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | Den Namen Ihres Unternehmens (mit Leerzeichen) | ```Contoso Inc``` |
| ```{!Tool Name}``` | Der Name des Tools (mit Leerzeichen) | ```Manage Foo Works``` |
| ```{!version}``` | SDK-Version | ```latest``` |

Es folgt ein Beispiel, das Erstellen einer neuen Erweiterung als Ziel ```insider```:

```
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version insider
```

## <a name="targeting-sdk-version-on-an-existing-project"></a>SDK-Zielversion in einem vorhandenen Projekt

Um einem vorhandenen Projekt eine andere SDK-Version als Ziel zu ändern, ändern Sie die folgende Zeile in ```package.json```:

```
"@microsoft/windows-admin-center-sdk": "latest",
```
Ersetzen Sie in diesem Beispiel ```latest``` Ihre gewünschte SDK-Version, d. h. ```insider```:

```
"@microsoft/windows-admin-center-sdk": "insider",
```

Führen Sie dann ```npm install``` so aktualisieren Sie Verweise im gesamten Projekt.