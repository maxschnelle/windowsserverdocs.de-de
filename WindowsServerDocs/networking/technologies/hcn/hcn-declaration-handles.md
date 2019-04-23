---
title: RPC-Kontexthandles für HCN
description: ''
ms.author: jmesser
author: jmesser81
ms.date: 11/05/2018
ms.openlocfilehash: 48e4626f52ef7af19da6d3e0bb28799665498fe5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884851"
---
# <a name="rpc-context-handles-for-hcn"></a>RPC-Kontexthandles für HCN

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016


## <a name="hcnnetwork"></a>HCN_Network

Ein Netzwerk HCN wird eine Entität, die Darstellung eines Hosts verwendet wird compute, Netzwerk und die zugeordneten Ressourcen und Richtlinien. Beispielsweise besteht ein Netzwerk HCN in der Regel einen Satz von Metadaten (z. B. Id, Name und Typ), aus einem virtuellen Switch, einen virtuellen Netzwerkadapter des Hosts (fungiert als Standardgateway für das Netzwerk), eine NAT-Instanz (falls es sich bei dem Typ des Netzwerks erforderlich), einen Satz von Subnetz und die MAC-pools , und die netzwerkweite Richtlinien werden angewendet (z. B. ACLs).

HCN-Netzwerkentitäten werden HCN_NETWORK RPC Kontexthandles dargestellt.

```

/// Handle to an operation
DECLARE_HANDLE(HCN_NETWORK);

/// Return a list of existing Networks
///
/// \param  Query          Optionally specifies a JSON document for a query
///                        containing properties of the specific Networks to
///                        return. By default, all Networks are returned.
/// \retval Networks       Receives a JSON document with the list of Networks.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnEnumerateNetworks(
    _In_ PCWSTR Query,
    _Outptr_ PWSTR* Networks,
    _Outptr_opt_ PWSTR* ErrorRecord
    );
/// Create a Network
///
/// \param  Id             Specifies the unique ID for the new Network.
/// \param  Settings       JSON document specifying the settings of the new Network.
/// \retval Network        Receives a handle to the new Network.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnCreateNetwork(
    _In_ REFGUID Id,
    _In_ PCWSTR Settings,
    _Out_ PHCN_NETWORK Network,
    _Outptr_opt_ PWSTR* ErrorRecord
    );
/// Opens a handle to an existing Network.
///
/// \param  Id             Unique ID of the existing Network.
/// \retval Network        Receives a handle to the Network.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnOpenNetwork(
    _In_ REFGUID Id,
    _Out_ PHCN_NETWORK Network,
    _Outptr_opt_ PWSTR* ErrorRecord
    );
/// Modify the settings of a Network
///
/// \param  Network        Handle to a Network.
/// \param  Settings       JSON document specifying the new settings of the Network.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnModifyNetwork(
    _In_ HCN_NETWORK Network,
    _In_ PCWSTR Settings,
    _Outptr_opt_ PWSTR* ErrorRecord
    );

/// Query Network properties
///
/// \param  Network        Handle to a Network.
/// \param  Query          Optionally specifies a JSON document for a query
///                        containing specific properties of the Network
///                        return. By default all properties are returned.
/// \retval Properties     Receives a JSON document with Network properties.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnQueryNetworkProperties(
    _In_ HCN_NETWORK Network,
    _In_ PCWSTR Query,
    _Outptr_ PWSTR* Properties,
    _Outptr_opt_ PWSTR* ErrorRecord
    );
/// Delete a Network
///
/// \param  Id             Unique ID of the existing Network.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnDeleteNetwork(
    _In_ REFGUID Id,
    _Outptr_opt_ PWSTR* ErrorRecord
    );
/// Close a handle to a Network
///
/// \param  Network        Handle to a Network.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnCloseNetwork(
    _In_ HCN_NETWORK Network
    ); 
```

## <a name="hcnendpoint"></a>HCN_Endpoint

Ein HCN-Endpunkt ist einer Entität, die Darstellung eines IP-Endpunkts in einem HCN-Netzwerk und die zugeordneten Ressourcen und Richtlinien verwendet wird. Z. B. ein HCN-Endpunkt in der Regel besteht aus einer Reihe von Metadaten (z. B. Id, Name und Id des übergeordneten Netzwerk), die Netzwerkidentität (z. B. IP-Adresse, MAC-Adresse), und jeder Endpunkt bestimmte Richtlinien werden angewendet (z. B. ACLs, Routen).
HCN Endpunkt Entitäten werden HCN_ENDPOINT RPC Kontexthandles dargestellt.

```

/// Handle to an operation
DECLARE_HANDLE(HCN_ENDPOINT);

/// Return a list of existing Endpoints
///
/// \param  Query          Optionally specifies a JSON document for a query
///                        containing properties of the specific Endpoints to
///                        return. By default all Endpoints are returned.
/// \retval Endpoints      Receives a JSON document with the list of Endpoints.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnEnumerateEndpoints(
    _In_ PCWSTR Query,
    _Outptr_ PWSTR* Endpoints,
    _Outptr_opt_ PWSTR* ErrorRecord
    );
/// Create an Endpoint
///
/// \param  Id             Specifies the unique ID for the new Endpoint.
/// \param  Network        Handle to the network on which endpoint is to be created.
/// \param  Settings       JSON document specifying the settings of the new Endpoint.
/// \retval Endpoint       Receives a handle to the new Endpoint.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnCreateEndpoint(
    _In_ HCN_NETWORK Network,
    _In_ REFGUID Id,
    _In_ PCWSTR Settings,
    _Out_ PHCN_ENDPOINT Endpoint,
    _Outptr_opt_ PWSTR* ErrorRecord
    );
/// Opens a handle to an existing Endpoint.
///
/// \param  Id             Unique ID of the existing Endpoint.
/// \retval Endpoint       Receives a handle to the Endpoint.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnOpenEndpoint(
    _In_ REFGUID Id,
    _Out_ PHCN_ENDPOINT Endpoint,
    _Outptr_opt_ PWSTR* ErrorRecord
    );
/// Modify the settings of an Endpoint
///
/// \param  Endpoint       Handle to an Endpoint.
/// \param  Settings       JSON document specifying the new settings of the Endpoint.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnModifyEndpoint(
    _In_ HCN_ENDPOINT Endpoint,
    _In_ PCWSTR Settings,
    _Outptr_opt_ PWSTR* ErrorRecord
    );
/// Query Endpoint properties
///
/// \param  Endpoint       Handle to an Endpoint.
/// \param  Query          Optionally specifies a JSON document for a query
///                        containing specific properties of the Endpoint
///                        return. By default all properties are returned.
/// \retval Properties     Receives a JSON document with Endpoint properties.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnQueryEndpointProperties(
    _In_ HCN_ENDPOINT Endpoint,
    _In_ PCWSTR Query,
    _Outptr_ PWSTR* Properties,
    _Outptr_opt_ PWSTR* ErrorRecord
    );
/// Delete an Endpoint
///
/// \param  Id             Unique ID of the existing Endpoint.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnDeleteEndpoint(
    _In_ REFGUID Id,
    _Outptr_opt_ PWSTR* ErrorRecord
    );
/// Close a handle to an Endpoint
///
/// \param  Endpoint       Handle to an Endpoint.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnCloseEndpoint(
    _In_ HCN_ENDPOINT Endpoint
    );
 
```

## <a name="hcnnamespace"></a>HCN_Namespace

Eine HCN-Namespace ist eine Entität, die zum Darstellen von eines Host Compute-Netzwerk-Namespaces verwendet wird. Namespaces ermöglichen es Ihnen, die auf einem Host, netzwerkumgebungen isoliert haben, in dem jeder Namespace einen eigenen Netzwerkschnittstellen und die Routingtabelle verfügt, aus anderen Namespaces getrennt.

HCN Namespace Entitäten werden HCN_NAMESPACE RPC Kontexthandles dargestellt.

```
/// Handle to an operation
DECLARE_HANDLE(HCN_NAMESPACE);

/// Return a list of existing Namespaces
///
/// \param  Query          Optionally specifies a JSON document for a query
///                        containing properties of the specific Namespaces to
///                        return. By default all Namespaces are returned.
/// \retval Namespaces     Receives a JSON document with the list of Namespaces.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnEnumerateNamespaces(
    _In_ PCWSTR Query,
    _Outptr_ PWSTR* Namespaces,
    _Outptr_opt_ PWSTR* ErrorRecord
    );

/// Create a Namespace
///
/// \param  Id             Specifies the unique ID for the new Namespace.
/// \param  Settings       JSON document specifying the settings of the new Namespace.
/// \retval Namespace      Receives a handle to the new Namespace.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnCreateNamespace(
    _In_ REFGUID Id,
    _In_ PCWSTR Settings,
    _Out_ PHCN_NAMESPACE Namespace,
    _Outptr_opt_ PWSTR* ErrorRecord
    );

/// Opens a handle to an existing Namespace.
///
/// \param  Id             Unique ID of the existing Namespace.
/// \retval Namespace      Receives a handle to the Namespace.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnOpenNamespace(
    _In_ REFGUID Id,
    _Out_ PHCN_NAMESPACE Namespace,
    _Outptr_opt_ PWSTR* ErrorRecord
    );
/// Modify the settings of a Namespace
///
/// \param  Namespace      Handle to a Namespace.
/// \param  Settings       JSON document specifying the new settings of the Namespace.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnModifyNamespace(
    _In_ HCN_NAMESPACE Namespace,
    _In_ PCWSTR Settings,
    _Outptr_opt_ PWSTR* ErrorRecord
    );

/// Query Namespace properties
///
/// \param  Namespace      Handle to a Namespace.
/// \param  Query          Optionally specifies a JSON document for a query
///                        containing specific properties of the Namespace
///                        return. By default all properties are returned.
/// \retval Properties     Receives a JSON document with Namespace properties.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnQueryNamespaceProperties(
    _In_ HCN_NAMESPACE Namespace,
    _In_ PCWSTR Query,
    _Outptr_ PWSTR* Properties,
    _Outptr_opt_ PWSTR* ErrorRecord
    );
/// Delete a Namespace
///
/// \param  Id             Unique ID of the existing Namespace.
/// \retval ErrorRecord    Optional, receives a JSON document on failure with extended result
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnDeleteNamespace(
    _In_ REFGUID Id,
    _Outptr_opt_ PWSTR* ErrorRecord
    );

/// Close a handle to a Namespace
///
/// \param  Namespace      Handle to a Namespace.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnCloseNamespace(
    _In_ HCN_NAMESPACE Namespace
    );

```

## <a name="hcnloadbalancer"></a>HCN_LoadBalancer

Keinem LoadBalancer HCN ist eine Entität, die verwendet wird, um einen Host Compute-Netzwerk-Loadbalancer darzustellen. Load Balancers ermöglichen Ihnen Load balanced Host-Endpunkte zu berechnen.
HCN LoadBalancer-Entitäten werden HCN_LOADBALANCER RPC Kontexthandles dargestellt.

```
/// Handle to an operation
DECLARE_HANDLE(HCN_LOADBALANCER);

//////
/// LoadBalancer Methods

/// Return a list of existing LoadBalancers
///
/// \param  Query          Optionally specifies a JSON document for a query
///                        containing properties of the specific LoadBalancers to
///                        return. By default all LoadBalancers are returned.
/// \retval LoadBalancers    Receives a JSON document with the list of LoadBalancers.
/// \retval ErrorRecord    Optional, receives a JSON document with extended errorCode
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnEnumerateLoadBalancers(
    _In_ PCWSTR Query,
    _Outptr_ PWSTR* LoadBalancer,
    _Outptr_opt_ PWSTR* ErrorRecord
    );

/// Create a LoadBalancer
///
/// \param  Id             Specifies the unique ID for the new LoadBalancer.
/// \param  Settings       JSON document specifying the settings of the new LoadBalancer.
/// \retval LoadBalancer     Receives a handle to the new LoadBalancer.
/// \retval ErrorRecord    Optional, receives a JSON document with extended errorCode
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnCreateLoadBalancer(
    _In_ REFGUID Id,
    _In_ PCWSTR Settings,
    _Out_ PHCN_LOADBALANCER LoadBalancer,
    _Outptr_opt_ PWSTR* ErrorRecord
    );

/// Opens a handle to an existing LoadBalancer.
///
/// \param  Id             Unique ID of the existing LoadBalancer.
/// \retval LoadBalancer     Receives a handle to the LoadBalancer.
/// \retval ErrorRecord    Optional, receives a JSON document with extended errorCode
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnOpenLoadBalancer(
    _In_ REFGUID Id,
    _Out_ PHCN_LOADBALANCER LoadBalancer,
    _Outptr_opt_ PWSTR* ErrorRecord
    );

/// Modify the settings of a PolcyList
///
/// \param  PolcyList      Handle to a PolcyList.
/// \param  Settings       JSON document specifying the new settings of the PolcyList.
/// \retval ErrorRecord    Optional, receives a JSON document with extended errorCode
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnModifyLoadBalancer(
    _In_ HCN_LOADBALANCER LoadBalancer,
    _In_ PCWSTR Settings,
    _Outptr_opt_ PWSTR* ErrorRecord
    );

/// Query LoadBalancer properties
///
/// \param  LoadBalancer     Handle to a LoadBalancer.
/// \param  Query          Optionally specifies a JSON document for a query
///                        containing specific properties of the LoadBalancer
///                        return. By default all properties are returned.
/// \retval Properties     Receives a JSON document with LoadBalancer properties.
/// \retval ErrorRecord    Optional, receives a JSON document with extended errorCode
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnQueryLoadBalancerProperties(
    _In_ HCN_LOADBALANCER LoadBalancer,
    _In_ PCWSTR Query,
    _Outptr_ PWSTR* Properties,
    _Outptr_opt_ PWSTR* ErrorRecord
    );

/// Delete a LoadBalancer
///
/// \param  Id             Unique ID of the existing LoadBalancer.
/// \retval ErrorRecord    Optional, receives a JSON document with extended errorCode
///                        information. The caller must release the buffer using
///                        CoTaskMemFree.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnDeleteLoadBalancer(
    _In_ REFGUID Id,
    _Outptr_opt_ PWSTR* ErrorRecord
    );

/// Close a handle to a LoadBalancer
///
/// \param  LoadBalancer     Handle to a LoadBalancer.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT
WINAPI
HcnCloseLoadBalancer(
    _In_ HCN_LOADBALANCER LoadBalancer

```

## <a name="hcnnotificationcallback"></a>HCN_Notification_Callback

Es bieten Funktionen Zugriff auf den gesamten Dienst umfassenden Vorgänge wie z. B. Benachrichtigungen (z. B. Empfangen von Benachrichtigungen von der netzwerkerstellung eines neuen).

```
/// Registers a callback function to receive notifications of service-wide events such as network
/// creations/deletions.
///
/// \param  Callback           Function pointer to notification callback.
/// \param  Context            Context pointer.
/// \retval CallbackHandle     Receives a handle to a callback registered on a Service.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT WINAPI
HcnRegisterServiceCallback(
    _In_ HCN_NOTIFICATION_CALLBACK Callback,
    _In_ void* Context,
    _Out_ HCN_CALLBACK* CallbackHandle
    );

/// Unregisters from service-wide notifications
///
/// \retval CallbackHandle     Handle to a callback registered on a Service.
///
/// \returns S_OK if successful; HResult error code on failures.
///
HRESULT WINAPI
HcnUnregisterServiceCallback(
    _In_ HCN_CALLBACK CallbackHandle
    );
```


