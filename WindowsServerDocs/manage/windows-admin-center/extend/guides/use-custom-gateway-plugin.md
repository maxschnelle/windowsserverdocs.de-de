---
title: Verwenden eines benutzerdefinierten Gateway-Plug-Ins in der Tool-Erweiterung
description: 'Entwickeln einer Tool-Erweiterungs Windows Admin Center SDK (Projekt Honolulu): Verwenden eines benutzerdefinierten Gateway-Plug-Ins in der Tool-Erweiterung'
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 4652616478b7b05bde97db48bf84648984b5a325
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296762"
---
# Verwenden eines benutzerdefinierten Gateway-Plug-Ins in der Tool-Erweiterung

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

In diesem Artikel verwenden wir einen benutzerdefinierten Gateway-Plug-in in eine neue, leere Tool-Erweiterung, die wir mit der Windows Admin Center-CLI erstellt haben.

## Vorbereiten der Umgebung ##

Wenn Sie noch nicht geschehen, führen Sie die Anweisungen in [entwickeln eine Tool-Erweiterung](..\develop-tool.md) zum Vorbereiten der Umgebung und zum Erstellen einer neuen, leeren Tool-Erweiterungs.

## Hinzufügen eines Moduls zu Ihrem Projekt ##

Wenn Sie noch nicht geschehen, fügen Sie ein neues [leeres Modul](add-module.md) zu Ihrem Projekt, das wir im nächsten Schritt verwenden.  

## Hinzufügen der Integration, benutzerdefinierten Gateway-Plug-in ##

Jetzt verwenden ein benutzerdefinierten Gateway-Plug-Ins in das neue, leere-Modul wir, die wir gerade erstellt haben.

### Erstellen von plugin.service.ts

Wechseln Sie zum Verzeichnis des oben erstellten neuen Tool Moduls (```\src\app\{!Module-Name}```), und erstellen Sie eine neue Datei ```plugin.service.ts```.

Fügen Sie den folgenden Code, um die soeben erstellte Datei:
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

[!WARNING]
> Es wird empfohlen, die den integrierten ```this.appContextService.node``` dient zum Aufrufen von jeder API, die in Ihrer benutzerdefinierten Gateway-Plug-in definiert ist. Dadurch wird die sichergestellt, wenn Anmeldeinformationen innerhalb Ihrer Gateway-Plug-in erforderlich sind, dass sie ordnungsgemäß behandelt werden.

### Ändern Sie module.ts

Öffnen der ```module.ts``` Datei des zuvor erstellten neuen Moduls (d. h. ```{!Module-Name}.module.ts```):

Fügen Sie die folgenden Import-Anweisungen hinzu:

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

### Ändern Sie component.ts

Öffnen der ```component.ts``` Datei des zuvor erstellten neuen Moduls (d. h. ```{!Module-Name}.component.ts```):

Fügen Sie die folgenden Import-Anweisungen hinzu:

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

Ändern Sie den Konstruktor, und ändern Sie/fügen Sie die folgenden Funktionen:

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

### Ändern Sie component.html ###

Öffnen der ```component.html``` Datei des zuvor erstellten neuen Moduls (d. h. ```{!Module-Name}.component.html```):

Fügen Sie der HTML-Datei den folgenden Inhalt hinzu:
``` html
<button (click)="onClick()" >go</button>
{{ responseResult }}
```

## Build und Seite laden die Erweiterung

Jetzt sind Sie bereit zum [Build und Seite laden](..\develop-tool.md#build-and-side-load-your-extension) die Erweiterung in Windows Admin Center.
