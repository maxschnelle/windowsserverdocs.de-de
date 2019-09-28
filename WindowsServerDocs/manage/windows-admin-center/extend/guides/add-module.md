---
title: Hinzufügen eines Moduls zu einer Tool-Erweiterung
description: 'Entwickeln einer Tool Erweiterung Windows Admin Center SDK (Project Honolulu): Hinzufügen eines Moduls zu einer Tool Erweiterung'
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 9d30980ca404187ff1481242c1c0ef0a3d571416
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357098"
---
# <a name="add-a-module-to-a-tool-extension"></a>Hinzufügen eines Moduls zu einer Tool-Erweiterung

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

In diesem Artikel fügen wir ein leeres Modul zu einer Tool Erweiterung hinzu, die wir mit der Windows Admin Center CLI erstellt haben.

## <a name="prepare-your-environment"></a>Vorbereiten der Umgebung

Wenn Sie dies noch nicht getan haben, befolgen Sie die Anweisungen unter Entwickeln einer [Tool](../develop-tool.md) Erweiterung [(oder Projekt](../develop-solution.md)Mappe), um die Umgebung vorzubereiten und eine neue, leere Tool Erweiterung zu erstellen.

## <a name="use-the-angular-cli-to-create-a-module-and-component"></a>Verwenden der Angular-CLI zum Erstellen eines Moduls (und einer Komponente)

Wenn Sie mit Angular vertraut sind, ist das Lesen Sie der Dokumentation zur Angular.Io Websiteseite, um weitere Informationen zu Angular und NgModule dringend empfohlen. Weitere Informationen zu NgModule finden Sie hier: [https://angular.io/guide/ngmodule](https://angular.io/guide/ngmodule )

* Weitere Informationen zum Generieren eines neuen Moduls in Winkel CLI: [https://github.com/angular/angular-cli/wiki/generate-module](https://github.com/angular/angular-cli/wiki/generate-module )
* Weitere Informationen zum Generieren von einer neuen Komponente in Winkel CLI: [https://github.com/angular/angular-cli/wiki/generate-component](https://github.com/angular/angular-cli/wiki/generate-component )


Öffnen Sie eine Eingabeaufforderung, wechseln Sie in Ihrem Projekt zum Verzeichnis "\src\app", und führen Sie dann die folgenden Befehle aus. ersetzen Sie dabei ```{!ModuleName}``` durch ihren Modulnamen (Leerzeichen entfernt):

```
cd \src\app
ng generate module {!ModuleName}
ng generate component {!ModuleName}
```

| Wert | Erläuterung | Beispiel |
| ----- | ----------- | ------- |
| ```{!ModuleName}``` | Ihre Modulnamen (entfernt Leerzeichen) | ```ManageFooWorksPortal``` |

Beispielanwendung:
```
cd \src\app
ng generate module ManageFooWorksPortal
ng generate component ManageFooWorksPortal
```


## <a name="add-routing-information"></a>Routing-Informationen hinzufügen

Wenn Sie mit Angular vertraut sind, wird empfohlen, dass Winkel Routing und Navigation lernen. In den folgenden Abschnitten werden die erforderlichen routing Elemente, mit denen Windows Admin Center, zur Erweiterung und zwischen Ansichten in der Erweiterung als Antwort auf die Aktivität des Benutzers zu navigieren definiert. Weitere Informationen finden Sie hier: [https://angular.io/guide/router](https://angular.io/guide/router )

Verwenden Sie den gleichen Modulnamen, den Sie im obigen Schritt verwendet haben.

### <a name="add-content-to-new-routing-file"></a>Hinzufügen von Inhalten zu neuen routing-Datei

* Navigieren Sie zu dem Modul-Ordner, die vom erstellt wurde ``` ng generate ``` im vorherigen Schritt.

* Erstellen Sie eine neue Datei ```{!module-name}.routing.ts```, befolgen die folgende Benennungskonvention:

    | Wert | Erläuterung | Beispiel-Dateiname |
    | ----- | ----------- | ------- |
    | ```{!module-name}``` | Ihre Modulnamen (Kleinbuchstabe, Leerzeichen ersetzt, die mit Bindestrichen) | ```manage-foo-works-portal.routing.ts``` |

* Fügen Sie diese Inhalte auf die soeben erstellte Datei hinzu:

    ``` ts
    import { NgModule } from '@angular/core';
    import { RouterModule, Routes } from '@angular/router';
    import { {!ModuleName}Component } from './{!module-name}.component';

    const routes: Routes = [
        {
            path: '',
            component: {!ModuleName}Component,
            // if the component has child components that need to be routed to, include them in the children array.
            children: [
                {
                    path: '', 
                    redirectTo: 'base',
                    pathMatch: 'full'
                }
            ]
    }];

    @NgModule({
        imports: [
            RouterModule.forChild(routes)
        ],
        exports: [
            RouterModule
        ]
    })
    export class Routing { }
    ```

* Ersetzen Sie die Werte in der Datei, die soeben erstellte durch Ihre gewünschten Werte:

    | Wert | Erläuterung | Beispiel |
    | ----- | ----------- | ------- |
    | ```{!ModuleName}``` | Ihre Modulnamen (entfernt Leerzeichen) | ```ManageFooWorksPortal``` |
    | ```{!module-name}``` | Ihre Modulnamen (Kleinbuchstabe, Leerzeichen ersetzt, die mit Bindestrichen) | ```manage-foo-works-portal``` |

### <a name="add-content-to-new-module-file"></a>Hinzufügen von Inhalten zu neue Moduldatei

Öffnen Sie die Datei ```{!module-name}.module.ts``` mit folgender Namenskonvention:

| Wert | Erläuterung | Beispiel-Dateiname |
| ----- | ----------- | ------- |
| ```{!module-name}``` | Ihre Modulnamen (Kleinbuchstabe, Leerzeichen ersetzt, die mit Bindestrichen) | ```manage-foo-works-portal.module.ts``` |

* Hinzufügen von Inhalt zu der Datei:

    ``` ts
    import { Routing } from './{!module-name}.routing';
    ```

* Ersetzen Sie die Werte in den Inhalt durch Ihre gewünschten Werte soeben hinzugefügt haben:

    | Wert | Erläuterung | Beispiel |
    | ----- | ----------- | ------- |
    | ```{!module-name}``` | Ihre Modulnamen (Kleinbuchstabe, Leerzeichen ersetzt, die mit Bindestrichen) | ```manage-foo-works-portal``` |

* Ändern Sie die Imports-Anweisung, um Routing zu importieren:

    | Originalwert | Neuer Wert |
    | -------------- | --------- |
    | ```imports: [ CommonModule ]``` | ```imports: [ CommonModule, Routing ]``` |

* Stellen Sie sicher, dass ```import``` Anweisungen werden alphabetisch sortiert nach Quelle.

### <a name="add-content-to-new-component-typescript-file"></a>Inhalt der neuen komponententypescript-Datei hinzufügen

Öffnen Sie die Datei ```{!module-name}.component.ts``` mit folgender Namenskonvention:

| Wert | Erläuterung | Beispiel-Dateiname |
| ----- | ----------- | ------- |
| ```{!module-name}``` | Ihre Modulnamen (Kleinbuchstabe, Leerzeichen ersetzt, die mit Bindestrichen) | ```manage-foo-works-portal.component.ts``` |
    
Ändern Sie Inhalt der Datei wie folgt:

``` ts
constructor() {
    // TODO
}

public ngOnInit() {
    // TODO
}
```
### <a name="update-app-routingmodulets"></a>Aktualisieren von App-Routing. Module. TS

Öffnen Sie die Datei ```app-routing.module.ts```, und ändern Sie den Standardpfad, damit das soeben erstellte neue Modul geladen wird.  Suchen Sie den Eintrag für ```path: ''```, und aktualisieren Sie ```loadChildren```, um das Modul anstelle des Standardmoduls zu laden:

| Wert | Erläuterung | Beispiel |
| ----- | ----------- | ------- |
| ```{!ModuleName}``` | Ihre Modulnamen (entfernt Leerzeichen) | ```ManageFooWorksPortal``` |
| ```{!module-name}``` | Ihre Modulnamen (Kleinbuchstabe, Leerzeichen ersetzt, die mit Bindestrichen) | ```manage-foo-works-portal``` |

``` ts
    {
        path: '', 
        loadChildren: 'app/{!module-name}/{!module-name}.module#{!ModuleName}Module'
    },
```
Im folgenden finden Sie ein Beispiel für einen aktualisierten Standardpfad:
``` ts
    {
        path: '', 
        loadChildren: 'app/manage-foo-works-portal/manage-foo-works-portal.module#ManageFooWorksPortalModule'
    },
```


## <a name="build-and-side-load-your-extension"></a>Erstellen und neben Laden Ihrer Erweiterung

Sie haben nun ein Modul zu ihrer Erweiterung hinzugefügt.  Als nächstes können Sie Ihre Erweiterung im Windows Admin Center [Erstellen und](../develop-tool.md#build-and-side-load-your-extension) auslagern, um die Ergebnisse anzuzeigen.
