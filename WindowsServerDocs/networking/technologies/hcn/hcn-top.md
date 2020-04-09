---
title: Host Compute Network (HCN)-Dienst-API für VMS und Container
description: Die HCN-Dienst-API (Host Compute Network) ist eine öffentlich zugänglichen Win32-API, die Zugriff auf Platt Form Ebene zum Verwalten der virtuellen Netzwerke, der virtuellen Netzwerk Endpunkte und der zugehörigen Richtlinien bietet. Dies ermöglicht die Konnektivität und Sicherheit für virtuelle Computer (Virtual Machines, VMS) und Container, die auf einem Windows-Host ausgeführt werden.
ms.author: jmesser
author: jmesser81
ms.prod: windows-server
ms.date: 11/05/2018
ms.openlocfilehash: 4afde574802bd63db8ea8ca8db9f5daf1a53dc93
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859843"
---
# <a name="host-compute-network-hcn-service-api-for-vms-and-containers"></a>Host Compute Network (HCN)-Dienst-API für VMS und Container

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019

Die HCN-Dienst-API (Host Compute Network) ist eine öffentlich zugänglichen Win32-API, die Zugriff auf Platt Form Ebene zum Verwalten der virtuellen Netzwerke, der virtuellen Netzwerk Endpunkte und der zugehörigen Richtlinien bietet. Dies ermöglicht die Konnektivität und Sicherheit für virtuelle Computer (Virtual Machines, VMS) und Container, die auf einem Windows-Host ausgeführt werden. 

Entwickler verwenden die HCN-Dienst-API, um Netzwerke für VMS und Container in ihren Anwendungs Workflows zu verwalten. Die HCN-API wurde entwickelt, um Entwicklern das beste Verhalten zu bieten. Endbenutzer interagieren nicht direkt mit diesen APIs.  

## <a name="features-of-the-hcn-service-api"></a>Features der HCN-Dienst-API
-    Wird als C-API implementiert, die vom Host Netzwerkdienst (HNS) auf der Oncore/VM gehostet wird.

-    Bietet die Möglichkeit, HCN-Objekte, z. b. Netzwerke, Endpunkte, Namespaces und Richtlinien, zu erstellen, zu ändern, zu löschen und aufzuzählen. Vorgänge werden in Handles für die Objekte (z. b. ein Netzwerk handle) durchgeführt, und intern werden diese Handles mithilfe von RPC-Kontext Handles implementiert.

-    Schema basiert. Die meisten Funktionen der API definieren Eingabe-und Ausgabeparameter als Zeichen folgen, die die Argumente des Funktions Aufrufes als JSON-Dokumente enthalten. Die JSON-Dokumente basieren auf stark typisierten und versionierten Schemas. diese Schemas sind Teil der öffentlichen Dokumentation. 

-    Eine Abonnement-/Rückruf-API wird bereitgestellt, um Clients das Registrieren für Benachrichtigungen von Dienst weiten Ereignissen wie z. b. Netzwerk Erstellungen und Löschungen zu ermöglichen.

-    HCN-API funktioniert in Desktop Bridge (auch bekannt als Centennial) apps, die in System Diensten ausgeführt werden. Die API überprüft die ACL, indem das Benutzer Token vom Aufrufer abgerufen wird.

>[!TIP]
>Die HCN-Dienst-API wird in Hintergrundaufgaben und nicht-Vordergrund-Fenstern unterstützt. 

## <a name="terminology-host-vs-compute"></a>Terminologie: Host und Compute
Der hostcomputedienst ermöglicht es Aufrufern, virtuelle Maschinen und Container auf einem einzelnen physischen Computer zu erstellen und zu verwalten. Sie hat den Namen, um die Branchen Terminologie zu befolgen. 

- Der **Host** wird in der Virtualisierungstechnologie häufig verwendet, um auf das Betriebssystem zu verweisen, das virtualisierte Ressourcen bereitstellt.

- **Compute** bezieht sich auf virtualisierungsmethoden, die breiter als nur virtuelle Computer sind. Der Host Compute-Netzwerkdienst ermöglicht Aufrufern das Erstellen und Verwalten von Netzwerken für virtuelle Maschinen und Container auf einem einzelnen physischen Computer.

## <a name="schema-based-configuration-documents"></a>Schema basierte Konfigurations Dokumente
Konfigurations Dokumente, die auf klar definierten Schemas basieren, sind im Virtualisierungsbereich ein etablierter Industriestandard. Die meisten Virtualisierungslösungen, wie z. b. docker und Kubernetes, stellen APIs auf der Grundlage von Konfigurations Dokumenten bereit. Mehrere Brancheninitiativen, mit der Teilnahme von Microsoft, fördern ein Ökosystem zum Definieren und validieren dieser Schemas, z. b. [OpenAPI](https://www.openapis.org/).  Diese Initiativen Steuern auch die Standardisierung spezifischer Schema Definitionen für die Schemas, die für Container verwendet werden, wie z. b. [Open Container Initiative (OCI)](https://www.opencontainers.org/).

Die Sprache, die zum Erstellen von Konfigurations Dokumenten verwendet wird, ist [JSON](https://tools.ietf.org/html/rfc8259), die Sie in Kombination mit verwenden:
-    Schema Definitionen, die ein Objektmodell für das Dokument definieren
-    Validierung, ob ein JSON-Dokument einem Schema entspricht
-    Automatisierte Konvertierung von JSON-Dokumenten in und aus nativen Darstellungen dieser Schemas in den Programmiersprachen, die von den Aufrufern der APIs verwendet werden 

Häufig verwendete Schema Definitionen sind das [OpenAPI](https://www.openapis.org/) -und [JSON-Schema](http://json-schema.org/), mit dem Sie die detaillierten Definitionen der Eigenschaften in einem Dokument angeben können, z. b.:
-    Der gültige Satz von Werten für eine Eigenschaft, z. b. 0-100 für eine Eigenschaft, die einen Prozentsatz darstellt.
-    Die Definition von Enumerationen, die als Satz gültiger Zeichen folgen für eine Eigenschaft dargestellt werden.
-    Ein regulärer Ausdruck für das erwartete Format einer Zeichenfolge. 

Als Teil der Dokumentation der HCN-APIs planen wir, das Schema unserer JSON-Dokumente als OpenAPI-Spezifikation zu veröffentlichen. Basierend auf dieser Spezifikation können sprachspezifische Darstellungen des Schemas eine typsichere Verwendung der Schema Objekte in der vom Client verwendeten Programmiersprache ermöglichen. 

### <a name="example"></a>Beispiel 

Im folgenden finden Sie ein Beispiel für diesen Workflow für das-Objekt, das einen SCSI-Controller im Konfigurations Dokument einer VM darstellt. 

Im Windows-Quellcode definieren wir Schemas mithilfe von Mars-Dateien: onecore/VM/DV/net/HNS/Schema/Mars/Schema/HCN. Schema. Network. Mars

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
>Die [newIn ("2.0")-Anmerkungen sind Teil der Versions Unterstützung für die Schema Definitionen.

Aus dieser internen Definition generieren wir die OpenAPI-Spezifikationen für das Schema:

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

Sie können Tools wie [Swagger](https://swagger.io/)verwenden, um sprachspezifische Darstellungen der von einem Client verwendeten Schema Programmiersprache zu generieren. Swagger unterstützt eine Vielzahl von Sprachen C#, wie z. b., go, JavaScript und python.

- [Beispiel für generierten C# Code](example-c-sharp.md) für das IPAM-& Subnetzobjekt der obersten Ebene.

- [Beispiel für generierten go-Code](example-go.md) für das IPAM-& Subnetzobjekt der obersten Ebene. Go wird von Docker und Kubernetes verwendet, bei denen es sich um zwei der Consumer der hostcompute Network Service-APIs handelt. Go verfügt über integrierte Unterstützung für das Mars Hallen von Go-Typen in und aus JSON-Dokumenten.

Zusätzlich zur Codegenerierung und-Validierung können Sie Tools verwenden, um die Arbeit mit JSON-Dokumenten zu vereinfachen, d. –. [Visual Studio Code](https://code.visualstudio.com/Docs/languages/json).

### <a name="top-level-objects-defined-in-the-hcnschemasmars-file"></a>Objekte der obersten Ebene, die in der HCN definiert sind. Datei "Schemas. Mars"
Wie bereits erwähnt, finden Sie das Dokument Schema für Dokumente, die von den HCN-APIs verwendet werden, in einem Satz von Mars-Dateien unter: onecore/VM/DV/net/HNS/Schema/Mars/Schema.

Die Objekte der obersten Ebene sind:
- [Hostcomputenetwork](hcn-scenarios.md#scenario-hcn)
- [Hostcomputeendpoint](hcn-scenarios.md#scenario-hcn-endpoint)
- [Hostcomputenamespace](hcn-scenarios.md#scenario-hcn-namespace)
- [Hostcomputeloadbalancer](hcn-scenarios.md#scenario-hcn-load-balancer)

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

- Erfahren Sie mehr über die [gängigen HCN-Szenarios](hcn-scenarios.md).

- Erfahren Sie mehr über die [RPC-Kontext Handles für HCN](hcn-declaration-handles.md).

- Erfahren Sie mehr über die [JSON-Dokument Schemas für HCN](hcn-json-document-schemas.md).