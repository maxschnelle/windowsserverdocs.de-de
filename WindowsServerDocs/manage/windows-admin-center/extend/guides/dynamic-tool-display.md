---
title: Steuern der Sichtbarkeit Ihres Tools in einer Lösung
description: Steuern der Sichtbarkeit Ihres Tools in einer Lösung Windows Admin Center SDK (Project Honolulu)
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: df939bb1a87c9ded77431661dcabd7faf607bb6e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87945003"
---
# <a name="control-your-tools-visibility-in-a-solution"></a>Steuern der Sichtbarkeit Ihres Tools in einer Lösung #

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Es kann vorkommen, dass Sie die Erweiterung oder das Tool aus der Liste der verfügbaren Tools ausschließen (oder ausblenden) möchten. Wenn Ihr Tool z. b. nur auf Windows Server 2016 (nicht ältere Versionen) ausgerichtet ist, möchten Sie möglicherweise nicht, dass ein Benutzer, der eine Verbindung mit einem Windows Server 2012 R2-Server herstellt, das Tool überhaupt anzeigen kann. (Stellen Sie sich die Benutzerumgebung vor: Sie klicken darauf, und warten Sie, bis das Tool geladen wird, um eine Meldung zu erhalten, dass ihre Features für Ihre Verbindung nicht verfügbar sind.) Sie können definieren, wann Sie Ihre Funktion in der manifest.jsDatei des Tools anzeigen (oder ausblenden) möchten.

## <a name="options-for-deciding-when-to-show-a-tool"></a>Optionen für die Entscheidung, wann ein Tool angezeigt werden soll ##

Es gibt drei verschiedene Optionen, die Sie verwenden können, um zu bestimmen, ob das Tool für eine bestimmte Server-oder Cluster Verbindung angezeigt und verfügbar sein soll.

* Localhost
* Inventar (ein Array von Eigenschaften)
* script

### <a name="localhost"></a>LocalHost ###

Die localhost-Eigenschaft des conditions-Objekts enthält einen booleschen Wert, der ausgewertet werden kann, um zu ableiten, ob der Verbindungsknoten "localhost" (derselbe Computer, auf dem Windows Admin Center installiert ist) ist. Wenn Sie einen Wert an die-Eigenschaft übergeben, geben Sie an, wann (die Bedingung) das Tool angezeigt werden soll. Wenn das Tool beispielsweise nur angezeigt werden soll, wenn der Benutzer tatsächlich eine Verbindung mit dem lokalen Host herstellt, legen Sie es wie folgt fest:

``` json
"conditions": [
{
    "localhost": true
}]
```

Wenn das Tool nur angezeigt werden soll, wenn der Verbindungsknoten nicht "localhost" *ist* :

``` json
"conditions": [
{
    "localhost": false
}]
```

In den Konfigurationseinstellungen sehen Sie, dass nur ein Tool angezeigt wird, wenn der Verbindungsknoten nicht "localhost" ist:

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

### <a name="inventory-properties"></a>Inventur Eigenschaften ###

Das SDK enthält einen vordefinierten Satz von Inventur Eigenschaften, mit denen Sie Bedingungen erstellen können, um zu bestimmen, wann das Tool verfügbar sein sollte. Das Array "Inventory" enthält neun verschiedene Eigenschaften:

| Eigenschaftenname | Erwarteter Werttyp |
| ------------- | ------------------- |
| Computerhersteller | Zeichenfolge |
| OperatingSystemSKU | number |
| operatingSystemVersion | version_string (z. b. "10,1. *") |
| productType | number |
| Cluster-qdn | Zeichenfolge |
| ishypervroleinstemmt | boolean |
| ishypervpowershellinstalliert | boolean |
| ismanagementtoolsavailable | boolean |
| iswmfingestrandet | boolean |

Jedes Objekt im Inventur Array muss der folgenden JSON-Struktur entsprechen:

``` json
"<property name>": {
    "type": "<expected type>",
    "operator": "<defined operator to use>",
    "value": "<expected value to evaluate using the operator>"
}
```

#### <a name="operator-values"></a>Operator Werte ####

| Operator | BESCHREIBUNG |
| -------- | ----------- |
| gt | Größer als |
| ge | Größer oder gleich |
| lt | Kleiner als |
| le | Kleiner oder gleich |
| eq | gleich |
| ne | not equal to (ungleich) |
| is | Überprüfen, ob ein Wert true ist |
| not | Überprüfen, ob ein Wert false ist |
| contains | Element ist in einer Zeichenfolge vorhanden. |
| notContains | das Element ist in einer Zeichenfolge nicht vorhanden. |

#### <a name="data-types"></a>Datentypen ####

Verfügbare Optionen für die Eigenschaft "Type":

| Typ | BESCHREIBUNG |
| ---- | ----------- |
| version | eine Versionsnummer (z. b. 10,1. *) |
| number | ein numerischer Wert |
| Zeichenfolge | ein Zeichen folgen Wert |
| boolean | true oder false |

#### <a name="value-types"></a>Werttypen ####

Die Value-Eigenschaft akzeptiert folgende Typen:

* Zeichenfolge
* Zahl
* boolean

Ein ordnungsgemäß geformter Inventur Bedingungs Satz sieht wie folgt aus:

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

Zum Schluss können Sie ein benutzerdefiniertes PowerShell-Skript ausführen, um die Verfügbarkeit und den Status des Knotens zu ermitteln. Alle Skripts müssen ein Objekt mit der folgenden Struktur zurückgeben:

``` ps
@{
    State = 'Available' | 'NotSupported' | 'NotConfigured';
    Message = '<Message to explain the reason of state such as not supported and not configured.>';
    Properties =
        @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' },
        @{Name='Prop2'; Value = 12345678; Type='number'; };
}
```
Die State-Eigenschaft ist der wichtige Wert, der die Entscheidung steuert, ihre Erweiterung in der Liste der Tools anzuzeigen oder auszublenden.  Zulässige Werte sind:

| Wert | BESCHREIBUNG |
| ---- | ----------- |
| Verfügbar | Die Erweiterung sollte in der Liste der Tools angezeigt werden. |
| NotSupported | Die Erweiterung sollte nicht in der Liste der Tools angezeigt werden. |
| NotConfigured | Dies ist ein Platzhalter für zukünftige arbeiten, der den Benutzer zur weiteren Konfiguration auffordert, bevor das Tool zur Verfügung gestellt wird.  Zurzeit führt dieser Wert dazu, dass das Tool angezeigt wird und das funktionale Äquivalent zu "available" ist. |

Wenn beispielsweise ein Tool nur geladen werden soll, wenn auf dem Remote Server BitLocker installiert ist, sieht das Skript wie folgt aus:

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

Eine Einstiegspunkt Konfiguration mit der Option Skript sieht wie folgt aus:

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

## <a name="supporting-multiple-requirement-sets"></a>Unterstützen mehrerer Anforderungs Sätze ##

Sie können mehr als einen Satz von Anforderungen verwenden, um zu bestimmen, wann das Tool durch Definieren mehrerer "Anforderungs Blöcke" angezeigt werden soll.

Wenn Sie z. b. das Tool anzeigen möchten, wenn "Szenario A" oder "Szenario B" true ist, definieren Sie zwei Anforderungs Blöcke. Wenn eine der beiden Bedingungen erfüllt ist (d. h. alle Bedingungen in einem Anforderungs Block sind erfüllt), wird das Tool angezeigt.

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

## <a name="supporting-condition-ranges"></a>Unterstützende Bedingungs Bereiche ##

Sie können auch einen Bereich von Bedingungen definieren, indem Sie mehrere "Bedingungen"-Blöcke mit derselben Eigenschaft definieren, aber mit unterschiedlichen Operatoren.

Wenn die gleiche Eigenschaft mit unterschiedlichen Operatoren definiert ist, wird das Tool so lange angezeigt, wie der Wert zwischen den beiden Bedingungen liegt.

Das Tool wird z. b. angezeigt, solange das Betriebssystem eine Version zwischen 6.3.0 und 10.0.0 ist:

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
