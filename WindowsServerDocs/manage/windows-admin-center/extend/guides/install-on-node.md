---
title: Entwickeln einer Tool-Erweiterung
description: Entwickeln einer Tool-Erweiterungs Windows Admin Center SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 2269a2ac2cabda6f8fdd829994f36e89d581bd23
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297012"
---
# Installieren Sie die Erweiterung Nutzlast auf einem verwalteten Knoten

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

## Setup
> [!NOTE]
> Um dieses Handbuch zu verfolgen, müssen erstellen Sie 1.2.1904.02001 oder höher. Um zu überprüfen, den Build Anzahl öffnen Sie Windows Admin Center und klicken Sie auf das Fragezeichen oben rechts.

Falls noch nicht geschehen, erstellen Sie eine [Tool-Erweiterung](../develop-tool.md) für Windows Admin Center. Nach Abschluss dieses stellen Notieren Sie sich die Werte verwendet, wenn eine Erweiterung zu erstellen:
| Wert | Erläuterung | Beispiel |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | Den Namen Ihres Unternehmens (mit Leerzeichen) | ```Contoso``` |
| ```{!Tool Name}``` | Der Name des Tools (mit Leerzeichen) | ```InstallOnNode``` |

Erstellen Sie innerhalb Ihrer Tool-Erweiterung-Ordners ein ```Node``` Ordner (```{!Tool Name}\Node```). Alle Elemente in diesem Ordner platziert wird mit dem verwalteten Knoten kopiert werden, bei der Verwendung dieser API. Fügen Sie alle Dateien, die für Ihren Zweck erforderlich. 

Erstellen Sie auch eine ```{!Tool Name}\Node\installNode.ps1``` Skript. Dieses Skript wird auf dem verwalteten Knoten ausgeführt werden, nachdem alle Dateien kopiert werden, aus der ```{!Tool Name}\Node``` Ordner mit dem verwalteten Knoten. Fügen Sie eine zusätzliche Logik für Ihren Zweck hinzu. Ein Beispiel ```{!Tool Name}\Node\installNode.ps1``` Datei:

``` ps1
# Add logic for installing payload on managed node
echo 'Success'
```

> [!NOTE]
> ```{!Tool Name}\Node\installNode.ps1``` ist einen bestimmter Name, den die API gesucht wird. Ändern den Namen dieser Datei verursachen einen Fehler.


## Integration in die Benutzeroberfläche

Update ```\src\app\default.component.ts``` wie folgt:

``` ts
import { Component } from '@angular/core';
import { AppContextService } from '@microsoft/windows-admin-center-sdk/angular';
import { Observable } from 'rxjs';

@Component({
  selector: 'default-component',
  templateUrl: './default.component.html',
  styleUrls: ['./default.component.css']
})

export class DefaultComponent {
  constructor(private appContextService: AppContextService) { }

  public response: any;
  public loading = false;

  public installOnNode() {
    this.loading = true;
    this.post('{!Company Name}.{!Tool Name}', '1.0.0',
      this.appContextService.activeConnection.nodeName).subscribe(
        (response: any) => {
          console.log(response);
          this.response = response;
          this.loading = false;
        },
        (error) => {
          console.log(error);
          this.response = error;
          this.loading = false;
        }
      );
  }

  public post(id: string, version: string, targetNode: string): Observable<any> {
    return this.appContextService.node.post(targetNode,
      `features/extensions/${id}/versions/${version}/install`);
  }

}
```
Aktualisieren Sie Platzhalter für Werte, die verwendet wurden, wenn Sie die Erweiterung zu erstellen:
``` ts
this.post('contoso.install-on-node', '1.0.0',
      this.appContextService.activeConnection.nodeName).subscribe(
        (response: any) => {
          console.log(response);
          this.response = response;
          this.loading = false;
        },
        (error) => {
          console.log(error);
          this.response = error;
          this.loading = false;
        }
      );
```

Aktualisieren Sie auch ```\src\app\default.component.html``` auf:
``` html
<button (click)="installOnNode()">Click to install</button>
<sme-loading-wheel *ngIf="loading" size="large"></sme-loading-wheel>
<p *ngIf="response">{{response}}</p>
```
Und schließlich ```\src\app\default.module.ts```:
``` ts
import { CommonModule } from '@angular/common';
import { NgModule } from '@angular/core';

import { LoadingWheelModule } from '@microsoft/windows-admin-center-sdk/angular';
import { DefaultComponent } from './default.component';
import { Routing } from './default.routing';

@NgModule({
  imports: [
    CommonModule,
    LoadingWheelModule,
    Routing
  ],
  declarations: [DefaultComponent]
})
export class DefaultModule { }

```

## Erstellen und Installieren von NuGet-Paket

Im letzte Schritt erstellt ein NuGet-Paket mit den Dateien, die wir hinzugefügt haben und dann dieses Paket im Windows Admin Center installieren.

Befolgen Sie die Anleitung [Veröffentlichen von Erweiterungen](../publish-extensions.md) , wenn Sie ein Erweiterungspaket vor nicht erstellt haben. 
> [!IMPORTANT]
> In der Datei .nuspec für diese Erweiterung ist es wichtig, die die ```<id>``` Wert entspricht dem Namen in Ihrem Projekts ```manifest.json``` und ```<version>``` entspricht, was hinzugefügt wurde ```\src\app\default.component.ts```. Fügen Sie auch einen Eintrag unter ```<files>```: 

> ```<file src="Node\**\*.*" target="Node" />```.

``` xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2011/08/nuspec.xsd">
  <metadata>
    <id>contoso.install-on-node</id>
    <version>1.0.0</version>
    <authors>Contoso</authors>
    <owners>Contoso</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <projectUrl>https://msft-sme.myget.org/feed/windows-admin-center-feed/package/nuget/contoso.sme.install-on-node-extension</projectUrl>
    <licenseUrl>http://YourLicenseLink</licenseUrl>
    <iconUrl>http://YourLogoLink</iconUrl>
    <description>Install on node extension by Contoso</description>
    <copyright>(c) Contoso. All rights reserved.</copyright> 
  </metadata>
    <files>
    <file src="bundle\**\*.*" target="ux" />
    <file src="package\**\*.*" target="gateway" />
    <file src="Node\**\*.*" target="Node" />
  </files>
</package>
```

Wenn dieses Paket erstellt wurde, fügen Sie einen Pfad zu dieser Feed hinzu. In Windows Admin Center wechseln Sie zu Einstellungen > Erweiterungen > Feeds, und fügen Sie den Pfad, wo dieses Paket vorhanden ist. Wenn die Erweiterung erfolgt, das installiert wird, Sie sollten in der Lage, klicken Sie auf die ```install``` Schaltfläche und die API aufgerufen wird.  