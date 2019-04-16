---
title: Problembehandlung bei der Windows Server-Software Defined Networking-Stapel
description: Dieses Handbuch für Windows Server prüft die Software Defined Networking (SDN)-Fehlermeldungen und Fehlerszenarien und erläutert, einen zur Problembehandlung Workflow, der den verfügbaren Diagnosetools nutzt.
manager: ravirao
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 9be83ed2-9e62-49e8-88e7-f52d3449aac5
ms.author: pashort
author: JMesser81
ms.openlocfilehash: af59ae6746467f9aecf384d1b3cf9af1e8baeb9a
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="troubleshoot-the-windows-server-software-defined-networking-stack"></a>Problembehandlung bei der Windows Server-Software Defined Networking-Stapel

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Handbuch untersucht die allgemeine Software Defined Networking (SDN)-Fehlern und Fehlerszenarien und erläutert, einen zur Problembehandlung Workflow, der den verfügbaren Diagnosetools nutzt.  

Weitere Informationen zu Microsoft Software-Defined Networking, finden Sie unter [Software Defined Networking](../../sdn/Software-Defined-Networking--SDN-.md).  

## <a name="error-types"></a>Error-Typen  
In der folgende Liste die Klasse von Problemen, die am häufigsten mit Hyper-V-Netzwerkvirtualisierung (HNVv1) in Windows Server2012 R2 auf dem Markt produktionsbereitstellungen darstellt und deckt in vielerlei Hinsicht mit der gleichen Arten von Problemen, die in Windows Server2016 HNVv2 mit der neuen Software definierten Netzwerk (SDN) Stapel angezeigt.  

Die meisten Fehler können in einer kleinen Gruppe von Klassen unterteilt werden:   
* **Ungültige oder nicht unterstützte Konfiguration**  
   Ein Benutzer ruft die NorthBound-API, falsch oder mit ungültiger Richtlinie.   

* **Fehler bei der Anwendung von Gruppenrichtlinien**  
     Netzwerkcontroller-Richtlinie wurde nicht auf einem Hyper-V-Host erheblich verzögert und / oder auf allen Hyper-V-Hosts (z.B. nach einer Livemigration) nicht auf dem neuesten Stand übermittelt.  
* **Konfiguration Drift oder Software-Fehler**  
 Datenpfad-Probleme, die sich ergebende Eingehende verworfene Pakete.  

* **Externer Fehler im Zusammenhang mit NIC-Hardware / Treiber oder die dabei Netzwerk-Fabric**  
 Fehlerhafte Aufgabe abladungen (z.B. VMQ) oder Netzwerk-Fabric dabei falsch konfiguriert (z.B. MTU)   

 Dieser Leitfaden zur Problembehandlung untersucht jede dieser Fehlerkategorien und empfiehlt bewährte Methoden und Diagnose-Tools zu identifizieren und beheben Sie den Fehler.  

## <a name="diagnostic-tools"></a>Diagnosetools  

Erläutert die Problembehandlung Workflows für jede dieser Art von Fehlern, betrachten wir den Diagnosetools zur Verfügung.   
  
Um den Diagnosetools Netzwerkcontroller (Steuerelement-Pfad) zu verwenden, müssen Sie zunächst installieren Sie die Remoteserver-Verwaltungstools NetworkController und Importieren der ``NetworkControllerDiagnostics``Modul:  

```  
Add-WindowsFeature RSAT-NetworkController -IncludeManagementTools  
Import-Module NetworkControllerDiagnostics  
```  

Um die Hyper-v-Diagnose (Datenpfad)-Diagnosetools zu verwenden, importieren Sie die ``HNVDiagnostics``Modul:
  
```  
# Assumes RSAT-NetworkController feature has already been installed
Import-Module hnvdiagnostics   
```  

### <a name="network-controller-diagnostics"></a>Domänencontroller-Netzwerkdiagnose  
Diese Cmdlets sind in TechNet dokumentiert die [Network Controller Diagnose Cmdlet Thema](https://docs.microsoft.com/en-us/powershell/module/networkcontrollerdiagnostics/). Auf diese Weise Erkennen von Problemen mit dem Netzwerk Richtlinie Konsistenz in der Steuerelement-Pfad zwischen dem Netzwerkcontroller Knoten und zwischen Netzwerkcontroller und den NC-Host-Agents auf den Hyper-V-Hosts ausgeführt werden.

 Die _Debug-ServiceFabricNodeStatus_ und _Get-NetworkControllerReplica_ Cmdlets müssen von einem Netzwerkcontroller Knoten virtuellen Computer ausgeführt werden. Alle anderen NC-Diagnose-Cmdlets können von jedem Host ausgeführt werden, die Verbindung mit dem Netzwerkcontroller und wird entweder in der Sicherheitsgruppe für die Verwaltung des Domänencontrollers (Kerberos) oder hat Zugriff auf das x. 509-Zertifikat für die Verwaltung von Netzwerkcontroller. 
   
### <a name="hyper-v-host-diagnostics"></a>Hyper-V-Host-Diagnose  
Diese Cmdlets sind in TechNet dokumentiert die [Hyper-V-Netzwerkvirtualisierung (HNV) Diagnose Cmdlet Thema](https://docs.microsoft.com/en-us/powershell/module/hnvdiagnostics/). Sie helfen, Probleme in der Datenpfad zwischen virtuellen Computern für die Mandanten / (OST-West) zu identifizieren und eingehende Datenverkehr über ein SLB VIP (Nord/Süd). 

Die _Debug-VirtualMachineQueueOperation_, _Get-CustomerRoute_, _Get-PACAMapping_, _Get-ProviderAddress_, _Get-VMNetworkAdapterPortId_, _Get-VMSwitchExternalPortId_, und _Test-EncapOverheadSettings_ werden alle lokalen Tests, die auf jedem Hyper-V-Host ausgeführt werden kann. Die anderen Cmdlets aufrufen Datenpfad-Tests durch den Netzwerk-Controller und benötigen daher den Zugriff auf den Netzwerkcontroller als descried oben.
 
### <a name="github"></a>GitHub
Die [Microsoft-SDN-GitHub-Repository](https://github.com/microsoft/sdn) bietet eine Reihe von Skripts und Workflows, die auf diese Cmdlets mitgelieferte aufbauen. Insbesondere Diagnose-Skripts finden Sie in der [Diagnose](https://github.com/Microsoft/sdn/diagnostics) Ordner. Helfen Sie uns übermitteln Pull-Anforderungen für diese Skripts auswirken.

## <a name="troubleshooting-workflows-and-guides"></a>Workflows und Handbücher zur Problembehandlung  

### <a name="hoster-validate-system-health"></a>[Hoster] Überprüfen des Systemstatus
Es ist eine eingebettete Ressource, die mit dem Namen _Konfigurationsstatus_ in verschiedenen Ressourcen, die Netzwerk-Controller. Konfigurationsstatus enthält Informationen zum Systemstatus einschließlich der Konsistenz zwischen den Netzwerk-Controller-Konfiguration und die tatsächliche (aktiven) auf den Hyper-V-Hosts. 

Um die Konfiguration zu überprüfen, führen Sie Folgendes auf jedem Hyper-V-Host mit Konnektivität mit dem Netzwerk-Controller.

>[!NOTE] 
>Der Wert für die *NetworkController* Parameter sollte entweder den FQDN oder IP-Adresse, die basierend auf der Antragstellername des x. 509 > Zertifikat für den Netzwerkcontroller erstellt wurde.
>
>Die *Credential* Parameter muss nur angegeben werden, wenn die Netzwerkcontroller Kerberos-Authentifizierung (Standard bei der VMM-Bereitstellung) verwendet wird. Die Anmeldeinformationen muss für einen Benutzer, der in der Netzwerk-Controller-Management-Sicherheitsgruppe ist.

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

Beispiel für eine Konfiguration Nachricht sieht folgendermaßen aus:

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
> Es ist ein Fehler im System, wo die Netzwerkschnittstelle Ressourcen für Öffentliche Verkehrsmittel SLB Mux-VM-NIC in einen Fehlerstatus mit Fehler "Virtual Switch – Host nicht verbunden, Controller" befinden. Dieser Fehler kann ignoriert werden, wenn die IP-Konfiguration in der VM-NIC-Ressource auf eine IP-Adresse aus den während der Übertragung logischen Netzwerk IP-Adresspool festgelegt ist. Ein zweite Fehler ist in das System, in dem die Netzwerkschnittstelle Ressourcen für das Gateway Hyper-v-Anbieter VM-NICs in einem Fehlerzustand mit dem Fehler "virtueller Switch – PortBlocked" vorhanden. Dieser Fehler kann auch ignoriert werden, wenn die IP-Konfiguration in der VM-NIC-Ressource festgelegt ist auf null (entwurfsbedingt).


In der folgenden Tabelle zeigt die Liste von Fehlercodes, Nachrichten und Aktionen basierend auf den Konfigurationsstatus eingehalten werden.

  
| **Code**| **Nachricht**| **Aktion**|  
|:--------:|:-----------:|----------:|  
| Unbekannt| Unbekannter Fehler| |  
| HostUnreachable                       | Host-Computer ist nicht erreichbar. | Überprüfen Sie die Management-Netzwerkkonnektivität zwischen Netzwerkcontroller und dem Host |  
| PAIpAddressExhausted                  | Die PA-IP-Adressen leer ist | Erhöhen Sie die Hyper-v-Anbieter logischen Subnetzes, IP-Pool-Größe |  
| PAMacAddressExhausted                 | Die PA-MAC-Adressen leer ist | Erhöhen Sie die Mac-Pool-Bereich |  
| PAAddressConfigurationFailure         | Fehler beim PA-Adressen auf dem Host zu nutzen | Überprüfen Sie die Management-Netzwerkkonnektivität zwischen Netzwerkcontroller und dem Host. |  
| CertificateNotTrusted                 | Zertifikat ist nicht vertrauenswürdig  |Beheben Sie die Zertifikate für die Kommunikation mit dem Host verwendet. |  
| CertificateNotAuthorized              | Zertifikat nicht autorisiert | Beheben Sie die Zertifikate für die Kommunikation mit dem Host verwendet. |  
| PolicyConfigurationFailureOnVfp       | Fehler beim Konfigurieren der VFP-Richtlinien | Dies ist ein Laufzeitfehler.  Keine definitive Scanning. Sammeln von Protokollen. |  
| PolicyConfigurationFailure            | Fehler bei der Push-Installation Richtlinien auf den Hosts, aufgrund von Kommunikationsfehlern oder andere Fehler in der NetworkController.| Keine definitiven Aktionen.  Dies ist aufgrund eines Fehlers beim Ziel Zustand in den Modulen Netzwerkcontroller verarbeiten. Sammeln von Protokollen. |  
| HostNotConnectedToController          | Der Host ist noch nicht mit den Netzwerk-Controller verbunden | Portprofil nicht angewendet, auf dem Host oder dem Host ist nicht erreichbar aus dem Netzwerkcontroller. Überprüfen Sie, ob der Registrierungsschlüssel HostID die Instanz-ID des Server-Ressource entspricht |  
| MultipleVfpEnabledSwitches            | Es gibt mehrere VFp Switches auf dem Host aktiviert.  | Löschen einer der Optionen, da Netzwerk-Agent für Domänencontroller nur ein vSwitch mit der VFP-Erweiterung aktiviert unterstützt |  
| PolicyConfigurationFailure            | Fehler beim VNet Richtlinien für eine VmNic aufgrund Zertifikatfehler oder Konnektivitätsfehler Pushbenachrichtigungen  | Überprüfen Sie, ob die richtigen Zertifikate bereitgestellt wurden (Antragstellername des Zertifikats muss der FQDN des Hosts übereinstimmen). Vergewissern Sie sich außerdem die Hostkonnektivität mit dem Netzwerkcontroller |  
| PolicyConfigurationFailure            | Fehler beim vSwitch-Richtlinien für eine VmNic aufgrund Zertifikatfehler oder Konnektivitätsfehler Pushbenachrichtigungen  | Überprüfen Sie, ob die richtigen Zertifikate bereitgestellt wurden (Antragstellername des Zertifikats muss der FQDN des Hosts übereinstimmen). Vergewissern Sie sich außerdem die Hostkonnektivität mit dem Netzwerkcontroller|
| PolicyConfigurationFailure            | Fehler beim Firewall-Richtlinien für eine VmNic aufgrund Zertifikatfehler oder Konnektivitätsfehler Pushbenachrichtigungen | Überprüfen Sie, ob die richtigen Zertifikate bereitgestellt wurden (Antragstellername des Zertifikats muss der FQDN des Hosts übereinstimmen). Vergewissern Sie sich außerdem die Hostkonnektivität mit dem Netzwerkcontroller|
| DistributedRouterConfigurationFailure | Fehler beim Konfigurieren der verteilten Router-Einstellungen auf dem Host-vNic                          | Fehler des TCP/IP-Stapel. Unter Umständen Bereinigen der PA und Dr. Host-vNICs auf dem Server, auf dem dieser Fehler gemeldet wurde |
| DhcpAddressAllocationFailure          | Fehler bei der DHCP-Adresszuweisung für eine VMNic                                                    | Überprüfen Sie, ob das Attribut der statische IP-Adresse für den NIC-Ressource konfiguriert ist |  
| CertificateNotTrusted<br>CertificateNotAuthorized | Fehler bei Verbindung mit Mux aufgrund von Netzwerk- oder Cert-Fehlern | Überprüfen den numerischen Code in der Meldung Fehlercode: Dies entspricht dem Winsock-Fehlercode. Zertifikatfehler präzise sind (z.B. Zertifikat nicht überprüft werden kann, nicht autorisiert Cert usw..) |  
| HostUnreachable                       | MUX ist fehlerhaft (meistens ist BGPRouter getrennt) | BGP-Peer auf dem RRAS (BGP virtueller Computer) oder das Top-of-Rack (ToR) Switch ist nicht erreichbar ist oder nicht transportpeering erfolgreich. Überprüfen der BGP-Einstellungen auf Software Load Balancer zur Vereinheitlichung der Ressource und BGP-Peer (ToR oder RRAS virtueller Computer) |  
| HostNotConnectedToController          | SLB Host-Agent ist nicht verbunden.  | Überprüfen Sie, dass SLB Host-Agent-Dienst ausgeführt wird. Weitere Informationen finden Sie unter SLB Host-Agent-Protokolle (automatisch ausgeführt wird) aus Gründen der Grund für den Fall, dass das Zertifikat, das von der hostagent ausgeführt wird zurückgewiesen, SLBM (NC) Zustand Nuancen Informationen angezeigt werden  |  
| PortBlocked                           | Der VFP-Port blockiert werden, aufgrund fehlender VNET / ACL-Richtlinien | Überprüfen Sie, ob es gibt andere Fehler, die die Richtlinien nicht konfiguriert werden, führen könnten. |  
| Überlastet                            | LoadBalancer MUX ist überlastet.  | Leistungsproblem bei MUX |  
| RoutePublicationFailure               | LoadBalancer MUX ist nicht mit einem BGP-Router verbunden. | Überprüfen Sie der MUX-Konnektivität mit dem BGP-Router verfügt und BGP-Peering richtig eingerichtet ist |  
| VirtualServerUnreachable              | LoadBalancer MUX ist nicht mit SLB Manager verbunden. | Überprüfen Sie die Verbindung zwischen SLBM und MUX |  
| QosConfigurationFailure               | Fehler beim Konfigurieren von QOS-Richtlinien | Überprüfen Sie, ob ausreichend Bandbreite ist für alle virtuellen Computer verfügbar, wenn QoS-Reservierung verwendet wird |


#### <a name="check-network-connectivity-between-the-network-controller-and-hyper-v-host-nc-host-agent-service"></a>Überprüfen Sie Netzwerkkonnektivität zwischen Netzwerkcontroller und Hyper-V-Host (NC-Host-Agent-Dienst)
Führen Sie die *Netstat* Geben Sie folgenden Befehl, um sicherzustellen, dass es drei ESTABLISHED Verbindungen zwischen NC-Agent und der Netzwerk-Controller-Knoten und eine SPRACHERKENNUNG Socket auf dem Hyper-V-Host Gibt
- Abhören von Port TCP:6640 auf Hyper-V-Host (NC-Host-Agent-Dienst)
- Zwei hergestellte Verbindungen von Hyper-V-Host-IP-Port 6640 IP-NC-Knoten auf kurzlebige Ports (> 32000)
- Eine Verbindung von Hyper-V-Host-IP auf ein kurzlebiger Port zum Netzwerk Controller REST-IP-Port 6640

>[!NOTE]
>Nur möglicherweise zwei hergestellte Verbindungen auf einem Hyper-V-Host keine Mandanten virtuelle Maschinen auf diesem bestimmten Host befinden.

```none
netstat -anp tcp |findstr 6640

# Successful output
  TCP    0.0.0.0:6640           0.0.0.0:0              LISTENING
  TCP    10.127.132.153:6640    10.127.132.213:50095   ESTABLISHED
  TCP    10.127.132.153:6640    10.127.132.214:62514   ESTABLISHED
  TCP    10.127.132.153:50023   10.127.132.211:6640    ESTABLISHED
```
#### <a name="check-host-agent-services"></a>Server-Agent-Dienste überprüfen
Netzwerkcontroller kommuniziert mit zwei Host-Agent-Dienste auf den Hyper-V-Hosts: SLB Host-Agent und NC-Host-Agent. Es ist möglich, dass eine oder beide dieser Dienste nicht ausgeführt wird. Überprüfen Sie ihren Status und neu starten Sie, wenn sie nicht ausgeführt werden.

```none
Get-Service SlbHostAgent
Get-Service NcHostAgent

# (Re)start requires -Force flag
Start-Service NcHostAgent -Force
Start-Service SlbHostAgent -Force
```

#### <a name="check-health-of-network-controller"></a>Überprüfen Sie die Integrität von Netzwerkcontroller
Überprüfen Sie wenn nicht drei ESTABLISHED Verbindungen oder Netzwerkcontroller reagiert nicht angezeigt wird, dass alle Knoten und Service Module einsatzbereit sind, mithilfe der folgenden Cmdlets. 

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

Überprüfen, die ReplicaStatus **bereit** und "healthstate" **Ok**.

In einer Bereitstellung mit einem Netzwerk mit mehreren Knoten Controller ist Sie können auch überprüfen, welcher Knoten jeder Dienst auf primären ist und den Status der einzelnen Replikats.

```none  
Get-NetworkControllerReplica

# Sample Output for the API service module
Replicas for service: ApiService

ReplicaRole   : Primary
NodeName      : SA18N30NC3.sa18.nttest.microsoft.com
ReplicaStatus : Ready

```
Überprüfen Sie, ob der Status des Replikats bereit für die einzelnen Dienste.
 
#### <a name="check-for-corresponding-hostids-and-certificates-between-network-controller-and-each-hyper-v-host"></a>Überprüfen Sie für die entsprechende Eigenschaft und Zertifikate zwischen Netzwerkcontroller und jedem Hyper-V-Host 
Führen Sie auf einem Hyper-V-Host die folgenden Befehle zu überprüfen, ob die Instanz-ID einer Server-Ressource auf dem Netzwerk-Controller die HostID entspricht

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

*Wiederherstellung* Wenn SDNExpress mit Skripts oder manuelle Bereitstellung den HostId Schlüssel in der Registrierung die Instanz-ID des Server-Ressource entsprechend zu aktualisieren. Starten Sie der Controller-Host-Agent auf dem Hyper-V-Host (physische Server) neu, wenn Sie mithilfe von VMM, löschen Sie den Hyper-V-Server aus VMM und entfernen Sie den HostId Registrierungsschlüssel. Dann fügen Sie den Server über VMM erneut.


Überprüfen Sie, dass die Fingerabdrücke der x. 509-Zertifikate (SouthBound) die Kommunikation zwischen dem Hyper-V-Host (NC-Host-Agent-Dienst) und Netzwerk-Controller-Knoten durch den Hyper-V-Host (Hostname ist Antragstellername des Zertifikats) zum identisch sind. Außerdem überprüfen Sie, ob die Netzwerkcontroller REST Zertifikat Name des Antragstellers *CN =<FQDN or IP>*.

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

Sie können auch überprüfen, die folgenden Parameter des jedes Zertifikats, um sicherzustellen, dass der Name des Antragstellers ist erwartet (Hostname oder NC-REST-FQDN oder IP), das Zertifikat noch nicht abgelaufen, und alle Zertifizierungsstellen in der Zertifikatkette in der vertrauenswürdigen Stammzertifizierungsstelle enthalten sind.

- Antragstellername  
- Ablaufdatum  
- Stammzertifizierungsstelle vertrauen  

*Wiederherstellung* Wenn mehrere Zertifikate auf dem Hyper-V-Host den gleichen Antragstellernamen aufweisen, der Agent-Host-Controller wird nach dem Zufallsprinzip auswählen, für die Darstellung für die Netzwerk-Controller. Dies kann den Fingerabdruck des Server-Ressource, die bekanntermaßen Netzwerkcontroller nicht überein. In diesem Fall löschen Sie eines der Zertifikate mit den gleichen Antragstellernamen auf dem Hyper-V-Host, und starten Sie den Netzwerk-Controller-Host-Agent-Dienst neu. Wenn weiterhin keine Verbindung hergestellt werden kann, löschen Sie das andere Zertifikat mit den gleichen Antragstellernamen auf dem Hyper-V-Host, und löschen Sie die entsprechenden Server-Ressource in VMM. Anschließend erstellen Sie die Server-Ressource in VMM ein neues x. 509-Zertifikat zu generieren und installieren Sie es auf dem Hyper-V-Host neu.
  

#### <a name="check-the-slb-configuration-state"></a>Überprüfen Sie den Status der SLB-Konfiguration
Der Konfigurationsstatus SLB kann als Teil der Ausgabe an das Cmdlet Debug-NetworkController ermittelt werden. Dieses Cmdlet wird auch die aktuellen Satz von Netzwerkcontroller Ressourcen in JSON-Dateien, die alle IP-Konfigurationen von jedem Hyper-V-Host (Server) und lokalen Netzwerk Datenbanktabellen Host-Agent-Richtlinie ausgegeben. 

Standardmäßig werden zusätzliche ablaufverfolgungen gesammelt. Fügen Sie zum Sammeln von ablaufverfolgungen nicht - IncludeTraces: $false-Parameter.

```none
Debug-NetworkController -NetworkController <FQDN or IP> [-Credential <PS Credential>] [-IncludeTraces:$false]

# Don't collect traces
$cred = Get-Credential 
Debug-NetworkController -NetworkController 10.127.132.211 -Credential $cred -IncludeTraces:$false

Transcript started, output file is C:\\NCDiagnostics.log
Collecting Diagnostics data from NC Nodes
```

>[!NOTE]
>Der Standardspeicherort für die Ausgabe wird das < Working_directory > \NCDiagnostics\-Verzeichnis sein. Das Standardverzeichnis für die Ausgabe kann geändert werden, mithilfe der `-OutputDirectory`Parameter. 

Die Zustandsinformationen des SLB-Konfiguration finden Sie der _Diagnose-slbstateResults.Json_ Datei in diesem Verzeichnis.

Dieser JSON-Datei kann in die folgenden Abschnitte unterteilt werden:
 * Fabric
   * SlbmVips – in diesem Abschnittlistet die IP-Adresse der SLB Manager VIP-Adresse der von dem Netzwerkcontroller Coodinate Konfiguration und der Integrität zwischen den SLB Muxes und SLB-Host-Agents verwendet wird.
   * MuxState – in diesem AbschnittListe einen Wert für die einzelnen SLB Mux bereitgestellt erteilen den Status der mux
   * Routerkonfiguration – in diesem Abschnittwerden die Upstream Router (BGP-Peer) aufgelistet Autonomous System Number (ASN), während der Übertragung IP-Adresse und -ID. Es werden auch die SLB Muxes ASN und während der Übertragung IP aufgelistet.
   * Host-Informationen – in diesem Abschnittverbunden wird Liste der Management-IP-Adresse alle Hyper-V-Hosts für Arbeitslasten mit Lastenausgleich ausführen.
   * VIP-Bereiche – in diesem Abschnittwerden die öffentlichen und privaten VIP-IP-Pool-Adressbereiche angezeigt. Die SLBM VIP-Adresse wird als eine zugewiesene IP-Adresse von einem dieser Bereiche enthalten sein. 
   * Routen MUX - werden in diesem Abschnitteinen Wert für die einzelnen SLB Mux bereitgestellt, die alle für die Routenankündigungen für dieses bestimmte Mux aufgelistet.
 * Mandanten
   * VipConsolidatedState - in diesem Abschnittwerden den Status der Konnektivität für jeden Mandanten VIP einschließlich angekündigte Routenpräfix, Hyper-V-Host und DIP-Endpunkte aufgeführt.
    
> [!NOTE]
> SLB Zustand ermittelt werden können, direkt mithilfe der [DumpSlbRestState](https://github.com/Microsoft/SDN/blob/master/Diagnostics/DumpSlbRestState.ps1) Skript auf den [Microsoft-SDN-GitHub-Repository](https://github.com/microsoft/sdn). 

#### <a name="gateway-validation"></a>Gateway-Überprüfung

**Aus Netzwerkcontroller:**
```
Get-NetworkControllerLogicalNetwork
Get-NetworkControllerPublicIPAddress
Get-NetworkControllerGatewayPool
Get-NetworkControllerGateway
Get-NetworkControllerVirtualGateway
Get-NetworkControllerNetworkInterface
```

**Von VM-Gateway:**
```
Ipconfig /allcompartments /all
Get-NetRoute -IncludeAllCompartments -AddressFamily
Get-NetBgpRouter
Get-NetBgpRouter | Get-BgpPeer
Get-NetBgpRouter | Get-BgpRouteInformation
```

**Von der Oberkante des Switch Rack (ToR):**

`sh ip bgp summary (for 3rd party BGP Routers)`

**Windows-BGP-Router**
```
Get-BgpRouter
Get-BgpPeer
Get-BgpRouteInformation
```

Zusätzlich zu diesen aus den Problemen, die bisher (Dies gilt besonders für SDNExpress-basierte Bereitstellungen) gesehen haben scheint die häufigste Ursache für Mandanten erste nicht auf virtuellen Computern GW konfiguriert werden, die Kapazität GW in FabricConfig.psd1 handelt es sich, dass weniger im Vergleich zu Was Personen versuchen, Zuweisen von Netzwerkverbindungen (S2S-Tunnels) im TenantConfig.psd1. Dies kann einfach durch einen Vergleich der Ausgaben eines der folgenden Befehle überprüft werden:

```
PS > (Get-NetworkControllerGatewayPool -ConnectionUri $uri).properties.Capacity
PS > (Get-NetworkControllerVirtualgatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "TenantName").properties.OutboundKiloBitsPerSecond
PS > (Get-NetworkControllerVirtualgatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "TenantName").property
```

### <a name="hoster-validate-data-plane"></a>[Hoster] Überprüfen der Datenschicht
Nach dem Netzwerkcontroller bereitgestellt wurde, virtuellen mandantennetzwerken und Subnetze erstellt wurden, und VMs die virtuellen Subnetze zugeordnet wurde haben, können vom Hostinganbieter Mandanten Verbindung überprüft zusätzlicher Fabric-Level-Tests ausgeführt werden.

#### <a name="check-hnv-provider-logical-network-connectivity"></a>Überprüfen Sie die Hyper-v-Anbieter logisches Netzwerk-Konnektivität
Nach der ersten Gast, virtueller Computer auf einem Hyper-V-Host mit einem virtuellen mandantennetzwerk verbunden wurde, werden die Netzwerkcontroller Hyper-V-Hosts zwei Hyper-v-Anbieter-IP-Adressen (PA-IP-Adressen) zuweisen. Diese IP-Adressen stammen vom IP-Pool im Hyper-v-Anbieter logischen Netzwerks und vom Netzwerkcontroller verwaltet werden.  Um herauszufinden, was diese zwei Hyper-v-IP-Adressen sind die

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

Diese Hyper-v-Anbieter-IP-Adressen (PA-IPs) erstellt in einem separaten TCP/IP-Netzwerk-Fach Ethernet-Adapter zugewiesen sind und einen Adapter Namen _VLANX_, wobei X das VLAN auf das logische Netzwerk von Hyper-v-Anbieter (Transport) zugewiesen ist.

Konnektivität zwischen zwei Hyper-V-Hosts mithilfe des Hyper-v-Anbieters logisches Netzwerk, durch einen Ping mit einer zusätzlichen Depot möglich ist (-c Y) Parameter, wobei Y ist die TCP/IP-netzwerkdepot in der die PAhostVNICs erstellt werden. Diese Depot kann dazu bestimmt werden:

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
> Die PA-Host-vNIC-Adapter werden nicht in der Datenpfad verwendet und daher keine IP-Adresse "vEthernet (PAhostVNic) Adapter" zugewiesen.

Beispielsweise wird davon ausgegangen Sie, dass Hyper-V-Host 1 und 2 IP-Adressen der Hyper-v-Anbieter (PA) verfügen:

|Hyper-V-Host –|-PA IP-Adresse 1|-PA IP-Adresse 2|
|---             |---            |---             |
|Host 1 | 10.10.182.64 | 10.10.182.65 |
|Host 2 | 10.10.182.66 | 10.10.182.67 |

Wir können zwischen den beiden mit dem folgenden Befehl so überprüfen Sie die logische Netzwerkkonnektivität Hyper-v-Anbieter ping.

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

*Wiederherstellung* Wenn Hyper-v-Anbieter-Ping nicht funktioniert, überprüfen Sie die physischen Netzwerk-Konnektivität, einschließlich der VLAN-Konfiguration. Die physischen Netzwerkkarten auf jedem Hyper-V-Host sollte im trunkmodus keine spezifischen VLAN zugewiesen sein. Die Management-Host-vNIC sollte das Management logische Netzwerk VLAN isoliert werden.

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
 
#### <a name="check-mtu-and-jumbo-frame-support-on-hnv-provider-logical-network"></a>Überprüfen Sie die MTU und Jumbo-Frame-Unterstützung in Hyper-v-Anbieter logischen Netzwerk

Ein weiteres gängiges Problem im logischen Netzwerk Hyper-v-Anbieter ist, dass das physische Netzwerk-Ports bzw. Ethernet-Karte keine große genug MTU konfiguriert, dass der Aufwand für die Kapselung von VXLAN (oder NVGRE) behandeln. 
>[!NOTE]
> Einige Ethernet-Karten und Treiber unterstützen die neue * EncapOverhead-Schlüsselwort, das von der Controller-Host-Agent auf einen Wert von 160 automatisch festgelegt wird. Dieser Wert wird auf den Wert des hinzugefügt werden die * JumboPacket-Schlüsselwort, deren Inhalt als die angekündigte MTU verwendet wird.
> z.B. * EncapOverhead = 160 und * JumboPacket = 1514 = > MTU = 1674B

```none
# Check whether or not your Ethernet card and driver support *EncapOverhead
PS C:\ > Test-EncapOverheadSettings

Verifying Physical Nic : <NIC> Ethernet Adapter #2
Physical Nic  <NIC> Ethernet Adapter #2 can support SDN traffic. Encapoverhead value set on the nic is  160
Verifying Physical Nic : <NIC> Ethernet Adapter
Physical Nic  <NIC> Ethernet Adapter can support SDN traffic. Encapoverhead value set on the nic is  160
```

Um zu testen, und zwar unabhängig davon, ob das logische Netzwerk von Hyper-v-Anbieter der größere MTU Größe End-to-End unterstützt, verwenden Sie die _Test-LogicalNetworkSupportsJumboPacket_ Cmdlet:
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
* Passen Sie die MTU-Größe auf den physischen Switchports mindestens 1674B (einschließlich 14 b Ethernet-Header und Trailer)
* Wenn die Netzwerkkarte nicht das Schlüsselwort EncapOverhead unterstützt wird, passen Sie das Schlüsselwort JumboPacket um mindestens 1674B


#### <a name="check-tenant-vm-nic-connectivity"></a>Überprüfen Sie die Mandanten-VM-NIC-Verbindung
Jede VM-NIC einem Gast-VM hat eine CA-PA-Zuordnung zwischen der privaten Kundenadressraum (CA) und den Hyper-v-Anbieter Adresse (PA) Speicherplatz. Diese Zuordnungen werden in den Tabellen OVSDB Server, auf jedem Hyper-V-Host gespeichert und können durch Ausführen des folgenden Cmdlets gefunden werden.

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
> Wenn die CA-PA-Zuordnungen, die Sie erwarten, dass für einen bestimmten Mandanten VM nicht ausgegeben werden, überprüfen Sie die VM-NIC und IP-Konfiguration Ressourcen auf dem Netzwerkcontroller mit der _Get-NetworkControllerNetworkInterface_ Cmdlet. Überprüfen Sie auch die hergestellte Verbindungen zwischen den Knoten NC-Host-Agent und dem Netzwerkcontroller.

Mit diesen Informationen können ein Mandanten VM-Ping kann jetzt ausgelöst werden, indem der Hoster aus dem Netzwerkcontroller mithilfe der _Test-VirtualNetworkConnection_ Cmdlet.

## <a name="specific-troubleshooting-scenarios"></a>Bestimmte Problembehandlung Szenarien

Die folgenden Abschnitte enthalten Richtlinien für die Problembehandlung für bestimmte Szenarien.

### <a name="no-network-connectivity-between-two-tenant-virtual-machines"></a>Keine Netzwerkkonnektivität zwischen zwei virtuellen mandantencomputer

1.  [Mandanten] Stellen Sie sicher, dass Windows-Firewall in virtuellen mandantencomputer Datenverkehr nicht blockiert wird.  
2.  [Mandanten] Überprüfen Sie, dass die IP-Adressen durch Ausführen der Mandant virtuellen Maschine zugewiesen wurden _Ipconfig_. 
3.  [Hoster] Führen Sie **Test-VirtualNetworkConnection** vom Hyper-V-Host an die Verbindung zwischen den zwei virtuellen mandantencomputern betreffenden überprüfen. 

>[!NOTE]
>Die VSID bezieht sich auf das virtuelle Subnetz-ID an. Im Fall von VXLAN ist dies der VXLAN Netzwerk-ID (VNI7D). Sie können diesen Wert erhalten Sie durch Ausführen der **Get-PACAMapping** Cmdlet.

#### <a name="example"></a>Beispiel

    $password = ConvertTo-SecureString -String "password" -AsPlainText -Force
    $cred = New-Object pscredential -ArgumentList (".\administrator", $password) 

Erstellen Sie CA-Ping zwischen "Grüne Web VM 1" mit SenderCA IP des 192.168.1.4 auf den Hosts "sa18n30-2.sa18.nttest.microsoft.com" Mgmt IP des 10.127.132.153 ListenerCA IP des 192.168.1.5 sowohl auf VSID (Virtual Subnet) 4114 angefügt.

    Test-VirtualNetworkConnection -OperationId 27 -HostName sa18n30-2.sa18.nttest.microsoft.com -MgmtIp 10.127.132.153 -Creds $cred -VMName "Green Web VM 1" -VMNetworkAdapterName "Green Web VM 1" -SenderCAIP 192.168.1.4 -SenderVSID 4114 -ListenerCAIP 192.168.1.5 -ListenerVSID 4114

    Test-VirtualNetworkConnection at command pipeline position 1

Kundenadressraum Ping-Test Starten von Adresse 192.168.1.4 Rtt erfolgreich starten Ablaufverfolgungssitzung Ping zu 192.168.1.5 = 0 ms


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

4.  [Mandanten] Überprüfen Sie, dass es keine verteilten Firewall-Richtlinien auf dem virtuellen Subnetz oder VM-Netzwerkschnittstellen, die Datenverkehr blockieren würde angegeben ist.    

Abfragen der REST-API von Netzwerkcontroller in Demo-Umgebung zu sa18n30nc in der Domäne sa18.nttest.microsoft.com gefunden.

    $uri = "https://sa18n30nc.sa18.nttest.microsoft.com"
    Get-NetworkControllerAccessControlList -ConnectionUri $uri 

# <a name="look-at-ip-configuration-and-virtual-subnets-which-are-referencing-this-acl"></a>Sehen Sie sich die IP-Konfiguration und virtuelle Subnetze, die diese ACL verweisen

1. [Hoster] Führen Sie ``Get-ProviderAddress``auf beiden Hyper-V-Hosts, die beiden hostet Mandanten virtuelle Maschinen in Frage, und führen Sie dann ``Test-LogicalNetworkConnection``oder ``ping -c <compartment>``vom Hyper-V-Host zur Überprüfung der Verbindung auf das logische Netzwerk von Hyper-v-Anbieter
2.  [Hoster] Stellen Sie sicher, dass die MTU-Einstellungen korrekt auf den Hyper-V-Hosts und alle Layer-2-Wechsel Geräte zwischen Hyper-V-Hosts sind. Führen Sie ``Test-EncapOverheadValue``auf allen Hyper-V-Hosts, die betreffenden. Auch überprüfen, ob alle Layer-2-Switches in zwischen MTU auf mindestens 1674 Bytes festgelegt werden, um maximale Auslastung von 160 Bytes zu berücksichtigen.  
3.  [Hoster] Wenn keine PA-IP-Adressen vorhanden sind bzw. CA-Verbindung getrennt wird, stellen Sie sicher, dass die Netzwerkrichtlinie empfangen wurde. Führen Sie ``Get-PACAMapping``um festzustellen, ob die Kapselung Regeln und die CA-PA-Zuordnungen, die für die Erstellung von virtuellen Netzwerken Overlay erforderlichen ordnungsgemäß eingerichtet werden.  
4.  [Hoster] Überprüfen Sie, dass der Agent-Host-Controller den Netzwerk-Controller angeschlossen ist. Führen Sie ``netstat -anp tcp |findstr 6640``feststellen, ob die   
5.  [Hoster] Überprüfung, die der Host in HKLM-ID / Server-Ressourcen, die Mandanten-VMs hostet die Instanz-ID entspricht.  
6. [Hoster] Überprüfen Sie, dass der Port-Profil-ID die Instanz-ID für die VM-Netzwerkschnittstellen von den virtuellen mandantencomputern entspricht.  

## <a name="logging-tracing-and-advanced-diagnostics"></a>Protokollierung, Verfolgung und erweiterte Diagnose

Die folgenden Abschnitte enthalten Informationen für erweiterte Diagnose, Protokollierung und Ablaufverfolgung.

### <a name="network-controller-centralized-logging"></a>Netzwerkcontroller zentralisierte Protokollierung 
 
Netzwerkcontroller können automatisch Debugger Protokolle erfassen und an einem zentralen Ort aufbewahren. Protokollsammlung kann aktiviert werden, wenn beim Netzwerkcontroller für den ersten oder jederzeit später bereitstellen. Die Protokolle von Netzwerkcontroller gesammelt werden und Netzwerk-Elemente, die von Netzwerkcontroller verwaltet werden: Computer, Software Load Balancers (SLB) und Gatewaycomputer hosten. 

Diese Protokolle enthalten Debugprotokolle für Cluster Netzwerkcontroller, die Anwendung Netzwerkcontroller, Gateway-Protokolle, SLB, virtuelle Netzwerke und verteilten Firewall. Netzwerkcontroller einen neuen Host/SLB /-Gateways hinzugefügt wird, wird die Protokollierung auf diesen Computern gestartet. Wenn ein Host/SLB /-Gateways aus Netzwerkcontroller entfernt wird, wird die Protokollierung auf diesen Computern beendet.

#### <a name="enable-logging"></a>Aktivieren der Protokollierung

Protokollierung ist automatisch aktiviert, wenn Sie die Netzwerk-Controller-Cluster mit Installieren der **Installation NetworkControllerCluster** Cmdlet. Standardmäßig werden die Protokolle auf den Knoten Netzwerkcontroller lokal gesammelt *%systemdrive%\SDNDiagnostics*. Es ist **empfohlen**, dass Sie diesen Speicherort zu einer Remotedateifreigabe (keine lokalen) ändern. 

Die Netzwerk-Controller-Cluster-Protokolle gespeichert werden *%programData%\Windows Fabric\log\Traces*. Sie können angeben, einen zentralen Ort zum Protokollsammlung mit der **DiagnosticLogLocation** Parameter der Empfehlung, die in diesem wird einer Remotedateifreigabe werden. 

Wenn Sie den Zugriff auf diesen Speicherort beschränken möchten, können Sie die Anmeldeinformationen für den Zugriff mit Bereitstellen der **LogLocationCredential** Parameter. Wenn Sie die Anmeldeinformationen für den Zugriff auf den Ort des Protokolls bereitstellen, sollten Sie auch Bereitstellen der **CredentialEncryptionCertificate** -Parameter, der zum Verschlüsseln der lokal auf den Knoten Netzwerkcontroller gespeicherten Anmeldeinformationen verwendet wird.  

Mit den Standardeinstellungen wird empfohlen, dass Sie mindestens 75GB freier Speicherplatz in den zentralen Standort und 25GB auf den lokalen Knoten verfügen (wenn keinem zentralen Ort) für einen Cluster mit 3 Knoten Netzwerkcontroller.

#### <a name="change-logging-settings"></a>Ändern der protokollierungseinstellungen

Sie können ändern, protokollierungseinstellungen jederzeit mit den ``Set-NetworkControllerDiagnostic``Cmdlet. Die folgenden Einstellungen können geändert werden:

- **Ort des Protokolls zentralisierte**.  Sie können den Speicherort zum Speichern der Protokolle mit Ändern der ``DiagnosticLogLocation``Parameter.  
- **Anmeldeinformationen Protokoll Ortung**.  Sie können ändern, die Anmeldeinformationen für den Ort des Protokolls, mit den Zugriff auf die ``LogLocationCredential``Parameter.  
- **Wechseln Sie zum lokalen Anmelden**.  Wenn Sie einen zentralen Ort zum Speichern von Protokollen angegeben haben, können Sie zurück zu wechseln lokal anmelden, auf den Knoten "Netzwerkcontroller" mit der ``UseLocalLogLocation``Parameter (aufgrund der großen Speicherplatzbedarf nicht empfohlen).  
- **Protokollierung Bereich**.  Standardmäßig werden alle Protokolle gesammelt. Sie können den Bereich, um nur Netzwerkcontroller Clusterprotokolle erfasst ändern.  
- **Protokollierungsstufe**.  Die standardmäßige Protokollierungsebene ist "Information". Sie können es in Fehler-, Warn- oder Verbose ändern.  
- **Protokolldatei Alterung Zeit**.  Die Protokolle werden in Round gespeichert. 3Tage der Protokollierung von Daten müssen in der Standardeinstellung, ob Sie lokale Anmeldung oder die zentralisierte Protokollierung verwenden. Sie können diese Frist mit ändern **LogTimeLimitInDays** Parameter.  
- **Protokolldatei Alterung Größe**.  Standardmäßig müssen Sie eine maximale 75GB protokollierter Daten, wenn zentralisierte Protokollierung und 25GB verwenden, wenn lokale Anmeldung zu verwenden. Sie können ändern, bei der **LogSizeLimitInMBs** Parameter.

#### <a name="collecting-logs-and-traces"></a>Sammlung von Protokollen und Ablaufverfolgungen

VMM-Bereitstellungen verwenden die zentralisierte Protokollierung für den Netzwerkcontroller standardmäßig. Ort der Dateifreigabe für diese Protokolle wird angegeben, wenn Sie die Dienstvorlage Netzwerkcontroller bereitstellen.

Wenn ein Speicherort nicht angegeben wird, lokale wird Protokollierung auf jedem Knoten Netzwerkcontroller mit Protokolle gespeichert werden, C:\Windows\tracing\SDNDiagnostics verwendet werden. Diese Protokolle werden mithilfe der folgenden Hierarchie gespeichert:

- CrashDumps
- NCApplicationCrashDumps
- NCApplicationLogs
- PerfCounters
- SDNDiagnostics
- Ablaufverfolgungen

Netzwerkcontroller verwendet die Service Fabric (Azure). Service Fabric-Protokolle können erforderlich sein, bei der Problembehandlung für bestimmte Probleme. Diese Protokolle können auf jedem Knoten Netzwerkcontroller C:\ProgramData\Microsoft\Service Fabric gefunden werden.

Wenn ein Benutzer ausgeführt wurde die _Debug-NetworkController_ -Cmdlet, zusätzliche Protokolle werden auf jedem Hyper-V-Host, der mit einer Ressource in den Netzwerkcontroller angegeben wurde. Diese Protokolle (und ablaufverfolgungen Wenn aktiviert) werden unter C:\NCDiagnostics beibehalten.

### <a name="slb-diagnostics"></a>SLB-Diagnose

#### <a name="slbm-fabric-errors-hosting-service-provider-actions"></a>SLBM Fabric-Fehler (Hosting Service Provider Aktionen)

1.  Überprüfen Sie, dass Software Load Balancer Manager (SLBM) funktioniert und dass die Orchestrierung Ebenen miteinander kommunizieren können: SLBM -> SLB Mux und SLBM -> SLB-Host-Agents. Führen Sie [DumpSlbRestState](https://github.com/Microsoft/SDN/blob/master/Diagnostics/DumpSlbRestState.ps1) aus einem beliebigen Knoten mit Zugriff auf Netzwerk-Controller-REST-Endpunkt.  
2.  Überprüfen der *SDNSLBMPerfCounters* im Systemmonitor auf einem der Knoten Netzwerkcontroller VMs (vorzugsweise primärer Netzwerkcontroller Knoten - Get-NetworkControllerReplica):
    1.  Werden Load Balancer (LB)-Modul ist mit SLBM verbunden? (*SLBM LBEngine Konfigurationen insgesamt* > 0)  
    2.  Weiß SLBM mindestens über einen eigenen Endpunkte? (*VIP-Endpunkte insgesamt* > = 2)  
    3.  Werden Hyper-V (DIP) Hosts sind mit SLBM verbunden? (*HP verbundenen Clients* == Num-Server)   
    4.  Werden SLBM ist mit Muxes verbunden? (*Muxes verbunden* == *Muxes fehlerfrei auf SLBM* == *Muxes reporting fehlerfrei* = # SLB Muxes VMs).  
3.  Stellen Sie sicher, dass der BGP-Router konfiguriert erfolgreich mit den SLB MUX-Peering wird  
    1.  Bei Verwendung von RRAS mit dem Remotezugriff (d.h. BGP virtueller Computer):  
        1.  Get-BgpPeer sollte verbundenen angezeigt.  
        2.  Get-BgpRouteInformation sollte mindestens eine Route angezeigt, für die SLBM selbst VIP  
    2.  Wenn mithilfe von physischen Top-of-Rack (ToR) als BGP-Peer wechseln, finden Sie in der Dokumentation  
        1.  Beispiel: # Bgp-Instanz anzeigen  
4.  Überprüfen der *SlbMuxPerfCounters* und *SLBMUX* Leistungsindikatoren im Systemmonitor auf die SLB Mux-VM
5.  Überprüfen Sie Konfigurationsstatus und VIP-Bereiche in Software Load Balancer-Manager-Ressourcen  
    1.  Get-NetworkControllerLoadBalancerConfiguration - ConnectionUri < https://<FQDN or IP>| ConvertTo-Json-Tiefe 8 (VIP-Bereiche in IP-Adresspools überprüfen und SLBM Self-VIP-Adresse sicherstellen (*LoadBalanacerManagerIPAddress*) und alle mandantenseitige VIPs befinden sich in diesen Bereichen)  
        1. Get-NetworkControllerIpPool - NetworkId "< öffentlichem/privatem VIP logischen Netzwerk Ressourcen-ID >" - Subnetzkennung "< öffentlichem/privatem VIP logischen Subnetz Ressourcen-ID >" - ResourceId "<IP Pool Resource Id>" - ConnectionUri $uri | Convertto-Json-Tiefe 8 
    2.  Debug-NetworkControllerConfigurationState-  

Ggf. der Überprüfungen über Fehler auftreten, werden der Mandant SLB Zustand auch in einem Fehlermodus.  

**Wiederherstellung**   
Basierend auf den folgenden Diagnoseinformationen angezeigt, beheben Sie die folgenden:  
* Stellen Sie sicher, dass SLB Multiplexers verbunden sind  
  * Beheben Sie Zertifikatprobleme  
  * Beheben von Netzwerkverbindungsproblemen  
* Stellen Sie sicher, dass BGP-Peers Informationen erfolgreich konfiguriert ist  
* Stellen Sie sicher, Host-ID in der Registrierung Server-Instanz-ID in Server-Ressource entspricht (Anhangverweisen *HostNotConnected* Fehlercode:)  
* Sammeln von Protokollen  

#### <a name="slbm-tenant-errors-hosting-service-provider--and-tenant-actions"></a>SLBM Mandanten-Fehler (Hosting Service-Anbieter und Mandanten Aktionen)

1.  [Hoster] Überprüfen Sie *Debug-NetworkControllerConfigurationState* um festzustellen, ob die Ressourcen des Systems zum Lastenausgleich in ein Fehler aufgetreten sind. Versuchen Sie anhand der Aufgaben im Anhangzu verringern.   
    1.  Überprüfen Sie, ob ein VIP-Endpunkt vorhanden und Werbung Routen  
    2.  Überprüfen Sie, wie viele DIP-Endpunkte für den VIP-Endpunkt ermittelt wurden  
2.  [Mandanten] Überprüfen Sie Load Balancer Ressourcen sind ordnungsgemäß angegeben.  
    1.  Überprüfen Sie die DIP Endpunkte, an denen in SLBM registrierte hosten Mandanten-VMs, die die LoadBalancer Back-End-Pool IP-Adresskonfiguration entsprechen  
3.  [Hoster] Wenn die DIP-Endpunkten nicht erkannt oder verbunden werden:   
    1.  Überprüfen Sie *Debug-NetworkControllerConfigurationState*  
        1.  Überprüfen Sie die NC und SLB Host-Agent wird erfolgreich mit dem Netzwerk Controller Ereignis Coordinator verbunden ``netstat -anp tcp |findstr 6640)``  
    2.  Überprüfen Sie *HostId* in *Nchostagent* Service Regkey (Referenz *HostNotConnected* Fehlercode im Anhang) die entsprechenden Server-Ressource Instanz-ID entspricht (``Get-NCServer |convertto-json -depth 8``)  
    3.  Überprüfen Sie, dass Port Profil-ID für die virtuelle Maschine Port entsprechenden NIC Ressource des virtuellen Computers die Instanz-ID entspricht   
4.  [Hosting-Anbieter] Sammeln von Protokollen   

#### <a name="slb-mux-tracing"></a>SLB Mux-Ablaufverfolgung

Informationen über die Software Load Balancer Muxes kann auch über die Ereignisanzeige ermittelt werden. 
1. Klicken Sie auf "Anzeigen analytische und Debugprotokolle" im Menü Ereignisansicht Viewer
2. Navigieren Sie zu "Anwendungs- und Dienstprotokolle" > Microsoft > Windows > SlbMuxDriver > Ablaufverfolgungsinformationen in der Ereignisanzeige 
3. Klicken Sie mit der rechten Maustaste darauf und wählen Sie "Protokoll aktivieren"

>[!NOTE]
>Es wird empfohlen, dass nur eine dieser Protokollierung aktiviert für kurze Zeit, während Sie versuchen, ein Problem zu reproduzieren.

### <a name="vfp-and-vswitch-tracing"></a>VFP und vSwitch verfolgen

Von jedem Hyper-V-Host die Gast-VM mit einem virtuellen mandantennetzwerk verbunden gehostet wird, können Sie eine VFP-Ablaufverfolgung zu ermitteln, wo die Probleme liegen können gesammelt.

```
netsh trace start provider=Microsoft-Windows-Hyper-V-VfpExt overwrite=yes tracefile=vfp.etl report=disable provider=Microsoft-Windows-Hyper-V-VmSwitch 
netsh trace stop
netsh trace convert .\vfp.etl ov=yes 
```
