---
title: Verwenden eines benutzerdefinierten Gateway-Plug-Ins in der Tool-Erweiterung
description: 'Entwickeln einer Tool Erweiterung Windows Admin Center SDK (Project Honolulu): Verwenden eines benutzerdefinierten Gateway-Plug-ins in ihrer Tool Erweiterung'
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 5bcaaa452a2b42a54cbc3b1d8f9a296504054e34
ms.sourcegitcommit: 20d07170c7f3094c2fb4455f54b13ec4b102f2d7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/13/2020
ms.locfileid: "81269227"
---
# <a name="use-a-custom-gateway-plugin-in-your-tool-extension"></a>Verwenden eines benutzerdefinierten Gateway-Plug-Ins in der Tool-Erweiterung

>Gilt für: Windows Admin Center, Windows Admin Center Vorschau

In diesem Artikel wird ein benutzerdefiniertes Gateway-Plug-in in einer neuen, leeren Tool Erweiterung verwendet, die wir mit der Windows Admin Center-CLI erstellt haben.

## <a name="prepare-your-environment"></a>Vorbereiten der Umgebung ##

Wenn Sie dies noch nicht getan haben, befolgen Sie die Anweisungen unter [Entwickeln einer Tool Erweiterung](../develop-tool.md) , um die Umgebung vorzubereiten und eine neue, leere Tool Erweiterung zu erstellen.

## <a name="add-a-module-to-your-project"></a>Hinzufügen eines Moduls zum Projekt ##

Wenn Sie dies noch nicht getan haben, fügen Sie Ihrem Projekt ein neues [leeres Modul](add-module.md) hinzu, das wir im nächsten Schritt verwenden werden.  

## <a name="add-integration-to-custom-gateway-plugin"></a>Integration zum benutzerdefinierten Gateway-Plug-in ##

Nun verwenden wir ein benutzerdefiniertes Gateway-Plug-in für das neue, leere Modul, das wir soeben erstellt haben.

### <a name="create-pluginservicets"></a>Erstellen von Plug-in. Service. TS

Wechseln Sie in das Verzeichnis des oben erstellten neuen Tool Moduls (```\src\app\{!Module-Name}```), und erstellen Sie eine neue Datei ```plugin.service.ts```.

Fügen Sie der soeben erstellten Datei den folgenden Code hinzu:
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

Ändern Sie die Verweise auf ```Sample Uno```, und ```Sample%20Uno``` Sie nach Bedarf auf den Funktionsnamen.

> [!WARNING]
> Es wird empfohlen, die integrierte ```this.appContextService.node``` zum Aufrufen einer API zu verwenden, die in Ihrem benutzerdefinierten Gateway-Plug-in definiert ist. Dadurch wird sichergestellt, dass, wenn Anmelde Informationen in Ihrem Gateway-Plug-in erforderlich sind, diese ordnungsgemäß verarbeitet werden.

### <a name="modify-modulets"></a>Modify Module. TS

Öffnen Sie die ```module.ts``` Datei des neuen Moduls, das Sie zuvor erstellt haben (d. h. ```{!Module-Name}.module.ts```):

Fügen Sie die folgenden Import-Anweisungen hinzu:

``` ts
import { HttpService } from '@microsoft/windows-admin-center-sdk/angular';
import { Http } from '@microsoft/windows-admin-center-sdk/core';
import { PluginService } from './plugin.service';
```

Fügen Sie die folgenden Anbieter hinzu (nach Deklarationen):

``` ts
  ,
  providers: [
    HttpService,
    PluginService,
    Http
  ]
```

### <a name="modify-componentts"></a>Component. TS ändern

Öffnen Sie die ```component.ts``` Datei des neuen Moduls, das Sie zuvor erstellt haben (d. h. ```{!Module-Name}.component.ts```):

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

Ändern Sie den Konstruktor, und ändern Sie die folgenden Funktionen:

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

### <a name="modify-componenthtml"></a>Component. HTML ändern ###

Öffnen Sie die ```component.html``` Datei des neuen Moduls, das Sie zuvor erstellt haben (d. h. ```{!Module-Name}.component.html```):

Fügen Sie der HTML-Datei den folgenden Inhalt hinzu:
``` html
<button (click)="onClick()" >go</button>
{{ responseResult }}
```

## <a name="build-and-side-load-your-extension"></a>Erstellen und neben Laden Ihrer Erweiterung

Nun können Sie Ihre Erweiterung im Windows Admin Center [Erstellen und](../develop-tool.md#build-and-side-load-your-extension) gleichzeitig laden.
