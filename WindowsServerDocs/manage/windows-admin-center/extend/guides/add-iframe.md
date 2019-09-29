---
title: Hinzufügen eines iFrames zu einer Tool-Erweiterung
description: 'Entwickeln einer Tool Erweiterung Windows Admin Center SDK (Project Honolulu): Hinzufügen eines IFRAMEs zu einer Tool Erweiterung'
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 0833b2fd92f2bf4b512120783bb71295a3112745
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406898"
---
# <a name="add-an-iframe-to-a-tool-extension"></a>Hinzufügen eines iFrames zu einer Tool-Erweiterung

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

In diesem Artikel wird ein IFRAME zu einer neuen, leeren Tool Erweiterung hinzugefügt, die mit der Windows Admin Center CLI erstellt wurde.

## <a name="prepare-your-environment"></a>Vorbereiten der Umgebung ##

Wenn Sie dies noch nicht getan haben, befolgen Sie die Anweisungen unter [Entwickeln einer Tool Erweiterung](../develop-tool.md) , um die Umgebung vorzubereiten und eine neue, leere Tool Erweiterung zu erstellen.

## <a name="add-a-module-to-your-project"></a>Hinzufügen eines Moduls zum Projekt ##

Fügen Sie dem Projekt ein neues [leeres Modul](add-module.md) hinzu, dem im nächsten Schritt ein IFRAME hinzugefügt wird.  

## <a name="add-an-iframe-to-your-module"></a>Hinzufügen eines IFRAMEs zum Modul ##

Nun fügen wir diesem neuen, leeren Modul, das wir soeben erstellt haben, ein IFRAME hinzu.

Navigieren Sie in "\src\app @ no__t-0" zum Modul Ordner, und öffnen Sie dann die Datei ```{!module-name}.component.html``` mit der folgenden Benennungs Konvention:

| Wert | Erläuterung | Beispiel-Dateiname |
| ----- | ----------- | ------- |
| ```{!module-name}``` | Ihre Modulnamen (Kleinbuchstabe, Leerzeichen ersetzt, die mit Bindestrichen) | ```manage-foo-works-portal.component.html``` |
    
Fügen Sie der HTML-Datei den folgenden Inhalt hinzu:

``` html
<div>
  <iframe  style="height: 850px;" src="https://www.bing.com"></iframe>
</div>
```

Sie haben der Erweiterung einen iframe hinzugefügt.  Als nächstes können Sie Ihre Erweiterung im Windows Admin Center [Erstellen und](../develop-tool.md#build-and-side-load-your-extension) auslagern, um die Ergebnisse anzuzeigen.

> [!Note]
> Die Einstellungen der Content Security Policy (CSP) könnten verhindern, dass einige Websites in einem IFRAME innerhalb des Windows Admin Centers gerendert werden. Weitere Informationen hierzu finden Sie [hier](https://content-security-policy.com/). 
