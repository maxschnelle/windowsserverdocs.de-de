---
title: Verwenden eines benutzerdefinierten Gateway-Plug-Ins in der Tool-Erweiterung
description: Entwickeln Sie eine toolerweiterung Windows Admin Center-SDK (Projekt Honolulu) – verwenden Sie ein benutzerdefiniertes Gateway-Plug-in in Ihre toolerweiterung
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: c9b2e9201d58472286b42a9c89a36423f40d143d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834511"
---
# <a name="use-a-custom-gateway-plugin-in-your-tool-extension"></a>Verwenden eines benutzerdefinierten Gateway-Plug-Ins in der Tool-Erweiterung

>Gilt für: Windows Admin Center, Windows Admin Center Preview

In diesem Artikel verwenden wir ein benutzerdefiniertes Gateway-Plug-in in einer neuen, leeren Tools-Erweiterung, die wir mit der Windows Admin Center-CLI erstellt haben.

## <a name="prepare-your-environment"></a>Vorbereiten der Umgebung ##

Wenn Sie nicht bereits getan haben, befolgen Sie die Anweisungen [Entwickeln einer toolerweiterung](..\develop-tool.md) zum Vorbereiten der Umgebung, und erstellen Sie eine neue, leere toolerweiterung.

## <a name="add-a-module-to-your-project"></a>Fügen Sie ein Modul zu Ihrem Projekt ##

Wenn Sie nicht bereits getan haben, fügen Sie einen neuen [leeres Modul](add-module.md) zu Ihrem Projekt, die wir im nächsten Schritt verwenden.  

## <a name="add-integration-to-custom-gateway-plugin"></a>Integration benutzerdefiniertes Gateway-Plug-In hinzufügen ##

Jetzt verwenden wir ein benutzerdefiniertes Gateway-Plug-in in das neue, leere-Modul, die wir gerade erstellt haben.

### <a name="create-pluginservicets"></a>Erstellen von plugin.service.ts

Wechseln Sie zum Verzeichnis des oben erstellten neuen Tool-Moduls (```\src\app\{!Module-Name}```), und erstellen Sie eine neue Datei ```plugin.service.ts```.

Fügen Sie den folgenden Code in die Datei, die gerade erstellt haben:
``` ts
import { Injectable } from '@angular/core';
import { AppContextService, HttpService } from '@microsoft/windows-admin-center-sdk/angular';
import { Cim, Http, PowerShell, PowerShellSession } from '@microsoft/windows-admin-center-sdk/core';
import { AjaxResponse, Observable } from 'rxjs';

@Injectable()
export class PluginService {
    constructor(private appContextService: AppContextService, private http: Http) {
    }
    
    public getGatewayRestResponse(): Observable<any> {
        let callUrl = this.appContextService.activeConnection.nodeName;

        return this.appContextService.node.get(callUrl, 'features/Sample%20Uno').map(
            (response: any) => {
                return response;
            }
        )
    }
}
```

Ändern Sie Verweise auf ```Sample Uno``` und ```Sample%20Uno``` Ihre Namen Features nach Bedarf.

### <a name="modify-modulets"></a>Module.ts ändern

Öffnen der ```module.ts``` Datei mit dem neuen Modul, das zuvor erstellt haben (d. h. ```{!Module-Name}.module.ts```):

Fügen Sie die folgenden importanweisungen hinzu:

``` ts
import { HttpService } from '@microsoft/windows-admin-center-sdk/angular';
import { Http } from '@microsoft/windows-admin-center-sdk/core';
import { PluginService } from './plugin.service';
```

Fügen Sie die folgenden Anbieter (nach Deklarationen):

``` ts
  ,
  providers: [
    HttpService,
    PluginService,
    Http
  ]
```

### <a name="modify-componentts"></a>Component.ts ändern

Öffnen der ```component.ts``` Datei mit dem neuen Modul, das zuvor erstellt haben (d. h. ```{!Module-Name}.component.ts```):

Fügen Sie die folgenden importanweisungen hinzu:

``` ts
import { ActivatedRouteSnapshot } from '@angular/router';
import { AppContextService } from '@microsoft/windows-admin-center-sdk/angular';
import { Subscription } from 'rxjs';
import { Strings } from '../../generated/strings';
import { PluginService } from './plugin.service';
```

Fügen Sie die folgenden Variablen hinzu:

``` ts
  private serviceSubscription: Subscription;
  private responseResult: string;
```

Ändern Sie den Konstruktor und fügen Sie die folgenden Funktionen ändern hinzu /:

``` ts
  constructor(private appContextService: AppContextService, private plugin: PluginService) {
    //
  }

  public ngOnInit() {
    this.responseResult = 'click go to do something';
  }

  public onClick() {
    this.serviceSubscription = this.plugin.getGatewayRestResponse().subscribe(
      (response: any) => {
        this.responseResult = 'response: ' + response.message;
      },
      (error) => {
        console.log(error);
      }
    );
  }
```

### <a name="modify-componenthtml"></a>Component.html ändern ###

Öffnen der ```component.html``` Datei mit dem neuen Modul, das zuvor erstellt haben (d. h. ```{!Module-Name}.component.html```):

Fügen Sie der HTML-Datei den folgenden Inhalt hinzu:
``` html
<button (click)="onClick()" >go</button>
{{ responseResult }}
```

## <a name="build-and-side-load-your-extension"></a>Erstellen und die Seite laden die Erweiterung

Nun können Sie auf [erstellen und die Seite laden](..\develop-tool.md#build-and-side-load-your-extension) Ihre Erweiterung in Windows Admin Center.
