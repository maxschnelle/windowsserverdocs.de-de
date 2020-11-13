---
title: Hinzufügen eines Moduls zu einer Toolerweiterung
description: 'Entwickeln einer Tool Erweiterung Windows Admin Center SDK (Project Honolulu): Hinzufügen eines Moduls zu einer Tool Erweiterung'
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 06331c23730cfdbf1752961f7867b0bebf45cacb
ms.sourcegitcommit: 01b3140f79f5614ce566e8036474feefafbeddc3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2020
ms.locfileid: "94581414"
---
# <a name="add-a-module-to-a-tool-extension"></a>Hinzufügen eines Moduls zu einer Toolerweiterung

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

In diesem Artikel fügen wir ein leeres Modul zu einer Tool Erweiterung hinzu, die wir mit der Windows Admin Center CLI erstellt haben.

## <a name="prepare-your-environment"></a>Vorbereiten der Umgebung

Wenn Sie dies noch nicht getan haben, befolgen Sie die Anweisungen unter Entwickeln einer [Tool](../develop-tool.md) Erweiterung [(oder Projekt](../develop-solution.md)Mappe), um die Umgebung vorzubereiten und eine neue, leere Tool Erweiterung zu erstellen.

## <a name="use-the-angular-cli-to-create-a-module-and-component"></a>Verwenden der Angular-CLI zum Erstellen eines Moduls (und einer Komponente)

Wenn Sie noch nicht mit Angular vertraut sind, wird dringend empfohlen, dass Sie die Dokumentation auf der Angular.IO-Website lesen, um mehr über Angular und ngmodule zu erfahren. Weitere Informationen zu ngmodule finden Sie hier: https://angular.io/guide/ngmodule

* Weitere Informationen zum Erstellen eines neuen Moduls in der Angular CLI: https://github.com/angular/angular-cli/wiki/generate-module
* Weitere Informationen zum Erstellen einer neuen Komponente in der Angular CLI: https://github.com/angular/angular-cli/wiki/generate-component


Öffnen Sie eine Eingabeaufforderung, wechseln Sie in Ihrem Projekt zum Verzeichnis ".\src\app", und führen Sie dann die folgenden Befehle aus. ersetzen ```{!ModuleName}``` Sie dabei durch den Namen Ihres Moduls (Leerzeichen entfernt):

```
cd .\src\app
ng generate module {!ModuleName}
ng generate component {!ModuleName}
```

| Wert | Erklärung | Beispiel |
| ----- | ----------- | ------- |
| ```{!ModuleName}``` | Name des Moduls (Leerzeichen entfernt) | ```ManageFooWorksPortal``` |

Beispielverwendung:
```
cd .\src\app
ng generate module ManageFooWorksPortal
ng generate component ManageFooWorksPortal
```


## <a name="add-routing-information"></a>Routing Informationen hinzufügen

Wenn Sie noch nicht mit Angular vertraut sind, wird dringend empfohlen, sich über das Angular-Routing und die Navigation zu informieren. In den folgenden Abschnitten werden die erforderlichen Routing Elemente definiert, mit denen Windows Admin Center in Reaktion auf die Benutzeraktivität zu ihrer Erweiterung und zwischen Sichten in ihrer Erweiterung navigieren kann. Weitere Informationen finden Sie hier: https://angular.io/guide/router

Verwenden Sie den gleichen Modulnamen, den Sie im obigen Schritt verwendet haben.

### <a name="add-content-to-new-routing-file"></a>Neuen Routing Dateiinhalt hinzufügen

* Navigieren Sie zum Modul Ordner, der  ``` ng generate ``` im vorherigen Schritt erstellt wurde.

* Erstellen Sie eine neue Datei ```{!module-name}.routing.ts``` , und befolgen Sie diese Benennungs Konvention:

    | Wert | Erklärung | Beispiel Dateiname |
    | ----- | ----------- | ------- |
    | ```{!module-name}``` | Der Modulname (in Kleinbuchstaben, Leerzeichen durch Bindestriche ersetzt) | ```manage-foo-works-portal.routing.ts``` |

* Fügen Sie den Inhalt der soeben erstellten Datei hinzu:

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

* Ersetzen Sie die Werte in der soeben erstellten Datei durch die gewünschten Werte:

    | Wert | Erklärung | Beispiel |
    | ----- | ----------- | ------- |
    | ```{!ModuleName}``` | Name des Moduls (Leerzeichen entfernt) | ```ManageFooWorksPortal``` |
    | ```{!module-name}``` | Der Modulname (in Kleinbuchstaben, Leerzeichen durch Bindestriche ersetzt) | ```manage-foo-works-portal``` |

### <a name="add-content-to-new-module-file"></a>Inhalt der neuen Modul Datei hinzufügen

Datei öffnen ```{!module-name}.module.ts``` , mit der folgenden Benennungs Konvention gefunden:

| Wert | Erklärung | Beispiel Dateiname |
| ----- | ----------- | ------- |
| ```{!module-name}``` | Der Modulname (in Kleinbuchstaben, Leerzeichen durch Bindestriche ersetzt) | ```manage-foo-works-portal.module.ts``` |

* Fügen Sie der Dateiinhalt hinzu:

    ``` ts
    import { Routing } from './{!module-name}.routing';
    ```

* Ersetzen Sie die Werte im soeben hinzugefügten Inhalt mit den gewünschten Werten:

    | Wert | Erklärung | Beispiel |
    | ----- | ----------- | ------- |
    | ```{!module-name}``` | Der Modulname (in Kleinbuchstaben, Leerzeichen durch Bindestriche ersetzt) | ```manage-foo-works-portal``` |

* Ändern Sie die Imports-Anweisung, um Routing zu importieren:

    | Ursprünglicher Wert | Neuer Wert |
    | -------------- | --------- |
    | ```imports: [ CommonModule ]``` | ```imports: [ CommonModule, Routing ]``` |

* Stellen Sie sicher, dass- ```import``` Anweisungen nach Quelle alphabetisch sortiert werden.

### <a name="add-content-to-new-component-typescript-file"></a>Inhalt der neuen komponententypescript-Datei hinzufügen

Datei öffnen ```{!module-name}.component.ts``` , mit der folgenden Benennungs Konvention gefunden:

| Wert | Erklärung | Beispiel Dateiname |
| ----- | ----------- | ------- |
| ```{!module-name}``` | Der Modulname (in Kleinbuchstaben, Leerzeichen durch Bindestriche ersetzt) | ```manage-foo-works-portal.component.ts``` |

Ändern Sie den Inhalt der Datei wie folgt:

``` ts
constructor() {
    // TODO
}

public ngOnInit() {
    // TODO
}
```
### <a name="update-app-routingmodulets"></a>Aktualisieren von App-Routing. Module. TS

Öffnen Sie die Datei ```app-routing.module.ts``` , und ändern Sie den Standardpfad, damit das neue Modul geladen wird, das Sie soeben erstellt haben.  Suchen Sie den Eintrag für ```path: ''``` , und aktualisieren  ```loadChildren``` Sie, um das Modul anstelle des Standardmoduls zu laden:

| Wert | Erklärung | Beispiel |
| ----- | ----------- | ------- |
| ```{!ModuleName}``` | Name des Moduls (Leerzeichen entfernt) | ```ManageFooWorksPortal``` |
| ```{!module-name}``` | Der Modulname (in Kleinbuchstaben, Leerzeichen durch Bindestriche ersetzt) | ```manage-foo-works-portal``` |

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
