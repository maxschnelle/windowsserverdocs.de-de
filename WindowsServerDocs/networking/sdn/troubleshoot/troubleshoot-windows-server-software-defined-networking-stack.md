---
title: Problembehandlung für die Windows Server-Software Defined Networking-Stapel
description: Windows Server in der vorliegenden untersucht, die häufig auftretenden Software Defined Networking (SDN)-Fehlern und Fehlerszenarien und beschreibt einen Problembehandlung Workflow, der die verfügbaren Diagnosetools nutzt.
manager: ravirao
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 9be83ed2-9e62-49e8-88e7-f52d3449aac5
ms.author: pashort
author: JMesser81
ms.date: 08/14/2018
ms.openlocfilehash: eeb0c335e4afd3c6835a04421a15073aeab6cdc6
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446238"
---
# <a name="troubleshoot-the-windows-server-software-defined-networking-stack"></a>Problembehandlung für die Windows Server-Software Defined Networking-Stapel

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Handbuch untersucht, die häufig auftretenden Software Defined Networking (SDN)-Fehlern und Fehlerszenarien und beschreibt einen Problembehandlung Workflow, der die verfügbaren Diagnosetools nutzt.  

Weitere Informationen zu Microsoft Software-Defined Networking, finden Sie unter [Software Defined Networking](../../sdn/Software-Defined-Networking--SDN-.md).  

## <a name="error-types"></a>Fehlertypen  
Die folgende Liste stellt die Klasse der Probleme, die am häufigsten mit Hyper-V-Netzwerkvirtualisierung (HNVv1) in Windows Server 2012 R2 aus auf dem Markt produktionsbereitstellungen und stimmt in vielerlei Hinsicht mit den gleichen Typen von Problemen finden Sie in Windows Server 2016 HNVv2 mit den neuen Stapel (Software Defined Network, SDN).  

Die meisten Fehler können in eine kleine Gruppe von Klassen unterteilt werden:   
* **Ungültige oder nicht unterstützte Konfiguration**  
   Ein Benutzer aufruft die NorthBound-API, falsch oder mit ungültiger Richtlinie.   

* **Fehler bei der richtlinienanwendung**  
     Richtlinie für vom Netzwerkcontroller wurde nicht auf einem Hyper-V-Host erheblich verzögert und / oder nicht auf dem neuesten Stand auf allen Hyper-V-Hosts (z. B. nach einer Livemigration) übermittelt.  
* **Konfiguration der letzten datenbankregistrierung bzw. Software-Fehler**  
  Datenpfad-Probleme, die verworfenen Pakete zu.  

* **Externer Fehler im Zusammenhang mit der NIC-Hardware / Treiber oder der dabei Netzwerk-Fabric**  
  Fehlerhaften Aufgabe abladungen (z. B. VMQ) oder falsch konfiguriert (z. B. MTU) dabei Netzwerk-fabric   

  Dieses Handbuch zur Problembehandlung untersucht jede der folgenden Fehlerkategorien und empfiehlt bewährte Methoden und Diagnosetools zur Verfügung, um zu identifizieren und beheben Sie den Fehler.  

## <a name="diagnostic-tools"></a>Diagnosetools  

Ehe wir näher auf die Workflows bei der Problembehandlung für jede dieser Art von Fehlern, betrachten wir die Diagnosetools zur Verfügung.   

Um die Diagnosetools für den Netzwerkcontroller (Steuerelement-Path) zu verwenden, müssen Sie zuerst die RSAT-NetworkController-Funktion installieren und Importieren der ``NetworkControllerDiagnostics`` Modul:  

```  
Add-WindowsFeature RSAT-NetworkController -IncludeManagementTools  
Import-Module NetworkControllerDiagnostics  
```  

Um die Diagnose der hnv-(Data-Path)-Diagnose-Tools verwenden zu können, müssen Sie importieren die ``HNVDiagnostics`` Modul:

```  
# Assumes RSAT-NetworkController feature has already been installed
Import-Module hnvdiagnostics   
```  

### <a name="network-controller-diagnostics"></a>Netzwerkdiagnose-controller  
Diese Cmdlets sind auf TechNet im dokumentiert die [Network Controller-Diagnose-Cmdlet Thema](https://docs.microsoft.com/powershell/module/networkcontrollerdiagnostics/). Sie helfen, Probleme mit Netzwerk-Richtlinie Konsistenz im Steuerelement-Pfad zwischen dem Netzwerkcontroller-Knoten und zwischen dem Netzwerkcontroller und die NC-Host-Agents auf den Hyper-V-Hosts ausgeführt.

 Die _Debug-ServiceFabricNodeStatus_ und _Get-NetworkControllerReplica_ Cmdlets müssen von einem der virtuellen Maschinen des Netzwerkcontrollers Knoten ausgeführt werden. Alle anderen NC-Diagnose-Cmdlets können von jedem Host ausgeführt werden, verfügt eine Verbindung mit dem Netzwerkcontroller und entweder in der Sicherheitsgruppe für die Verwaltung von Netzwerkcontrollern (Kerberos) oder hat Zugriff auf das x. 509-Zertifikat für die Verwaltung des Netzwerkcontrollers. 

### <a name="hyper-v-host-diagnostics"></a>Hyper-V-Host-Diagnose  
Diese Cmdlets sind auf TechNet im dokumentiert die [Hyper-V-Netzwerkvirtualisierung (HNV)-Diagnose-Cmdlet Thema](https://docs.microsoft.com/powershell/module/hnvdiagnostics/). Sie bei der Fehlersuche im Daten-Pfad zwischen Mandanten-VMs (OST-West) und die eingehenden Datenverkehr durch eine SLB-VIP (Nord/Süd). 

Die _Debug-VirtualMachineQueueOperation_, _Get-CustomerRoute_, _Get-PACAMapping_, _Get-ProviderAddress_, _Get-VMNetworkAdapterPortId_, _Get-VMSwitchExternalPortId_, und _Test-EncapOverheadSettings_ sind alle lokalen Tests, die von jedem Hyper-V-Host ausgeführt werden können. Die andere Cmdlets aufrufen Datenpfad-Tests über den Netzwerkcontroller und aus diesem Grund benötigen Zugriff auf der Netzwerkcontroller als descried oben.

### <a name="github"></a>GitHub
Die [Microsoft-SDN GitHub-Repository](https://github.com/microsoft/sdn) verfügt über eine Reihe von Beispielskripts und Workflows, die zusätzlich zu diesen integrierten-Cmdlets erstellen. Insbesondere-Diagnose-Skripts finden Sie in der [Diagnose](https://github.com/Microsoft/sdn/diagnostics) Ordner. Helfen Sie uns diese Skripts beitragen, indem Pull-Anforderungen senden.

## <a name="troubleshooting-workflows-and-guides"></a>Problembehandlung von Workflows und Handbücher  

### <a name="hoster-validate-system-health"></a>[Hoster] Überprüfen der Integrität des Dateisystems
Es ist eine eingebettete Ressource, die mit dem Namen _Konfigurationsstatus_ in einigen der die Netzwerkcontroller-Ressourcen. Konfigurationsstatus stellt Informationen über die Systemintegrität, einschließlich der Konsistenz zwischen den Netzwerkcontroller-Konfiguration und den tatsächlichen (aktiven) Zustand auf den Hyper-V-Hosts bereit. 

Um die Konfiguration zu überprüfen, führen Sie Folgendes von jedem Hyper-V-Host mit der Konnektivität und den Netzwerkcontroller.

>[!NOTE] 
>Der Wert für die *NetworkController* Parameter sollte entweder den FQDN oder IP-Adresse, die basierend auf den Antragstellernamen des x. 509 > Zertifikat für den Netzwerkcontroller erstellt wurde.
>
>Die *Anmeldeinformationen* -Parameter muss nur angegeben werden, wenn die Netzwerkcontroller Kerberos-Authentifizierung (typisch bei Bereitstellungen mit VMM) verwendet. Die Anmeldeinformationen muss für einen Benutzer sein, die in der Netzwerk-Controller-Management-Sicherheitsgruppe ist.

```none
Debug-NetworkControllerConfigurationState -NetworkController <FQDN or NC IP> [-Credential <PS Credential>]

# Healthy State Example - no status reported
$cred = Get-Credential
Debug-NetworkControllerConfigurationState -NetworkController 10.127.132.211 -Credential $cred

Fetching ResourceType:     accessControlLists
Fetching ResourceType:     servers
Fetching ResourceType:     virtualNetworks
Fetching ResourceType:     networkInterfaces
Fetching ResourceType:     virtualGateways
Fetching ResourceType:     loadbalancerMuxes
Fetching ResourceType:     Gateways
```

Eine beispielmeldung für Konfigurationsstatus ist unten dargestellt:

```none
Fetching ResourceType:     servers
---------------------------------------------------------------------------------------------------------
ResourcePath:     https://10.127.132.211/Networking/v1/servers/4c4c4544-0056-4b10-8058-b8c04f395931
Status:           Warning

Source:           SoftwareLoadBalancerManager
Code:             HostNotConnectedToController
Message:          Host is not Connected.
----------------------------------------------------------------------------------------------------------
```

>[!NOTE]
> Es ist ein Fehler im System, in dem die Netzwerkschnittstelle Ressourcen für die SLB/Mux während der Übertragung VM-NIC in einem Fehlerzustand mit Fehler "Virtuellen Switch – Host nicht verbunden, Controller" sind. Dieser Fehler kann sicher ignoriert werden, wenn die IP-Konfiguration in der VM-NIC-Ressource auf eine IP-Adresse aus das logische Transitnetzwerk des IP-Pool festgelegt ist. Es ist ein zweiter Fehler im System, in dem die Netzwerkschnittstelle-Ressourcen für das Gateway hnv-Anbieter-VM-NICs in einem Fehlerzustand mit Fehler "Virtuellen Switch – PortBlocked" sind. Dieser Fehler kann auch ignoriert werden, wenn die IP-Konfiguration in der VM-NIC-Ressource festgelegt ist auf null (entwurfsbedingt).


Die folgende Tabelle zeigt die Liste der Fehlercodes, Nachrichten und Aktionen basierend auf den Konfigurationszustand beobachtet werden.


| **Code**| **Nachricht**| **Aktion**|  
|--------|-----------|----------|  
| Unbekannt| Unbekannter Fehler| |  
| HostUnreachable                       | Der Hostcomputer ist nicht erreichbar | Überprüfen Sie die Konnektivität des Verwaltungsnetzwerks zwischen Netzwerkcontroller und dem Host |  
| PAIpAddressExhausted                  | Die PA-IP-Adressen wurde erreicht. | Erhöhen Sie des logischen hnv-Anbieternetzwerk-Subnetzes-IP-Pool-Größe |  
| PAMacAddressExhausted                 | PA-Mac-Adressen wurde erreicht. | Erhöhen Sie den Bereich der Mac-Pool |  
| PAAddressConfigurationFailure         | Fehler beim PA-Adressen an den Host zu installieren. | Überprüfen Sie die Konnektivität des Verwaltungsnetzwerks zwischen Netzwerkcontroller und dem Host. |  
| CertificateNotTrusted                 | Zertifikat ist nicht vertrauenswürdig  |Beheben Sie die Zertifikate für die Kommunikation mit dem Host verwendet. |  
| CertificateNotAuthorized              | Zertifikat nicht autorisiert | Beheben Sie die Zertifikate für die Kommunikation mit dem Host verwendet. |  
| PolicyConfigurationFailureOnVfp       | Fehler beim Konfigurieren von VFP-Richtlinien | Dies ist ein Laufzeitfehler.  Keine definitive Scanning. Sammeln von Protokollen. |  
| PolicyConfigurationFailure            | Bei der Richtlinien auf den Hosts, aufgrund von Kommunikationsfehlern oder andere Personen übertragen Fehler in der NetworkController.| Keine definitiven Aktionen.  Dies ist aufgrund eines Fehlers bei der Verarbeitung in die Netzwerkcontroller-Module Zielzustand. Sammeln von Protokollen. |  
| HostNotConnectedToController          | Der Host ist nicht noch mit Netzwerkcontroller verbunden. | Portprofil, die nicht auf dem Host oder den Host angewendet ist nicht erreichbar ist, aus dem Netzwerkcontroller. Überprüfen Sie, dass der Registrierungsschlüssel "HostID" die Instanz-ID, der die Server-Ressource entspricht |  
| MultipleVfpEnabledSwitches            | Es gibt mehrere VFp Switches auf dem Host aktiviert.  | Ein Schalter, gelöscht werden, da es sich bei Netzwerk-Controller-Host-Agent die VFP-Erweiterung aktiviert nur ein vSwitch unterstützt |  
| PolicyConfigurationFailure            | Fehler beim VNet-Richtlinien, die für eine VmNic aufgrund Zertifikatfehler oder Verbindungsfehler per Push übertragen  | Überprüfen Sie, ob die richtigen Zertifikate bereitgestellt wurden (Zertifikatantragstellername muss für den FQDN des Hosts übereinstimmen). Überprüfen Sie auch das Hostkonnektivität mit dem Netzwerkcontroller |  
| PolicyConfigurationFailure            | Fehler beim vSwitch-Richtlinien, die für eine VmNic aufgrund Zertifikatfehler oder Verbindungsfehler per Push übertragen  | Überprüfen Sie, ob die richtigen Zertifikate bereitgestellt wurden (Zertifikatantragstellername muss für den FQDN des Hosts übereinstimmen). Überprüfen Sie auch das Hostkonnektivität mit dem Netzwerkcontroller|
| PolicyConfigurationFailure            | Fehler beim Firewall-Richtlinien, die für eine VmNic aufgrund Zertifikatfehler oder Verbindungsfehler per Push übertragen | Überprüfen Sie, ob die richtigen Zertifikate bereitgestellt wurden (Zertifikatantragstellername muss für den FQDN des Hosts übereinstimmen). Überprüfen Sie auch das Hostkonnektivität mit dem Netzwerkcontroller|
| DistributedRouterConfigurationFailure | Fehler beim Konfigurieren der Einstellungen für verteilten Router für die Host-vNic                          | TCP/IP-Stack-Fehler. Unter Umständen Bereinigen der PA- und DR-Host-vNIC auf dem Server, auf dem dieser Fehler gemeldet wurde |
| DhcpAddressAllocationFailure          | Fehler bei der DCHP-Adresszuordnung für eine VMNic                                                    | Überprüfen Sie, ob das Attribut "static IP-Adresse" auf der NIC-Ressource konfiguriert ist |  
| CertificateNotTrusted<br>CertificateNotAuthorized | Fehler bei der verbindungsherstellung zu MUX-Instanz aufgrund von Netzwerk- oder Cert-Fehlern | Überprüfen Sie den numerischen Code in den Fehlercode für die Nachricht bereitgestellt: Dies entspricht dem Winsock-Fehlercode. Zertifikatfehler werden differenzierte (z. B. Zertifikat kann nicht überprüft werden, usw. Cert-nicht autorisiert.) |  
| HostUnreachable                       | MUX ist fehlerhaft. (meistens ist BGPRouter getrennt) | BGP-Peers auf dem RRAS (BGP virtueller Computer) oder die Top-of-Rack (ToR) Switch ist nicht erreichbar ist oder kein peering erfolgreich. Überprüfen Sie die BGP-Einstellungen auf Multiplexer Software Load Balancer-Ressource und BGP-Peers (ToR oder RRAS-VM) |  
| HostNotConnectedToController          | SLB-Host-Agent ist nicht verbunden.  | Überprüfen Sie, dass SLB-Host-Agent-Dienst ausgeführt wird; In der SLB-Host-Agent-Protokolle (automatisch ausführen) finden Sie Gründe Warum, für den Fall, dass SLBM (NC) des Zertifikats, präsentiert von Host-Agent ausgeführt wird abgelehnt Zustand facettenreichen Informationen angezeigt werden  |  
| PortBlocked                           | Die VFP-Port blockiert wird, aufgrund einer fehlenden VNET / ACL-Richtlinien | Überprüfen Sie, ob andere Fehler auftreten, die die Richtlinien nicht konfiguriert werden, verursachen kann. |  
| Überlastung                            | LoadBalancer MUX ist überlastet.  | Leistungsproblem MUX |  
| RoutePublicationFailure               | LoadBalancer MUX ist nicht mit einem BGP-Router verbunden. | Überprüfen Sie, ob die Mux-Instanz verfügt über eine Verbindung mit BGP-Router und diese BGP-peering ordnungsgemäß eingerichtet ist |  
| VirtualServerUnreachable              | LoadBalancer MUX ist nicht mit der SLB-Manager verbunden werden. | Überprüfen Sie die Konnektivität zwischen SLBM und MUX-Instanz |  
| QosConfigurationFailure               | Fehler beim Konfigurieren von QOS-Richtlinien | Überprüfen Sie, ob genügend Bandbreite ist für alle virtuellen Computer verfügbar, wenn QoS-Reservierung verwendet wird |


#### <a name="check-network-connectivity-between-the-network-controller-and-hyper-v-host-nc-host-agent-service"></a>Überprüfen Sie die Netzwerkkonnektivität zwischen dem Netzwerkcontroller und den Hyper-V-Host (NC-Host-Agent-Dienst)
Führen Sie die *Netstat* Befehl aus, um sicherzustellen, dass es drei geltende Verbindungen zwischen den NC-Host-Agent und den Netzwerkcontroller-Knoten und einen EMPFANGSBEREIT-Socket, auf dem Hyper-V-Host sind
- LAUSCHT auf Port TCP:6640 auf Hyper-V-Host (NC-Host-Agent-Dienst)
- Zwei hergestellte Verbindungen von Hyper-V-host-IP an Port 6640 für NC-Knoten-IP für kurzlebige Ports (32000 >)
- Eine hergestellte Verbindung zum Netzwerk Controller REST-IP-Port 6640 von Hyper-V-Host IP-Adresse für ein kurzlebiger port

>[!NOTE]
>Nur möglicherweise zwei hergestellte Verbindungen auf einem Hyper-V-Host befinden sich keine virtuellen mandantenmaschinen auf diesem bestimmten Host.

```none
netstat -anp tcp |findstr 6640

# Successful output
  TCP    0.0.0.0:6640           0.0.0.0:0              LISTENING
  TCP    10.127.132.153:6640    10.127.132.213:50095   ESTABLISHED
  TCP    10.127.132.153:6640    10.127.132.214:62514   ESTABLISHED
  TCP    10.127.132.153:50023   10.127.132.211:6640    ESTABLISHED
```
#### <a name="check-host-agent-services"></a>Überprüfen Sie die Host-Agent-Dienste
Netzwerkcontroller kommuniziert mit zwei Host-Agent-Dienste auf den Hyper-V-Hosts: SLB-Host-Agent und der NC-Host-Agent. Es ist möglich, dass eine oder beide dieser Dienste wird nicht ausgeführt. Überprüfen Sie ihren Status und neu starten Sie, wenn sie nicht ausgeführt werden.

```none
Get-Service SlbHostAgent
Get-Service NcHostAgent

# (Re)start requires -Force flag
Start-Service NcHostAgent -Force
Start-Service SlbHostAgent -Force
```

#### <a name="check-health-of-network-controller"></a>Überprüfen Sie die Integrität des Netzwerkcontrollers
Überprüfen Sie wenn es nicht drei geltende Verbindungen oder des Netzwerkcontrollers reagiert nicht angezeigt wird, feststellen, dass alle Knoten und-Dienstmodule ausgeführt werden, mithilfe der folgenden Cmdlets. 

```none
# Prints a DIFF state (status is automatically updated if state is changed) of a particular service module replica 
Debug-ServiceFabricNodeStatus [-ServiceTypeName] <Service Module>
```
Die Netzwerk-Controller-Dienst-Module sind:
- ControllerService
- ApiService
- SlbManagerService
- ServiceInsertion
- FirewallService
- VSwitchService
- GatewayManager
- FnmService
- HelperService
- UpdateService

Überprüfen Sie, ob ReplicaStatus **bereit** und ist für "healthstate" **Ok**.

In einer produktionsumgebung bietet die Bereitstellung eines Netzwerkcontrollers mit mehreren Knoten, Sie können auch überprüfen, welcher Knoten, die jeder Dienst auf primären ist und den Status der einzelnen Replikats.

```none  
Get-NetworkControllerReplica

# Sample Output for the API service module 
Replicas for service: ApiService

ReplicaRole   : Primary
NodeName      : SA18N30NC3.sa18.nttest.microsoft.com
ReplicaStatus : Ready

```
Überprüfen Sie, dass der Status des Replikats bereit ist für jeden Dienst.

#### <a name="check-for-corresponding-hostids-and-certificates-between-network-controller-and-each-hyper-v-host"></a>Überprüfen Sie für die entsprechende Eigenschaft sowie Zertifikate zwischen Netzwerkcontroller und jedem Hyper-V-Host 
Führen Sie auf einem Hyper-V-Host die folgenden Befehle aus, um zu überprüfen, dass die "HostID", die Instanz-Id von einer Server-Ressource, auf dem Netzwerkcontroller entspricht

```none
Get-ItemProperty "hklm:\system\currentcontrolset\services\nchostagent\parameters" -Name HostId |fl HostId

HostId : **162cd2c8-08d4-4298-8cb4-10c2977e3cfe**

Get-NetworkControllerServer -ConnectionUri $uri |where { $_.InstanceId -eq "162cd2c8-08d4-4298-8cb4-10c2977e3cfe"}

Tags             :
ResourceRef      : /servers/4c4c4544-0056-4a10-8059-b8c04f395931
InstanceId       : **162cd2c8-08d4-4298-8cb4-10c2977e3cfe**
Etag             : W/"50f89b08-215c-495d-8505-0776baab9cb3"
ResourceMetadata : Microsoft.Windows.NetworkController.ResourceMetadata
ResourceId       : 4c4c4544-0056-4a10-8059-b8c04f395931
Properties       : Microsoft.Windows.NetworkController.ServerProperties
```

*Wiederherstellung* Wenn SDNExpress mit Skripts oder manuelle Bereitstellung, den Schlüssel "HostID" in der Registrierung der Instanz-Id, der die Server-Ressource entsprechend aktualisieren. Starten Sie der Netzwerk-Controller-Host-Agent auf dem Hyper-V-Host (physische Server) neu, wenn Sie mithilfe von VMM, löschen Sie den Hyper-V-Server aus VMM, und entfernen Sie den Registrierungsschlüssel "HostID". Anschließend fügen Sie den Server über VMM neu.


Überprüfen Sie, dass die Fingerabdrücke der x. 509-Zertifikate (SouthBound) die Kommunikation zwischen den Hyper-V-Host (NC-Host-Agent-Dienst) und den Netzwerkcontroller-Knoten zum durch den Hyper-V-Host (die Hostnamen werden Antragstellername des Zertifikats des) identisch sind. Überprüfen Sie auch, dass der Netzwerkcontroller-REST-Zertifikat Name des Antragstellers ist *CN =<FQDN or IP>* .

```  
# On Hyper-V Host
dir cert:\\localmachine\my  

Thumbprint                                Subject
----------                                -------
2A3A674D07D8D7AE11EBDAC25B86441D68D774F9  CN=SA18n30-4.sa18.nttest.microsoft.com
...

dir cert:\\localmachine\root

Thumbprint                                Subject
----------                                -------
30674C020268AA4E40FD6817BA6966531FB9ADA4  CN=10.127.132.211 **# NC REST IP ADDRESS**

# On Network Controller Node VM
dir cert:\\localmachine\root  

Thumbprint                                Subject
----------                                -------
2A3A674D07D8D7AE11EBDAC25B86441D68D774F9  CN=SA18n30-4.sa18.nttest.microsoft.com
30674C020268AA4E40FD6817BA6966531FB9ADA4  CN=10.127.132.211 **# NC REST IP ADDRESS**
...
```  

Sie können auch überprüfen, die folgenden Parameter, der jedes Zertifikat, um sicherzustellen, dass der Name des Antragstellers ist erwartet (Hostname oder NC-REST-FQDN oder IP-), das Zertifikat ist noch nicht abgelaufen, und allen Zertifizierungsstellen in der Zertifikatskette in der vertrauenswürdigen Stammzertifizierungsstelle enthalten sind Autorität.

- Antragstellername  
- Ablaufdatum  
- Von der Stammzertifizierungsstelle vertraut  

*Wiederherstellung* Falls mehrere Zertifikate den gleichen Antragstellernamen auf dem Hyper-V-Host verfügen, der Netzwerk-Controller-Host-Agent wird nach dem Zufallsprinzip wählen Sie eine bieten, die dem Netzwerkcontroller. Dies entspricht möglicherweise nicht über den Fingerabdruck des der Server-Ressource, die dem Netzwerkcontroller bekannt. In diesem Fall löschen Sie eines der Zertifikate mit dem gleichen Antragstellernamen auf dem Hyper-V-Host aus, und starten Sie den Netzwerk-Controller-Host-Agent-Dienst neu. Wenn weiterhin keine Verbindung hergestellt werden kann, löschen Sie das andere Zertifikat mit dem gleichen Antragstellernamen auf dem Hyper-V-Host, und löschen Sie die entsprechenden Serverressource in VMM. Anschließend erstellen Sie die Server-Ressource in VMM ein neues x. 509-Zertifikat zu generieren und installieren Sie es auf dem Hyper-V-Host neu.


#### <a name="check-the-slb-configuration-state"></a>Überprüfen Sie die SLB-Konfigurationsstatus
Der Konfigurationsstatus des SLB kann als Teil der Ausgabe an das Debug-NetworkController-Cmdlet ermittelt werden. Dieses Cmdlet gibt auch den aktuellen Satz von Netzwerkcontroller-Ressourcen in JSON-Dateien, die alle IP-Konfigurationen von jedem Hyper-V-Host (Server) und lokale Netzwerkrichtlinie von Host-Agent-Datenbanktabellen. 

Zusätzliche ablaufverfolgungen werden standardmäßig gesammelt. Damit ablaufverfolgungen nicht erfasst werden soll, fügen Sie die - IncludeTraces: $false-Parameter.

```none
Debug-NetworkController -NetworkController <FQDN or IP> [-Credential <PS Credential>] [-IncludeTraces:$false]

# Don't collect traces
$cred = Get-Credential 
Debug-NetworkController -NetworkController 10.127.132.211 -Credential $cred -IncludeTraces:$false

Transcript started, output file is C:\\NCDiagnostics.log
Collecting Diagnostics data from NC Nodes
```

>[!NOTE]
>Der Standardspeicherort für die Ausgabe wird das < Working_directory > \NCDiagnostics\-Verzeichnis sein. Das Standardverzeichnis für die Ausgabe kann geändert werden, indem die `-OutputDirectory` Parameter. 

Informationen über den Zustand der SLB-Konfiguration finden Sie in der _-Diagnose-slbstateResults.Json_ Dateien im Verzeichnis.

Diese JSON-Datei kann in folgende Abschnitte unterteilt werden:
 * Fabric
   * SlbmVips - Listet die in diesem Abschnitt die IP-Adresse der SLB-Manager-VIP-Adresse, die von der Netzwerkcontroller zum Coodinate-Konfiguration und Integrität zwischen der SLB/MUX und die SLB-Host-Agents verwendet wird.
   * MuxState – in diesem Abschnitt sind ein Wert für jedes SLB MUX-Instanz bereitgestellt erteilen den Status der MUX-Instanz
   * Routerkonfiguration – in diesem Abschnitt wird der Upstream Router (BGP-Peer) sind autonome Systemnummer (ASN), während der Übertragung von IP-Adresse und -ID. Es werden auch die SLB/MUX-ASN und die während der Übertragung IP-aufgelistet.
   * Hostinformationen – in diesem Abschnitt verbundenen Liste der Verwaltungs-IP-geht es um alle Hyper-V-Hosts für die Ausführung von Workloads mit Lastenausgleich verfügbar.
   * VIP-Adressbereiche – in diesem Abschnitt werden die öffentlichen und privaten VIP-IP-Pool-Bereiche aufgelistet. Die SLBM-VIP-Adresse wird als eine zugewiesene IP-Adresse von einem dieser Bereiche enthalten sein. 
   * MUX Routen – werden in diesem Abschnitt, einen Wert für jede SLB MUX-Instanz bereitgestellt, das alle von der Routenankündigungen für diese bestimmte MUX-Instanz aufgeführt.
 * Mandant
   * VipConsolidatedState – in diesem Abschnitt werden der Status der Verbindung für jeden Mandanten VIP einschließlich angekündigte Routenpräfix, Hyper-V-Host und der DIP-Endpunkte aufgelistet.

> [!NOTE]
> SLB-Zustand ermittelt werden können, direkt unter Verwendung der [DumpSlbRestState](https://github.com/Microsoft/SDN/blob/master/Diagnostics/DumpSlbRestState.ps1) Skript zur Verfügung, auf die [Microsoft SDN GitHub-Repository](https://github.com/microsoft/sdn). 

#### <a name="gateway-validation"></a>Gatewayüberprüfung

**Vom Netzwerkcontroller:**
```
Get-NetworkControllerLogicalNetwork
Get-NetworkControllerPublicIPAddress
Get-NetworkControllerGatewayPool
Get-NetworkControllerGateway
Get-NetworkControllerVirtualGateway
Get-NetworkControllerNetworkInterface
```

**Von Gateway-VM:**
```
Ipconfig /allcompartments /all
Get-NetRoute -IncludeAllCompartments -AddressFamily
Get-NetBgpRouter
Get-NetBgpRouter | Get-BgpPeer
Get-NetBgpRouter | Get-BgpRouteInformation
```

**Von Anfang Rack (ToR) Switch:**

`sh ip bgp summary (for 3rd party BGP Routers)`

**Windows BGP Router**
```
Get-BgpRouter
Get-BgpPeer
Get-BgpRouteInformation
```

Zusätzlich zu diesen von den Problemen, die wir bisher gesehen haben, (insbesondere auf Grundlage SDNExpress-Bereitstellungen), die häufigste Ursache für das Mandanten-Depot, die nicht auf GW-VMs konfiguriert erste anscheinend die Tatsache, die die Kapazität GW FabricConfig.psd1 ist, dass ein kleiner, was im Vergleich Entwickler versuchen, die die Netzwerk-Verbindungen (S2S-Tunnel) in TenantConfig.psd1 zuweisen. Dies kann leicht überprüft werden, durch einen Vergleich der Ausgaben der folgenden Befehle aus:

```
PS > (Get-NetworkControllerGatewayPool -ConnectionUri $uri).properties.Capacity
PS > (Get-NetworkControllerVirtualgatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "TenantName").properties.OutboundKiloBitsPerSecond
PS > (Get-NetworkControllerVirtualgatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "TenantName").property
```

### <a name="hoster-validate-data-plane"></a>[Hoster] Überprüfen der Datenebene
Nachdem der Netzwerkcontroller bereitgestellt wurde, mehrinstanzenfähige virtuelle Netzwerke und Subnetze erstellt wurden, und VMs wurden auf die virtuellen Subnetze angefügt, können die Tests der zusätzlicher Fabric-Ebene vom Hoster zur Überprüfung der Konnektivität mit Mandanten ausgeführt werden.

#### <a name="check-hnv-provider-logical-network-connectivity"></a>Hnv-Anbieter Konnektivität des logischen Netzwerks überprüfen
Nach der ersten Gast, die auf einem Hyper-V-Host ausgeführten VM mit einem virtuellen mandantennetzwerk verbunden ist, weist der Netzwerkcontroller zwei hnv-Anbieter-IP-Adressen (PA-IP-Adressen) an den Hyper-V-Host. Diese IP-Adressen werden von der HNV-Anbieternetzwerk als logischen Netzwerks-IP-Pool und vom Netzwerkcontroller verwaltet werden.  Um herauszufinden, was diese beiden hnv-IP-Adressen sind die

```none
PS > Get-ProviderAddress

# Sample Output
ProviderAddress : 10.10.182.66
MAC Address     : 40-1D-D8-B7-1C-04
Subnet Mask     : 255.255.255.128
Default Gateway : 10.10.182.1
VLAN            : VLAN11

ProviderAddress : 10.10.182.67
MAC Address     : 40-1D-D8-B7-1C-05
Subnet Mask     : 255.255.255.128
Default Gateway : 10.10.182.1
VLAN            : VLAN11
```

Diese hnv-Anbieter IP-Adressen (PA-IPs) zugewiesen sind Ethernet-Adapter, die in einem separaten Depot des TCP/IP-Netzwerk erstellt und der Adaptername eines des _VLANX_ wobei X für das VLAN auf das logische hnv-Anbieternetzwerk (Transport)-Netzwerk zugewiesen ist.

Konnektivität zwischen zwei Hyper-V-Hosts, die das logisches Netzwerk, indem ein Ping mit einem zusätzlichen Depot erfolgen kann HNV-Anbieternetzwerk mit (-c-Y) Parameter, wobei Y ist die TCP/IP-netzwerkdepot, in dem die PAhostVNICs erstellt werden. Diese Depot kann dazu bestimmt werden:

```none
C:\> ipconfig /allcompartments /all

<snip> ...
==============================================================================
Network Information for *Compartment 3*
==============================================================================
   Host Name . . . . . . . . . . . . : SA18n30-2
<snip> ...

Ethernet adapter VLAN11:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : Microsoft Hyper-V Network Adapter
   Physical Address. . . . . . . . . : 40-1D-D8-B7-1C-04
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::5937:a365:d135:2899%39(Preferred)
   IPv4 Address. . . . . . . . . . . : 10.10.182.66(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.128
   Default Gateway . . . . . . . . . : 10.10.182.1
   NetBIOS over Tcpip. . . . . . . . : Disabled

Ethernet adapter VLAN11:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : Microsoft Hyper-V Network Adapter
   Physical Address. . . . . . . . . : 40-1D-D8-B7-1C-05
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::28b3:1ab1:d9d9:19ec%44(Preferred)
   IPv4 Address. . . . . . . . . . . : 10.10.182.67(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.128
   Default Gateway . . . . . . . . . : 10.10.182.1
   NetBIOS over Tcpip. . . . . . . . : Disabled

*Ethernet adapter vEthernet (PAhostVNic):*
<snip> ...
```

>[!NOTE]
> Die PA-Host-vNIC-Adapter nicht in den Daten-Pfad verwendet werden und daher keine IP-Adresse zugewiesen, die an den Adapter"vEthernet (PAhostVNic)".

Beispielsweise wird vorausgesetzt, dass Hyper-V-Host 1 und 2 hnv-Anbieter (PA) IP-Adressen:

|Hyper-V-Host –|-PA IP-Adresse 1|-PA IP-Adresse 2|
|---             |---            |---             |
|Host 1 | 10.10.182.64 | 10.10.182.65 |
|Host 2 | 10.10.182.66 | 10.10.182.67 |

Wir können zwischen den beiden mit dem folgenden Befehl zur Überprüfung der Konnektivität von HNV-Anbieternetzwerk als logisches Netzwerk zu pingen.

```none
# Ping the first PA IP Address on Hyper-V Host 2 from the first PA IP address on Hyper-V Host 1 in compartment (-c) 3
C:\> ping -c 3 10.10.182.66 -S 10.10.182.64

# Ping the second PA IP Address on Hyper-V Host 2 from the first PA IP address on Hyper-V Host 1 in compartment (-c) 3
C:\> ping -c 3 10.10.182.67 -S 10.10.182.64

# Ping the first PA IP Address on Hyper-V Host 2 from the second PA IP address on Hyper-V Host 1 in compartment (-c) 3
C:\> ping -c 3 10.10.182.66 -S 10.10.182.65

# Ping the second PA IP Address on Hyper-V Host 2 from the second PA IP address on Hyper-V Host 1 in compartment (-c) 3
C:\> ping -c 3 10.10.182.67 -S 10.10.182.65
```

*Wiederherstellung* HNV-Anbieternetzwerk als wenn Ping nicht funktioniert, überprüfen Sie die physische Netzwerkverbindung, einschließlich der VLAN-Konfiguration. Die physischen NICs auf jedem Hyper-V-Host sollte im Modus "Trunk" keine spezifischen VLAN zugewiesen sein. Die Management-Host-vNIC muss mit dem logischen Verwaltungsnetzwerk des VLAN isoliert sein.

```none
PS C:\> Get-NetAdapter "Ethernet 4" |fl

Name                       : Ethernet 4
InterfaceDescription       : <NIC> Ethernet Adapter
InterfaceIndex             : 2
MacAddress                 : F4-52-14-55-BC-21
MediaType                  : 802.3
PhysicalMediaType          : 802.3
InterfaceOperationalStatus : Up
AdminStatus                : Up
LinkSpeed(Gbps)            : 10
MediaConnectionState       : Connected
ConnectorPresent           : True
*VlanID                     : 0*
DriverInformation          : Driver Date 2016-08-28 Version 5.25.12665.0 NDIS 6.60

# VMM uses the older PowerShell cmdlet <Verb>-VMNetworkAdapterVlan to set VLAN isolation
PS C:\> Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName <Mgmt>

VMName VMNetworkAdapterName Mode     VlanList
------ -------------------- ----     --------
<snip> ...        
       Mgmt                 Access   7
<snip> ...

# SDNExpress deployments use the newer PowerShell cmdlet <Verb>-VMNetworkAdapterIsolation to set VLAN isolation
PS C:\> Get-VMNetworkAdapterIsolation -ManagementOS

<snip> ...

IsolationMode        : Vlan
AllowUntaggedTraffic : False
DefaultIsolationID   : 7
MultiTenantStack     : Off
ParentAdapter        : VMInternalNetworkAdapter, Name = 'Mgmt'
IsTemplate           : True
CimSession           : CimSession: .
ComputerName         : SA18N30-2
IsDeleted            : False

<snip> ...
```

#### <a name="check-mtu-and-jumbo-frame-support-on-hnv-provider-logical-network"></a>Überprüfen Sie die MTU und Jumbo Frame-Unterstützung für logische Hnv-Anbieternetzwerk

Ein häufiges Problem in das logische hnv-anbieternetzwerk ist, dass die physischen Ports und/oder Ethernet-Karte keine große genug ist, MTU so konfiguriert, dass um den Mehraufwand durch VXLAN (oder NVGRE)-Kapselung zu behandeln. 
>[!NOTE]
> Einige Ethernet-Karten und Treiber unterstützen die neue * EncapOverhead-Schlüsselwort, das automatisch durch den Netzwerk-Controller-Host-Agent auf einen Wert von 160 festgelegt werden sollen. Dieser Wert wird dann hinzugefügt werden, auf den Wert des der * JumboPacket-Schlüsselwort, deren Summe als die angekündigte MTU verwendet wird.
> z. B. * EncapOverhead = 160 und * JumboPacket = 1514 = > MTU 1674B =

```none
# Check whether or not your Ethernet card and driver support *EncapOverhead
PS C:\ > Test-EncapOverheadSettings

Verifying Physical Nic : <NIC> Ethernet Adapter #2
Physical Nic  <NIC> Ethernet Adapter #2 can support SDN traffic. Encapoverhead value set on the nic is  160
Verifying Physical Nic : <NIC> Ethernet Adapter
Physical Nic  <NIC> Ethernet Adapter can support SDN traffic. Encapoverhead value set on the nic is  160
```

Verwenden Sie zum Testen, und zwar unabhängig davon, ob das logische hnv-anbieternetzwerk der größeren MTU Größe End-to-End unterstützt die _Test-LogicalNetworkSupportsJumboPacket_ Cmdlet:
```none
# Get credentials for both source host and destination host (or use the same credential if in the same domain)
$sourcehostcred = Get-Credential
$desthostcred = Get-Credential

# Use the Management IP Address or FQDN of the Source and Destination Hyper-V hosts
Test-LogicalNetworkSupportsJumboPacket -SourceHost sa18n30-2 -DestinationHost sa18n30-3 -SourceHostCreds $sourcehostcred -DestinationHostCreds $desthostcred

# Failure Results
SourceCompartment : 3
pinging Source PA: 10.10.182.66 to Destination PA: 10.10.182.64 with Payload: 1632
pinging Source PA: 10.10.182.66 to Destination PA: 10.10.182.64 with Payload: 1472
Checking if physical nics support jumbo packets on host
Physical Nic  <NIC> Ethernet Adapter #2 can support SDN traffic. Encapoverhead value set on the nic is  160
Cannot send jumbo packets to the destination. Physical switch ports may not be configured to support jumbo packets.
Checking if physical nics support jumbo packets on host
Physical Nic  <NIC> Ethernet Adapter #2 can support SDN traffic. Encapoverhead value set on the nic is  160
Cannot send jumbo packets to the destination. Physical switch ports may not be configured to support jumbo packets.

# TODO: Success Results aftering updating MTU on physical switch ports
```

*Wiederherstellung*
* Passen Sie die MTU-Größe auf den physischen Switchports mindestens 1674B (einschließlich 14 b-Ethernet-Header und Nachspann)
* Wenn Ihre Netzwerkkarte (NIC) das EncapOverhead-Schlüsselwort nicht unterstützt, passen Sie die JumboPacket-Schlüsselwort, um mindestens 1674B


#### <a name="check-tenant-vm-nic-connectivity"></a>Überprüfen Sie die Mandanten-VM-NIC-Konnektivität
Jede VM-NIC an einen Gast-VM zugewiesen hat eine CA-PA-Zuordnung zwischen der privaten Kundenadressraum (CA) und den Speicherplatz des hnv-Anbieter Adresse (PA). Diese Zuordnungen werden in den Tabellen OVSDB Server, auf jedem Hyper-V-Host gespeichert und können gefunden werden, indem Sie das folgende Cmdlet ausführen.

```none
# Get all known PA-CA Mappings from this particular Hyper-V Host
PS > Get-PACAMapping

CA IP Address CA MAC Address    Virtual Subnet ID PA IP Address
------------- --------------    ----------------- -------------
10.254.254.2  00-1D-D8-B7-1C-43              4115 10.10.182.67
10.254.254.3  00-1D-D8-B7-1C-43              4115 10.10.182.67
192.168.1.5   00-1D-D8-B7-1C-07              4114 10.10.182.65
10.254.254.1  40-1D-D8-B7-1C-06              4115 10.10.182.66
192.168.1.1   40-1D-D8-B7-1C-06              4114 10.10.182.66
192.168.1.4   00-1D-D8-B7-1C-05              4114 10.10.182.66
```
>[!NOTE]
> Wenn die CA-PA-Zuordnungen, die Sie erwarten, dass für einen bestimmten Mandanten-VM nicht ausgegeben werden, überprüfen Sie die VM-NIC und die IP-Konfiguration die Ressourcen auf dem Netzwerkcontroller unter Verwendung der _Get-NetworkControllerNetworkInterface_ Cmdlet. Überprüfen Sie außerdem die hergestellte Verbindungen zwischen den NC-Host-Agent und dem Netzwerkcontroller.

Mit diesen Informationen ein Mandanten-VM-Ping kann jetzt ausgelöst werden, indem der Hoster über den Netzwerkcontroller mit der _Test-VirtualNetworkConnection_ Cmdlet.

## <a name="specific-troubleshooting-scenarios"></a>Bestimmte Problembehandlungsszenarien

Die folgenden Abschnitte enthalten Hinweise zur Behandlung von spezifischen Szenarien.

### <a name="no-network-connectivity-between-two-tenant-virtual-machines"></a>Keine Netzwerkkonnektivität zwischen zwei virtuellen Computern von Mandanten

1.  [Mandant] Stellen Sie sicher, dass der Verkehr von Windows-Firewall in der Mandanten-VMs nicht blockiert wird.  
2.  [Mandant] Überprüfen Sie, dass die IP-Adressen der Mandanten-VM mit zugewiesenen _Ipconfig_. 
3.  [Hoster] Führen Sie **Test-VirtualNetworkConnection** zwischen dem Hyper-V-Host, und Überprüfen der Konnektivität zwischen zwei virtuellen Maschinen des Mandanten betreffende. 

>[!NOTE]
>Die VSID bezieht sich auf das virtuelle Subnetz-ID an. Im Fall von VXLAN ist dies die VXLAN Netzwerk-ID (VNI). Sie finden diesen Wert durch Ausführen der **Get-PACAMapping** Cmdlet.

#### <a name="example"></a>Beispiel

    $password = ConvertTo-SecureString -String "password" -AsPlainText -Force
    $cred = New-Object pscredential -ArgumentList (".\administrator", $password) 

Erstellen Sie CA-Ping zwischen "Grüne Web VM-1" mit SenderCA IP des 192.168.1.4 auf Host "sa18n30-2.sa18.nttest.microsoft.com" Mgmt-IP des 10.127.132.153 ListenerCA IP des 192.168.1.5 erstellt, die beide auf VSID (Virtual Subnet) 4114 angefügt.

    Test-VirtualNetworkConnection -OperationId 27 -HostName sa18n30-2.sa18.nttest.microsoft.com -MgmtIp 10.127.132.153 -Creds $cred -VMName "Green Web VM 1" -VMNetworkAdapterName "Green Web VM 1" -SenderCAIP 192.168.1.4 -SenderVSID 4114 -ListenerCAIP 192.168.1.5 -ListenerVSID 4114

    Test-VirtualNetworkConnection at command pipeline position 1

Kundenadressraum Ping-Test gestartet, die Absenderadresse 192.168.1.4 erfolgreich starten der Ablaufverfolgungssitzung Ping zum 192.168.1.5 erstellt Rtt = 0 ms


CA-Routing-Informationen:

    Local IP: 192.168.1.4
    Local VSID: 4114
    Remote IP: 192.168.1.5
    Remote VSID: 4114
    Distributed Router Local IP: 192.168.1.1
    Distributed Router Local MAC: 40-1D-D8-B7-1C-06
    Local CA MAC: 00-1D-D8-B7-1C-05
    Remote CA MAC: 00-1D-D8-B7-1C-07
    Next Hop CA MAC Address: 00-1D-D8-B7-1C-07

PA-Routing-Informationen:

    Local PA IP: 10.10.182.66
    Remote PA IP: 10.10.182.65

 <snip> ...

4. [Mandant] Überprüfen Sie, dass keine verteilten Firewall-Richtlinien für die virtuelle Subnetz oder einer VM-Netzwerkschnittstellen, die Datenverkehr blockieren würde angegebenen vorhanden ist.    

Fragen Sie die REST-API von Netzwerkcontroller finden Sie in der Demo-Umgebung auf sa18n30nc in der Domäne sa18.nttest.microsoft.com.

    $uri = "https://sa18n30nc.sa18.nttest.microsoft.com"
    Get-NetworkControllerAccessControlList -ConnectionUri $uri 

# <a name="look-at-ip-configuration-and-virtual-subnets-which-are-referencing-this-acl"></a>Sehen Sie sich die IP-Konfiguration und virtuelle Subnetze, die mit dieser ACL verweisen

1. [Hoster] Führen Sie ``Get-ProviderAddress`` auf beiden Hyper-V-Hosts gehostet, die zwei Mandanten-VMs in Frage, und führen Sie dann ``Test-LogicalNetworkConnection`` oder ``ping -c <compartment>`` aus dem Hyper-V-Host zum Überprüfen der Konnektivität auf das logische hnv-anbieternetzwerk
2.  [Hoster] Stellen Sie sicher, dass die MTU-Einstellungen auf den Hyper-V-Hosts korrekt und jede Schicht-2-Geräte, die zwischen den Hyper-V-Hosts gewechselt werden. Führen Sie ``Test-EncapOverheadValue`` auf allen Hyper-V-Hosts, die betreffende. Auch überprüfen, ob alle Layer-2 Switches zwischen MTU auf mindestens 1674 Bytes festgelegt, um die maximale Mehraufwand von 160 Bytes zu berücksichtigen.  
3.  [Hoster] Wenn PA-IP-Adressen nicht vorhanden sind, und/oder CA-Verbindung unterbrochen ist, stellen Sie sicher, dass die Netzwerkrichtlinie empfangen wurde. Führen Sie ``Get-PACAMapping`` um festzustellen, ob die Kapselung-Regeln und die CA-PA-Zuordnungen, die zum Erstellen von virtuellen Netzwerken Overlay erforderlich sind, ordnungsgemäß eingerichtet werden.  
4.  [Hoster] Überprüfen Sie, dass der Netzwerk-Controller-Host-Agent und den Netzwerkcontroller verbunden ist. Führen Sie ``netstat -anp tcp |findstr 6640`` um festzustellen, ob die   
5.  [Hoster] Überprüfen Sie, die der Host in der HKLM-ID / entspricht die Instanz-ID der Serverressourcen Hosten von virtuellen Maschinen des Mandanten.  
6. [Hoster] Überprüfen Sie, dass die Port-Profil-ID der Instanz-ID, der die VM-Netzwerkschnittstellen der virtuellen Maschinen des Mandanten übereinstimmt.  

## <a name="logging-tracing-and-advanced-diagnostics"></a>Protokollierung, Ablaufverfolgung und erweiterte Diagnose

Die folgenden Abschnitte enthalten Informationen für erweiterte Diagnose, Protokollierung und Ablaufverfolgung an.

### <a name="network-controller-centralized-logging"></a>Netzwerkcontroller zentralisierte Protokollierung 

Der Netzwerkcontroller kann automatisch Debugger-Protokolle erfassen und an einem zentralen Ort speichern. Sammlung von Protokollen kann aktiviert werden, bei der Bereitstellung des Netzwerkcontrollers für erstmalig verwenden oder jederzeit später noch mal. Die Protokolle werden über den Netzwerkcontroller erfasst, und Elemente, die vom Netzwerkcontroller verwalteten Netzwerk: Computer, der Software Load balancer (SLB) und der Gatewaycomputer zu hosten. 

Diese Protokolle enthalten die Debugprotokolle für den Netzwerkcontroller-Cluster, die Netzwerkcontroller-Anwendung, Gateway-Protokolle, SLB, virtuelle Netzwerke und die verteilte Firewall. Wenn ein neues Host/SLB/Gateway und den Netzwerkcontroller hinzugefügt wird, wird die Protokollierung auf diesen Computern gestartet. Auf ähnliche Weise, wenn ein Host/SLB/Gateway aus dem Netzwerkcontroller entfernt wird, wird auf diesen Computern Protokollierung beendet.

#### <a name="enable-logging"></a>Protokollierung aktivieren

Protokollierung wird automatisch aktiviert, bei der Installation den Netzwerkcontroller-Cluster mithilfe der **Install-NetworkControllerCluster** Cmdlet. Standardmäßig werden die Protokolle auf dem Netzwerkcontroller Knoten lokal gesammelt *%systemdrive%\SDNDiagnostics*. Es ist **dringend empfohlen,** , dass Sie diesen Speicherort als einer Remotedateifreigabe (nicht lokal) zu ändern. 

Auf der Netzwerkcontroller Clusterprotokolle gespeichert werden *%programData%\Windows Fabric\log\Traces*. Sie können angeben, einen zentralen Ort für die Erfassung von Protokollen mit der **DiagnosticLogLocation** Parameter mit den Empfehlungen, die in diesem wird werden einer Remotedateifreigabe befindet. 

Wenn Sie den Zugriff auf diesen Speicherort beschränken möchten, können Sie die Anmeldeinformationen für den Zugriff mit Bereitstellen der **LogLocationCredential** Parameter. Wenn Sie die Anmeldeinformationen für den Zugriff auf den Protokollspeicherort bereitstellen, sollten Sie auch angeben der **CredentialEncryptionCertificate** -Parameter, der zum Verschlüsseln der Anmeldeinformationen, die lokal gespeichert, auf den Knoten für den Netzwerkcontroller verwendet wird.  

Mit den Standardeinstellungen empfiehlt es sich, dass Sie mindestens 75 GB freier Speicherplatz in den zentralen Standort und 25 GB auf den lokalen Knoten haben (sofern nicht mithilfe von einem zentralen Speicherort) für einen Cluster mit 3 Knoten dem Netzwerkcontroller.

#### <a name="change-logging-settings"></a>Ändern der Einstellungen für diagnoseprotokollierung

Sie können ändern, dass die protokollierungseinstellungen auf jederzeit mithilfe der ``Set-NetworkControllerDiagnostic`` Cmdlet. Die folgenden Einstellungen können geändert werden:

- **Speicherort des Fehlerprotokolls zentralisierte**.  Sie können ändern, den Speicherort für alle Protokolle, mit der ``DiagnosticLogLocation`` Parameter.  
- **Anmeldeinformationen zum Zugreifen auf Protokolldateien Speicherort**.  Sie können ändern, dass die Anmeldeinformationen für den Zugriff auf den Protokollspeicherort, mit der ``LogLocationCredential`` Parameter.  
- **Verschieben in die lokale Protokollierung**.  Wenn Sie einen zentralen Ort zum Speichern der Protokolle angegeben haben, können Sie verschieben wieder lokal auf den Knoten "Netzwerkcontroller" mit der Protokollierung der ``UseLocalLogLocation`` Parameter (nicht empfohlen, da große Erforderlicher Speicherplatz).  
- **Umfang der Protokollierung**.  Standardmäßig werden alle Protokolle gesammelt. Sie können den Bereich, um nur den Netzwerkcontroller-Cluster-Protokolle sammeln ändern.  
- **Protokolliergrad**.  Der Standardprotokolliergrad ist Informational. Sie können es auf Fehler, Warnung oder ausführlich ändern.  
- **Log altern Zeit**.  Die Protokolle werden in einer kreisförmigen Weise gespeichert. Drei Tage Protokollierungsdaten erhalten in der Standardeinstellung Sie, ob Sie lokale Protokollierung oder die zentrale Protokollierung verwenden. Sie können ändern, dass dieses Zeitlimit mit **LogTimeLimitInDays** Parameter.  
- **Log Size altern**.  Standardmäßig müssen Sie eine maximale 75 GB von Protokollierungsdaten, wenn die zentrale Protokollierung und 25 GB verwenden, wenn lokale Protokollierung zu verwenden. Sie können diese Grenze aus, und Ändern der **LogSizeLimitInMBs** Parameter.

#### <a name="collecting-logs-and-traces"></a>Das Erfassen von Protokollen und Ablaufverfolgungen

VMM-Bereitstellungen, die die zentrale Protokollierung für den Netzwerkcontroller wird standardmäßig verwendet wird. Des Speicherorts der Dateifreigabe für diese Protokolle wird angegeben, wenn Sie die Netzwerkcontroller-Dienstvorlage bereitstellen.

Wenn ein Dateispeicherort nicht angegeben wird, lokale wird auf jedem Knoten des Netzwerkcontrollers mit Protokollen C:\Windows\tracing\SDNDiagnostics eingesparten Protokollierung verwendet werden. Diese Protokolle werden mithilfe der folgenden Hierarchie gespeichert:

- CrashDumps
- NCApplicationCrashDumps
- NCApplicationLogs
- PerfCounters
- SDNDiagnostics
- Ablaufverfolgungen

Die dem Netzwerkcontroller verwendet die Service Fabric (Azure). Service Fabric-Protokollen können erforderlich sein, bei der Problembehandlung für bestimmte Probleme. Diese Protokolle finden Sie auf jedem Knoten des Netzwerkcontrollers auf C:\ProgramData\Microsoft\Service Fabric.

Wenn ein Benutzer ausgeführt, wurde die _Debug-NetworkController_ Cmdlet zusätzliche Protokolle stehen auf jedem Hyper-V-Host, der mit einer Server-Ressource im Netzwerkcontroller angegeben wurde. Diese Protokolle (und ablaufverfolgungen, wenn aktiviert) werden unter C:\NCDiagnostics beibehalten.

### <a name="slb-diagnostics"></a>SLB Diagnostics

#### <a name="slbm-fabric-errors-hosting-service-provider-actions"></a>SLBM fabricfehler (Hosting-Anbieter Dienstaktionen)

1.  Überprüfen Sie, dass Software Load Balancer Manager SLBM () funktioniert und Orchestrierungsebene miteinander kommunizieren können: SLBM > SLB MUX-Instanz aus, und SLBM -> SLB-Host-Agents. Führen Sie [DumpSlbRestState](https://github.com/Microsoft/SDN/blob/master/Diagnostics/DumpSlbRestState.ps1) von einem beliebigen Knoten mit Zugriff auf Netzwerk-Controller-REST-Endpunkt.  
2.  Überprüfen Sie die *SDNSLBMPerfCounters* in PerfMon auf eines der Netzwerkcontroller-Knoten-VM (vorzugsweise dem Netzwerkcontroller Primärknoten - Get-NetworkControllerReplica):
    1.  Werden Load Balancer (LB)-Engine ist mit SLBM verbunden? (*Gesamtanzahl der SLBM LBEngine-Konfigurationen* > 0)  
    2.  Weiß SLBM mindestens über eine eigene Endpunkte? (*VIP-Endpunkten insgesamt* > = 2)  
    3.  Sind Hyper-V (DIP) Hosts SLBM verbunden? (*Verbundenen Clients von HP* == Num-Server)   
    4.  Werden SLBM wird mit/MUX verbunden? (*MUX verbunden* == *MUX fehlerfrei auf SLBM* == *MUX betriebsbereit gemeldet* = # SLB/MUX-VMs).  
3.  Stellen Sie sicher, dass der BGP-Router konfiguriert wurde erfolgreich mit der SLB MUX-peering ist  
    1.  Bei Verwendung von RRAS mit Remote Access (d. h. BGP virtueller Computer):  
        1.  Get-Peer-sollte verbundene angezeigt.  
        2.  Get-BgpRouteInformation sollte mindestens eine Route für die SLBM anzeigen selbst VIP-Adresse  
    2.  Wenn mit der physischen Top-of-Rack (ToR) als BGP-Peers zu wechseln, in der Dokumentation  
        1.  Zum Beispiel: # Anzeigen Bgp-Instanz  
4.  Überprüfen Sie die *SlbMuxPerfCounters* und *SLBMUX* Leistungsindikatoren im Systemmonitor auf die SLB/Mux-VM
5.  Überprüfen Sie Konfigurationsstatus und VIP-Bereiche in den Software Load Balancer-Manager-Ressource  
    1.  Get-NetworkControllerLoadBalancerConfiguration - ConnectionUri < https://<FQDN or IP>| Convertto-Json-Tiefe 8 (Überprüfen Sie die VIP-Bereiche in den IP-Pools und stellen Sie sicher Self SLBM-VIP-Adresse (*LoadBalanacerManagerIPAddress*) und ein beliebiger mandantenseitige VIPs sind in diesen Bereichen)  
        1. "< Öffentlichen/privaten VIP-Adresse logischen Netzwerk Ressourcen-ID >" Get-NetworkControllerIpPool - %NetworkID - SubnetId "< öffentlichen/privaten VIP-Adresse logischen Subnetz Ressourcen-ID >" - Ressourcen-ID "<IP Pool Resource Id>" - ConnectionUri $uri | Convertto-Json-Tiefe 8 
    2.  Debug-NetworkControllerConfigurationState -  

Wenn eine der oben angegebenen Fehler Überprüfungen, wird der Mandant SLB Status auch in ein Fehler oder Fehlermodus sein.  

**Wiederherstellung**   
Basierend auf die folgenden Diagnoseinformationen angezeigt, beheben Sie die folgenden:  
* Stellen Sie sicher, dass SLB Multiplexers verbunden sind  
  * Beheben von Problemen mit Zertifikaten  
  * Beheben von Netzwerkverbindungsproblemen  
* Stellen Sie sicher, dass BGP-peeringinformationen erfolgreich konfiguriert ist  
* Stellen Sie sicher, Host-ID in der Registrierung übereinstimmt, Server-Instanz-ID in Server-Ressource (Anhang verweisen *HostNotConnected* Fehlercode:)  
* Protokolle erfassen  

#### <a name="slbm-tenant-errors-hosting-service-provider--and-tenant-actions"></a>Fehler der SLBM-Mandanten (Hosting-Dienst und Aktionen)

1.  [Hoster] Überprüfen Sie *Debug-NetworkControllerConfigurationState* um festzustellen, ob alle LoadBalancer-Ressourcen in einem Fehlerzustand sind. Versuchen Sie es, zu verringern, indem Sie die Aufgaben im Anhang.   
    1.  Überprüfen Sie, ob ein VIP-Endpunkt vorhanden und Werbung Routen  
    2.  Überprüfen Sie, wie viele der DIP-Endpunkte für den VIP-Endpunkt ermittelt wurden  
2.  [Mandant] Überprüfen Sie Load Balancer-Ressourcen sind ordnungsgemäß angegeben.  
    1.  Überprüfen Sie die DIP-Adresse Endpunkten, die im SLBM registriert sind die Mandanten-VMs, die die Adresse der LoadBalancer-Back-End-Pool IP-Konfigurationen entsprechen gehostet werden  
3.  [Hoster] Wenn der DIP-Endpunkte nicht erkannt oder verbunden sind:   
    1.  Überprüfen Sie *Debug-NetworkControllerConfigurationState*  
        1.  Überprüfen, NC und SLB-Host-Agent wird erfolgreich mit dem Netzwerk Controller der Ereigniskoordinator verbunden ``netstat -anp tcp |findstr 6640)``  
    2.  Überprüfen Sie *"HostID"* in *Nchostagent* Service Regkey (Verweis *HostNotConnected* Fehlercode im Anhang) die entsprechenden Server-Ressource-Instanz-Id (entspricht ``Get-NCServer |convertto-json -depth 8``)  
    3.  Überprüfen Sie, dass Port Profil-Id für den Port des virtuellen Computers entsprechende VM NIC-Ressource des Instanz-Id übereinstimmt   
4.  [Hostinganbieter] Sammeln von Protokollen   

#### <a name="slb-mux-tracing"></a>SLB Mux Tracing

Informationen über den Software Load Balancer-MUX kann auch über die Ereignisanzeige ermittelt werden. 
1. Klicken Sie auf "Anzeigen analytische und Debugprotokolle", unter der Ereignis-Viewer-Ansicht-Menü
2. Navigieren Sie zu "Anwendungs- und Dienstprotokolle" > Microsoft > Windows > SlbMuxDriver > verfolgen Sie in der Ereignisanzeige 
3. Klicken Sie mit der rechten Maustaste darauf und wählen Sie "Protokoll aktivieren"

>[!NOTE]
>Es wird empfohlen, dass nur diese Protokollierung für kurze Zeit aktiviert werden, wenn Sie versuchen, ein Problem zu reproduzieren.

### <a name="vfp-and-vswitch-tracing"></a>VFP und vSwitch-Ablaufverfolgung

Von jedem Hyper-V-host der eine Gast-VM mit einem virtuellen mandantennetzwerk verbunden gehostet wird, können Sie eine VFP-Ablaufverfolgung, um zu bestimmen, wo die Probleme liegen möglicherweise erfasst.

```
netsh trace start provider=Microsoft-Windows-Hyper-V-VfpExt overwrite=yes tracefile=vfp.etl report=disable provider=Microsoft-Windows-Hyper-V-VmSwitch 
netsh trace stop
netsh trace convert .\vfp.etl ov=yes 
```
