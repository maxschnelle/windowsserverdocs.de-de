---
title: Hinzufügen eines Moduls zu einer Tool-Erweiterung
description: 'Entwickeln Sie eine toolerweiterung Windows Admin Center-SDK (Projekt Honolulu): Fügen Sie ein Modul zu einer Tools-Erweiterung'
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: d8d901097eb280679a388ff66161e3514befcd13
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66452651"
---
# <a name="add-a-module-to-a-tool-extension"></a>Hinzufügen eines Moduls zu einer Tool-Erweiterung

>Gilt für: Windows Admin Center, Windows Admin Center Preview

In diesem Artikel werden wir eine leere Modul zu einer Tools-Erweiterung hinzufügen, die wir mit der Windows Admin Center-CLI erstellt haben.

## <a name="prepare-your-environment"></a>Vorbereiten der Umgebung

Wenn Sie nicht bereits getan haben, befolgen Sie die Anweisungen in Entwickeln einer [Tool](../develop-tool.md) (oder [Lösung](../develop-solution.md)) Erweiterung für die Vorbereitung Ihrer Umgebung und erstellen Sie eine neue, leere Tools-Erweiterung.

## <a name="use-the-angular-cli-to-create-a-module-and-component"></a>Verwenden der Angular-Befehlszeilenschnittstelle zum Erstellen eines Moduls (und die Komponente)

Wenn Sie mit Angular vertraut sind, ist das Lesen Sie der Dokumentation zur Angular.Io Websiteseite, um weitere Informationen zu Angular und NgModule dringend empfohlen. Weitere Informationen zu NgModule finden Sie hier:https://angular.io/guide/ngmodule

* Weitere Informationen zum Generieren eines neuen Moduls in Winkel CLI:https://github.com/angular/angular-cli/wiki/generate-module
* Weitere Informationen zum Generieren von einer neuen Komponente in Winkel CLI:https://github.com/angular/angular-cli/wiki/generate-component


Öffnen Sie eine Eingabeaufforderung, wechseln Sie zu \src\app in Ihrem Projekt, und führen Sie die folgenden Befehle aus, und Ersetzen Sie dabei ```{!ModuleName}``` durch den Modulnamen Ihres (Leerzeichen):

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

Wenn Sie mit Angular vertraut sind, wird empfohlen, dass Winkel Routing und Navigation lernen. In den folgenden Abschnitten werden die erforderlichen routing Elemente, mit denen Windows Admin Center, zur Erweiterung und zwischen Ansichten in der Erweiterung als Antwort auf die Aktivität des Benutzers zu navigieren definiert. Weitere Informationen finden Sie hier:https://angular.io/guide/router

Verwenden Sie den gleichen Modulnamen, den Sie im vorherigen Schritt verwendet.

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

### <a name="add-content-to-new-component-typescript-file"></a>Neue Typescript-Komponentendatei Inhalte hinzufügen

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
### <a name="update-app-routingmodulets"></a>Aktualisieren der app-routing.module.ts

Öffnen von Dateien ```app-routing.module.ts```, und den standardmäßige Pfad ändern, damit sie das neue Modul geladen werden, die Sie gerade erstellt haben.  Suchen Sie den Eintrag für ```path: ''```, und Aktualisieren von ```loadChildren``` beim Laden des Moduls, anstatt das Standardmodul:

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
Hier ist ein Beispiel für einen Standardpfad für die aktualisierte:
``` ts
    {
        path: '', 
        loadChildren: 'app/manage-foo-works-portal/manage-foo-works-portal.module#ManageFooWorksPortalModule'
    },
```


## <a name="build-and-side-load-your-extension"></a>Erstellen und die Seite laden die Erweiterung

Sie haben nun ein Modul zu Ihrer Erweiterung hinzugefügt.  Als Nächstes können Sie [erstellen und die Seite laden](../develop-tool.md#build-and-side-load-your-extension) Ihre Erweiterung in Windows Admin Center, um die Ergebnisse anzuzeigen.
