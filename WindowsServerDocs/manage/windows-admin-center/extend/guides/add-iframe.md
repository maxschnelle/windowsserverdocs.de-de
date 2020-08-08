---
title: Hinzufügen eines iFrames zu einer Toolerweiterung
description: 'Entwickeln einer Tool Erweiterung Windows Admin Center SDK (Project Honolulu): Hinzufügen eines IFRAMEs zu einer Tool Erweiterung'
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: da145d4ef3a58af51846d395081fb643af7c78ac
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87945107"
---
# <a name="add-an-iframe-to-a-tool-extension"></a>Hinzufügen eines iFrames zu einer Toolerweiterung

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

In diesem Artikel wird ein IFRAME zu einer neuen, leeren Tool Erweiterung hinzugefügt, die mit der Windows Admin Center CLI erstellt wurde.

## <a name="prepare-your-environment"></a>Vorbereiten der Umgebung ##

Wenn Sie dies noch nicht getan haben, befolgen Sie die Anweisungen unter [Entwickeln einer Tool Erweiterung](../develop-tool.md) , um die Umgebung vorzubereiten und eine neue, leere Tool Erweiterung zu erstellen.

## <a name="add-a-module-to-your-project"></a>Hinzufügen eines Moduls zum Projekt ##

Fügen Sie dem Projekt ein neues [leeres Modul](add-module.md) hinzu, dem im nächsten Schritt ein IFRAME hinzugefügt wird.

## <a name="add-an-iframe-to-your-module"></a>Hinzufügen eines IFRAMEs zum Modul ##

Nun fügen wir diesem neuen, leeren Modul, das wir soeben erstellt haben, ein IFRAME hinzu.

Navigieren Sie in \src\app \, zum Ordner "Module", und öffnen Sie dann ```{!module-name}.component.html``` die Datei mit der folgenden Benennungs Konvention:

| Wert | Erklärung | Beispiel Dateiname |
| ----- | ----------- | ------- |
| ```{!module-name}``` | Der Modulname (in Kleinbuchstaben, Leerzeichen durch Bindestriche ersetzt) | ```manage-foo-works-portal.component.html``` |

Fügen Sie der HTML-Datei den folgenden Inhalt hinzu:

``` html
<div>
  <iframe  style="height: 850px;" src="https://www.bing.com"></iframe>
</div>
```

Sie haben der Erweiterung einen iframe hinzugefügt.  Als nächstes können Sie Ihre Erweiterung im Windows Admin Center [Erstellen und](../develop-tool.md#build-and-side-load-your-extension) auslagern, um die Ergebnisse anzuzeigen.

> [!Note]
> Die Einstellungen der Content Security Policy (CSP) könnten verhindern, dass einige Websites in einem IFRAME innerhalb des Windows Admin Centers gerendert werden. Weitere Informationen hierzu finden Sie [hier](https://content-security-policy.com/).
