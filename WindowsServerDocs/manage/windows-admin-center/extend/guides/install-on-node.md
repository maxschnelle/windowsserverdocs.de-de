---
title: Entwickeln einer Tool-Erweiterung
description: Entwickeln einer Tool Erweiterung Windows Admin Center SDK (Project Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: c5c87be882a32958946198eb6ff1b9d7000577e7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385291"
---
# <a name="install-extension-payload-on-a-managed-node"></a>Installieren der Erweiterungs Nutzlast auf einem verwalteten Knoten

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

## <a name="setup"></a>Setup
> [!NOTE]
> Um dieser Anleitung zu folgen, benötigen Sie Build 1.2.1904.02001 oder höher. Um die Buildnummer zu überprüfen, öffnen Sie das Windows Admin Center, und klicken Sie oben rechts auf das Fragezeichen.

Wenn Sie dies noch nicht getan haben, erstellen Sie eine [Tool Erweiterung](../develop-tool.md) für Windows Admin Center. Nachdem Sie dies abgeschlossen haben, notieren Sie sich die Werte, die beim Erstellen einer Erweiterung verwendet wurden:

| Wert | Erläuterung | Beispiel |
| ----- | ----------- | ------- |
| ```{!Company Name}``` | Name Ihres Unternehmens (mit Leerzeichen) | ```Contoso``` |
| ```{!Tool Name}``` | Ihr Toolname (mit Leerzeichen) | ```InstallOnNode``` |

Erstellen Sie in Ihrem Tool Erweiterungs Ordner einen Ordner "```Node```" (```{!Tool Name}\Node```). Alle Elemente, die in diesem Ordner platziert werden, werden bei Verwendung dieser API auf den verwalteten Knoten kopiert. Fügen Sie alle Dateien hinzu, die für Ihren Anwendungsfall erforderlich sind. 

Erstellen Sie auch ein ```{!Tool Name}\Node\installNode.ps1```-Skript. Dieses Skript wird auf dem verwalteten Knoten ausgeführt, sobald alle Dateien aus dem Ordner "```{!Tool Name}\Node```" auf den verwalteten Knoten kopiert wurden. Fügen Sie zusätzliche Logik für Ihren Anwendungsfall hinzu. Ein Beispiel ```{!Tool Name}\Node\installNode.ps1```-Datei:

``` ps1
# Add logic for installing payload on managed node
echo 'Success'
```

> [!NOTE]
> ```{!Tool Name}\Node\installNode.ps1``` hat einen bestimmten Namen, nach dem die API sucht. Wenn Sie den Namen dieser Datei ändern, tritt ein Fehler auf.


## <a name="integration-with-ui"></a>Integration in die Benutzeroberfläche

Aktualisieren Sie ```\src\app\default.component.ts``` auf Folgendes:

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
Aktualisieren Sie die Platzhalter auf Werte, die beim Erstellen der Erweiterung verwendet wurden:
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

Aktualisieren Sie außerdem ```\src\app\default.component.html``` auf:
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

## <a name="creating-and-installing-a-nuget-package"></a>Erstellen und Installieren eines nuget-Pakets

Der letzte Schritt ist das Entwickeln eines nuget-Pakets mit den Dateien, die wir hinzugefügt haben, und die anschließende Installation des Pakets im Windows Admin Center.

Wenn Sie noch kein Erweiterungspaket erstellt haben, befolgen Sie das Handbuch zum [Veröffentlichen von Erweiterungen](../publish-extensions.md) . 
> [!IMPORTANT]
> In der nuspec-Datei für diese Erweiterung ist es wichtig, dass der ```<id>```-Wert mit dem Namen im ```manifest.json``` Ihres Projekts übereinstimmt und ```<version>``` übereinstimmt, was ```\src\app\default.component.ts``` hinzugefügt wurde. Fügen Sie außerdem einen Eintrag unter ```<files>``` hinzu: 
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

Fügen Sie nach dem Erstellen dieses Pakets einen Pfad zu diesem Feed hinzu. Wechseln Sie im Windows Admin Center zu Einstellungen > Erweiterungen > Feeds, und fügen Sie den Pfad zum Speicherort dieses Pakets hinzu. Wenn die Erweiterung installiert ist, sollten Sie auf die Schaltfläche ```install``` klicken können, und die API wird aufgerufen.  