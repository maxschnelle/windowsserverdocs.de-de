---
title: Steuern des Tools Sichtbarkeit in einer Projektmappe
description: Steuern des Tools Sichtbarkeit in einer Projektmappe Windows Admin Center-SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 3cce07ba5b3d2cc89f1363bbb2af5acd048c0466
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445943"
---
# <a name="control-your-tools-visibility-in-a-solution"></a>Steuern des Tools Sichtbarkeit in einer Projektmappe #

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Es gibt möglicherweise Situationen ausschließen (oder ausblenden) Sie Ihre Extension oder Tool aus der Liste der verfügbaren Tools. Z. B. wenn das Tool nur Windows Server 2016 (nicht für ältere Versionen) ausgerichtet ist, empfiehlt keinen Benutzer, die auf einem Windows Server 2012 R2-Server, Ihr Tool überhaupt finden eine Verbindung herstellt. (Stellen Sie sich vor der benutzererfahrung: sie klicken Sie darauf, warten Sie, bis das Tool zu laden, nur für eine Meldung angezeigt, dass die Funktionen nicht für die Verbindung verfügbar sind.) Sie können definieren, wenn das Feature in der manifest.json-Datei des Tools angezeigt (oder ausgeblendet).

## <a name="options-for-deciding-when-to-show-a-tool"></a>Optionen für die Entscheidung, wann ein Tool angezeigt werden. ##

Es gibt drei verschiedene Optionen, die Sie verwenden können, um zu bestimmen, ob Ihr Tool angezeigt werden und für einen bestimmten Server oder Cluster-Verbindung verfügbar sein soll.

* localhost
* Softwareinventur (ein Array von Eigenschaften)
* Skript

### <a name="localhost"></a>LocalHost ###

Die "localhost"-Eigenschaft des Objekts Bedingungen enthält einen booleschen Wert, der ausgewertet werden kann, um zu ermitteln, ob der verbindende Knoten "localhost" (dem gleichen Computer, die ist auf Windows Admin Center installiert ist) oder nicht. Durch Übergeben eines Werts der Eigenschaft an, Sie zeigen an, wann (Bedingung) das Tool angezeigt. Z. B., wenn Sie nur vom Tool angezeigt wird, wenn der Benutzer tatsächlich auf dem lokalen Host eine Verbindung herstellt richten sie Sie wie folgt:

``` json
"conditions": [
{
    "localhost": true
}]
```

Auch wenn Sie nur das Tool angezeigt wird, wenn der Knoten eine Verbindung herstellen *ist nicht* "localhost":

``` json
"conditions": [
{
    "localhost": false
}]
```

Hier wird die Konfigurationseinstellungen, zeigt nur ein Tool aussehen, wenn der Knoten eine Verbindung herstellt, nicht "localhost" ist:

``` json
"entryPoints": [
{
    "entryPointType": "tool",
    "name": "main",
    "urlName": "processes",
    "displayName": "resources:strings:displayName",
    "description": "resources:strings:description",
    "icon": "sme-icon:icon-win-serverProcesses",
    "path": "",
    "requirements": [
    {
        "solutionIds": [
        "msft.sme.server-manager!windowsClients"
        ],
        "connectionTypes": [
        "msft.sme.connection-type.windows-client"
        ],
        "conditions": [
        {
            "localhost": true
        }
        ]
    }
    ]
}
```

### <a name="inventory-properties"></a>Eigenschaften der Hardwareinventur ###

Das SDK enthält einen vorab zusammengestellten Satz von Eigenschaften des Hardwareinventurclient, die Sie verwenden können, um zu bestimmen, wenn das Tool verfügbar sein sollen oder nicht erstellen. Es gibt neun verschiedene Eigenschaften in das Array 'Inventur' ein:

| Eigenschaftenname | Erwarteter Wert |
| ------------- | ------------------- |
| computerManufacturer | String |
| operatingSystemSKU | number |
| operatingSystemVersion | Version_string (z.B.: "10.1.*") |
| productType | number |
| clusterFqdn | String |
| isHyperVRoleInstalled | boolean |
| isHyperVPowershellInstalled | boolean |
| isManagementToolsAvailable | boolean |
| isWmfInstalled | boolean |

Jedes Objekt in das Inventar-Array muss die folgenden JSON-Struktur entsprechen:

``` json
"<property name>": {
    "type": "<expected type>",
    "operator": "<defined operator to use>",
    "value": "<expected value to evaluate using the operator>"
}
```

#### <a name="operator-values"></a>Operatorwerte ####

| Operator | Beschreibung |
| -------- | ----------- |
| gt | Größer als |
| ge | Größer als oder gleich |
| lt | Kleiner als |
| LE | Kleiner als oder gleich |
| eq | Gleich |
| ne | Ungleich |
| auf | überprüft, ob ein Wert "true" ist. |
| not | überprüft, ob ein Wert "false" ist. |
| Enthält | Element vorhanden ist, in einer Zeichenfolge |
| notContains | Element ist in einer Zeichenfolge nicht vorhanden. |

#### <a name="data-types"></a>Datentypen ####

Verfügbare Optionen für die Eigenschaft "Type":

| Typ | Beschreibung |
| ---- | ----------- |
| version | eine Versionsnummer (z. B.: 10.1.*) |
| number | ein numerischer Wert |
| String | Ein String-Wert |
| boolean | "true" oder "false" |

#### <a name="value-types"></a>Werttypen ####

Die Eigenschaft "Value" akzeptiert diese Typen:

* String
* number
* boolean

Bedingung festgelegt. eine ordnungsgemäß formatierte Inventur sieht folgendermaßen aus:

``` json
"entryPoints": [
{
    "entryPointType": "tool",
    "name": "main",
    "urlName": "processes",
    "displayName": "resources:strings:displayName",
    "description": "resources:strings:description",
    "icon": "sme-icon:icon-win-serverProcesses",
    "path": "",
    "requirements": [
    {
        "solutionIds": [
        "msft.sme.server-manager!servers"
        ],
        "connectionTypes": [
        "msft.sme.connection-type.server"
        ],
        "conditions": [
        {
            "inventory": {
            "operatingSystemVersion": {
                "type": "version",
                "operator": "gt",
                "value": "6.3"
            },
            "operatingSystemSKU": {
                "type": "number",
                "operator": "eq",
                "value": "8"
            }
            }
        }
        ]
    }
    ]
}
```

### <a name="script"></a>Skript ###

Schließlich können Sie ein benutzerdefiniertes Powershellskript zum Identifizieren der Verfügbarkeit und Zustand des Knotens ausführen. Alle Skripts müssen es sich um ein Objekt mit der folgenden Struktur zurückgeben:

``` ps
@{
    State = 'Available' | 'NotSupported' | 'NotConfigured';
    Message = '<Message to explain the reason of state such as not supported and not configured.>';
    Properties =
        @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' },
        @{Name='Prop2'; Value = 12345678; Type='number'; };
}
```
Die State-Eigenschaft ist wichtig, Wert, mit der gesteuert wird, die Entscheidung, ein- oder Ausblenden von Ihre Erweiterung in der Liste der Tools.  Zulässige Werte sind:

| Wert | Beschreibung |
| ---- | ----------- |
| Verfügbar | Die Erweiterung sollte in der Liste der Tools angezeigt werden. |
| NotSupported | Die Erweiterung sollte nicht in der Liste der Tools angezeigt werden. |
| NotConfigured | Dies ist ein Platzhalterwert für künftige Entwicklungen, die der Benutzer für die weitere Konfiguration aufgefordert wird, bevor das Tool zur Verfügung gestellt wird.  Derzeit wird dieser Wert führt dazu, dass das Tool, das angezeigt wird, und entspricht funktional auf "Verfügbar". |

Wenn Sie möchten ein Tool zum Laden nur dann, wenn der Remoteserver BitLocker installiert wurde, sucht das Skript beispielsweise wie folgt:

``` ps
$response = @{
    State = 'NotSupported';
    Message = 'Not executed';
    Properties = @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' },
        @{Name='Prop2'; Value = 12345678; Type='number'; };
}

if (Get-Module -ListAvailable -Name servermanager) {
    Import-module servermanager; 
    $isInstalled = (Get-WindowsFeature -name bitlocker).Installed;
    $isGood = $isInstalled;
}

if($isGood) {
    $response.State = 'Available';
    $response.Message = 'Everything should work.';
}

$response
```

Eine Punkt der Konfiguration des standardanmeldeeintrags mithilfe der Skriptoption sieht folgendermaßen aus:

``` json
"entryPoints": [
{
    "entryPointType": "tool",
    "name": "main",
    "urlName": "processes",
    "displayName": "resources:strings:displayName",
    "description": "resources:strings:description",
    "icon": "sme-icon:icon-win-serverProcesses",
    "path": "",
    "requirements": [
    {
        "solutionIds": [
        "msft.sme.server-manager!windowsClients"
        ],
        "connectionTypes": [
        "msft.sme.connection-type.windows-client"
        ],
        "conditions": [
        {
            "localhost": true,
            "inventory": {
            "operatingSystemVersion": {
                "type": "version",
                "operator": "eq",
                "value": "10.0.*"
            },
            "operatingSystemSKU": {
                "type": "number",
                "operator": "eq",
                "value": "4"
            }
            },
            "script": "$response = @{ State = 'NotSupported'; Message = 'Not executed'; Properties = @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' }, @{Name='Prop2'; Value = 12345678; Type='number'; }; }; if (Get-Module -ListAvailable -Name servermanager) { Import-module servermanager; $isInstalled = (Get-WindowsFeature -name bitlocker).Installed; $isGood = $isInstalled; }; if($isGood) { $response.State = 'Available'; $response.Message = 'Everything should work.'; }; $response"
        }
        ]
    }
    ]
}
```

## <a name="supporting-multiple-requirement-sets"></a>Unterstützt mehrere Sätze von Anforderungen ##

Sie können mehr als ein Satz von Anforderungen verwenden, um zu bestimmen, wann Ihr Tool anzeigen, indem Sie mehrere Blöcke von "Anforderungen" definieren.

Das Tool anzeigen, wenn beispielsweise "Szenario A" oder "Szenario B" ist "true", definieren Sie zwei Anforderungen Blöcke; Wenn entweder "true" ist (d. h. alle Bedingungen in einem Block Anforderungen erfüllt sind), das Tool wird angezeigt.

``` json
"entryPoints": [
{
    "requirements": [
    {
        "solutionIds": [
            …"scenario A"…
        ],
        "connectionTypes": [
            …"scenario A"…
        ],
        "conditions": [
            …"scenario A"…
        ]
    },
    {
        "solutionIds": [
            …"scenario B"…
        ],
        "connectionTypes": [
            …"scenario B"…
        ],
        "conditions": [
            …"scenario B"…
        ]
    }
    ]
}

```

## <a name="supporting-condition-ranges"></a>Unterstützung von Bereichen der Bedingung ##

Sie können auch einen Bereich von Bedingungen definieren, durch Definieren von mehreren "Bedingungen"-Blöcken, die mit der gleichen Eigenschaft, aber mit verschiedenen Operatoren verwenden.

Wenn die gleiche Eigenschaft, die mit anderen Operatoren definiert ist, wird das Tool angezeigt, solange der Wert zwischen den zwei Bedingungen.

Dieses Tool wird beispielsweise angezeigt, solange das Betriebssystem eine Version 6.3.0 bis 10.0.0 ist:

``` json
"entryPoints": [
{
    "entryPointType": "tool",
    "name": "main",
    "urlName": "processes",
    "displayName": "resources:strings:displayName",
    "description": "resources:strings:description",
    "icon": "sme-icon:icon-win-serverProcesses",
    "path": "",
    "requirements": [
    {
        "solutionIds": [
             "msft.sme.server-manager!servers"
        ],
        "connectionTypes": [
             "msft.sme.connection-type.server"
        ],
        "conditions": [
        {
            "inventory": {
                "operatingSystemVersion": {
                    "type": "version",
                    "operator": "gt",
                    "value": "6.3.0"
                },
            }
        },
        {
            "inventory": {
                "operatingSystemVersion": {
                    "type": "version",
                    "operator": "lt",
                    "value": "10.0.0"
                }
            }
        }
        ]
    }
    ]
}

```
