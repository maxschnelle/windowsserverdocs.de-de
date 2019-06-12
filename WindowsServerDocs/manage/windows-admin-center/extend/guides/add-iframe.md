---
title: Hinzufügen eines iFrames zu einer Tool-Erweiterung
description: Entwickeln Sie eine toolerweiterung Windows Admin Center-SDK (Projekt Honolulu) – iFrame ein Tools-Erweiterung hinzufügen
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: da3850b75a0e069f9153d3c66baef9f00b67d61c
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66452587"
---
# <a name="add-an-iframe-to-a-tool-extension"></a>Hinzufügen eines iFrames zu einer Tool-Erweiterung

>Gilt für: Windows Admin Center, Windows Admin Center Preview

In diesem Artikel werden wir einen iFrame zu einer neuen, leeren Tools-Erweiterung hinzufügen, die wir mit der Windows Admin Center-CLI erstellt haben.

## <a name="prepare-your-environment"></a>Vorbereiten der Umgebung ##

Wenn Sie nicht bereits getan haben, befolgen Sie die Anweisungen [Entwickeln einer toolerweiterung](../develop-tool.md) zum Vorbereiten der Umgebung, und erstellen Sie eine neue, leere toolerweiterung.

## <a name="add-a-module-to-your-project"></a>Fügen Sie ein Modul zu Ihrem Projekt ##

Fügen Sie einen neuen [leeres Modul](add-module.md) zu Ihrem Projekt, dem wir einen iFrame im nächsten Schritt hinzufügen.  

## <a name="add-an-iframe-to-your-module"></a>Fügen Sie einen iFrame Ihrem Modul ##

Jetzt fügen einen iFrame für das neue, leere Modul wir, die wir gerade erstellt haben.

In \src\app\, navigieren Sie zu Ihrem Ordner "Module", und öffnen Sie die Datei ```{!module-name}.component.html```, die sich mit der folgenden Benennungskonvention:

| Wert | Erläuterung | Beispiel-Dateiname |
| ----- | ----------- | ------- |
| ```{!module-name}``` | Ihre Modulnamen (Kleinbuchstabe, Leerzeichen ersetzt, die mit Bindestrichen) | ```manage-foo-works-portal.component.html``` |
    
Fügen Sie der HTML-Datei den folgenden Inhalt hinzu:

``` html
<div>
  <iframe  style="height: 850px;" src="https://www.bing.com"></iframe>
</div>
```

Das war alles, Sie haben die Erweiterung ein IFRAMES hinzugefügt.  Als Nächstes können Sie [erstellen und die Seite laden](../develop-tool.md#build-and-side-load-your-extension) Ihre Erweiterung in Windows Admin Center, um die Ergebnisse anzuzeigen.

> [!Note]
> Inhaltseinstellungen für den (Security Policy, CSP) konnten einige Standorte Rendern in einen iFrame auf Windows Admin Center zu verhindern, dass. Erfahren Sie mehr über den [hier](https://content-security-policy.com/). 
