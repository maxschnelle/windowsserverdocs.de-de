---
title: Steuern des Tools Sichtbarkeit in einer Projektmappe
description: Steuern des Tools Sichtbarkeit in einer Projektmappe Windows Admin Center SDK (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: f3f34b4c86854bfc55cf4b1b57a0fd3c2baf2ffc
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/20/2018
ms.locfileid: "4080967"
---
# Steuern des Tools Sichtbarkeit in einer Projektmappe #

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Möglicherweise soll ausschließen (oder ausblenden) Sie Ihre Erweiterung oder das Tool aus der Liste der verfügbaren Tools. Z. B. wenn das Tool nur Windows Server 2016 (nicht ältere Versionen) ausgerichtet ist, sollten keinen Benutzer Sie, die mit einem Windows Server 2012 R2-Server für das Tool überhaupt finden Sie unter verbindet. (Stellen Sie sich vor der Benutzeroberfläche - sie für dieses auf, klicken Sie auf, warten, bis das Tool zum Laden, nur um eine Meldung angezeigt, dass die Funktionen nicht für die Verbindung verfügbar sind.) Sie können festlegen, wann Ihre Funktion in das Tool manifest.json Datei anzeigen (oder ausblenden).

## Optionen für die Entscheidung darüber, wann ein Tool angezeigt ##

Es gibt drei verschiedene Optionen, die Sie verwenden können, um festzustellen, ob Ihr Tool angezeigt und für einen bestimmten Server oder Cluster-Verbindung verfügbar sein sollte.

* localhost
* Inventar (ein Array von Eigenschaften)
* Skript

### LocalHost ###

Die LocalHost-Eigenschaft des Objekts Bedingungen enthält einen booleschen Wert, der zum ableiten, wenn der Verbindung Knoten LocalHost (dem gleichen Computer, die auf Windows Admin Center installiert ist) ausgewertet werden kann, oder nicht. Durch die Eigenschaft einen Wert übergeben, Sie zeigen an, wann (Bedingung) das Tool angezeigt. Beispiel, wenn Sie nur die Verwendung des Tools anzuzeigen, wenn der Benutzer tatsächlich mit dem lokalen Host verbunden ist richten Sie wie folgt aus:

``` json
"conditions": [
{
    "localhost": true
}]
```

Auch wenn Sie nur Ihr Tool angezeigt wird, wenn die Verbindung Knoten *ist nicht* Localhost:

``` json
"conditions": [
{
    "localhost": false
}]
```

Hier wird die Konfigurationseinstellungen auf nur anzeigen ein Tool aussehen bei der Verbindung Knoten kein lokaler Host ist:

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

### Inventareigenschaften ###

Das SDK enthält einen vorab zusammengestellten Satz von Inventareigenschaften, die Sie zum Erstellen von Bedingungen herausfinden, wann das Tool verfügbar oder nicht verwenden können. Es gibt neun verschiedene Eigenschaften im Array 'Bestand':

| Eigenschaftennamen | Erwarteten Wertetyp |
| ------------- | ------------------- |
| computerManufacturer | string |
| "OperatingSystemSKU" | number |
| operatingSystemVersion | Version_string (z. B.: "10.1. *") |
| Produkttyp | number |
| clusterFqdn | string |
| isHyperVRoleInstalled | boolean |
| isHyperVPowershellInstalled | boolean |
| isManagementToolsAvailable | boolean |
| isWmfInstalled | boolean |

Jedes Objekt im Array Bestand, muss die folgende Json-Struktur entsprechen:

``` json
"<property name>": {
    "type": "<expected type>",
    "operator": "<defined operator to use>",
    "value": "<expected value to evaluate using the operator>"
}
```

#### Über den Mobilfunkanbieter-Werte ####

| Operator | Beschreibung |
| -------- | ----------- |
| gt | größer als |
| ge | größer als oder gleich |
| lt | kleiner als |
| LE | kleiner als oder gleich |
| EQ | gleich |
| ne | nicht gleich |
|  auf  | Überprüfen, ob ein Wert "true" ist. |
| nicht | Überprüfen, ob ein Wert "falsch" ist. |
| enthält | Element in einer Zeichenfolge vorhanden ist |
| notContains | Element ist in einer Zeichenfolge nicht vorhanden. |

#### Datentypen ####

Verfügbare Optionen für die Eigenschaft "Typ":

| Typ | Beschreibung |
| ---- | ----------- |
| version | eine Versionsnummer aufweist (z. B.: 10.1. *) |
| number | einen numerischen Wert |
| string | einen Zeichenfolgenwert |
| boolean | "true" oder "false" |

#### Werttypen ####

Die Value-Eigenschaft akzeptiert die folgenden Typen:

* string
* number
* boolean

Ein korrekt formatiertes Inventar Bedingungssatz sieht wie folgt aus:

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

### Skript ###

Schließlich können Sie ein benutzerdefiniertes PowerShell-Skript, um die Verfügbarkeit und den Status des Knotens zu identifizieren ausführen. Alle Skripts müssen es sich um ein Objekt mit folgender Struktur zurückgegeben:

``` ps
@{
    State = 'Available' | 'NotSupported' | 'NotConfigured';
    Message = '<Message to explain the reason of state such as not supported and not configured.>';
    Properties =
        @{ Name = 'Prop1'; Value = 'prop1 data'; Type = 'string' },
        @{Name='Prop2'; Value = 12345678; Type='number'; };
}
```
Die State-Eigenschaft ist der wichtige Wert, der die Entscheidung zum Anzeigen oder Ausblenden der Erweiterungs in der Liste Tools gesteuert werden.  Zulässige Werte sind:
| Wert | Beschreibung |
| ---- | ----------- |
| Verfügbar | Die Erweiterung sollte in der Liste Tools angezeigt werden. |
| NotSupported | Die Erweiterung sollte nicht in der Liste Tools angezeigt werden. |
| Nicht konfiguriert | Dies ist ein Platzhalterwert für zukünftige Aufgaben, die der Benutzer für die weitere Konfiguration aufgefordert wird, bevor das Tool zur Verfügung gestellt wird.  Derzeit wird dieser Wert führt dazu, dass das Tool, das angezeigt wird, und entspricht der funktionalen "Verfügbar". |

Wenn Sie ein Tool zum Laden von nur dann, wenn der Remoteserver BitLocker installiert möchten, sieht das Skript beispielsweise wie folgt aus:

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

Eine Eintrag Punkt-Konfiguration, die mit der Skriptoption sieht wie folgt aus:

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

## Unterstützung von mehreren Anforderung Produktgruppen ##

Sie können mehr als eine Reihe von Anforderungen verwenden, um zu bestimmen, wann das Tool durch mehrere "Anforderungen" Blöcke definieren angezeigt werden sollen.

Z. B. das Tool anzeigen, wenn "Scenario A" oder "Scenario B" auf "true" festgelegt ist, definieren Sie zwei Anforderungen Blöcke; Wenn entweder "true" ist (d. h. alle Bedingungen in einem Block Anforderungen erfüllt sind), das Tool wird angezeigt.

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

## Unterstützung von Bedingung Bereiche ##

Sie können auch einen Bereich von Bedingungen definieren, indem mehrere "Bedingungen" Blöcke mit derselben, jedoch mit verschiedenen Operatoren definieren.

Wenn dieselbe Eigenschaft mit anderen Operatoren definiert ist, wird das Tool angezeigt werden, solange der Wert zwischen den beiden Bedingungen ist.

Dieses Tool wird beispielsweise angezeigt, solange das Betriebssystem eine Version zwischen 6.3.0 und 10.0.0 ist:

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
