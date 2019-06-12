---
title: Entwickeln einer Tool-Erweiterung
description: Entwickeln Sie eine toolerweiterung Windows Admin Center-SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 1a068c0d33887e8e9287ff15c1aa14f3dc84915a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445931"
---
# <a name="install-extension-payload-on-a-managed-node"></a>Installieren der Erweiterung Nutzlast auf einem verwalteten Knoten

>Gilt für: Windows Admin Center, Windows Admin Center Preview

## <a name="setup"></a>Setup
> [!NOTE]
> Damit dieser Anleitung folgen zu können, müssen erstellen Sie 1.2.1904.02001 oder höher. Überprüfen Sie Ihren Build Anzahl Windows Admin Center zu öffnen und klicken Sie auf das Fragezeichen in der rechten oberen Ecke.

Wenn Sie noch nicht geschehen, erstellen Sie eine [tool Erweiterung](../develop-tool.md) für Windows Admin Center. Nach Abschluss dieser stellen sich die Werte, die beim Erstellen einer Erweiterungs verwendet:

| Wert | Erläuterung | Beispiel |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | Den Namen Ihres Unternehmens (mit Leerzeichen) | ```Contoso``` |
| ```{!Tool Name}``` | Der Name des Tools (mit Leerzeichen) | ```InstallOnNode``` |

Erstellen Sie in den Ordner Ihrer Erweiterung ein ```Node``` Ordner (```{!Tool Name}\Node```). Sämtliche Elemente in diesem Ordner werden an den verwalteten Knoten kopiert werden, bei der Verwendung dieser API. Fügen Sie alle Dateien, die für Ihren Anwendungsfall erforderlich sind. 

Erstellen Sie auch eine ```{!Tool Name}\Node\installNode.ps1``` Skript. Dieses Skript wird auf dem verwalteten Knoten ausgeführt werden, nachdem alle Dateien aus dem kopiert werden die ```{!Tool Name}\Node``` Ordner an den verwalteten Knoten. Fügen Sie zusätzliche Logik für Ihren Anwendungsfall hinzu. Ein Beispiel für ```{!Tool Name}\Node\installNode.ps1``` Datei:

``` ps1
# Add logic for installing payload on managed node
echo 'Success'
```

> [!NOTE]
> ```{!Tool Name}\Node\installNode.ps1``` verfügt über einen bestimmten Namen, den die API gesucht wird. Ändern des Namens der Datei verursacht einen Fehler.


## <a name="integration-with-ui"></a>UI-Integration

Update ```\src\app\default.component.ts``` folgt:

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

## <a name="creating-and-installing-a-nuget-package"></a>Erstellen und Installieren eines NuGet-Pakets

Der letzte Schritt ist beim Erstellen eines NuGet-Pakets mit der Dateien, die wir hinzugefügt haben und das Paket dann in Windows Admin Center installieren.

Führen Sie die [Publishing Erweiterungen](../publish-extensions.md) führen, wenn Sie ein Erweiterungspaket vor nicht erstellt haben. 
> [!IMPORTANT]
> In der NuSpec-Datei für diese Erweiterung ist es wichtig, die ```<id>``` Wert entspricht dem Namen in Ihrem Projekts ab ```manifest.json``` und die ```<version>``` übereinstimmt, was hinzugefügte ```\src\app\default.component.ts```. Fügen Sie auch einen Eintrag unter ```<files>```: 
> 
> ```<file src="Node\**\*.*" target="Node" />```. installiert haben.

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

Sobald dieses Paket erstellt wurde, können fügen Sie einen Pfad zu diesen Feed hinzu. Wechseln Sie in Windows Admin Center zu Einstellungen > Erweiterungen >-Feeds, und fügen Sie den Pfad an, in dem das Paket vorhanden ist. Die Erweiterung wird nach Abschluss wird installiert, Sie sollten in der Lage, klicken Sie auf die ```install``` Schaltfläche und die API aufgerufen werden.  