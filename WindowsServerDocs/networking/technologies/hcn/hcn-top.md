---
title: Hosten von Compute-Netzwerk (HCN)-Dienst-API für virtuelle Computer und Container
description: Der Host Compute-Netzwerk (HCN)-Dienst-API ist eine öffentlich zugängliche Win32-API, die Zugriff auf Plattformebene, um den virtuellen Netzwerken, die Endpunkte des virtuellen Netzwerks und die zugeordneten Richtlinien zu verwalten. Zusammen bietet diese Konnektivität und Sicherheit für virtuelle Computer (VMs) und Container, die auf einem Windows-Host ausgeführt.
ms.author: jmesser
author: jmesser81
ms.date: 11/05/2018
ms.openlocfilehash: 50af0dab69633aa6e07ded68e9246aa0315377f0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844981"
---
# <a name="host-compute-network-hcn-service-api-for-vms-and-containers"></a>Hosten von Compute-Netzwerk (HCN)-Dienst-API für virtuelle Computer und Container

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Der Host Compute-Netzwerk (HCN)-Dienst-API ist eine öffentlich zugängliche Win32-API, die Zugriff auf Plattformebene, um den virtuellen Netzwerken, die Endpunkte des virtuellen Netzwerks und die zugeordneten Richtlinien zu verwalten. Zusammen bietet diese Konnektivität und Sicherheit für virtuelle Computer (VMs) und Container, die auf einem Windows-Host ausgeführt. 

Entwickler verwenden die HCN-API zum Verwalten von Netzwerken für virtuelle Computer und Container in ihrer anwendungsworkflows. Die HCN-API-wurde entwickelt, um die beste für Entwickler bereit. Endbenutzer nicht direkt mit diesen APIs interagieren werden.  

## <a name="features-of-the-hcn-service-api"></a>Features der HCN-API
-   Als C-API, die vom Host Network Service (HNS) auf dem OnCore/virtuellen Computer gehostete implementiert.

-   Bietet die Möglichkeit zum Erstellen, ändern, löschen und Auflisten von HCN-Objekte, z. B. Netzwerke, Endpunkte, Namespaces und Richtlinien. Operationen auf Handles an den Objekten (z. B. einen Netzwerkhandle), und intern sind diese Handles mithilfe von RPC-Kontexthandles implementiert.

-   Schema-basiert. Die meisten Funktionen der API definieren die ein- und Ausgabeparameter als Zeichenfolgen, die die Argumente des Funktionsaufrufs als JSON-Dokumente enthält. Die JSON-Dokumente basieren auf stark typisierte und mit Versionsangabe Schemas, die diese Schemas sind Teil der öffentlichen Dokumentation. 

-   So ermöglichen Sie Clients zur Registrierung für Benachrichtigungen von den gesamten Dienst umfassenden Ereignissen wie z. B. Netzwerk, wann ein Abonnement/Rückruf-API bereitgestellt.

-   HCN API funktioniert in Desktop-Brücke (auch als) Centennial)-apps, die in die Systemdienste ausgeführt. Die API überprüft die ACL durch Abrufen von Benutzertoken vom Aufrufer an.

>[!TIP]
>Die HCN-API wird in Hintergrundaufgaben und Foreground-nicht-Windows unterstützt. 

## <a name="terminology-host-vs-compute"></a>Terminologie: Im Vergleich zu hosten. Compute
Der Host Compute-Dienst ermöglicht es dem Aufrufer erstellen und Verwalten von virtuellen Computern und Containern in einem einzelnen physischen Computer. Es heißt, Branche, Terminologie zu befolgen. 

- **Host** ist branchenweit verbreitet in der Branche Virtualisierung des Betriebssystems zu verweisen, die Ressourcen bereitstellt.

- **Compute-** wird verwendet, um auf Virtualisierung-Methoden zu verweisen, die umfangreicher als nur virtuelle Computer sind. Netzwerk-Compute-Hostdienst können Aufrufer zum Erstellen und Verwalten von Netzwerken für virtuelle Computer und Container auf einem einzelnen physischen Computer.

## <a name="schema-based-configuration-documents"></a>Schema-basierte Konfigurationsdokumente
Konfigurationsdokumente basierend auf umfassend definierte Schemas ist ein Branchenstandard im Bereich der Virtualisierung. Die meisten Virtualisierungslösungen, z. B. Docker und Kubernetes, geben Sie, dass die Konfigurationsdokumente APIs abhängig. Mehrere Branche, mit die Teilnahme von Microsoft oder kompetente ein Ökosystem zum Definieren und überprüfen diese Schemas, z. B. [OpenAPI](https://www.openapis.org/).  Diese auch kompetente der Standardisierung von bestimmten Schemadefinitionen für die Schemas verwendet für Container, z. B. [Open Container Initiative (OCI)](https://www.opencontainers.org/).

Die verwendete Sprache zum Erstellen von Dokumenten [JSON](https://tools.ietf.org/html/rfc8259), die Sie in Kombination mit verwenden:
-   Schema-Definitionen, die ein Objektmodell für das Dokument definieren.
-   Überprüfung, ob ein JSON-Dokument ein Schema entspricht
-   Automatisiert die Konvertierung von JSON-Dokumente in und aus systemeigenen Darstellungen dieser Schemas in den Programmiersprachen, die verwendet werden, durch den Aufrufer der APIs 

Werden Sie häufig verwendete Schemadefinitionen [OpenAPI](https://www.openapis.org/) und [JSON-Schema](http://json-schema.org/), dem Sie die ausführlichen Definitionen der Eigenschaften in einem Dokument, z. B. angeben können:
-   Die gültigen Satz von Werten für eine Eigenschaft, z. B. 0 – 100 für eine Eigenschaft, die einen Prozentsatz darstellt.
-   Die Definition von Enumerationen, die als einen Satz von gültigen Zeichenfolgen für eine Eigenschaft dargestellt werden.
-   Ein regulärer Ausdruck für das erwartete Format einer Zeichenfolge. 

Im Rahmen der HCN APIs dokumentieren planen wir das Schema von unserem JSON-Dokumenten als einer OpenAPI-Spezifikation zu veröffentlichen. Auf der Grundlage dieser Spezifikation, können sprachspezifische Darstellung des Schemas für die typsichere Verwendung Schemaobjekte in der Programmiersprache, die vom Client verwendet wird. 

### <a name="example"></a>Beispiel 

Folgendes ist ein Beispiel für diesen Workflow für das Objekt, das einen SCSI-Controller, in dem Dokument zur Konfiguration eines virtuellen Computers darstellt. 

In der Windows-Quellcode, definieren wir die Schemas, die mithilfe von .mars-Dateien: onecore/vm/dv/net/hns/schema/mars/Schema/HCN.Schema.Network.mars

```
enum IpamType
{
    [NewIn("2.0")] Static,
    [NewIn("2.0")] Dhcp,
};

class Ipam
{
    // Type : dhcp
    [NewIn("2.0"),OmitEmpty] IpamType   Type;
    [NewIn("2.0"),OmitEmpty] Subnet     Subnets[];
};

class Subnet : HCN.Schema.Common.Base
{
    [NewIn("2.0"),OmitEmpty] string         IpAddressPrefix;
    [NewIn("2.0"),OmitEmpty] SubnetPolicy   Policies[];
    [NewIn("2.0"),OmitEmpty] Route          Routes[];
};


enum SubnetPolicyType
{
    [NewIn("2.0")] VLAN
};

class SubnetPolicy
{
    [NewIn("2.0"),OmitEmpty] SubnetPolicyType                 Type;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Common.PolicySettings Data;
};

class PolicySettings
{
    [NewIn("2.0"),OmitEmpty]  string      Name;
};

class VlanPolicy : HCN.Schema.Common.PolicySettings 
{
    [NewIn("2.0")] uint32 IsolationId;
};

class Route 
{
    [NewIn("2.0"),OmitEmpty] string NextHop;
    [NewIn("2.0"),OmitEmpty] string DestinationPrefix;
    [NewIn("2.0"),OmitEmpty] uint16 Metric;
};

```

>[!TIP]
>Die [NewIn("2.0") Anmerkungen sind Teil der Unterstützung der versionsverwaltung für die Schemadefinitionen.

Aus dieser Definition interne generieren wir die OpenAPI-Spezifikationen für das Schema ein:

```
{ 
    "swagger" : "2.0", 
    "info" : { 
       "version" : "2.1", 
       "title" : "HCN API" 
    },
    "definitions": {        
        "Ipam": {
            "type": "object",
            "properties": {
                "Type": {
                    "type": "string",
                    "enum": [
                        "Static",
                        "Dhcp"
                    ],
                    "description": " Type : dhcp"
                },
                "Subnets": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/Subnet"
                    }
                }
            }
        },
        "Subnet": {
            "type": "object",
            "properties": {
                "ID": {
                    "type": "string",
                    "pattern": "^[0-9A-Fa-f]{8}-([0-9A-Fa-f]{4}-){3}[0-9A-Fa-f]{12}$"
                },                
                "IpAddressPrefix": {
                    "type": "string"
                },
                "Policies": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/SubnetPolicy"
                    }
                },
                "Routes": {
                    "type": "array",
                    "items": {
                        "$ref": "#/definitions/Route"
                    }
                }
            }
        },
        "SubnetPolicy": {
            "type": "object",
            "properties": {
                "Type": {
                    "type": "string",
                    "enum": [
                        "VLAN",
                        "VSID"
                    ]
                },
                "Data": {
                    "$ref": "#/definitions/PolicySettings"
                }
            }
        },
        "PolicySettings": {
            "type": "object",
            "properties": {
                "Name": {
                    "type": "string"
                }
            }
        },                      
        "VlanPolicy": {
            "type": "object",
            "properties": {
                "Name": {
                    "type": "string"
                },
                "IsolationId": {
                    "type": "integer",
                    "format": "uint32"
                }
            }
        },
        "Route": {
            "type": "object",
            "properties": {
                "NextHop": {
                    "type": "string"
                },
                "DestinationPrefix": {
                    "type": "string"
                },
                "Metric": {
                    "type": "integer",
                    "format": "uint16"
                }
            }
        }        
    }
} 
```

Sie verwenden die Tools, z. B. [Swagger](https://swagger.io/), um sprachspezifische Darstellung des Schemas von einem Client verwendete Programmiersprache zu generieren. Swagger unterstützt eine Vielzahl von Sprachen wie z. B. C#, Go, Javascript und Python).

- [Beispiel für generierte C# Code](example-c-sharp.md) Objekt der obersten Ebene IPAM & Subnetz.

- [Beispiel für Go-Code generierten](example-go.md) Objekt der obersten Ebene IPAM & Subnetz. Go wird von Docker und Kubernetes sind zwei der Nutzer von der Host Compute-Netzwerk-APIs verwendet. Wechseln Sie verfügt über integrierte Unterstützung für das Marshalling von Go-Typen in und aus JSON-Dokumente.

Zusätzlich zur codegenerierung und-Validierung, können Sie Tools zur Vereinfachung der Arbeit mit JSON-Dokumenten, d. h. [Visual Studio Code](https://code.visualstudio.com/Docs/languages/json).

### <a name="top-level-objects-defined-in-the-hcnschemasmars-file"></a>Objekte der obersten Ebene in der HCN definiert. Schemas.MARS-Datei
Wie bereits erwähnt, finden Sie das Dokumentschema für Dokumente, die von den HCN-APIs in einem Satz von .mars-Dateien verwendet: Onecore/Vm/Dv/Net/Hns/Schema/Mars/Schema

Objekte der obersten Ebene sind:
- [HostComputeNetwork](hcn-scenarios.md#scenario-hcn)
- [HostComputeEndpoint](hcn-scenarios.md#scenario-hcn-endpoint)
- [HostComputeNamespace](hcn-scenarios.md#scenario-hcn-namespace)
- [HostComputeLoadBalancer](hcn-scenarios.md#scenario-hcn-load-balancer)

```
class HostComputeNetwork : HCN.Schema.Common.Base
{
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.NetworkMode          Type;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.NetworkPolicy        Policies[];
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.MacPool              MacPool;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.DNS                  Dns;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.Ipam                 Ipams[];
};

class HostComputeEndpoint : HCN.Schema.Common.Base
{
    [NewIn("2.0"),OmitEmpty] string                                     HostComputeNetwork;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.Endpoint.EndpointPolicy Policies[];
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.Endpoint.IpConfig       IpConfigurations[];
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.DNS                     Dns;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Network.Route                   Routes[];
    [NewIn("2.0"),OmitEmpty] string                                     MacAddress;
};

class HostComputeNamespace : HCN.Schema.Common.Base
{
    [NewIn("2.0"),OmitEmpty] uint32                                    NamespaceId;
    [NewIn("2.0"),OmitEmpty] Guid                                      NamespaceGuid;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Namespace.NamespaceType        Type;
    [NewIn("2.0"),OmitEmpty] HCN.Schema.Namespace.NamespaceResource    Resources[];
};

class HostComputeLoadBalancer : HCN.Schema.Common.Base
{
    [NewIn("2.0"), OmitEmpty] string                                               HostComputeEndpoints[]; 
    [NewIn("2.0"), OmitEmpty] string                                               VirtualIPs[]; 
    [NewIn("2.0"), OmitEmpty] HCN.Schema.Network.Endpoint.Policy.PortMappingPolicy PortMappings[]; 
    [NewIn("2.0"), OmitEmpty] HCN.Schema.LoadBalancer.LoadBalancerPolicy           Policies[];
};
```

## <a name="next-steps"></a>Nächste Schritte

- Erfahren Sie mehr über die [Szenarios HCN](hcn-scenarios.md).

- Erfahren Sie mehr über die [RPC-Kontext für HCN behandelt](hcn-declaration-handles.md).

- Erfahren Sie mehr über die [HCN JSON-Dokumentschemas](hcn-json-document-schemas.md).