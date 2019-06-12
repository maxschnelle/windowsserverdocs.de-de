---
title: Erstellen Sie einen Verbindungsanbieter für eine projektmappenerweiterung
description: Entwickeln einer Lösung Erweiterungs Windows Admin Center-SDK (Projekt Honolulu) – erstellen Sie einen Verbindungsanbieter
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: b79e832ee45990d18baf4c211ab68b907134ceb7
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811833"
---
# <a name="create-a-connection-provider-for-a-solution-extension"></a>Erstellen Sie einen Verbindungsanbieter für eine projektmappenerweiterung

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Verbindungsanbieter spielen eine wichtige Rolle beim wie Windows Admin Center definiert und kommuniziert mit verbindungsfähige Objekte oder -Ziele. Ein Verbindungsanbieter führt in erster Linie Aktionen, während eine Verbindung hergestellt wird, wird wie z. B. sicherstellen, dass das Ziel online und verfügbar ist, und sicherzustellen, dass es sich bei der verbindenden Benutzer die Zugriffsberechtigung für das Ziel hat.

Standardmäßig sind in Windows Admin Center mit den folgenden Verbindungs-Anbietern:

* Server
* Windows-Client
* Failovercluster
* HCI-Cluster

Um einen eigenen benutzerdefinierten Anbieter für die Verbindung zu erstellen, gehen Sie folgendermaßen vor:

* Verbindungsanbieter Details hinzugefügt werden ```manifest.json```
* Definieren von Verbindungsanbieter-Status
* Verbindungsanbieter-Anwendungsschicht zu implementieren.

## <a name="add-connection-provider-details-to-manifestjson"></a>Verbindungsanbieter-Details "Manifest.JSON" hinzugefügt

Nun wir erläutern werde wissen, um einen Anbieter für die Verbindung in Ihres Projekts zu definieren, was Sie ```manifest.json``` Datei.

### <a name="create-entry-in-manifestjson"></a>Erstellen Sie in "Manifest.JSON" Eintrag

Die ```manifest.json``` Datei befindet sich im Ordner "\src" und enthält unter anderem die Definitionen von Einstiegspunkten in Ihr Projekt. Arten von Einstiegspunkten enthalten Tools, Lösungen und Verbindungsanbieter. Wir werden einen Verbindungsanbieter definiert.

Ein Beispiel für einen Verbindungsanbieter-Eintrag in "Manifest.JSON" liegt unter:

``` json
    {
      "entryPointType": "connectionProvider",
      "name": "addServer",
      "path": "/add",
      "displayName": "resources:strings:addServer_displayName",
      "icon": "sme-icon:icon-win-server",
      "description": "resources:strings:description",
      "connectionType": "msft.sme.connection-type.server",
      "connectionTypeName": "resources:strings:addServer_connectionTypeName",
      "connectionTypeUrlName": "server",
      "connectionTypeDefaultSolution": "msft.sme.server-manager!servers",
      "connectionTypeDefaultTool": "msft.sme.server-manager!overview",
      "connectionStatusProvider": {
        "powerShell": {
          "script": "## Get-My-Status ##\nfunction Get-Status()\n{\n# A function like this would be where logic would exist to identify if a node is connectable.\n$status = @{label = $null; type = 0; details = $null; }\n$caption = \"MyConstCaption\"\n$productType = \"MyProductType\"\n# A result object needs to conform to the following object structure to be interpreted properly by the Windows Admin Center shell.\n$result = @{ status = $status; caption = $caption; productType = $productType; version = $version }\n# DO FANCY LOGIC #\n# Once the logic is complete, the following fields need to be populated:\n$status.label = \"Display Thing\"\n$status.type = 0 # This value needs to conform to the LiveConnectionStatusType enum. >= 3 represents a failure.\n$status.details = \"success stuff\"\nreturn $result}\nGet-Status"
        },
        "displayValueMap": {
          "wmfMissing-label": "resources:strings:addServer_status_wmfMissing_label",
          "wmfMissing-details": "resources:strings:addServer_status_wmfMissing_details",
          "unsupported-label": "resources:strings:addServer_status_unsupported_label",
          "unsupported-details": "resources:strings:addServer_status_unsupported_details"
        }
      }
    },
```

Einstiegspunkt vom Typ "ConnnectionProvider" zeigt die Shell Windows Admin Center, dass das Element konfiguriert wird, einen Anbieter, der von einer Lösung verwendet wird handelt, um einen Verbindungsstatus zu überprüfen. Verbindung Anbieter Einstiegspunkte enthält zahlreiche wichtige Eigenschaften, die nachstehend definiert:

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| entryPointType | Dies ist eine erforderliche Eigenschaft. Es gibt drei gültigen Werte: "Tool", "Projektmappe" und "ConnectionProvider-". | 
| NAME | Identifiziert die Verbindungsanbieter innerhalb des Bereichs einer Lösung. Dieser Wert muss innerhalb einer vollständigen Windows Admin Center-Instanz (nicht nur eine Projektmappe) eindeutig sein. |
| path | Stellt den URL-Pfad für die "Verbindung hinzufügen"-Benutzeroberfläche dar, wenn es von der Lösung konfiguriert wird. Dieser Wert muss eine Route zuordnen, die in-app-routing.module.ts-Datei konfiguriert ist. Wenn der Einstiegspunkt für die Lösung mit den Verbindungen RootNavigationBehavior konfiguriert ist, wird diese Route das Modul geladen, das von der Shell zum Anzeigen der Benutzeroberfläche der hinzufügen-Verbindung verwendet wird. Weitere Informationen finden Sie im Abschnitt für RootNavigationBehavior. |
| displayName | Der hier eingegebene Wert wird angezeigt, auf der rechten Seite der Shell, unter der schwarze Windows Admin Center angezeigt, wenn ein Benutzer eine Lösung auf der Seite "Verbindungen" geladen. |
| Symbol | Stellt das Symbol in der Lösungen Dropdown-Menü verwendet, um die Lösung darstellen. |
| description | Geben Sie eine kurze Beschreibung des Einstiegspunkts. |
| connectionType | Stellt den Verbindungstyp, den der Anbieter geladen werden. Der hier eingegebene Wert wird auch der Einstiegspunkt der Lösung verwendet werden, um anzugeben, dass diese Verbindungen von die Projektmappe geladen werden kann. Der hier eingegebene Wert wird auch im Tool Eintrag Datenpunkt(en) verwendet werden, um anzugeben, dass das Tool mit diesem Typ kompatibel ist. Dieser Wert, der hier eingegebene wird auch in das Verbindungsobjekt, das an die RPC übermittelt wird verwendet "Add im Fenster" im Application Layer Implementierung Schritt aufrufen. |
| connectionTypeName | In der Verbindungstabelle verwendet, um eine Verbindung darzustellen, die Anbieter Ihre Verbindung verwendet. Dies wird erwartet, zum der Pluralname des Typs sein. |
| connectionTypeUrlName | Zum Erstellen der URL die geladene Projektmappe darstellen, nachdem Windows Admin Center eine Verbindung mit einer Instanz hergestellt hat. Dieser Eintrag ist nach Verbindungen, und bevor das Ziel verwendet. In diesem Beispiel ist die "Connectionexample", wo dieser Wert in der URL angezeigt wird: `http://localhost:6516/solutionexample/connections/connectionexample/con-fake1.corp.contoso.com` |
| connectionTypeDefaultSolution | Stellt die Standardkomponente, die vom Verbindungsanbieter geladen werden soll. Dieser Wert ist eine Kombination aus: <br>[a] der Name des Erweiterungspakets definiert, die am oberen Rand des Manifests; <br>[b] Ausrufezeichen (!); <br>[c] der Lösungsname des Einstiegspunkts.    <br>Für ein Projekt mit dem Namen "msft.sme.mySample-Extension", und eine Lösung-Einstiegspunkt mit dem Namen "Example", wäre dieser Wert "msft.sme.solutionExample-Erweiterung Beispiel". |
| connectionTypeDefaultTool | Stellt das Tool, das bei einer erfolgreichen Verbindung geladen werden soll. Dieser Eigenschaftswert besteht aus zwei Teilen, die die ConnectionTypeDefaultSolution ähnelt. Dieser Wert ist eine Kombination aus: <br>[a] der Name des Erweiterungspakets definiert, die am oberen Rand des Manifests; <br>[b] Ausrufezeichen (!); <br>[c] Toolname des Einstiegspunkts für das Tool, das anfänglich geladen werden soll. <br>Für ein Projekt mit dem Namen "msft.sme.solutionExample-Extension", und eine Lösung-Einstiegspunkt mit dem Namen "Example", wäre dieser Wert "msft.sme.solutionExample-Erweiterung Beispiel". |
| connectionStatusProvider | Informieren Sie sich im Abschnitt "Definieren Status Verbindungsanbieter" |

## <a name="define-connection-status-provider"></a>Definieren von Verbindungsanbieter-Status

Statusprovider für die Verbindung ist ein Mechanismus mit dem Ziel überprüft wird, um online und verfügbar sein, sicherzustellen, dass es sich bei der verbindenden Benutzer die Zugriffsberechtigung für das Ziel hat. Es gibt derzeit zwei Arten von Verbindungsanbieter-Status:  PowerShell und RelativeGatewayUrl.

*   <strong>PowerShell-Status Verbindungsanbieter</strong> -bestimmt, ob ein Ziel online und mit einem Powershellskript zugänglich ist. Das Ergebnis muss in einem Objekt mit einer einzelnen Eigenschaft "Status", die unten definierte zurückgegeben werden.
*   <strong>Status-Verbindungsanbieter RelativeGatewayUrl</strong> -bestimmt, ob ein Ziel, online und zugänglich ist, mit einem Rest-Aufruf ist. Das Ergebnis muss in einem Objekt mit einer einzelnen Eigenschaft "Status", die unten definierte zurückgegeben werden.

### <a name="define-status"></a>Definieren von status

Status Verbindungsanbieter sind erforderlich, um ein Objekt mit einer einzelnen Eigenschaft zurückgeben ```status``` entspricht dem folgenden Format:

``` json
{
    status: {
        label: string;
        type: int;
        details: string;
    }
}
```

Eigenschaften von Standortsystemstatus

* <strong>Bezeichnung</strong> – eine Bezeichnung, die den Rückgabetyp Status beschreibt. Beachten Sie, dass Werte für die Bezeichnung in der Common Language Runtime zugeordnet werden können. Finden Sie unter Eintrag für die Werte in Common Language Runtime.

* <strong>Typ</strong> -Typ für der Status zurück. Typ verfügt über die folgenden Enumerationswerte. Für jeden Wert 2 oder höher ist wird die Plattform wird nicht auf das verbundene Objekt navigieren, und eine Fehlermeldung angezeigt, die in der Benutzeroberfläche.

   Typen:

  | Wert | Description |
  | ----- | ----------- |
  | 0 | Online |
  | 1 | Warnung |
  | 2 | Nicht autorisiert |
  | 3 | Fehler |
  | 4 | Schwerwiegender |
  | 5 | Unbekannt |

* <strong>Details</strong> – Weitere Informationen, die den Rückgabetyp Status beschreibt.

### <a name="powershell-connection-status-provider-script"></a>Status-Verbindungsanbieter PowerShell-Skript

Das Verbindung-Status-Anbieter-PowerShell-Skript wird bestimmt, ob ein Ziel online und mit einem Powershellskript zugänglich ist. Das Ergebnis muss in einem Objekt mit einer einzelnen Eigenschaft "Status" zurückgegeben werden. Ein Beispielskript ist unten dargestellt.

Beispiel-PowerShell-Skript:

```PowerShell
## Get-My-Status ##

function Get-Status()
{
    # A function like this would be where logic would exist to identify if a node is connectable.
    $status = @{label = $null; type = 0; details = $null; }
    $caption = "MyConstCaption"
    $productType = "MyProductType"

    # A result object needs to conform to the following object structure to be interperated properly by the Windows Admin Center shell.
    $result = @{ status = $status; caption = $caption; productType = $productType; version = $version }

    # DO FANCY LOGIC #

    # Once the logic is complete, the following fields need to be populated:
    $status.label = "Display Thing"
    $status.type = 0 # This value needs to conform to the LiveConnectionStatusType enum. >= 3 represents a failure.
    $status.details = "success stuff"

    return $result
}

Get-Status
```

### <a name="define-relativegatewayurl-connection-status-provider-method"></a>Definieren Sie RelativeGatewayUrl Verbindungsanbieter-Status-Methode

Der Status-Verbindungsanbieter ```RelativeGatewayUrl``` Methode ruft eine Rest-API, um festzustellen, ob ein Ziel online und zugänglich ist. Das Ergebnis muss in einem Objekt mit einer einzelnen Eigenschaft "Status" zurückgegeben werden. Ein Beispiel einer RelativeGatewayUrl Verbindungsanbieter-Eintrag in "Manifest.JSON" finden Sie weiter unten.

``` json
    {
      "entryPointType": "connectionProvider",
      "name": "addServer",
      "path": "/add/server",
      "displayName": "resources:strings:addServer_displayName",
      "icon": "sme-icon:icon-win-server",
      "description": "resources:strings:description",
      "connectionType": "msft.sme.connection-type.server",
      "connectionTypeName": "resources:strings:addServer_connectionTypeName",
      "connectionTypeUrlName": "server",
      "connectionTypeDefaultSolution": "msft.sme.server-manager!servers",
      "connectionTypeDefaultTool": "msft.sme.server-manager!overview",
      "connectionStatusProvider": {
        "relativeGatewayUrl": "<URL here post /api>",
        "displayValueMap": {
          "wmfMissing-label": "resources:strings:addServer_status_wmfMissing_label",
          "wmfMissing-details": "resources:strings:addServer_status_wmfMissing_details",
          "unsupported-label": "resources:strings:addServer_status_unsupported_label",
          "unsupported-details": "resources:strings:addServer_status_unsupported_details"
        }
      }
    },
```

Hinweise zur Verwendung von RelativeGatewayUrl:

* "RelativeGatewayUrl" gibt an, wo Sie den Status der Verbindung von einer Gateway-URL zu erhalten. Dieser URI ist relativ aus "/ API". Wenn $connectionName in der URL gefunden wird, wird er durch den Namen der Verbindung ersetzt werden.
* Alle RelativeGatewayUrl Eigenschaften müssen für das hostgateway ausgeführt werden, die ausgeführt werden können, durch das Erstellen einer Gateway-Erweiterungs

### <a name="map-values-in-runtime"></a>Ordnen Sie Werte in Common Language runtime

Die Bezeichnung und Details-Werte in den Status Rückgabeobjekt formatiert werden kann optimieren Sie Zeit durch Einschließen von Schlüsseln und Werten in der Eigenschaft "DefaultValueMap" des Anbieters.

Z. B. Wenn Sie den folgenden Wert hinzufügen, jedes Mal, "DefaultConnection_test" wurde als Wert für Bezeichnung oder Informationen Windows Admin Center automatisch den Schlüssel mit dem Zeichenfolgenwert konfigurierten Ressource ersetzt wird.

``` json
    "defaultConnection_test": "resources:strings:addServer_status_defaultConnection_label"
```

## <a name="implement-connection-provider-in-application-layer"></a>Verbindungsanbieter-Anwendungsschicht zu implementieren.

Jetzt sind wir so implementieren Sie die Verbindungsanbieter in der Anwendungsschicht, erstellen eine TypeScript-Klasse, OnInit implementiert. Die Klasse hat die folgenden Funktionen:

| Funktion | Beschreibung |
| -------- | ----------- |
| Constructor(private appContextService: AppContextService, private Route: ActivatedRoute) |  |
| public ngOnInit() |  |
| public onSubmit() | Enthält die Logik, um die Shell zu aktualisieren, wenn ein hinzufügen Verbindungsversuche |
| Öffentliche onCancel() | Enthält die Logik, um die Shell zu aktualisieren, wenn ein Verbindungsversuch hinzufügen abgebrochen wird |

### <a name="define-onsubmit"></a>Definieren von onSubmit

```onSubmit``` Probleme ein RPC-Aufrufe zurück an den app-Kontext um die Shell eine "Verbindung hinzufügen" zu benachrichtigen. Der einfache Aufruf verwendet "UpdateData" wie folgt:

``` ts
this.appContextService.rpc.updateData(
    EnvironmentModule.nameOfShell,
    '##',
    <RpcUpdateData>{
        results: {
            connections: connections,
            credentials: this.useCredentials ? this.creds : null
        }
    }
);
```

Das Ergebnis ist eine Connection-Eigenschaft wird ein Array von Objekten, die der folgenden Struktur entsprechen:

``` ts

/**
 * The connection attributes class.
 */
export interface ConnectionAttribute {

    /**
     * The id string of this attribute
     */
    id: string;

    /**
     * The value of the attribute. used for attributes that can have variable values such as Operating System
     */
    value?: string | number;
}

/**
 * The connection class.
 */
export interface Connection {

    /**
     * The id of the connection, this is unique per connection
     */
    id: string;

    /**
     * The type of connection
     */
    type: string;

    /**
     * The name of the connection, this is unique per connection type
     */
    name: string;

    /**
     * The property bag of the connection
     */
    properties?: ConnectionProperties;

    /**
     * The ids of attributes identified for this connection
     */
    attributes?: ConnectionAttribute[];

    /**
     * The tags the user(s) have assigned to this connection
     */
    tags?: string[];
}

/**
 * Defines connection type strings known by core
 * Be careful that these strings match what is defined by the manifest of @msft-sme/server-manager
 */
export const connectionTypeConstants = {
    server: 'msft.sme.connection-type.server',
    cluster: 'msft.sme.connection-type.cluster',
    hyperConvergedCluster: 'msft.sme.connection-type.hyper-converged-cluster',
    windowsClient: 'msft.sme.connection-type.windows-client',
    clusterNodesProperty: 'nodes'
};
```

### <a name="define-oncancel"></a>OnCancel definieren

```onCancel``` Bricht einen "hinzufügen" Verbindungsversuch durch Übergeben eines Arrays leere Verbindungen ab:

``` ts
this.appContextService.rpc.updateData(EnvironmentModule.nameOfShell, '##', <RpcUpdateData>{ results: { connections: [] } });
```

## <a name="connection-provider-example"></a>Beispiel für Anbieter eine Verbindung

Die vollständige TypeScript-Klasse für die Implementierung einer Verbindungsanbieter unterschreitet. Beachten Sie, dass die Zeichenfolge "-ConnectionType", die "ConnectionType entspricht wie in der manifest.json-Verbindungsanbieter definiert.

``` ts
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';
import { AppContextService } from '@msft-sme/shell/angular';
import { Connection, ConnectionUtility } from '@msft-sme/shell/core';
import { EnvironmentModule } from '@msft-sme/shell/dist/core/manifest/environment-modules';
import { RpcUpdateData } from '@msft-sme/shell/dist/core/rpc/rpc-base';
import { Strings } from '../../generated/strings';

@Component({
  selector: 'add-example',
  templateUrl: './add-example.component.html',
  styleUrls: ['./add-example.component.css']
})
export class AddExampleComponent implements OnInit {
  public newConnectionName: string;
  public strings = MsftSme.resourcesStrings<Strings>().SolutionExample;
  private connectionType = 'msft.sme.connection-type.example'; // This needs to match the connectionTypes value used in the manifest.json.
  
  constructor(private appContextService: AppContextService, private route: ActivatedRoute) {
    // TODO:
  }

  public ngOnInit() {
    // TODO
  }

  public onSubmit() {
    let connections: Connection[] = [];

    let connection = <Connection> {
      id: ConnectionUtility.createConnectionId(this.connectionType, this.newConnectionName),
      type: this.connectionType,
      name: this.newConnectionName
    };

    connections.push(connection);

    this.appContextService.rpc.updateData(
      EnvironmentModule.nameOfShell,
      '##',
      <RpcUpdateData> {
        results: {
          connections: connections,
          credentials: null
        }
      }
    );
  }

  public onCancel() {
    this.appContextService.rpc.updateData(
      EnvironmentModule.nameOfShell, '##', <RpcUpdateData>{ results: { connections: [] } });
  }
}

```
