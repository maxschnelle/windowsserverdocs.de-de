---
title: Interner DNS-Dienst (iDNS) für SDN
description: In diesem Thema wird erläutert, wie Sie mithilfe interner DNS (IDNs), das in Software-Defined Networking in Windows Server 2016 integriert ist, DNS-Dienste für Ihre gehosteten mandantenworkloads bereitstellen können.
manager: grcusanz
ms.topic: get-started-article
ms.assetid: ad848a5b-0811-4c67-afe5-6147489c0384
ms.author: anpaul
author: AnirbanPaul
ms.openlocfilehash: 2980e073c34d6177846175563e4d374b439ced44
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952600"
---
# <a name="internal-dns-service-idns-for-sdn"></a>Interner DNS-Dienst (iDNS) für SDN

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Wenn Sie für einen clouddienstanbieter- \( CSP \) oder-Unternehmen arbeiten, der die Bereitstellung von Software-Defined Networking \( Sdn \) in Windows Server 2016 plant, können Sie mithilfe interner DNS- \( IDNs \) , die in Sdn integriert sind, DNS-Dienste für Ihre gehosteten mandantenworkloads bereitstellen.

Virtuelle Computer und Anwendungen für gehostete virtuelle Computer \( \) erfordern DNS, um in ihren eigenen Netzwerken und externen Ressourcen im Internet zu kommunizieren. Mit IDNs können Sie Mandanten DNS-Namens Auflösungs Diensten für Ihren isolierten lokalen Namespace und für Internet Ressourcen bereitstellen.

Da auf den IDNs-Dienst nicht über den IDNs-Proxy von virtuellen Mandanten Netzwerken aus zugegriffen werden kann, ist der Server nicht anfällig für böswillige Aktivitäten in Mandanten Netzwerken.

**Wichtige Features**

Im folgenden finden Sie die wichtigsten Features für IDNs.

- Stellt freigegebene DNS-Namensauflösungsdienste für mandantenworkloads bereit
- Autorisierender DNS-Dienst für die Namensauflösung und DNS-Registrierung innerhalb des Mandanten namesplatzes
- Rekursiver DNS-Dienst für die Auflösung von Internetnamen aus den Mandanten-VMs.
- Wenn gewünscht, können Sie das parallele Hosting von Fabric-und Mandanten Namen konfigurieren.
- Eine kostengünstige DNS-Lösung: Mandanten müssen keine eigene DNS-Infrastruktur bereitstellen.
- Hohe Verfügbarkeit mit Active Directory-Integration, die erforderlich ist.

Wenn Sie Bedenken haben, dass Ihre AD Integrated DNS-Server im Internet geöffnet bleiben, können Sie zusätzlich zu diesen Features IDNs-Server hinter einem anderen rekursiven Konflikt Löser im Umkreis Netzwerk bereitstellen.

Da es sich bei IDNs um einen zentralisierten Server für alle DNS-Abfragen handelt, kann ein CSP oder Enterprise auch Mandanten-DNS-Firewalls implementieren, Filter anwenden, schädliche Aktivitäten erkennen und Transaktionen an einem zentralen Ort überwachen.

## <a name="idns-infrastructure"></a>IDNs-Infrastruktur
Die IDNs-Infrastruktur umfasst IDNs-Server und IDNs-Proxy.

### <a name="idns-servers"></a>IDNs-Server
IDNs umfasst eine Reihe von DNS-Servern, die Mandanten spezifische Daten hosten, z. b. VM-DNS-Ressourcen Einträge.

iDNS-Server sind die autorisierenden Server für ihre internen DNS-Zonen und fungieren auch als Konfliktlöser für öffentliche Namen, wenn Mandanten-VMs versuchen, eine Verbindung mit externen Ressourcen herzustellen.

Alle Hostnamen für virtuelle Computer in virtuellen Netzwerken werden als DNS-Ressourcen Einträge in derselben Zone gespeichert. Wenn Sie z. b. IDNs für eine Zone mit dem Namen "" "" "" "" "" "" "" "" ".

Voll qualifizierte Domänen Namen der Mandanten \( -VM FQDNs \) bestehen aus dem Computernamen und der DNS-Suffixzeichenfolge für die Virtual Network im GUID-Format. Wenn Sie z. b. über eine Mandanten-VM mit dem Namen TENANT1 verfügen, die sich auf dem Virtual Network lokalen Computer (lokal) befindet, lautet der voll qualifizierte Name des virtuellen Computers TENANT1. *VN-GUID*. Configuration. local, wobei *VN-GUID* die DNS-Suffixzeichenfolge für die Virtual Network ist.

>[!NOTE]
>Wenn Sie ein Fabric-Administrator sind, können Sie Ihre CSP-oder Enterprise-DNS-Infrastruktur als IDNs-Server verwenden, anstatt neue DNS-Server speziell für die Verwendung als IDNs-Server bereitzustellen. Unabhängig davon, ob Sie neue Server für IDNs bereitstellen oder Ihre vorhandene Infrastruktur verwenden, nutzt IDNs Active Directory, um Hochverfügbarkeit bereitzustellen. Daher müssen ihre IDNs-Server in Active Directory integriert werden.

### <a name="idns-proxy"></a>IDNs-Proxy
der IDNs-Proxy ist ein Windows-Dienst, der auf jedem Host ausgeführt wird und der Mandanten Virtual Network DNS-Datenverkehr an den IDNs-Server weiterleitet.

Die folgende Abbildung zeigt DNS-Datenverkehrs Pfade von virtuellen Mandanten Netzwerken über den IDNs-Proxy zum IDNs-Server und zum Internet.

![IDNs-Infrastruktur](../../media/Internal-Dns/Internal-Dns.jpg)

## <a name="how-to-deploy-idns"></a>Bereitstellen von IDNs
Wenn Sie Sdn in Windows Server 2016 mithilfe von Skripts bereitstellen, ist IDNs automatisch in der Bereitstellung enthalten.

Weitere Informationen finden Sie in den nachfolgenden Themen.

- [Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts](https://docs.microsoft.com/windows-server/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)


## <a name="understanding-idns-deployment-steps"></a>Informationen zu IDNs-Bereitstellungs Schritten
In diesem Abschnitt erfahren Sie, wie IDNs installiert und konfiguriert wird, wenn Sie Sdn mithilfe von Skripts bereitstellen.

Im folgenden finden Sie eine Zusammenfassung der zum Bereitstellen von IDNs erforderlichen Schritte.

>[!NOTE]
>Wenn Sie Sdn mithilfe von Skripts bereitgestellt haben, müssen Sie diese Schritte nicht ausführen. Die Schritte dienen nur zu Informationszwecken und zur Problembehandlung.

### <a name="step-1-deploy-dns"></a>Schritt 1: Bereitstellen von DNS
Sie können einen DNS-Server bereitstellen, indem Sie den folgenden Windows PowerShell-Beispiel Befehl verwenden.

```powershell
Install-WindowsFeature DNS -IncludeManagementTools
```

### <a name="step-2-configure-idns-information-in-network-controller"></a>Schritt 2: Konfigurieren von IDNs-Informationen im Netzwerk Controller
Bei diesem Skript Segment handelt es sich um einen Rest-Befehl, der vom Administrator an den Netzwerk Controller über die IDNs-Zonen Konfiguration (z. b. die IP-Adresse von idnsserver und die Zone, die zum Hosten der IDNs-Namen verwendet wird) erfolgt.

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
>Dies ist ein Auszug aus dem Abschnitt **Configuration configureidns** in SDNExpress.ps1. Weitere Informationen finden Sie unter [Bereitstellen einer durch Software definierten Netzwerkinfrastruktur mithilfe von Skripts](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts).

### <a name="step-3-configure-the-idns-proxy-service"></a>Schritt 3: Konfigurieren Sie den IDNs-Proxy Dienst.
Der IDNs-Proxy Dienst wird auf allen Hyper-V-Hosts ausgeführt und stellt die Brücke zwischen den virtuellen Netzwerken der Mandanten und dem physischen Netzwerk bereit, in dem sich die IDNs-Server befinden. Die folgenden Registrierungsschlüssel müssen auf jedem Hyper-V-Host erstellt werden.

**DNS-Port:** Fester Port 53

- Registrierungsschlüssel = hklm\system\currentcontrolset\services\nchostagent\parameters\plugins\vnet\infraservices\dnsproxyservice
- ValueName = "Port"
- Valuedata = 53
- ValueType = "DWORD"

**DNS-ProxyPort:** Fester Port 53

- Registrierungsschlüssel = hklm\system\currentcontrolset\services\nchostagent\parameters\plugins\vnet\infraservices\dnsproxyservice
- ValueName = "ProxyPort"
- Valuedata = 53
- ValueType = "DWORD"

**DNS-IP:** An der Netzwerkschnittstelle konfigurierte IP-Adresse für den Fall, dass der Mandant den IDNs-Dienst verwendet

- Registrierungsschlüssel = hklm\system\currentcontrolset\services\nchostagent\parameters\plugins\vnet\infraservices\dnsproxyservice
- ValueName = "IP"
- Valuedata = "169.254.169.254"
- ValueType = "Zeichenfolge"

**MAC-Adresse:** Medien Access Control Adresse des DNS-Servers

- Registrierungsschlüssel = hklm\system\currentcontrolset\services\nchostagent\parameters\plugins\vnet\infraservices\dnsproxyservice
- ValueName = "Mac"
- Valuedata = "AA-BB-CC-AA-BB-CC"
- ValueType = "Zeichenfolge"

**IDNs-Server Adresse:** Eine durch Kommas getrennte Liste von IDNs-Servern.

- Registrierungsschlüssel: hklm\system\currentcontrolset\services\dnsproxy\parameters
- ValueName = "Weiterleitungen"
- Valuedata = "10.0.0.9"
- ValueType = "Zeichenfolge"

>[!NOTE]
>Dies ist ein Auszug aus dem Abschnitt **Configuration configureidnsproxy** in SDNExpress.ps1. Weitere Informationen finden Sie unter [Bereitstellen einer durch Software definierten Netzwerkinfrastruktur mithilfe von Skripts](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts).

### <a name="step-4-restart-the-network-controller-host-agent-service"></a>Schritt 4: Neustarten des Netzwerk Controller-Host-Agent-Diensts
Sie können den folgenden Windows PowerShell-Befehl verwenden, um den Netzwerk Controller-Host-Agent-Dienst neu zu starten.

```powershell
Restart-Service nchostagent -Force
```

Weitere Informationen finden Sie unter [Restart-Service](https://technet.microsoft.com/library/hh849823.aspx).

### <a name="enable-firewall-rules-for-the-dns-proxy-service"></a>Aktivieren von Firewallregeln für den DNS-Proxy Dienst
Sie können den folgenden Windows PowerShell-Befehl verwenden, um eine Firewallregel zu erstellen, die Ausnahmen für die Kommunikation des Proxys mit dem virtuellen Computer und dem IDNs-Server zulässt.

```powershell
Enable-NetFirewallRule -DisplayGroup 'DNS Proxy Firewall'
```

Weitere Informationen finden Sie unter [enable-netfirewallrule](https://technet.microsoft.com/library/jj554869.aspx).

### <a name="validate-the-idns-service"></a>Überprüfen Sie den IDNs-Dienst
Um den IDNs-Dienst zu überprüfen, müssen Sie eine Beispiel Arbeitsauslastung für einen Mandanten bereitstellen.

Weitere Informationen finden Sie unter [Erstellen eines virtuellen Computers und Herstellen einer Verbindung mit einem Mandanten Virtual Network oder VLAN](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create-a-tenant-vm).

Wenn der Mandanten-VM den IDNs-Dienst verwenden soll, müssen Sie die DNS-Server Konfiguration für die VM-Netzwerkschnittstellen leer lassen und den Schnittstellen die Verwendung von DHCP erlauben.

Nachdem der virtuelle Computer mit einer solchen Netzwerkschnittstelle initiiert wurde, erhält er automatisch eine Konfiguration, die es dem virtuellen Computer ermöglicht, IDNs zu verwenden, und der virtuelle Computer beginnt sofort mit dem Ausführen der Namensauflösung mithilfe des IDNs-Dienstanbieter.

Wenn Sie die Mandanten-VM so konfigurieren, dass Sie den IDNs-Dienst verwendet, indem Sie den DNS-Server und die alternativen DNS-Server Informationen für die Netzwerkschnittstelle nicht angeben, stellt der Netzwerk Controller dem virtuellen Computer eine IP-Adresse bereit und führt eine DNS-Namens Registrierung für die VM mit dem IDNs-Server

Der Netzwerk Controller informiert außerdem den IDNs-Proxy über den virtuellen Computer und die erforderlichen Details, um die Namensauflösung für die VM auszuführen.

Wenn die VM eine DNS-Abfrage initiiert, fungiert der Proxy als Weiterleitung der Abfrage vom Virtual Network zum IDNs-Dienst.

Der DNS-Proxy stellt außerdem sicher, dass die Mandanten-VM-Abfragen isoliert sind. Wenn der IDNs-Server für die Abfrage autorisierend ist, antwortet der IDNs-Server mit einer autorisierenden Antwort. Wenn der IDNs-Server für die Abfrage nicht autorisierend ist, führt er eine DNS-Rekursion zum Auflösen von Internet Namen aus.

>[!NOTE]
>Diese Informationen finden Sie im Abschnitt " **Configuration AttachTo VirtualNetwork** " in SDNExpressTenant.ps1. Weitere Informationen finden Sie unter [Bereitstellen einer durch Software definierten Netzwerkinfrastruktur mithilfe von Skripts](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts).

