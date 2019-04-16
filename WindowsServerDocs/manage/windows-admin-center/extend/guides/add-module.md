---
title: Fügen Sie ein Modul zu einer Tool-Erweiterung
description: 'Entwickeln Sie eine Tool-Erweiterung Windows Admin Center SDK (Projekt Honolulu): Hinzufügen von ein Modul zu einer Tool-Erweiterung'
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: e6978ce20a7c6da8addb217de8d30f733b40d261
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081207"
---
# Fügen Sie ein Modul zu einer Tool-Erweiterung

>Gilt für: Windows Admin Center, Windows Admin Center Preview

In diesem Artikel werden ein leeres Modul eine Tool-Erweiterung hinzugefügt, die wir mit der Windows Admin Center-CLI erstellt haben.

## Vorbereiten der Umgebung

Wenn Sie noch nicht geschehen, führen Sie die Anweisungen in Entwicklung eine Erweiterung [Tool](..\develop-tool.md) (oder [Lösung](..\develop-solution.md)) zum Vorbereiten der Umgebung, und erstellen Sie eine neue, leere Tool-Erweiterung.

## Verwenden Sie der Winkel CLI, um ein Modul (und die Komponente) zu erstellen

Wenn Sie mit Angular vertraut sind, ist das Lesen Sie der Dokumentation zur Angular.Io Websiteseite, um weitere Informationen zu Angular und NgModule dringend empfohlen. Weitere Informationen zu NgModule finden Sie hier:https://angular.io/guide/ngmodule

* Weitere Informationen zum Generieren eines neuen Moduls in Winkel CLI:https://github.com/angular/angular-cli/wiki/generate-module
* Weitere Informationen zum Generieren von einer neuen Komponente in Winkel CLI:https://github.com/angular/angular-cli/wiki/generate-component


Öffnen Sie ein Eingabeaufforderungsfenster, ändern Sie das Verzeichnis auf \src\app in Ihrem Projekt, und führen Sie die folgenden Befehle ```{!ModuleName}``` durch Ihre Modulnamen (entfernt Leerzeichen):

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


## Routing-Informationen hinzufügen

Wenn Sie mit Angular vertraut sind, wird empfohlen, dass Winkel Routing und Navigation lernen. In den folgenden Abschnitten werden die erforderlichen routing Elemente, mit denen Windows Admin Center, zur Erweiterung und zwischen Ansichten in der Erweiterung als Antwort auf die Aktivität des Benutzers zu navigieren definiert. Weitere Informationen finden Sie hier:https://angular.io/guide/router

Verwenden Sie den Namen des gleichen Moduls, den Sie im vorigen Schritt verwendet.

### Hinzufügen von Inhalten zu neuen routing-Datei

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

### Hinzufügen von Inhalten zu neue Moduldatei

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

### Hinzufügen von Inhalten zu neue Komponentendatei Schreibmaschine

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
### App-routing.module.ts aktualisieren

Öffnen Sie die Datei ```app-routing.module.ts```, und ändern Sie den Standardpfad, damit sie das neue Modul geladen wird, die Sie gerade erstellt haben.  Suchen Sie den Eintrag für ```path: ''```, und aktualisieren Sie ```loadChildren``` zum Laden des Moduls anstelle der Standardmodul:

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
Hier ist ein Beispiel für eine aktualisierte Standardpfad:
``` ts
    {
        path: '', 
        loadChildren: 'app/manage-foo-works-portal/manage-foo-works-portal.module#ManageFooWorksPortalModule'
    },
```


## Build und Seite laden die Erweiterung

Sie haben jetzt ein Modul zur Erweiterung hinzugefügt.  Als Nächstes können Sie [Build und Seite laden](..\develop-tool.md#build-and-side-load-your-extension) die Erweiterung in Windows Admin Center, um die Ergebnisse anzuzeigen.
