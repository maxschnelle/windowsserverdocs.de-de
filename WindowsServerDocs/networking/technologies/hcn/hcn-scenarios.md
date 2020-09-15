---
title: HCN-Szenarios (Host Compute Network)
description: Beispiel, das zeigt, wie Sie mithilfe der hostcompute-Netzwerkdienst-API ein hostcomputenetzwerk auf dem Host erstellen, das zum Verbinden virtueller NICs mit Virtual Machines oder Containern verwendet werden kann.
ms.author: daschott
author: daschott
ms.date: 11/05/2018
ms.openlocfilehash: e865326b77fbdec19af3e7db347734715458b18a
ms.sourcegitcommit: 0b3d6661c44aa1a697087e644437279142726d84
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083681"
---
# <a name="common-scenarios"></a>Häufige Szenarios

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019

## <a name="scenario-hcn"></a>Szenario: HCN

### <a name="create-an-hcn"></a>Erstellen einer HCN

In diesem Beispiel wird gezeigt, wie Sie mithilfe der hostcompute-Netzwerkdienst-API ein hostcomputenetzwerk auf dem Host erstellen, das zum Herstellen einer Verbindung von virtuellen NICs mit Virtual Machines oder Containern verwendet werden kann.

```C++
using unique_hcn_network = wil::unique_any<
    HCN_NETWORK,
    decltype(&HcnCloseNetwork),
    HcnCloseNetwork>;
/// Creates a simple HCN Network, waiting synchronously to finish the task
void CreateHcnNetwork()
{
    unique_hcn_network hcnnetwork;
    wil::unique_cotaskmem_string result;
    std::wstring settings = LR"(
    {
        "SchemaVersion": {
            "Major": 2,
            "Minor": 0
        },
        "Owner" : "WDAGNetwork",
        "Flags" : 0,
        "Type"  : 0,
        "Ipams" : [
            {
                "Type" : 0,
                "Subnets" : [
                    {
                        "IpAddressPrefix" : "192.168.1.0/24",
                        "Policies" : [
                            {
                                "Type" : "VLAN",
                                "IsolationId" : 100,
                            }
                        ],
                        "Routes" : [
                            {
                                "NextHop" : "192.168.1.1",
                                "DestinationPrefix" : "0.0.0.0/0",
                            }
                        ]
                    }
                ],
            },
        ],
        "MacPool":  {
            "Ranges" : [
                {
                    "EndMacAddress":  "00-15-5D-52-CF-FF",
                    "StartMacAddress":  "00-15-5D-52-C0-00"
                }
            ],
        },
        "Dns" : {
            "Suffix" : "net.home",
            "ServerList" : ["10.0.0.10"],
        }
    }
    })";
    GUID networkGuid;
    HRESULT result = CoCreateGuid(&networkGuid);
    result = HcnCreateNetwork(
        networkGuid,              // Unique ID
        settings.c_str(),      // Compute system settings document
        &hcnnetwork,
        &result
        );
    if (FAILED(result))
    {
                    // UnMarshal  the result Json
     // ErrorSchema
        //   {
        //    "ErrorCode" : <uint32>,
        //    "Error" : <string>,
        //    "Success" : <bool>,
       //   }
        // Failed to create network
        THROW_HR(result);
    }
    // Close the Handle
    result = HcnCloseNetwork(hcnnetwork.get());
    if (FAILED(result))
    {
        // UnMarshal  the result Json
        THROW_HR(result);
    }
}
```
### <a name="delete-an-hcn"></a>Löschen einer HCN
In diesem Beispiel wird gezeigt, wie Sie die Host Compute Network Service-API zum Öffnen & Löschen eines hostcompute-Netzwerks verwenden.
```C++
    wil::unique_cotaskmem_string errorRecord;
    GUID networkGuid; // Initialize it to appropriate network guid value
    HRESULT hr = HcnDeleteNetwork(networkGuid, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
```
### <a name="enumerate-all-networks"></a>Alle Netzwerke auflisten
In diesem Beispiel wird gezeigt, wie Sie die hostcompute-Netzwerkdienst-API verwenden, um alle hostcomputenetzwerke aufzulisten.
```C++
     wil::unique_cotaskmem_string resultNetworks;
     wil::unique_cotaskmem_string errorRecord;
     // Filter to select Networks based on properties
     std::wstring filter [] = LR"(
     {
         "Name"  : "WDAG",
     })";
     HRESULT result = HcnEnumerateNetworks(filter.c_str(), &resultNetworks, &errorRecord);
     if (FAILED(result))
     {
         // UnMarshal  the result Json
         THROW_HR(result);
     }
```
### <a name="query-network-properties"></a>Abfragen von Netzwerk Eigenschaften
In diesem Beispiel wird gezeigt, wie die Host Compute Network Service-API zum Abfragen von Netzwerk Eigenschaften verwendet wird.
```C++
    unique_hcn_network hcnnetwork;
    wil::unique_cotaskmem_string errorRecord;
    wil::unique_cotaskmem_string properties;
    std:wstring query = LR"(
    {
        // Future
    })";
    GUID networkGuid; // Initialize it to appropriate network guid value
    HRESULT hr = HcnOpenNetwork(networkGuid, &hcnnetwork, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
    hr = HcnQueryNetworkProperties(hcnnetwork.get(), query.c_str(), &properties, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```
## <a name="scenario-hcn-endpoint"></a>Szenario: HCN-Endpunkt
### <a name="create-an-hcn-endpoint"></a>Erstellen eines HCN-Endpunkts
In diesem Beispiel wird gezeigt, wie Sie die hostcompute-Netzwerkdienst-API verwenden, um einen hostcompute-Netzwerk Endpunkt zu erstellen und ihn dann dem virtuellen Computer oder einem Container hinzuzufügen.
```C++
using unique_hcn_endpoint = wil::unique_any<
    HCN_ENDPOINT,
    decltype(&HcnCloseEndpoint),
    HcnCloseEndpoint>;
void CreateAndHotAddEndpoint()
{
    unique_hcn_endpoint hcnendpoint;
    unique_hcn_network hcnnetwork;
    wil::unique_cotaskmem_string errorRecord;
    std::wstring settings[] = LR"(
    {
        "SchemaVersion": {
            "Major": 2,
            "Minor": 0
        },
        "Owner" : "Sample",
                   "Flags" : 0,
        "HostComputeNetwork" : "87fdcf16-d210-426e-959d-2a1d4f41d6d3",
        "DNS" : {
            "Suffix" : "net.home",
            "ServerList" : "10.0.0.10",
        }
    })";
    GUID endpointGuid;
    HRESULT result = CoCreateGuid(&endpointGuid);
    result = HcnOpenNetwork(
        networkGuid,              // Unique ID
        &hcnnetwork,
        &errorRecord
        );
    if (FAILED(result))
    {
        // Failed to find network
        THROW_HR(result);
    }
    result = HcnCreateEndpoint(
        hcnnetwork.get(),
        endpointGuid,              // Unique ID
        settings.c_str(),      // Compute system settings document
        &hcnendpoint,
        &errorRecord
        );
    if (FAILED(result))
    {
        // Failed to create endpoint
        THROW_HR(result);
    }
    // Can use the sample from HCS API Spec on how to attach this endpoint
    // to the VM using AddNetworkAdapterToVm
    result = HcnCloseEndpoint(hcnendpoint.get());
    if (FAILED(result))
    {
        // UnMarshal  the result Json
        THROW_HR(result);
    }
}
```
### <a name="delete-an-endpoint"></a>Einen Endpunkt löschen
Dieses Beispiel zeigt, wie Sie mithilfe der Host Compute Network Service-API einen hostcompute-Netzwerk Endpunkt löschen.
```C++
    wil::unique_cotaskmem_string errorRecord;
    GUID endpointGuid; // Initialize it to appropriate endpoint guid value
    HRESULT hr = HcnDeleteEndpoint(endpointGuid, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```
### <a name="modify-and-endpoint"></a>Ändern und Endpunkt
Dieses Beispiel zeigt, wie Sie mithilfe der Host Compute Network Service-API einen hostcompute-Netzwerk Endpunkt ändern.
```C++
    unique_hcn_endpoint hcnendpoint;
    GUID endpointGuid; // Initialize it to appropriate endpoint guid value
    HRESULT hr = HcnOpenEndpoint(endpointGuid, &hcnendpoint, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
    std::wstring  ModifySettingAddPortJson = LR"(
    {
        "ResourceType" : 0,
        "RequestType" : 0,
        "Settings" : {
            "PortName" : "acbd341a-ec08-44c0-9d5e-61af0ee86902"
            "VirtualNicName" : "641313e1-7ae8-4ddb-94e5-3215f3a0b218--87fdcf16-d210-426e-959d-2a1d4f41d6d1"
            "VirtualMachineId" : "641313e1-7ae8-4ddb-94e5-3215f3a0b218"
        }
    }
    )";
    hr = HcnModifyEndpoint(hcnendpoint.get(), ModifySettingAddPortJson.c_str(), &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```
### <a name="enumerate-all-enpoints"></a>Alle-Punkte aufzählen
In diesem Beispiel wird gezeigt, wie Sie die hostcompute-Netzwerkdienst-API verwenden, um alle hostcompute-Netzwerk Endpunkte aufzulisten.
```C++
    wil::unique_cotaskmem_string errorRecord;
    wil::unique_cotaskmem_string resultEndpoints;
    wil::unique_cotaskmem_string errorRecord;
    // Filter to select Endpoint based on properties
    std::wstring filter [] = LR"(
    {
        "Name"  : "sampleNetwork",
    })";
    result = HcnEnumerateEndpoints(filter.c_str(), &resultEndpoints, &errorRecord);
    if (FAILED(result))
    {
        THROW_HR(result);
    }
```
### <a name="query-endpoint-properties"></a>Eigenschaften von Abfrage Endpunkt
In diesem Beispiel wird gezeigt, wie Sie die hostcompute-Netzwerkdienst-API verwenden, um alle Eigenschaften eines Host Compute-Netzwerk Endpunkts abzufragen.
```C++
    unique_hcn_endpoint hcnendpoint;
    wil::unique_cotaskmem_string errorRecord;
    GUID endpointGuid; // Initialize it to appropriate endpoint guid value
    HRESULT hr = HcnOpenEndpoint(endpointGuid, &hcnendpoint, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
    wil::unique_cotaskmem_string properties;
    std:wstring query = LR"(
    {
        // Future
    })";
    hr = HcnQueryEndpointProperties(hcnendpoint.get(), query.c_str(), &properties, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the errorRecord Json
        THROW_HR(hr);
    }
```
## <a name="scenario-hcn-namespace"></a>Szenario: HCN-Namespace
### <a name="create-an-hcn-namespace"></a>Erstellen eines HCN-Namespace
In diesem Beispiel wird gezeigt, wie Sie mithilfe der hostcompute-Netzwerkdienst-API einen hostcompute-Netzwerk Namespace auf dem Host erstellen, der zum Verbinden von Endpunkten und Containern verwendet werden kann.
```C++
using unique_hcn_namespace = wil::unique_any<
    HCN_NAMESPACE,
    decltype(&HcnCloseNamespace),
    HcnCloseNamespace>;
/// Creates a simple HCN Network, waiting synchronously to finish the task
void CreateHcnNamespace()
{
    unique_hcn_namespace handle;
    wil::unique_cotaskmem_string errorRecord;
    std::wstring settings = LR"(
    {
        "SchemaVersion": {
            "Major": 2,
            "Minor": 0
        },
        "Owner" : "Sample",
        "Flags" : 0,
        "Type" : 0,
    })";
    GUID namespaceGuid;
    HRESULT result = CoCreateGuid(&namespaceGuid);
    result = HcnCreateNamespace(
        namespaceGuid,              // Unique ID
        settings.c_str(),      // Compute system settings document
        &handle,
        &errorRecord
        );
    if (FAILED(result))
    {
                    // UnMarshal  the result Json
     // ErrorSchema
        //   {
        //    "ErrorCode" : <uint32>,
        //    "Error" : <string>,
        //    "Success" : <bool>,
       //   }
        // Failed to create network
        THROW_HR(result);
    }
    result = HcnCloseNamespace(handle.get());
    if (FAILED(result))
    {
        // UnMarshal  the result Json
        THROW_HR(result);
    }
}
```
### <a name="delete-an-hcn-namespace"></a>Löschen eines HCN-Namespace
In diesem Beispiel wird gezeigt, wie Sie mit der Host Compute Network Service-API einen hostcompute-Netzwerk Namespace löschen.
```C++
    wil::unique_cotaskmem_string errorRecord;
    GUID namespaceGuid; // Initialize it to appropriate namespace guid value
    HRESULT hr = HcnDeleteNamespace(namespaceGuid, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
```
### <a name="modify-an-hcn-namespace"></a>Ändern eines HCN-Namespace
In diesem Beispiel wird gezeigt, wie Sie die Host Compute Network Service-API verwenden, um einen hostcompute-Netzwerk Namespace zu ändern.
```C++
    unique_hcn_namespace handle;
    GUID namespaceGuid; // Initialize it to appropriate namespace guid value
    HRESULT hr = HcnOpenNamespace(namespaceGuid, &handle, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
    wil::unique_cotaskmem_string errorRecord;
    static std::wstring  ModifySettingAddEndpointJson = LR"(
    {
        "ResourceType" : 1,
        "ResourceType" : 0,
        "Settings" : {
            "EndpointId" : "87fdcf16-d210-426e-959d-2a1d4f41d6d1"
        }
    }
    )";
    hr = HcnModifyNamespace(handle.get(), ModifySettingAddEndpointJson.c_str(), &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
    hr = HcnCloseNamespace(handle.get());
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```
### <a name="enumerate-all-namespaces"></a>Alle Namespaces auflisten
In diesem Beispiel wird gezeigt, wie Sie die hostcompute-Netzwerkdienst-API verwenden, um alle hostcompute-Netzwerk Namespaces aufzuzählen.
```C++
    wil::unique_cotaskmem_string resultNamespaces;
    wil::unique_cotaskmem_string errorRecord;
    std::wstring filter [] = LR"(
    {
            // Future
    })";
    HRESULT hr = HcnEnumerateNamespace(filter.c_str(), &resultNamespaces, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```
### <a name="query-namespace-properties"></a>Eigenschaften von "Abfrage Namespace"
In diesem Beispiel wird gezeigt, wie die hostcompute-Netzwerkdienst-API verwendet wird, um Eigenschaften des Host Compute-Netzwerk Namespace
```C++
    unique_hcn_namespace handle;
    GUID namespaceGuid; // Initialize it to appropriate namespace guid value
    HRESULT hr = HcnOpenNamespace(namespaceGuid, &handle, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
    wil::unique_cotaskmem_string errorRecord;
    wil::unique_cotaskmem_string properties;
    std:wstring query = LR"(
    {
        // Future
    })";
    HRESULT hr = HcnQueryNamespaceProperties(handle.get(), query.c_str(), &properties, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```
## <a name="scenario-hcn-load-balancer"></a>Szenario: HCN Load Balancer
### <a name="create-an-hcn-load-balancer"></a>Erstellen eines HCN-Lasten Ausgleichs
In diesem Beispiel wird gezeigt, wie Sie mithilfe der hostcompute-Netzwerkdienst-API ein hostcompute-Netzwerk Load Balancer auf dem Host erstellen, mit dem ein Lastenausgleich für den Endpunkt über Compute erfolgen kann.
```C++
using unique_hcn_loadbalancer = wil::unique_any<
    HCN_LOADBALANCER,
    decltype(&HcnCloseLoadBalancer),
    HcnCloseLoadBalancer>;
/// Creates a simple HCN LoadBalancer, waiting synchronously to finish the task
void CreateHcnLoadBalancer()
{
    unique_hcn_loadbalancer handle;
    wil::unique_cotaskmem_string errorRecord;
    std::wstring settings = LR"(
     {
        "SchemaVersion": {
            "Major": 2,
            "Minor": 0
        },
        "Owner" : "Sample",
        "HostComputeEndpoints" : [
            "87fdcf16-d210-426e-959d-2a1d4f41d6d1"
        ],
        "VirtualIPs" : [ "10.0.0.10" ],
        "PortMappings" : [
            {
                "Protocol" : 0,
                "InternalPort" : 8080,
                "ExternalPort" : 80,
            }
        ],
        "EnableDirectServerReturn" : true,
        "InternalLoadBalancer" : false,
    }
     )";
    GUID lbGuid;
    HRESULT result = CoCreateGuid(&lbGuid);
    HRESULT hr = HcnCreateLoadBalancer(
        lbGuid,              // Unique ID
        settings.c_str(),      // LoadBalancer settings document
        &handle,
        &errorRecord
        );
    if (FAILED(hr))
    {
                    // UnMarshal  the result Json
     // ErrorSchema
        //   {
        //    "ErrorCode" : <uint32>,
        //    "Error" : <string>,
        //    "Success" : <bool>,
       //   }
        // Failed to create network
        THROW_HR(hr);
    }
    hr = HcnCloseLoadBalancer(handle.get());
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
}
```
### <a name="delete-an-hcn-load-balancer"></a>Löschen eines HCN-Lasten Ausgleichs
In diesem Beispiel wird gezeigt, wie Sie mithilfe der Host Compute Network Service-API einen Compute Network-LoadBalancer eines Hosts löschen.
```C++
    wil::unique_cotaskmem_string errorRecord;
    GUID lbGuid; // Initialize it to appropriate loadbalancer guid value
    HRESULT hr = HcnDeleteLoadBalancer(lbGuid , &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
```
### <a name="modify-an-hcn-load-balancer"></a>Ändern eines HCN-Lasten Ausgleichs
In diesem Beispiel wird gezeigt, wie Sie die Host Compute Network Service-API verwenden, um einen hostcompute-Netzwerk Namespace zu ändern.
```C++
    unique_hcn_loadbalancer handle;
    GUID lbGuid; // Initialize it to appropriate loadbalancer guid value
    HRESULT hr = HcnOpenLoadBalancer(lbGuid, &handle, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
    wil::unique_cotaskmem_string errorRecord;
    static std::wstring  ModifySettingAddEndpointJson = LR"(
    {
        "ResourceType" : 1,
        "ResourceType" : 0,
        "Settings" : {
            "EndpointId" : "87fdcf16-d210-426e-959d-2a1d4f41d6d1"
        }
    }
    )";
    hr = HcnModifyLoadBalancer(handle.get(), ModifySettingAddEndpointJson.c_str(), &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal the result Json
        THROW_HR(hr);
    }
    hr = HcnCloseLoadBalancer(handle.get());
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```
### <a name="enumerate-all-load-balancers"></a>Alle Load Balancer auflisten
In diesem Beispiel wird gezeigt, wie die hostcompute-Netzwerkdienst-API verwendet wird, um alle hostcompute-Netzwerk Load Balancer aufzuzählen.
```C++
    wil::unique_cotaskmem_string resultLoadBalancers;
    wil::unique_cotaskmem_string errorRecord;
    std::wstring filter [] = LR"(
    {
         // Future
    })";
    HRESULT result = HcnEnumerateLoadBalancers(filter.c_str(), & resultLoadbalancers, &errorRecord);
    if (FAILED(result))
    {
            // UnMarshal  the result Json
            THROW_HR(result);
    }
```
### <a name="query-load-balancer-properties"></a>Eigenschaften des Abfrage Load Balancers
In diesem Beispiel wird gezeigt, wie die hostcompute-Netzwerkdienst-API verwendet wird, um die Eigenschaften des Host Compute-Netzwerks zu Abfragen.
```C++
    unique_hcn_loadbalancer handle;
    GUID lbGuid; // Initialize it to appropriate loadbalancer guid value
    HRESULT hr = HcnOpenLoadBalancer(lbGuid, &handle, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
    wil::unique_cotaskmem_string errorRecord;
    wil::unique_cotaskmem_string properties;
    std:wstring query = LR"(
    {
        "ID"  : "",
        "Type" : 0,
    })";
    hr = HcnQueryNProperties(handle.get(), query.c_str(), &properties, &errorRecord);
    if (FAILED(hr))
    {
        // UnMarshal  the result Json
        THROW_HR(hr);
    }
```
## <a name="scenario-hcn-notifications"></a>Szenario: HCN-Benachrichtigungen
### <a name="register-and-unregister-service-wide-notifications"></a>Registrieren und Aufheben der Registrierung von Dienst weiten Benachrichtigungen
In diesem Beispiel wird veranschaulicht, wie Sie die Host-Compute-Netzwerkdienst-API verwenden, um Dienst weite Benachrichtigungen zu registrieren und deren Registrierung aufzuheben. Dies ermöglicht es dem Aufrufer, eine Benachrichtigung (über die Rückruffunktion, die Sie während der Registrierung angegeben haben) zu empfangen, wenn ein Dienst weiter Vorgang wie ein neues Netzwerk Erstellungs Ereignis aufgetreten ist.
```C++
using unique_hcn_callback = wil::unique_any<
    HCN_CALLBACK,
    decltype(&HcnUnregisterServiceCallback),
    HcnUnregisterServiceCallback>;
// Callback handle returned by registration api. Kept at
// global or module scope as it will automatically be
// unregistered when it goes out of scope.
unique_hcn_callback g_Callback;
// Event notification callback function.
void
CALLBACK
ServiceCallback(
    DWORD   NotificationType,
    void*   Context,
    HRESULT NotificationStatus,
    PCWSTR  NotificationData)
{
    // Optional client context
    UNREFERENCED_PARAMETER(context);
    // Reserved for future use
    UNREFERENCED_PARAMETER(NotificationStatus);
    switch (NotificationType)
    {
        case HcnNotificationNetworkCreate:
            // TODO: UnMarshal the NotificationData
            //
            // // Notification
            // {
            //     "ID" : Guid,
            //     "Flags" : <uint32>,
            // };
            break;
        case HcnNotificationNetworkDelete:
            // TODO: UnMarshal the NotificationData
            break;
        Default:
            // TODO: handle other events.
            break;
    }
}
/// Register for service-wide notifications
void RegisterForServiceNotifications()
{
    THROW_IF_FAILED(HcnRegisterServiceCallback(
        ServiceCallback,
        nullptr,
        &g_Callback));
}
/// Unregister from service-wide notifications
void UnregisterForServiceNotifications()
{
    // As this is a unique_hcn_callback, this will cause HcnUnregisterServiceCallback to be invoked
    g_Callback.reset();
}
```
## <a name="next-steps"></a>Nächste Schritte
- Erfahren Sie mehr über die [RPC-Kontext Handles für HCN](hcn-declaration-handles.md).
- Erfahren Sie mehr über die [JSON-Dokument Schemas für HCN](hcn-json-document-schemas.md).