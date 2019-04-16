---
title: Eine andere Version von Windows Admin Center SDK
description: Eine andere Version von Windows Admin Center SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 47ae669e517f963762ee6267594e18f3413a72ff
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081037"
---
# Eine andere Version von Windows Admin Center SDK

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Halten die Erweiterung auf dem neuesten Stand mit SDK-Änderungen und Plattform Änderungen ist einfach.  Wir verwenden [NPM-Tags](https://www.npmjs.com/package/@microsoft/windows-admin-center-sdk) , um die Version der neuen Features in SDK-Versionen zu organisieren.

Es gibt drei SDK-Versionen, die, denen Sie auswählen können:

* ```latest``` – Dieser SDK-Paket richtet, mit der aktuellen GA-Version von Windows Admin Center
* ```insider``` – Dieser SDK-Paket für die aktuelle Preview-Version von Windows Admin Center (verfügbar unter Windows Server Insider Preview) ausgerichtet
* ```next``` – Dieser SDK-Paket enthält die neueste Funktionen

> [!NOTE]
> Erfahren Sie mehr über die verschiedenen [Versionen](https://aka.ms/WACDownloadPage) von Windows Admin Center, die heruntergeladen werden.

## Als Ziel die SDK-Version auf ein neues Projekt

Wenn Sie eine neue Erweiterung zu erstellen, können Sie enthalten die ```--version``` Parameter, um eine andere Version des SDKS abzielen:

```
wac create --company "{!Company Name}" --tool "{!Tool Name}" --version {!version}
```

| Wert | Erläuterung | Beispiel |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | Den Namen Ihres Unternehmens (mit Leerzeichen) | ```Contoso Inc``` |
| ```{!Tool Name}``` | Der Name des Tools (mit Leerzeichen) | ```Manage Foo Works``` |
| ```{!version}``` | SDK-Version | ```latest``` |

Hier ist ein Beispiel erstellen eine neue Erweiterung Zielgruppenadressierung ```insider```:

```
wac create --company "Contoso Inc" --tool "Manage Foo Works" --version insider
```

## Als Ziel die SDK-Version auf einem vorhandenen Projekt

Um ein vorhandenes Projekt zu eine andere SDK-Version als Ziel zu ändern, ändern Sie die folgende Zeile in ```package.json```:

```
"@microsoft/windows-admin-center-sdk": "latest",
```
Ersetzen Sie in diesem Beispiel ```latest``` mit der gewünschten SDK-Version, d. h. ```insider```:

```
"@microsoft/windows-admin-center-sdk": "insider",
```

Führen Sie ```npm install``` Verweise in Ihr Projekt aktualisieren.