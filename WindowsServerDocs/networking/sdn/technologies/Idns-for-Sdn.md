---
title: Interne DNS-Dienst (iDNS) für SDN
description: In diesem Thema wird erläutert, bereitstellen können, das DNS-Dienste auf Ihrer gehosteten mandantenarbeitsauslastungen mithilfe von internen DNS (iDNS), die mit Software Defined Networking in Windows Server 2016 integriert ist.
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
ms.openlocfilehash: 4bdb495b585cf60315dee60f9365e282877fdc1d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="internal-dns-service-idns-for-sdn"></a>Interne DNS-Dienst \(iDNS\) für SDN

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Wenn Sie für eine Cloud-Dienstanbieter \(CSP\) oder Unternehmen, das Planen der Bereitstellung von Software Defined Networking \(SDN\) in Windows Server 2016 ist arbeiten, können Sie die DNS-Dienste für mandantenarbeitsauslastungen gehosteten bereitstellen, mithilfe der interne DNS-\(iDNS\), das in SDN integriert ist.

\(VMs\) gehosteten virtuellen Computer und Anwendungen benötigen DNS innerhalb ihrer eigenen Netzwerke und mit externen Ressourcen im Internet kommunizieren. Mit iDNS können Sie Mandanten mit DNS-Namensauflösungsdienste für ihre isoliert, lokale Namensbereich und Ressourcen im Internet bereitstellen.

Da der Dienst iDNS nicht aus der Mandant virtuelle Netzwerke zugänglich ist, ist nicht durch den Proxy iDNS der Server nicht anfällig für böswillige Aktivitäten auf mandantennetzwerke.

**Wichtige Features**

Im folgenden werden die wichtigsten Features für iDNS.

- Bietet freigegebenen DNS-Namensauflösungsdienst für Mandanten Arbeitslasten name
- Autorisierenden DNS-Dienst für die namensauflösung und DNS-Registrierung innerhalb der Namespace Mandanten
- Recursive DNS-Dienst für die Auflösung von Internetnamen von Mandanten-VMs.
- Falls gewünscht, können Sie konfigurieren, gleichzeitige Hosten von Fabric und Mandanten
- Eine kostengünstige Lösung für DNS - Mandanten müssen keine eigene DNS-Infrastruktur bereitstellen
- Hohe Verfügbarkeit mit Active Directory-Integration, die erforderlich ist.

Zusätzlich zu diesen Features können Sie Sie erhalten Ihre Anzeige integriert sind mit dem Internet-DNS-Server zu öffnen, können Sie iDNS Server hinter einer anderen rekursive Resolver im Umkreisnetzwerk bereitstellen.

Da iDNS auf einem zentralen Server für alle DNS-Abfragen ist, kann einen CSP oder Enterprise auch Implementieren von Mandanten DNS-Firewalls, Filter anwenden, böswillige Aktivitäten zu erkennen und Transaktionen an einem zentralen Speicherort überwachen

## <a name="idns-infrastructure"></a>iDNS Infrastruktur
Die iDNS Infrastruktur umfasst iDNS Servern und iDNS Proxy.

### <a name="idns-servers"></a>iDNS Servern
iDNS enthält eine Reihe von DNS-Servern, die Mandanten-spezifischen Daten, z. B. VM DNS-Ressourceneinträge enthalten.

iDNS Server autorisierenden Server für die internen DNS-Zonen sind und auch als Resolver für öffentliche Namen dienen Wenn Mandanten VMs Verbindungsversuch mit externen Ressourcen.

Alle Hostnamen für virtuelle Maschinen in virtuelle Netzwerke werden als DNS-Ressourceneinträge unter der gleichen Zone gespeichert. Wenn Sie für eine Zone mit dem Namen "contoso.Local" iDNS bereitstellen, werden die DNS-Ressourceneinträge für die virtuellen Computer auf das Netzwerk in der Zone "contoso.Local" gespeichert.

Mandanten VM Fully Qualified Domain Names \(FQDNs\) bestehen aus den Computernamen und die DNS-Suffix-Zeichenfolge für das virtuelle Netzwerk, im GUID-Format. Besitzen Sie ein Mandant virtuellen Computer namens TENANT1, die im virtuellen Netzwerk Contoso, lokal, ist die VM-FQDN z. B. TENANT1. *Vn-Guid*. "contoso.Local", wobei *Vn-Guid* die DNS-Suffix-Zeichenfolge für das virtuelle Netzwerk ist.

>[!NOTE]
>Wenn Sie ein fabricadministrator sind, können Sie Ihre CSP oder Unternehmens-DNS-Infrastruktur, wie iDNS Server anstelle von neuen DNS-Server speziell für die Bereitstellung als iDNS Server verwenden. Ob Sie die neuen Server für iDNS bereitstellen, oder Sie Ihre vorhandene Infrastruktur verwenden, verwendet iDNS Active Directory, um hohe Verfügbarkeit bereitzustellen. Ihre iDNS Server müssen daher in Active Directory integriert werden.

### <a name="idns-proxy"></a>iDNS Proxy
iDNS-Proxy ist ein Windows-Dienst, der auf jedem Host ausgeführt wird und die Mandanten virtuelle Netzwerk-DNS-Datenverkehr die iDNS Server weiterleitet.

Die folgende Abbildung zeigt die DNS-Datenverkehr Pfade von Mandanten virtuelle Netzwerke durch den Proxy iDNS, um die iDNS Server und dem Internet.

![iDNS Infrastruktur](../../media/Internal-Dns/Internal-Dns.jpg)

## <a name="how-to-deploy-idns"></a>Vorgehensweise beim Bereitstellen iDNS
Wenn Sie SDN in Windows Server 2016 mithilfe von Skripts bereitstellen, ist iDNS automatisch in Ihrer Bereitstellung enthalten.

Weitere Informationen finden Sie unter den folgenden Themen.

- [Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)


## <a name="understanding-idns-deployment-steps"></a>Grundlegendes zu iDNS Bereitstellungsschritte
In diesem Abschnitt können Sie verstehen, wie iDNS installiert und konfiguriert werden, wenn Sie mithilfe von Skripts SDN bereitstellen.

Es folgt eine Übersicht über die erforderlichen Schritte zum Bereitstellen von iDNS.

>[!NOTE]
>Wenn Sie mithilfe von Skripts SDN bereitgestellt haben, müssen Sie keinen der folgenden Schritte ausführen. Die Schritte werden Informationen und dienen nur zur Problembehandlung zu bereitgestellt.

### <a name="step-1-deploy-dns"></a>Schritt 1: Bereitstellen von DNS
Sie können einen DNS-Server bereitstellen, mit der folgende Windows PowerShell-Befehl.
    
    Install-WindowsFeature DNS -IncludeManagementTools
    
### <a name="step-2-configure-idns-information-in-network-controller"></a>Schritt 2: Konfigurieren von iDNS Informationen im Netzwerk-Controller
Dieses Skript-Segment ist ein REST-Aufruf, der erfolgt durch den Administrator auf Netzwerkcontroller, informiert die iDNS Zonenkonfiguration – z. B. die IP-Adresse der iDNSServer und die Zone, die zum Hosten der iDNS Namen verwendet wird. 

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
>Hierbei handelt es sich um einen Auszug aus Abschnitt **Konfiguration ConfigureIDns** in SDNExpress.ps1. Weitere Informationen finden Sie unter [Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts).

### <a name="step-3-configure-the-idns-proxy-service"></a>Schritt 3: Konfigurieren der iDNS Proxy-Dienst
Die der iDNS Proxy-Dienst ausgeführt wird, auf jedem Hyper-V-Hosts, die Bereitstellung von der Brücke zwischen virtuellen Netzwerk des Mandanten und dem physischen Netzwerk, in dem sich die iDNS Server befinden. Die folgenden Registrierungsschlüssel müssen auf jedem Hyper-V-Host erstellt werden.


**DNS-Port:** fester Port 53

- Registrierungsschlüssel = HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService "
- Wert = "Port"
- ValueData = 53
- ValueType = "Dword"
       

**DNS-Proxy-Port:** fester Port 53

- Registrierungsschlüssel = HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService "
- Wert = "ProxyPort"
- ValueData = 53
- ValueType = "Dword"
        
**DNS IP:** dies die festen IP-Adresse für die Netzwerkschnittstelle konfiguriert ist, für den Fall, dass Mandanten den Dienst iDNS verwenden möchte.

- Registrierungsschlüssel = HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService "
- Wert = "IP"
- ValueData = "169.254.169.254"
- ValueType = "String"

        
**MAC-Adresse:** Media Access Control-Adresse des DNS-Servers

- Registrierungsschlüssel = HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService
- Wert = "MAC"
- ValueData = "aa-bb-cc-aa-bb-cc"
- ValueType = "String"

**Adresse des Servers IDNS:** eine durch Kommas getrennte Liste mit iDNS Servern.

- Registrierungsschlüssel: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNSProxy\Parameters
- Wert = "Weiterleitung"
- ValueData = "10.0.0.9"
- ValueType = "String"



>[!NOTE]
>Hierbei handelt es sich um einen Auszug aus Abschnitt **Konfiguration ConfigureIDnsProxy** in SDNExpress.ps1. Weitere Informationen finden Sie unter [Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts).

### <a name="step-4-restart-the-network-controller-host-agent-service"></a>Schritt 4: Starten den Netzwerk-Controller-Host-Agent-Dienst neu.
Die folgenden Windows PowerShell-Befehl können Sie den Netzwerk-Controller Host-Agent-Dienst neu starten.
    
    Restart-Service nchostagent -Force
    
Weitere Informationen finden Sie unter [Restart-Service](https://technet.microsoft.com/library/hh849823.aspx).

### <a name="enable-firewall-rules-for-the-dns-proxy-service"></a>Aktivieren Sie Firewallregeln für den DNS-Proxy-Dienst
Die folgenden Windows PowerShell-Befehl können Sie eine Firewallregel erstellen, die Ausnahmen für den Proxy zur Kommunikation mit dem virtuellen Computer und Server iDNS zulässt.
    
    Enable-NetFirewallRule -DisplayGroup 'DNS Proxy Firewall'

Weitere Informationen finden Sie unter [Enable-NetFirewallRule](https://technet.microsoft.com/library/jj554869.aspx).
    
### <a name="validate-the-idns-service"></a>Überprüfen Sie den Dienst iDNS
Um die iDNS Service zu überprüfen, müssen Sie eine Beispiel für die Mandanten-Arbeitslast bereitstellen.

Weitere Informationen finden Sie unter [erstellen Sie eine virtuelle Maschine und Verbinden mit einem virtuellen Mandantennetzwerk oder VLAN](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create-a-tenant-vm).

Wenn Sie die Mandanten-VM, den Dienst iDNS verwenden möchten, müssen Sie die Schnittstellen VM-Netzwerk-DNS-Server-Konfiguration leer lassen und die Schnittstellen DHCP verwenden. 

Nach der virtuellen Computer mit solchen eine Netzwerkschnittstelle initiiert wird, es erhält automatisch eine Konfiguration, die den virtuellen Computer mit iDNS ermöglicht, und die virtuelle Maschine sofort namensauflösung mithilfe des Diensts iDNS ausführen.

Wenn Sie die Mandanten-VM mit dem iDNS Dienst von Netzwerk-DNS-Server und alternativer DNS-Server Informationen zur Benutzeroberfläche leer lassen konfigurieren, Netzwerkcontroller stellt den virtuellen Computer mit einer IP-Adresse und führt eine Registrierung der DNS-Namen für die virtuelle Maschine mit dem iDNS Server. 

Netzwerkcontroller informiert den Proxy iDNS auch über den virtuellen Computer und die erforderlichen Details namensauflösung für den virtuellen Computer ausführen. 

Wenn der virtuelle Computer eine DNS-Abfrage initiiert, fungiert der Proxy als Weiterleitung der Abfrage aus dem virtuellen Netzwerk an den Dienst iDNS. 

Der DNS-Proxy wird sichergestellt, dass die Mandanten-VM-Abfragen isoliert sind. Wenn der iDNS Server für die Abfrage der iDNS Server antwortet mit eine autorisierende Antwort. Ist der Server iDNS nicht autorisierend für die Abfrage, eine Rekursion DNS zum Auflösen von Internetnamen ausgeführt.

>[!NOTE]
>Diese Informationen finden Sie im Abschnitt **Konfiguration AttachToVirtualNetwork** in SDNExpressTenant.ps1. Weitere Informationen finden Sie unter [Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts).

