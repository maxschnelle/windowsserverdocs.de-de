---
title: Fügen Sie iFrame hinzu, um eine Tool-Erweiterung
description: 'Entwickeln Sie eine Tool-Erweiterung Windows Admin Center SDK (Projekt Honolulu): Hinzufügen von iFrame zu einer Tool-Erweiterung'
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 7b4a7b688e4b2d9f52e44395c19211b91b964578
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/20/2018
ms.locfileid: "4080927"
---
# Fügen Sie iFrame hinzu, um eine Tool-Erweiterung

>Gilt für: Windows Admin Center, Windows Admin Center Preview

In diesem Artikel werden wir eine neue, leere Tool-Erweiterung iFrame hinzufügen, die wir mit der Windows Admin Center-CLI erstellt haben.

## Vorbereiten der Umgebung ##

Wenn Sie noch nicht geschehen, führen Sie die Anweisungen in [eine Tool-Erweiterung entwickeln](..\develop-tool.md) , zum Vorbereiten der Umgebung und zum Erstellen einer neuen, leeren Tool-Erweiterungs.

## Fügen Sie dem Projekt ein Modul ##

Fügen Sie ein neues [leeres Modul](add-module.md) zu Ihrem Projekt, das wir iFrame im nächsten Schritt hinzugefügt wird.  

## IFrame Ihrem Modul hinzufügen ##

Jetzt werden wir einen iFrame für dieses Modul neue, leere hinzufügen, die wir gerade erstellt haben.

In \src\app\, navigieren Sie in den Modulordner aus, und öffnen Sie die Datei ```{!module-name}.component.html```mit folgender Namenskonvention:

| Wert | Erläuterung | Beispiel-Dateiname |
| ----- | ----------- | ------- |
| ```{!module-name}``` | Ihre Modulnamen (Kleinbuchstabe, Leerzeichen ersetzt, die mit Bindestrichen) | ```manage-foo-works-portal.component.html``` |
    
Fügen Sie der HTML-Datei den folgenden Inhalt hinzu:

``` html
<div>
  <iframe  style="height: 850px;" src="https://www.bing.com"></iframe>
</div>
```

Das war's, Sie haben die Erweiterung iFrame hinzugefügt.  Als Nächstes können Sie [Build und Seite laden](..\develop-tool.md#build-and-side-load-your-extension) die Erweiterung in Windows Admin Center, um die Ergebnisse anzuzeigen.
