---
title: Erstellen eines Verbindungs Anbieters für eine projektmappenerweiterung
description: Entwickeln einer projektmappenerweiterung Windows Admin Center SDK (Project Honolulu)-Erstellen eines Verbindungs Anbieters
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/06/2019
ms.localizationpriority: medium
ms.openlocfilehash: ec11b8a6b9129348ec2405548c21fa9d6ec5deff
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952683"
---
# <a name="create-a-connection-provider-for-a-solution-extension"></a>Erstellen eines Verbindungs Anbieters für eine projektmappenerweiterung

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Verbindungsanbieter spielen eine wichtige Rolle in der Art und Weise, in der das Windows Admin Center Verbindungs fähige Objekte oder Ziele definiert und kommuniziert. In erster Linie führt ein Verbindungsanbieter Aktionen aus, während eine Verbindung hergestellt wird, z. b. sicherzustellen, dass das Ziel Online und verfügbar ist, und stellt außerdem sicher, dass der Benutzer, der die Verbindung herstellt, über die Berechtigung zum Zugreifen auf

Standardmäßig wird das Windows Admin Center mit den folgenden Verbindungs Anbietern ausgeliefert:

* Server
* Windows-Client
* Failovercluster
* HCI-Cluster

Führen Sie die folgenden Schritte aus, um einen eigenen benutzerdefinierten Verbindungsanbieter zu erstellen:

* Verbindungsanbieter Details hinzufügen```manifest.json```
* Verbindungs Status Anbieter definieren
* Implementieren des Verbindungs Anbieters in der Anwendungsschicht

## <a name="add-connection-provider-details-to-manifestjson"></a>Verbindungsanbieter Details zu manifest.jshinzufügen

Nun gehen wir darauf ein, was Sie wissen müssen, um einen Verbindungsanbieter in der Datei des Projekts zu definieren ```manifest.json``` .

### <a name="create-entry-in-manifestjson"></a>Eintrag in manifest.jserstellen

Die ```manifest.json``` Datei befindet sich im Ordner "\src" und enthält unter anderem Definitionen der Einstiegspunkte in Ihr Projekt. Zu den Typen von Einstiegspunkten zählen Tools, Projektmappen und Verbindungsanbieter. Wir definieren einen Verbindungsanbieter.

Ein Beispiel für einen Verbindungsanbieter Eintrag in manifest.json lautet unten:

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

Ein Einstiegspunkt des Typs "Verbindungsanbieter" zeigt der Windows Admin Center-Shell an, dass das konfigurierte Element ein Anbieter ist, der von einer Lösung verwendet wird, um einen Verbindungsstatus zu überprüfen. Einstiegspunkte für Verbindungsanbieter enthalten eine Reihe wichtiger Eigenschaften, die unten definiert sind:

| Eigenschaft | BESCHREIBUNG |
| -------- | ----------- |
| entryPointType | Dies ist eine erforderliche Eigenschaft. Es gibt drei gültige Werte: "Tool", "Solution" und "ConnectionProvider". |
| Name | Identifiziert den Verbindungsanbieter innerhalb des Gültigkeits Bereichs einer Projekt Mappe. Dieser Wert muss innerhalb einer vollständigen Windows Admin Center-Instanz (nicht nur einer Lösung) eindeutig sein. |
| path | Stellt den URL-Pfad für die Benutzeroberfläche "Verbindung hinzufügen" dar, wenn Sie von der Lösung konfiguriert wird. Dieser Wert muss einer Route zugeordnet werden, die in der Datei App-Routing. Module. TS konfiguriert ist. Wenn der projektmappeneinstiegs Punkt für die Verwendung der Verbindungen rootnavigationbehavior konfiguriert ist, lädt diese Route das Modul, das von der Shell verwendet wird, um die Benutzeroberfläche zum Hinzufügen von Verbindungen anzuzeigen. Weitere Informationen finden Sie im Abschnitt zu rootnavigationbehavior. |
| displayName | Der hier eingegebene Wert wird auf der rechten Seite der Shell angezeigt, wenn ein Benutzer die Verbindungs Seite eines Projektmappen lädt. |
| icon | Stellt das Symbol dar, das im Dropdown Menü Lösungen zum Darstellen der Projekt Mappe verwendet wird. |
| description | Geben Sie eine kurze Beschreibung für den Einstiegspunkt ein. |
| connectionType | Stellt den Verbindungstyp dar, der vom Anbieter geladen wird. Der hier eingegebene Wert wird auch im Einstiegspunkt der Projekt Mappe verwendet, um anzugeben, dass diese Verbindungen von der Lösung geladen werden können. Der hier eingegebene Wert wird auch in Tool Einstiegspunkten verwendet, um anzugeben, dass das Tool mit diesem Typ kompatibel ist. Dieser hier eingegebene Wert wird auch in dem Verbindungs Objekt verwendet, das an den RPC-Aufruf im Fenster "hinzufügen" im Implementierungs Schritt der Anwendungsschicht gesendet wird. |
| connectiontyname | Wird in der Verbindungstabelle verwendet, um eine Verbindung darzustellen, die ihren Verbindungsanbieter verwendet. Es wird davon ausgegangen, dass es sich um den Plural Namen des Typs handelt. |
| connectiontypeurlname | Wird beim Erstellen der URL zur Darstellung der geladenen Lösung verwendet, nachdem das Windows Admin Center eine Verbindung mit einer Instanz hergestellt hat. Dieser Eintrag wird nach Verbindungen und vor dem Ziel verwendet. In diesem Beispiel wird in "connectionexample" der Wert in der URL angezeigt:`http://localhost:6516/solutionexample/connections/connectionexample/con-fake1.corp.contoso.com` |
| connectiontypedefaultsolution | Stellt die Standardkomponente dar, die vom Verbindungsanbieter geladen werden soll. Dieser Wert ist eine Kombination aus: <br>[a] der Name des Erweiterungspakets, das am Anfang des Manifests definiert ist. <br>[b] Ausrufezeichen (!); <br>[c] der Name des projektmappeneinstiegs Punkts.    <br>Bei einem Projekt mit dem Namen "MSFT. SME. MySample-Extension" und einem Lösungs Einstiegspunkt mit dem Namen "example" lautet dieser Wert "MSFT. SME. solutionexample-Extension! example". |
| connectiontypedefaulttool | Stellt das Standard Tool dar, das bei erfolgreicher Verbindung geladen werden soll. Dieser Eigenschafts Wert besteht aus zwei Teilen, ähnlich wie bei connectiontypedefaultsolution. Dieser Wert ist eine Kombination aus: <br>[a] der Name des Erweiterungspakets, das am Anfang des Manifests definiert ist. <br>[b] Ausrufezeichen (!); <br>[c] der Name des Tool Einstiegs Punkts für das Tool, das anfänglich geladen werden soll. <br>Bei einem Projekt mit dem Namen "MSFT. SME. solutionexample-Extension" und einem Lösungs Einstiegspunkt mit dem Namen "example" lautet dieser Wert "MSFT. SME. solutionexample-Extension! example". |
| connectionstatusprovider | Weitere Informationen finden Sie im Abschnitt "definieren des Verbindungs Status Anbieters". |

## <a name="define-connection-status-provider"></a>Verbindungs Status Anbieter definieren

Der Verbindungs Status Anbieter ist der Mechanismus, mit dem ein Ziel validiert und verfügbar ist. Außerdem wird sichergestellt, dass der Benutzer, der die Verbindung herstellt, über die Berechtigung zum Zugreifen auf das Ziel verfügt. Zurzeit gibt es zwei Arten von Verbindungs Status Anbietern: PowerShell und relativegatewayurl.

*   <strong>PowerShell-Verbindungs Status Anbieter</strong> : legt fest, ob ein Ziel Online ist und mit einem PowerShell-Skript zugänglich ist. Das Ergebnis muss in einem Objekt mit einer einzelnen Eigenschaft "Status" zurückgegeben werden, die unten definiert ist.
*   <strong>Relativegatewayurl-Verbindungs Status Anbieter</strong> : bestimmt, ob ein Ziel Online ist und mit einem Rest-Aufruf zugänglich ist. Das Ergebnis muss in einem Objekt mit einer einzelnen Eigenschaft "Status" zurückgegeben werden, die unten definiert ist.

### <a name="define-status"></a>Status definieren

Verbindungs Status Anbieter müssen ein Objekt mit einer einzelnen Eigenschaft zurückgeben ```status``` , die dem folgenden Format entspricht:

``` json
{
    status: {
        label: string;
        type: int;
        details: string;
    }
}
```

Status Eigenschaften:

* <strong>Bezeichnung</strong> : eine Bezeichnung, die den Status Rückgabetyp beschreibt. Beachten Sie, dass die Werte für die Bezeichnung in der Laufzeit zugeordnet werden können. Weitere Informationen zur Zuordnung von Werten zur Laufzeit finden Sie im folgenden Eintrag.

* <strong>Type</strong> : der Status Rückgabetyp. Type weist die folgenden Enumerationswerte auf. Bei einem beliebigen Wert von 2 oder höher navigiert die Plattform nicht zum verbundenen Objekt, und es wird ein Fehler in der Benutzeroberfläche angezeigt.

   Solche

  | Wert | BESCHREIBUNG |
  | ----- | ----------- |
  | 0 | Online |
  | 1 | Warnung |
  | 2 | Nicht autorisiert |
  | 3 | Fehler |
  | 4 | FAT |
  | 5 | Unbekannt |

* <strong>Details</strong> : zusätzliche Details, die den Status Rückgabetyp beschreiben.

### <a name="powershell-connection-status-provider-script"></a>PowerShell-Verbindungs Status-Anbieter Skript

Das PowerShell-Skript für den Verbindungs Status Anbieter bestimmt, ob ein Ziel Online ist und mit einem PowerShell-Skript zugänglich ist. Das Ergebnis muss in einem Objekt mit der einzelnen Eigenschaft "Status" zurückgegeben werden. Ein Beispielskript ist unten dargestellt.

PowerShell-Beispielskript:

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

### <a name="define-relativegatewayurl-connection-status-provider-method"></a>Verbindungs Status-Anbieter Methode für relativegatewayurl definieren

Die Verbindungs Status ```RelativeGatewayUrl``` -Anbieter Methode ruft eine Rest-API auf, um zu bestimmen, ob ein Ziel Online und zugänglich ist. Das Ergebnis muss in einem Objekt mit der einzelnen Eigenschaft "Status" zurückgegeben werden. Unten ist ein Beispiel für einen Verbindungsanbieter Eintrag in manifest.json von relativegatewayurl angegeben.

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

Hinweise zur Verwendung von relativegatewayurl:

* "relativegatewayurl" gibt an, wo der Verbindungsstatus aus einer Gateway-URL angezeigt werden soll. Dieser URI ist relativ zu/API.. Wenn $ConnectionName in der URL gefunden wird, wird Sie durch den Namen der Verbindung ersetzt.
* Alle relativegatewayurl-Eigenschaften müssen für das Host Gateway ausgeführt werden. Dies kann durch Erstellen einer gatewayerweiterung erreicht werden.

### <a name="map-values-in-runtime"></a>Zuordnen von Werten zur Laufzeit

Die Bezeichnungs-und Detail Werte im Status Rückgabe Objekt können zum Zeitpunkt der Optimierung formatiert werden, indem Sie Schlüssel und Werte in die Eigenschaft "defaultvaluemap" des Anbieters einschließen.

Wenn Sie z. b. den unten angegebenen Wert hinzufügen, wird der Schlüssel automatisch durch den konfigurierten Wert der Ressourcen Zeichenfolge ersetzt, wenn "defaultConnection_test" als Wert für "Bezeichnung" oder "Details" angezeigt wird.

``` json
    "defaultConnection_test": "resources:strings:addServer_status_defaultConnection_label"
```

## <a name="implement-connection-provider-in-application-layer"></a>Implementieren des Verbindungs Anbieters in der Anwendungsschicht

Nun wird der Verbindungsanbieter in der Anwendungsschicht implementiert, indem eine typescript-Klasse erstellt wird, die OnInit implementiert. Die-Klasse verfügt über die folgenden Funktionen:

| Funktion | BESCHREIBUNG |
| -------- | ----------- |
| Konstruktor (privater appcontextservice: appcontextservice, private Route: activatedroute) |  |
| Public ngoninit () |  |
| Public onsubmit () | Enthält Logik zum Aktualisieren der Shell, wenn ein Add connection-Versuch durchgeführt wird. |
| Public OnCancel () | Enthält Logik zum Aktualisieren der Shell, wenn ein Add connection-Versuch abgebrochen wird. |

### <a name="define-onsubmit"></a>Onsubmit definieren

```onSubmit```Gibt einen RPC-Rückruf an den App-Kontext aus, um die Shell über eine "Verbindung hinzufügen" zu benachrichtigen. Der Basic-Befehl verwendet "UpdateData" wie folgt:

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

Das Ergebnis ist eine Connection-Eigenschaft, bei der es sich um ein Array von-Objekten handelt, die der folgenden-Struktur entsprechen:

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

### <a name="define-oncancel"></a>Definieren von OnCancel

```onCancel```bricht den Versuch zum Hinzufügen einer Verbindung ab, indem ein leeres Verbindungs Array übergeben wird:

``` ts
this.appContextService.rpc.updateData(EnvironmentModule.nameOfShell, '##', <RpcUpdateData>{ results: { connections: [] } });
```

## <a name="connection-provider-example"></a>Beispiel für Verbindungsanbieter

Die vollständige typescript-Klasse zum Implementieren eines Verbindungs Anbieters finden Sie unten. Beachten Sie, dass die "connectionType"-Zeichenfolge mit der "connectionType" übereinstimmt, wie im Verbindungsanbieter in manifest.json definiert.

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
