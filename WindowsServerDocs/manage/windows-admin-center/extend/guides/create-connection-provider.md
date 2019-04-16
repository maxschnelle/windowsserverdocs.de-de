---
title: Erstellen eines Anbieters für die Verbindung für eine lösungserweiterung
description: Entwickeln Sie eine lösungserweiterung Windows Admin Center SDK (Projekt Honolulu) – Erstellen eines Anbieters für die Verbindung
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 883fba96fcb71cb1c6e8162c1564d66924c4e24d
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/20/2018
ms.locfileid: "4081137"
---
# Erstellen eines Anbieters für die Verbindung für eine lösungserweiterung

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Verbindung Anbieter spielen eine wichtige Rolle beim wie Windows Admin Center definiert und kommuniziert mit verbindbaren Objekte oder Ziele. In erster Linie, führt ein Anbieter für die Verbindung Aktionen, während eine Verbindung z. B. um sicherzustellen, dass das Ziel online und verfügbar ist und die Sicherstellung, dass der Verbindung Benutzer Zugriffsberechtigung für das Ziel hat, erfolgt.

Die folgenden Verbindung Anbieter Lieferumfang Windows Admin Center, in der Standardeinstellung:

* Server
* Windows-Client
* Failovercluster
* HCI Cluster

Um Ihren eigenen benutzerdefinierten Anbieter für die Verbindung zu erstellen, gehen Sie folgendermaßen vor:

* Verbindungsanbieter Details hinzugefügt werden ```manifest.json```
* Definieren Sie die Verbindung Status-Anbieter
* Verbindungsanbieter in Anwendungsebene implementieren

## Hinzufügen von Verbindungsanbieter Details zu manifest.json

Nachdem wir sehen was Sie wissen, dass um ein Anbieter für die Verbindung in Ihrem Projekts zu definieren müssen durchlaufen ```manifest.json``` Datei.

### Erstellen Sie Eintrag in manifest.json

Die ```manifest.json``` Datei befindet sich im Ordner "\src" und enthält, u. a. die Definitionen der Einstiegspunkte in Ihr Projekt. Einstiegspunkte gehören Tools, Lösungen und Anbieter-Verbindung. Wir werden ein Anbieter Verbindung definiert.

Ein Beispiel für die Eingabe eines Verbindungsanbieter in manifest.json ist unten:

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

Einstiegspunkt vom Typ "ConnnectionProvider" zeigt die Windows Admin Center-Shell, dass der zu konfigurierenden Artikel ein Anbieter, der eine Lösung verwendet wird ist, um einen Status der Verbindung überprüfen. Einstiegspunkte für Verbindung Anbieter enthält eine Reihe von wichtige Eigenschaften, die unten definiert:

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| entryPointType | Dies ist eine erforderliche Eigenschaft. Es gibt drei gültige Werte: "Tools", "Lösung" und "ConnectionProvider". | 
| name | Wird die Verbindung-Anbieter innerhalb des Bereichs einer Lösung identifiziert. Dieser Wert muss innerhalb einer vollständigen Windows Admin Center-Instanz (nicht nur eine Lösung) eindeutig sein. |
| path | Gibt den URL-Pfad für die "Verbindung hinzufügen" UI, an, ob sie von der Lösung konfiguriert werden soll. Dieser Wert muss eine Route zugeordnet werden, die in-app-routing.module.ts Datei konfiguriert ist. Wenn der Einstiegspunkt für die Lösung verwenden Sie die Verbindungen RootNavigationBehavior konfiguriert ist, wird diese Route das Modul geladen, das von der Shell verwendet wird, um die Verbindung-Benutzeroberfläche angezeigt. Weitere Informationen zur Verfügung im Abschnitt zur RootNavigationBehavior. |
| displayName | Der hier eingegebene Wert wird auf der rechten Seite der Shell, unter der Schwarz, wenn ein Benutzer eine Lösung Verbindungsseite geladen wird Windows Admin Center-Leiste angezeigt. |
| icon | Stellt das Symbol in das Dropdownmenü Lösungen verwendet, um die Lösung darstellen. |
| description | Geben Sie eine kurze Beschreibung für den Einstiegspunkt. |
| connectionType | Steht für den Verbindungstyp, den der Anbieter lädt. Der hier eingegebene Wert wird auch in der Lösung Einstiegspunkt verwendet werden, um anzugeben, dass die Lösung dieser Verbindungen laden kann. Der hier eingegebene Wert wird im Tool Eintrag erhalten auch verwendet werden, um anzugeben, dass das Tool bei dieser Art kompatibel ist. Dieser Wert, der hier eingegebene auch verwendet werden in der Verbindung-Objekten, die an die RPC übermittelt wird "hinzufügen im Fenster" in der Anwendung Ebene Implementierung Schritt aufrufen. |
| connectionTypeName | In der Verbindungstabelle verwendet, um eine Verbindung darzustellen, die Ihren Anbieter für die Verbindung verwendet. Dies ist die Mehrzahl der Name des Typs sein soll. |
| connectionTypeUrlName | Erstellen Sie die URL verwendet, um die geladene Projektmappe darzustellen, nachdem Windows Admin Center auf eine Instanz Verbindung hergestellt hat. Dieser Eintrag wird nach Verbindungen und vor dem Ziel verwendet. In diesem Beispiel ist "Connectionexample", in denen dieser Wert in der URL wird angezeigt:http://localhost:6516/solutionexample/connections/connectionexample/con-fake1.corp.contoso.com |
| connectionTypeDefaultSolution | Stellt die Standardkomponente, die vom Anbieter Verbindung geladen werden soll. Dieser Wert ist eine Kombination aus: [a] der Name des Erweiterungspakets definiert am oberen Rand des Manifests; [b] Ausrufezeichen (!); [c] die Lösung Name des Einstiegspunkts.    Dieser Wert wäre für ein Projekt mit dem Namen "msft.sme.mySample-Erweiterung" und einen Einstiegspunkt Lösung mit dem Namen "Example", "msft.sme.solutionExample-Erweiterung! Beispiel". |
| connectionTypeDefaultTool | Stellt die Standard-Tool, das über eine erfolgreiche Verbindung geladen werden soll. Dieser Wert besteht aus zwei Teilen, die ConnectionTypeDefaultSolution ähnelt. Dieser Wert ist eine Kombination aus: [a] der Name des Erweiterungspakets definiert am oberen Rand des Manifests; [b] Ausrufezeichen (!); [c] das Toolname des Einstiegspunkts für das Tool, das ursprünglich geladen werden soll. Dieser Wert wäre für ein Projekt mit dem Namen "msft.sme.solutionExample-Erweiterung" und einen Einstiegspunkt Lösung mit dem Namen "Example", "msft.sme.solutionExample-Erweiterung! Beispiel". |
| connectionStatusProvider | Finden Sie im Abschnitt "Definieren der Verbindung Status-Anbieter" |

## Definieren Sie die Verbindung Status-Anbieter

Verbindung Status Anbieter ist der Mechanismus, mit dem Ziel überprüft wird, um online und verfügbar ist, werden, die Sicherstellung, dass der Verbindung Benutzer Zugriffsberechtigung für das Ziel hat. Es gibt derzeit zwei Arten von Verbindung Status Anbieter: PowerShell und RelativeGatewayUrl.

*   PowerShell-Verbindung Status-Anbieter
    *   Bestimmt, ob ein Ziel online und mit einem Powershellskript verfügbar ist. Das Ergebnis muss in ein Objekt mit einer einzelnen Eigenschaft "Status", die unten definierten zurückgegeben werden.
*   RelativeGatewayUrl Verbindung Status Anbieter
    *   Bestimmt, ob ein Ziel online und mit einem Aufruf Rest verfügbar ist. Das Ergebnis muss in ein Objekt mit einer einzelnen Eigenschaft "Status", die unten definierten zurückgegeben werden.

### Definieren von status

Verbindung Status Anbieter sind erforderlich, um ein Objekt mit einer einzelnen Eigenschaft zurückzugeben ```status``` entspricht, die das folgende Format:

``` json
{
    status: {
        label: string;
        type: int;
        details: string;
    }
}
```

Statuseigenschaften:

* Label
    * Eine Bezeichnung, die den Status der Rückgabetyp. Beachten Sie, dass Werte für die Beschriftung-Laufzeit zugeordnet werden können. Finden Sie unter Eintrag unten für Zuordnungswerte-Laufzeit.

* Typ
    * Der Rückgabetyp Status. Art hat die folgenden Enumerationswerte. Für einen beliebigen Wert 2 oder höher ist die Plattform wird nicht auf das verbundene Objekt navigieren, und ein Fehler wird in der Benutzeroberfläche angezeigt werden.

Typen:

| Wert | Beschreibung |
| ----- | ----------- |
| 0 | Online |
| 1 | Warnung |
| 2 | Nicht autorisiert |
| 3 | Fehler |
| 4 | Schwerwiegender |
| 5 | Unknown |

* Details
    * Zusätzliche Details, die den Status der Rückgabetyp.

### PowerShell-Verbindung Status-Anbieter-Skript

Das Verbindung Status Anbieter PowerShell-Skript wird bestimmt, ob ein Ziel online und mit einem Powershellskript verfügbar ist. Das Ergebnis muss in ein Objekt mit einer einzelnen Eigenschaft "Status" zurückgegeben werden. Unten sehen Sie ein Beispielskript.

Beispiel-PowerShell-Skript:

``` ts
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

### Definieren Sie RelativeGatewayUrl Verbindung Status Anbieter-Methode

Der Verbindung Status Anbieter ```RelativeGatewayUrl``` Methode ruft eine Rest-API, um festzustellen, ob ein Ziel online und verfügbar ist. Das Ergebnis muss in ein Objekt mit einer einzelnen Eigenschaft "Status" zurückgegeben werden. Ein Beispiel Verbindungsanbieter Eintrag in manifest.json für eine RelativeGatewayUrl wird unten dargestellt.

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

* "RelativeGatewayUrl" gibt an, wie Sie den Status der Verbindung von einem Gateway-URL zu erhalten. Dieser URI ist relativ/API. Wenn $connectionName in der URL gefunden wird, wird es mit dem Namen der Verbindung ersetzt.
* Alle Eigenschaften des RelativeGatewayUrl müssen vor dem hostgateway, ausgeführt, die durch Erstellen einer Gateway-Erweiterung erreicht werden können

### Ordnen Sie Werte in der Common Language runtime

Die Beschriftung und Details Werte in den Status zurück Objekt formatiert werden kann anpassen Zeit, indem Sie die Schlüssel und Werte in der "DefaultValueMap"-Eigenschaft des Anbieters einschließen.

Z. B. Wenn Sie den folgenden Wert hinzufügen, jederzeit, "DefaultConnection_test" wurde gezeigt, Sie als Wert für die Beschriftung oder Details, Windows Admin Center den Schlüssel automatisch mit der konfigurierten Resource Zeichenfolgenwert ersetzen.

``` json
    "defaultConnection_test": "resources:strings:addServer_status_defaultConnection_label"
```

## Verbindungsanbieter in Anwendungsebene implementieren

Jetzt werden wir die Verbindung-Anbieter in der Anwendungsebene implementieren, indem eine TypeScript Klasse erstellen, OnInit implementiert. Die Klasse hat die folgenden Funktionen:

| Funktion | Beschreibung |
| -------- | ----------- |
| Konstruktor (private AppContextService: AppContextService, private Route: ActivatedRoute) |  |
| Öffentliche ngOnInit() |  |
| Öffentliche onSubmit() | Enthält die Logik Shell zu aktualisieren, wenn ein hinzufügen Verbindungsversuch |
| Öffentliche onCancel() | Enthält die Logik Shell zu aktualisieren, wenn ein Add-Verbindungsversuch abgebrochen wird |

### Definieren Sie onSubmit

```onSubmit``` Probleme RPC rufen Sie zurück an den app-Kontext zu benachrichtigen, die eine "Verbindung hinzufügen"-Shell. Der grundlegende-Aufruf verwendet "UpdateData" wie folgt aus:

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

Das Ergebnis ist eine Verbindungseigenschaft, die ein Array von Objekten, die die folgende Struktur entsprechen:

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

### Definieren Sie onCancel

```onCancel``` Bricht einen "hinzufügen" Verbindungsversuch durch Übergeben eines leeren Verbindungen Arrays ab:

``` ts
this.appContextService.rpc.updateData(EnvironmentModule.nameOfShell, '##', <RpcUpdateData>{ results: { connections: [] } });
```

## Beispiel für eine Verbindung Anbieter

Die vollständige Schreibmaschine-Klasse für die Implementierung eines Anbieters für die Verbindung finden Sie unten. Beachten Sie, dass die Zeichenfolge "ConnectionType", die "ConnectionType übereinstimmt gemäß der Definition in der Verbindungsanbieter in manifest.json.

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
