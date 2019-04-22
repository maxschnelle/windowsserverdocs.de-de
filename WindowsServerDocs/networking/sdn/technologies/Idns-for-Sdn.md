---
title: Interner DNS-Dienst (iDNS) für SDN
description: In diesem Thema wird erläutert, wie Sie bereitstellen können DNS-Dienste für Ihre mandantenworkloads gehosteten mithilfe von internen DNS (iDNS), die in der Software Defined Networking unter Windows Server 2016 integriert ist.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ad848a5b-0811-4c67-afe5-6147489c0384
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4d4ae5ee5f5600d86349ca26b7acbdb284b45bac
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824081"
---
# <a name="internal-dns-service-idns-for-sdn"></a>Interner DNS-Dienst (iDNS) für SDN

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Wenn Sie für einen Cloud-Dienstanbieter arbeiten \(CSP\) oder Unternehmen, die beabsichtigen, das Bereitstellen von Software Defined Networking \(SDN\) in Windows Server 2016 können Sie den DNS-Dienste bereitstellen, Ihre gehosteten mandantenworkloads Mithilfe von internen DNS \(iDNS\), die mit SDN integriert ist.

Virtual Machines gehostet \(VMs\) und Anwendungen erfordern, DNS, um in jeweils eigenen Netzwerken, und klicken Sie mit externen Ressourcen im Internet kommunizieren. Mit iDNS können Sie Mandanten mit DNS-Namensauflösungsdienste für ihren Namespace isolierte, lokalen und Ressourcen für Internet bereitstellen.

Da der Dienst iDNS nicht zugegriffen werden kann, aus der Mandant virtuelle Netzwerke ist, ist nicht über den Proxy iDNS der Server nicht anfällig für böswillige Aktivitäten auf mandantennetzwerken.

**Wichtige Features**

Im folgenden werden die wichtigsten Features IDNs.

- Bietet freigegebenen DNS-Server adressauflösungsdienste für Mandanten Workloads ein
- Autorisierender DNS-Dienst für namensauflösung und DNS-Registrierung innerhalb des Bereichs der Tenant-name
- Recursive DNS-Dienst für die Auflösung von Internetnamen aus den VMs des Mandanten.
- Falls gewünscht, können Sie konfigurieren, gleichzeitige Hosten von Fabric und Mandanten
- Eine kostengünstige Lösung für DNS - Mandanten müssen keine eigene DNS-Infrastruktur bereitstellen.
- Hohe Verfügbarkeit mit Active Directory-Integration, die erforderlich ist.

Neben diesen Features können Sie Wenn Sie bedenken, halten Ihre AD integriert sind DNS-Server öffnen, mit dem Internet, können Sie iDNS-Server hinter einer anderen rekursiven Resolver im Umkreisnetzwerk bereitstellen.

Da iDNS einen zentralen Server für alle DNS-Abfragen ist, kann einen CSP oder Enterprise auch Mandanten DNS-Firewalls zu implementieren, Filter anwenden, böswillige Aktivitäten zu erkennen und überwachen Transaktionen an einem zentralen Ort

## <a name="idns-infrastructure"></a>iDNS Infrastruktur
Die iDNS-Infrastruktur umfasst iDNS-Servern und iDNS Proxy.

### <a name="idns-servers"></a>iDNS Server
iDNS umfasst eine Reihe von DNS-Server, die mandantenspezifische-Daten, z. B. VM-DNS-Ressourceneinträgen zu hosten.

iDNS Server sind die autorisierenden Server für ihre internen DNS-Zonen, und auch als einen Resolver zum öffentlichen Namen Wenn Mandanten VMs Versuch, auf externe Ressourcen zu verbinden.

Alle Hostnamen für virtuelle Computer in virtuellen Netzwerken werden unter der gleichen Zone als DNS-Ressourceneinträge gespeichert. Wenn Sie iDNS für eine Zone mit dem Namen "contoso.Local" bereitstellen, werden z. B. die DNS-Ressourceneinträge für die virtuellen Computer im Netzwerk in der Zone "contoso.Local" gespeichert.

Mandanten-VM von vollständig qualifizierten Domänennamen \(FQDNs\) bestehen aus den Namen des Computers und die DNS-Suffix-Zeichenfolge für das Virtuellenetzwerk, im GUID-Format. Beispielsweise ist verfügen Sie über eine Mandanten-VM mit dem Namen 1, der auf das virtuelle Netzwerk Contoso, lokal, befindet FQDN der VM 1. *Vn-Guid*. "contoso.Local", wobei *Vn-Guid* ist die DNS-Suffix-Zeichenfolge für das Virtuellenetzwerk.

>[!NOTE]
>Wenn Sie ein Fabric-Administrator sind, können Sie Ihrer CSP oder Unternehmens-DNS-Infrastruktur, wie iDNS-Server, ohne neue DNS-Server speziell für die Bereitstellung als iDNS Server verwenden. Ob Sie neue Server IDNs bereitstellen, oder Sie Ihre vorhandene Infrastruktur nutzen, verwendet iDNS Active Directory, um hochverfügbarkeit zu gewährleisten. Ihre iDNS-Server müssen daher in Active Directory integriert werden.

### <a name="idns-proxy"></a>iDNS Proxy
iDNS Proxy ist ein Windows-Dienst auf jedem Host ausgeführt wird und die Mandanten virtuelle Netzwerk-DNS-Datenverkehr die iDNS Server weiterleitet.

Die folgende Abbildung zeigt die DNS-Datenverkehr Pfade aus Mandant virtuelle Netzwerke über die iDNS-Proxy, um die iDNS Server und dem Internet.

![iDNS Infrastruktur](../../media/Internal-Dns/Internal-Dns.jpg)

## <a name="how-to-deploy-idns"></a>Wie bereitstellen iDNS
Wenn Sie SDN in Windows Server 2016 mithilfe von Skripts bereitstellen, ist die iDNS automatisch in Ihrer Bereitstellung enthalten.

Weitere Informationen finden Sie in den folgenden Themen.

- [Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts](https://docs.microsoft.com/windows-server/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)


## <a name="understanding-idns-deployment-steps"></a>Grundlegendes zu iDNS Bereitstellungsschritte
Sie können in diesem Abschnitt verwenden, erhalten Sie einen Überblick darüber, wie iDNS installiert und konfiguriert werden, wenn Sie SDN mithilfe von Skripts bereitstellen.

Es folgt eine Übersicht über die erforderlichen Schritte zum Bereitstellen von iDNS.

>[!NOTE]
>Wenn Sie SDN mithilfe von Skripts bereitgestellt haben, müssen Sie nicht diese Schritte ausführen. Die Schritte finden Sie Informationen und nur zur Problembehandlung zu.

### <a name="step-1-deploy-dns"></a>Schritt 1: Bereitstellen von DNS
Sie können einen DNS-Server bereitstellen, anhand des folgenden Beispiels Windows PowerShell-Befehl.
    
    Install-WindowsFeature DNS -IncludeManagementTools
    
### <a name="step-2-configure-idns-information-in-network-controller"></a>Schritt 2: In den Netzwerkcontroller iDNS Informationen konfigurieren
Dieses Skript-Segment ist ein REST-Aufruf, der erfolgt durch den Administrator für den Netzwerkcontroller, informiert sie über die Konfiguration des iDNS-Zone – z. B. die IP-Adresse der iDNSServer und die Zone, die zum Hosten der iDNS Namen verwendet wird. 

```
    Url: https://<url>/networking/v1/iDnsServer/configuration
Method: PUT
{
      "properties": {
        "connections": [
          {
            "managementAddresses": [
              "10.0.0.9"
            ],
            "credential": {
              "resourceRef": "/credentials/iDnsServer-Credentials"
            },
            "credentialType": "usernamePassword"
          }
        ],
        "zone": "contoso.local"
      }
    }
```

>[!NOTE]
>Dies ist ein Auszug aus dem Abschnitt **Konfiguration ConfigureIDns** in SDNExpress.ps1. Weitere Informationen finden Sie unter [Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts).

### <a name="step-3-configure-the-idns-proxy-service"></a>Schritt 3: Konfigurieren Sie die iDNS Proxydienst
Die iDNS Aktivierungsproxydienst ausgeführt wird, auf jedem der Hyper-V-Hosts bereitstellen als Brücke zwischen der virtuellen Netzwerke von Mandanten und dem physischen Netzwerk, in denen die iDNS-Server befinden. Die folgenden Registrierungsschlüssel müssen auf jedem Hyper-V-Host erstellt werden.


**DNS-Port:** Fester Port 53

- Registry Key = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService"
- ValueName = "Port"
- ValueData = 53
- ValueType = "Dword"
       

**DNS-Proxy-Port:** Fester Port 53

- Registry Key = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService"
- ValueName = "ProxyPort"
- ValueData = 53
- ValueType = "Dword"
        
**DNS-IP-ADRESSE:** Feste IP-Adresse der Netzwerkschnittstelle konfiguriert werden, für den Fall, dass der Mandant entscheidet sich für den iDNS-Dienst verwenden

- Registry Key = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService"
- ValueName = "IP"
- ValueData = "169.254.169.254"
- ValueType = "String"

        
**MAC-Adresse:** Media Access Control-Adresse des DNS-Servers

- Registry Key = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService
- ValueName = "MAC"
- ValueData = “aa-bb-cc-aa-bb-cc”
- ValueType = "String"

**IDNS-Serveradresse:** Eine durch Trennzeichen getrennte Liste mit iDNS Server.

- Registrierungsschlüssel: HKLM\SYSTEM\CurrentControlSet\Services\DNSProxy\Parameters
- ValueName = "Forwarders"
- "ValueData" an "10.0.0.9" =
- ValueType = "String"



>[!NOTE]
>Dies ist ein Auszug aus dem Abschnitt **Konfiguration ConfigureIDnsProxy** in SDNExpress.ps1. Weitere Informationen finden Sie unter [Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts).

### <a name="step-4-restart-the-network-controller-host-agent-service"></a>Schritt 4: Den Netzwerk-Controller-Host-Agent-Dienst neu starten
Folgende Windows PowerShell-Befehle können den Netzwerk-Controller-Host-Agent-Dienst neu starten.
    
    Restart-Service nchostagent -Force
    
Weitere Informationen finden Sie unter [Restart-Service](https://technet.microsoft.com/library/hh849823.aspx).

### <a name="enable-firewall-rules-for-the-dns-proxy-service"></a>Aktivieren Sie Firewallregeln für den DNS-Proxy-Dienst
Folgende Windows PowerShell-Befehle können eine Firewallregel erstellen, die Ausnahmen für den Proxy für die Kommunikation mit dem virtuellen Computer und Server iDNS ermöglicht.
    
    Enable-NetFirewallRule -DisplayGroup 'DNS Proxy Firewall'

Weitere Informationen finden Sie unter [Enable-NetFirewallRule](https://technet.microsoft.com/library/jj554869.aspx).
    
### <a name="validate-the-idns-service"></a>Überprüfen Sie die iDNS Service
Um die iDNS Service überprüfen zu können, müssen Sie eine Beispiel-mandantenarbeitslast bereitstellen.

Weitere Informationen finden Sie unter [Erstellen eines virtuellen Computers und Herstellen einer Verbindung mit einem virtuellen Mandantennetzwerk oder VLAN](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create-a-tenant-vm).

Wenn Sie die Mandanten-VM zur Verwendung des Diensts iDNS möchten, müssen Sie die VM-Netzwerk-Schnittstellen-DNS-Server-Konfiguration leer lassen und ermöglichen die Schnittstellen für die Verwendung von DHCP. 

Nachdem Sie der virtuellen Computer mit solchen eine Netzwerkschnittstelle initiiert wird, er erhält automatisch eine Konfiguration, die dem virtuellen Computer mit iDNS ermöglicht, und des virtuellen Computers beginnt sofort die namensauflösung mithilfe des Diensts iDNS ausführen.

Sie konfigurieren, dass die Mandanten-VM in den iDNS-Dienst verwenden, indem DNS-Server und alternativer DNS-Server Netzwerkschnittstelleninformationen leer lassen, Netzwerkcontroller stellt den virtuellen Computer mit einer IP-Adresse an und führt eine DNS-Name-Registrierung im Namen des virtuellen Computers mit der iDNS Server . 

Netzwerkcontroller enthält außerdem die iDNS-Proxy über den virtuellen Computer und die erforderlichen Details namensauflösung für den virtuellen Computer ausführen. 

Wenn eine DNS-Abfrage mit der virtuellen Computer initiiert wird, fungiert der Proxy als Weiterleitung die Abfrage aus dem Virtuellenetzwerk an den Dienst iDNS. 

Der DNS-Proxy wird sichergestellt, dass die Mandanten-VM-Abfragen isoliert sind. Wenn die iDNS-Server für die Abfrage autorisierend ist, antwortet der iDNS-Server eine autorisierende Antwort. Wenn der Server iDNS nicht autorisierend für die Abfrage ist, führt es eine Rekursion DNS zum Auflösen von Internetnamen.

>[!NOTE]
>Diese Informationen sind im Abschnitt enthalten **Konfiguration AttachToVirtualNetwork** in SDNExpressTenant.ps1. Weitere Informationen finden Sie unter [Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts).

