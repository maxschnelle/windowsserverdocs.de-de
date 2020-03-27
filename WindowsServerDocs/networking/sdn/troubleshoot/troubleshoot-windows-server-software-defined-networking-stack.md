---
title: Problembehandlung für die Windows Server-Software Defined Networking-Stapel
description: In diesem Windows Server-Handbuch werden die allgemeinen Sdn (Software Defined Networking)-Fehler und-Fehler Szenarios untersucht, und es wird ein Problem Behandlungs Workflow mit den verfügbaren Diagnosetools beschrieben.
manager: ravirao
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 9be83ed2-9e62-49e8-88e7-f52d3449aac5
ms.author: lizross
author: JMesser81
ms.date: 08/14/2018
ms.openlocfilehash: 5827ad3b23d6f084e0138bf34ad47223eccb4e76
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312846"
---
# <a name="troubleshoot-the-windows-server-software-defined-networking-stack"></a>Problembehandlung für die Windows Server-Software Defined Networking-Stapel

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In dieser Anleitung werden allgemeine Sdn (Software Defined Networking)-Fehler und-Fehler Szenarios untersucht, und es wird ein Problem Behandlungs Workflow beschrieben, der die verfügbaren Diagnosetools nutzt.  

Weitere Informationen zu Software-Defined Networking von Microsoft finden Sie unter [Software Defined Networking (Software-Defined Networking](../../sdn/Software-Defined-Networking--SDN-.md)).  

## <a name="error-types"></a>Fehlertypen  
In der folgenden Liste sind Probleme aufgeführt, die am häufigsten mit der Hyper-V-Netzwerkvirtualisierung (HNVv1) in Windows Server 2012 R2 von in-Market-Produktions Bereitstellungen erkannt werden und in vielerlei Hinsicht mit denselben Typen von Problemen in Windows Server 2016 auftreten. HNVv2 mit dem neuen Sdn-Stapel (Software Defined Network).  

Die meisten Fehler können zu einer kleinen Gruppe von Klassen klassifiziert werden:   
* **Ungültige oder nicht unterstützte Konfiguration**  
   Ein Benutzer ruft die Northbound-API falsch oder mit ungültiger Richtlinie auf.   

* **Fehler in Richtlinien Anwendung**  
     Die Richtlinie vom Netzwerk Controller wurde nicht an einen Hyper-v-Host übermittelt, die auf allen Hyper-v-Hosts (z. b. nach einer Livemigration) erheblich verzögert und/oder nicht auf dem neuesten Stand ist.  
* **Konfigurations Abweichung oder Softwarefehler**  
  Daten Pfad Probleme, die zu gelöschten Paketen führen.  

* **Externer Fehler im Zusammenhang mit NIC-Hardware/-Treibern oder der zugrunde liegenden netzwerkfabric**  
  Falsch konfigurierte Aufgaben Abladungen (z. b. VMQ) oder falsch konfigurierte netzwerkfabric (z. b. MTU)   

  In diesem Handbuch zur Problembehandlung werden die einzelnen Fehlerkategorien untersucht, und es werden bewährte Methoden und Diagnosetools empfohlen, um den Fehler zu identifizieren und zu beheben.  

## <a name="diagnostic-tools"></a>Diagnosetools  

Vor der Erörterung der Problem Behandlungs Workflows für die einzelnen Fehlertypen betrachten wir die verfügbaren Diagnosetools.   

Um die Diagnosetools für den Netzwerk Controller (Steuerungs Pfad) zu verwenden, müssen Sie zunächst das Feature RSAT-networkcontroller installieren und das ``NetworkControllerDiagnostics`` Modul importieren:  

```  
Add-WindowsFeature RSAT-NetworkController -IncludeManagementTools  
Import-Module NetworkControllerDiagnostics  
```  

Um die Tools für die HNV-Diagnose (Datenpfad) zu verwenden, müssen Sie das ``HNVDiagnostics`` Modul importieren:

```  
# Assumes RSAT-NetworkController feature has already been installed
Import-Module hnvdiagnostics   
```  

### <a name="network-controller-diagnostics"></a>Netzwerk Controller Diagnose  
Diese Cmdlets sind auf TechNet im [Thema Network Controller Diagnostics Cmdlet](https://docs.microsoft.com/powershell/module/networkcontrollerdiagnostics/)dokumentiert. Sie helfen bei der Identifizierung von Problemen mit der Netzwerk Richtlinien Konsistenz im Steuerungs Pfad zwischen den Netzwerk Controller Knoten und zwischen dem Netzwerk Controller und den NC-Host-Agents, die auf den Hyper-V-Hosts ausgeführt werden.

 Die Cmdlets _Debug-servicefabricnodestatus_ und _Get-networkcontrollerreplica_ müssen von einem der virtuellen Computer mit dem Netzwerk Controller Knoten ausgeführt werden. Alle anderen NC-Diagnose-Cmdlets können von jedem Host ausgeführt werden, der über eine Verbindung mit dem Netzwerk Controller verfügt und sich entweder in der Netzwerk Controller-Verwaltungs Sicherheitsgruppe (Kerberos) befindet oder über Zugriff auf das X. 509-Zertifikat zum Verwalten des Netzwerk Controllers verfügt. 

### <a name="hyper-v-host-diagnostics"></a>Hyper-V-Host Diagnose  
Diese Cmdlets sind auf TechNet im Thema zum [Hyper-v-netzwerkvirtualisierungsdiagnose-Cmdlet (HNV)](https://docs.microsoft.com/powershell/module/hnvdiagnostics/)dokumentiert. Sie helfen bei der Identifizierung von Problemen im Daten Pfad zwischen virtuellen Mandanten Computern (Ost/West) und dem eingehenden Datenverkehr über eine SLB-VIP (Nord/Süd). 

Die Befehle _Debug-virtualmachinequeueoperation_, _Get-customerroute_, _Get-pacamapping_, _Get-provideraddress_, _Get-vmnetworkadapterportid_, _Get-vmswitchexternalportid_und _Test-eincapoverheadsettings_ sind alle lokalen Tests, die von jedem Hyper-V-Host ausgeführt werden können. Die anderen Cmdlets rufen Daten Pfad Tests über den Netzwerk Controller auf und benötigen daher Zugriff auf den Netzwerk Controller, wie oben beschrieben.

### <a name="github"></a>GitHub
Das [GitHub-Repository für Microsoft/Sdn](https://github.com/microsoft/sdn) enthält eine Reihe von Beispiel Skripts und-Workflows, die zusätzlich zu diesen Cmdlets erstellt werden. Vor allem können Sie Diagnose Skripts im [Diagnose](https://github.com/Microsoft/sdn/diagnostics) Ordner finden. Helfen Sie uns, durch die Übermittlung von Pull Requests an diesen Skripts mitzuwirken.

## <a name="troubleshooting-workflows-and-guides"></a>Problembehandlung bei Workflows und Führungslinien  

### <a name="hoster-validate-system-health"></a>Hoster System Integrität überprüfen
Es gibt eine eingebettete Ressource namens " _Configuration State_ " in mehreren der Netzwerk Controller Ressourcen. Der Konfigurations Status enthält Informationen zur Systemintegrität, einschließlich der Konsistenz zwischen der Konfiguration des Netzwerk Controllers und dem tatsächlichen (laufenden) Status auf den Hyper-V-Hosts. 

Um den Konfigurations Status zu überprüfen, führen Sie auf jedem Hyper-V-Host mit Verbindung mit dem Netzwerk Controller Folgendes aus.

>[!NOTE] 
>Der Wert für den *networkcontroller* -Parameter muss entweder der FQDN oder die IP-Adresse sein, die auf dem Antragsteller Namen des X. 509-> Zertifikats basiert, das für den Netzwerk Controller erstellt wurde.
>
>Der *Credential* -Parameter muss nur angegeben werden, wenn der Netzwerk Controller die Kerberos-Authentifizierung verwendet (typisch in VMM-bereit Stellungen). Die Anmelde Informationen müssen für einen Benutzer angegeben werden, der sich in der Sicherheitsgruppe für die Netzwerk Controller Verwaltung befindet.

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

Im folgenden wird eine beispielhafte Konfigurations Zustands Meldung angezeigt:

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
> Im System ist ein Fehler aufgetreten, bei dem die Netzwerkschnittstellen Ressourcen für die VM-NIC der SLB MUX-Übertragung in einem Fehlerzustand mit dem Fehler "virtueller Switch-Host ist nicht mit Controller verbunden" angezeigt wird. Dieser Fehler kann ignoriert werden, wenn die IP-Konfiguration in der NIC-Ressource des virtuellen Computers auf eine IP-Adresse aus dem IP-Pool des logischen Transit Netzwerks festgelegt ist. Im System ist ein zweiter Fehler aufgetreten, bei dem die Netzwerkschnittstellen Ressourcen für die VM-NICs des Gateway-HNV-Anbieters in einem Fehlerzustand mit dem Fehler "virtueller Switch-portblockiert" angezeigt werden. Dieser Fehler kann auch ignoriert werden, wenn die IP-Konfiguration in der VM-NIC-Ressource auf NULL festgelegt ist (Entwurfs bedingt).


Die folgende Tabelle zeigt die Liste der Fehlercodes, Meldungen und nach Verfolgungs Aktionen, die basierend auf dem beobachteten Konfigurations Status ausgeführt werden müssen.


| **Ordnung**| **Nachricht**| **Aktion**|  
|--------|-----------|----------|  
| Unbekannt| Unbekannter Fehler.| |  
| Host nicht erreichbar                       | Der Host Computer ist nicht erreichbar. | Überprüfen Sie die Konnektivität des Verwaltungs Netzwerks zwischen Netzwerk Controller und Host. |  
| "Pipadressssextrasted"                  | Die PA-IP-Adressen sind erschöpft | Vergrößern der IP-Pool Größe des HNV-Anbieters des logischen Subnetzes |  
| Pamacadressssextrasted                 | Die PA-Mac-Adressen sind erschöpft | Vergrößern des Mac-Pool Bereichs |  
| "Paddressconfigurationfailure"         | Fehler beim Durchreichen von PA-Adressen auf den Host. | Überprüfen Sie die Konnektivität des Verwaltungs Netzwerks zwischen Netzwerk Controller und Host. |  
| Certifiupumottrusted                 | Das Zertifikat ist nicht vertrauenswürdig.  |Korrigieren Sie die Zertifikate, die für die Kommunikation mit dem Host verwendet werden. |  
| Certifiin zertificerautorisiert              | Zertifikat nicht autorisiert | Korrigieren Sie die Zertifikate, die für die Kommunikation mit dem Host verwendet werden. |  
| Policyconfigurationfailureonvfp       | Fehler beim Konfigurieren von VFP-Richtlinien | Dies ist ein Laufzeitfehler.  Keine definitive Arbeit. Sammeln von Protokollen. |  
| Policyconfigurationfailure            | Fehler beim Übertragen von Richtlinien an die Hosts aufgrund von Kommunikationsfehlern oder anderen Fehlern in Network Controller.| Keine konkreten Aktionen.  Dies liegt an einem Fehler bei der Verarbeitung des Ziel Zustands in den Netzwerk Controller Modulen. Sammeln von Protokollen. |  
| Hostnotconnectedto Controller          | Der Host ist noch nicht mit dem Netzwerk Controller verbunden. | Das auf dem Host nicht angewendete Port Profil oder der Host ist vom Netzwerk Controller aus nicht erreichbar. Überprüft, ob der Hostid-Registrierungsschlüssel mit der Instanz-ID der Server Ressource übereinstimmt. |  
| Multiplevfpabledswitches            | Es gibt mehrere VFP-aktivierte Switches auf dem Host.  | Löschen eines der Switches, da der Netzwerk Controller-Host-Agent nur einen Vswitch unterstützt, bei dem die VFP-Erweiterung aktiviert ist. |  
| Policyconfigurationfailure            | Fehler beim Pushen von vnet-Richtlinien für eine Vmnic aufgrund von Zertifikat Fehlern oder Verbindungsfehlern.  | Überprüfen Sie, ob richtige Zertifikate bereitgestellt wurden (der Name des Zertifikat Antragstellers muss dem FQDN des Hosts entsprechen). Überprüfen Sie außerdem die Host Konnektivität mit dem Netzwerk Controller. |  
| Policyconfigurationfailure            | Fehler beim Pushen von Vswitch-Richtlinien für eine Vmnic aufgrund von Zertifikat Fehlern oder Verbindungsfehlern.  | Überprüfen Sie, ob richtige Zertifikate bereitgestellt wurden (der Name des Zertifikat Antragstellers muss dem FQDN des Hosts entsprechen). Überprüfen Sie außerdem die Host Konnektivität mit dem Netzwerk Controller.|
| Policyconfigurationfailure            | Fehler beim Pushen von Firewallrichtlinien für eine Vmnic aufgrund von Zertifikat Fehlern oder Verbindungsfehlern. | Überprüfen Sie, ob richtige Zertifikate bereitgestellt wurden (der Name des Zertifikat Antragstellers muss dem FQDN des Hosts entsprechen). Überprüfen Sie außerdem die Host Konnektivität mit dem Netzwerk Controller.|
| Distributedrouterconfigurationfailure | Fehler beim Konfigurieren der Einstellungen verteilter Router auf der Host-vNIC.                          | Tcpip-Stapelfehler. Erfordert möglicherweise das Bereinigen der PA-und Dr-Host-vNICs auf dem Server, auf dem dieser Fehler gemeldet wurde. |
| Dhcpaddresszugecationfailure          | Fehler bei der DHCP-Adress Zuordnung für eine Vmnic.                                                    | Überprüfen Sie, ob das statische IP-Adress Attribut für die NIC-Ressource konfiguriert ist. |  
| Certifiupumottrusted<br>Certifiin zertificerautorisiert | Fehler beim Herstellen einer Verbindung mit MUX aufgrund von Netzwerk-oder Zertifikat Fehlern. | Überprüfen Sie den numerischen Code, der im Fehlermeldungs Code bereitgestellt wird: Dies entspricht dem Winsock-Fehlercode. Zertifikat Fehler sind differenzierbar (z. b. kann das Zertifikat nicht verifiziert werden, das Zertifikat ist nicht autorisiert usw.) |  
| Host nicht erreichbar                       | MUX ist fehlerhaft (allgemeiner Fall ist der bgprouter getrennt). | Der BGP-Peer auf dem RRAS-Switch (virtueller BGP-Computer) oder dem Tor-Switch (Top-of-Rack) ist nicht erreichbar oder kann nicht erfolgreich per Peering erstellt werden. Überprüfen Sie die BGP-Einstellungen sowohl für die Software Load Balancer Multiplexer-Ressource als auch für den BGP-Peer (Virtual Machine (Tor) |  
| Hostnotconnectedto Controller          | Der SLB-Host-Agent ist nicht verbunden.  | Überprüfen, ob der SLB-Host-Agent-Dienst ausgeführt wird In den SLB-Host-Agent-Protokollen (automatische Ausführung) finden Sie Gründe dafür, warum das vom Host-Agent mit dem Status "wird ausgeführt" angegebene Zertifikat von SLBM (NC) abgelehnt wird.  |  
| Portblockiert                           | Der VFP-Port ist aufgrund fehlender vnet-/ACL-Richtlinien blockiert. | Überprüfen Sie, ob andere Fehler vorhanden sind, was dazu führen kann, dass die Richtlinien nicht konfiguriert werden. |  
| Überlastung                            | LoadBalancer MUX ist überladen  | Leistungsprobleme mit MUX |  
| Routepublicationfailure               | LoadBalancer MUX ist nicht mit einem BGP-Router verbunden. | Überprüfen Sie, ob die Verbindung mit den BGP-Routern besteht und ob das BGP-Peering ordnungsgemäß eingerichtet ist. |  
| Virtualserverunerreichbare              | LoadBalancer MUX ist nicht mit dem SLB-Manager verbunden. | Überprüfen der Konnektivität zwischen SLBM und MUX |  
| Qosconfigurationfailure               | Fehler beim Konfigurieren der QoS-Richtlinien | Überprüfen Sie, ob für alle VMs ausreichend Bandbreite verfügbar ist, wenn die QoS-Reservierung verwendet wird. |


#### <a name="check-network-connectivity-between-the-network-controller-and-hyper-v-host-nc-host-agent-service"></a>Überprüfen der Netzwerk Konnektivität zwischen dem Netzwerk Controller und dem Hyper-V-Host (NC-Host-Agent-Dienst)
Führen Sie den folgenden *netstat* -Befehl aus, um zu überprüfen, ob zwischen dem NC-Host-Agent und den Netzwerk Controller Knoten und einem Überwachungs Socket auf dem Hyper-V-Host drei Verbindungen hergestellt wurden.
- Lauschen an Port TCP: 6640 auf dem Hyper-V-Host (NC-Host-Agent-Dienst)
- Zwei festgelegte Verbindungen von der Hyper-V-Host-IP auf Port 6640 zu NC-Knoten-IP auf kurzlebigen Ports (> 32000)
- Eine Verbindung von der Hyper-V-Host-IP-Adresse auf dem kurzlebigen Port zur Netzwerk Controller-Rest-IP auf Port 6640

>[!NOTE]
>Auf einem Hyper-V-Host können nur zwei Verbindungen hergestellt werden, wenn auf diesem Host keine virtuellen Mandanten Maschinen bereitgestellt werden.

```none
netstat -anp tcp |findstr 6640

# Successful output
  TCP    0.0.0.0:6640           0.0.0.0:0              LISTENING
  TCP    10.127.132.153:6640    10.127.132.213:50095   ESTABLISHED
  TCP    10.127.132.153:6640    10.127.132.214:62514   ESTABLISHED
  TCP    10.127.132.153:50023   10.127.132.211:6640    ESTABLISHED
```
#### <a name="check-host-agent-services"></a>Host-Agent-Dienste überprüfen
Der Netzwerk Controller kommuniziert mit zwei Host-Agent-Diensten auf den Hyper-V-Hosts: SLB-Host-Agent und NC-Host-Agent. Es ist möglich, dass einer oder beide dieser Dienste nicht ausgeführt werden. Überprüfen Sie Ihren Status und starten Sie ihn neu, wenn er nicht ausgeführt wird

```none
Get-Service SlbHostAgent
Get-Service NcHostAgent

# (Re)start requires -Force flag
Start-Service NcHostAgent -Force
Start-Service SlbHostAgent -Force
```

#### <a name="check-health-of-network-controller"></a>Integritäts Status des Netzwerk Controllers überprüfen
Wenn nicht drei Verbindungen hergestellt wurden oder der Netzwerk Controller nicht reagiert, überprüfen Sie, ob alle Knoten und Dienst Module mit den folgenden Cmdlets ausgeführt werden. 

```none
# Prints a DIFF state (status is automatically updated if state is changed) of a particular service module replica 
Debug-ServiceFabricNodeStatus [-ServiceTypeName] <Service Module>
```
Die Module des Netzwerk Controller Dienstanbieter lauten wie folgt:
- ControllerService
- Apiservice
- Slbmanagerservice
- Servicabsertion
- Firewallservice
- Vswitchservice
- Gatewaymanager
- Fnmservice
- Helperservice
- PLB

Überprüfen Sie, ob replicastatus **bereit** ist und healthstate den Wert **OK**aufweist.

In einer Produktions Bereitstellung mit einem Netzwerk Controller mit mehreren Knoten können Sie auch überprüfen, auf welchem Knoten sich die einzelnen Dienste als primär Dienst und den jeweiligen Replikat Status befinden.

```none  
Get-NetworkControllerReplica

# Sample Output for the API service module 
Replicas for service: ApiService

ReplicaRole   : Primary
NodeName      : SA18N30NC3.sa18.nttest.microsoft.com
ReplicaStatus : Ready

```
Überprüfen Sie, ob der Replikat Status für jeden Dienst bereit ist.

#### <a name="check-for-corresponding-hostids-and-certificates-between-network-controller-and-each-hyper-v-host"></a>Überprüfen Sie die entsprechenden hostids und Zertifikate zwischen Netzwerk Controller und Hyper-V-Host. 
Führen Sie auf einem Hyper-V-Host die folgenden Befehle aus, um zu überprüfen, ob die Hostid der Instanz-ID einer Server Ressource auf dem Netzwerk Controller entspricht.

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

*Remediation* Wiederherstellung Wenn Sie sdnexpress-Skripts oder die manuelle Bereitstellung verwenden, aktualisieren Sie den Hostid-Schlüssel in der Registrierung entsprechend der Instanz-ID der Server Ressource. Starten Sie den Netzwerk Controller-Host-Agent auf dem Hyper-v-Host (physischer Server), wenn Sie VMM verwenden, löschen Sie den Hyper-V-Server aus VMM, und entfernen Sie den Hostid-Registrierungsschlüssel. Fügen Sie den Server dann über VMM erneut hinzu.


Überprüfen Sie, ob die Fingerabdrücke der X. 509-Zertifikate, die vom Hyper-v-Host verwendet werden (der Hostname ist der Antragsteller Name des Zertifikats), für die (Southbound) Kommunikation zwischen dem Hyper-v-Host (NC-Host-Agent-Dienst) und den Netzwerk Controller Knoten identisch sind. Überprüfen Sie auch, ob das Rest-Zertifikat des Netzwerk Controllers den Antragsteller Namen *CN =<FQDN or IP>* hat.

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

Sie können auch die folgenden Parameter jedes Zertifikats überprüfen, um sicherzustellen, dass der Name des Antragstellers erwartet wird (Hostname oder NC-Rest-FQDN oder IP), das Zertifikat noch nicht abgelaufen ist und dass alle Zertifizierungsstellen in der Zertifikat Kette in den vertrauenswürdigen Stamm eingefügt werden. Herrschaft.

- Antragstellername  
- Ablaufdatum  
- Vertrauenswürdig durch Stamm Zertifizierungsstelle  

*Remediation* Wiederherstellung Wenn mehrere Zertifikate denselben Antragsteller Namen auf dem Hyper-V-Host aufweisen, wählt der Netzwerk Controller-Host-Agent nach dem Zufallsprinzip einen aus, der dem Netzwerk Controller vorgelegt werden soll. Dies entspricht möglicherweise nicht dem Fingerabdruck der Server Ressource, die dem Netzwerk Controller bekannt ist. Löschen Sie in diesem Fall eines der Zertifikate mit dem gleichen Antragsteller Namen auf dem Hyper-V-Host, und starten Sie dann den Netzwerk Controller-Host-Agent-Dienst neu. Wenn noch keine Verbindung hergestellt werden kann, löschen Sie das andere Zertifikat mit dem gleichen Antragsteller Namen auf dem Hyper-V-Host, und löschen Sie die entsprechende Server Ressource in VMM. Erstellen Sie dann die Server Ressource in VMM neu, wodurch ein neues X. 509-Zertifikat generiert und auf dem Hyper-V-Host installiert wird.


#### <a name="check-the-slb-configuration-state"></a>Überprüfen des SLB-Konfigurations Status
Der SLB-Konfigurations Status kann als Teil der Ausgabe an das Debug-networkcontroller-Cmdlet festgelegt werden. Mit diesem Cmdlet werden auch die aktuellen Netzwerk Controller Ressourcen in JSON-Dateien, alle IP-Konfigurationen von den einzelnen Hyper-V-Hosts (Server) und die lokale Netzwerk Richtlinie aus den Host-Agent-Datenbanktabellen ausgegeben. 

Standardmäßig werden weitere Ablauf Verfolgungen erfasst. Fügen Sie den Parameter "-incluenttraces: $false" hinzu, um keine Ablauf Verfolgungen zu erfassen.

```none
Debug-NetworkController -NetworkController <FQDN or IP> [-Credential <PS Credential>] [-IncludeTraces:$false]

# Don't collect traces
$cred = Get-Credential 
Debug-NetworkController -NetworkController 10.127.132.211 -Credential $cred -IncludeTraces:$false

Transcript started, output file is C:\\NCDiagnostics.log
Collecting Diagnostics data from NC Nodes
```

>[!NOTE]
>Der Standardausgabe Speicherort ist der < working_directory > Verzeichnis "\ncdiagnostics\". Das Standardausgabe Verzeichnis kann mithilfe des `-OutputDirectory`-Parameters geändert werden. 

Die SLB-Konfigurations Zustandsinformationen finden Sie in der Datei " _Diagnostics-slbstateresults. JSON_ " in diesem Verzeichnis.

Diese JSON-Datei kann in die folgenden Abschnitte unterteilt werden:
 * Fabric
   * Slbmvips: in diesem Abschnitt wird die IP-Adresse der SLB-Manager-VIP-Adresse aufgelistet, die vom Netzwerk Controller zum Konfigurieren der Konfiguration und Integrität zwischen den SLB-muxes und SLB-Host-Agents verwendet wird.
   * Muxstate: in diesem Abschnitt wird ein Wert für jede bereitgestellte SLB-MUX-Datei mit dem Status der Mux-Datei aufgelistet.
   * Routerkonfiguration: in diesem Abschnitt werden die autonome System Nummer (ASN) des Upstream-Routers (BGP-Peer), die Transit-IP-Adresse und die ID aufgelistet. Außerdem werden die SLB-muxes ASN und Transit-IP aufgelistet.
   * Informationen zum verbundenen Host: in diesem Abschnitt werden die Verwaltungs-IP-Adressen für alle Hyper-V-Hosts aufgelistet, die zum Ausführen von Arbeits Auslastungen mit Lastenausgleich verfügbar sind.
   * VIP-Bereiche: in diesem Abschnitt werden die IP-Poolbereiche für öffentliche und private VIP-Adressen aufgelistet. Die SLBM-VIP wird als zugeordnete IP-Adresse aus einem dieser Bereiche eingeschlossen. 
   * MUX-Routen: in diesem Abschnitt wird ein Wert für jede bereitgestellte SLB-MUX-Datei aufgelistet, die alle Routen Ankündigungen für das jeweilige MUX enthält.
 * Mandant
   * Vipkonsolidatedstate: in diesem Abschnitt wird der Verbindungsstatus für jede Mandanten-VIP aufgeführt, einschließlich des angekündigten Routen Präfixes, des Hyper-V-Hosts und der DIP-Endpunkte.

> [!NOTE]
> Der SLB-Status kann direkt mithilfe des im [Microsoft Sdn GitHub-Repository](https://github.com/microsoft/sdn)verfügbaren [dumpslbreststate](https://github.com/Microsoft/SDN/blob/master/Diagnostics/DumpSlbRestState.ps1) -Skripts ermittelt werden. 

#### <a name="gateway-validation"></a>Gatewayvalidierung

**Vom Netzwerk Controller:**
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

**Vom Tor-Switch (Top of Rack):**

`sh ip bgp summary (for 3rd party BGP Routers)`

**Windows BGP-Router**
```
Get-BgpRouter
Get-BgpPeer
Get-BgpRouteInformation
```

Abgesehen von den bisher genannten Problemen (insbesondere bei sdnexpress-basierten bereit Stellungen) ist der häufigste Grund für ein nicht konfiguriertes Mandanten Depot auf GW-VMS anscheinend die Tatsache, dass die GW-Kapazität in fabricconfig. psd1 kleiner ist als Es wird versucht, den Netzwerkverbindungen (S2S-Tunnel) in tenantconfig. psd1 zuzuweisen. Dies lässt sich problemlos überprüfen, indem Ausgaben der folgenden Befehle verglichen werden:

```
PS > (Get-NetworkControllerGatewayPool -ConnectionUri $uri).properties.Capacity
PS > (Get-NetworkControllerVirtualgatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "TenantName").properties.OutboundKiloBitsPerSecond
PS > (Get-NetworkControllerVirtualgatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "TenantName").property
```

### <a name="hoster-validate-data-plane"></a>Hoster Datenebene überprüfen
Nachdem der Netzwerk Controller bereitgestellt wurde, werden virtuelle Mandanten Netzwerke und Subnetze erstellt und VMS an die virtuellen Subnetze angefügt. es können weitere Tests auf Fabric-Ebene vom hostercomputer durchgeführt werden, um die Mandanten Konnektivität zu überprüfen.

#### <a name="check-hnv-provider-logical-network-connectivity"></a>Überprüfen der logischen Netzwerk Konnektivität des HNV-Anbieters
Nachdem der erste virtuelle Gastcomputer, der auf einem Hyper-v-Host ausgeführt wird, mit einem virtuellen Mandanten Netzwerk verbunden ist, weist der Netzwerk Controller zwei HNV-Anbieter-IP-Adressen (PA-IP-Adressen) dem Hyper-v-Host zu. Diese IPS stammen aus dem logischen Netzwerk des HNV-Anbieter Netzwerks und werden vom Netzwerk Controller verwaltet.  So ermitteln Sie, was diese beiden HNV-IP-Adressen sind

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

Die IP-Adressen des HNV-Anbieters (PA-IPS) werden Ethernet-Adaptern zugewiesen, die in einem separaten tcpip-Netzwerk Depot erstellt wurden, und haben den Adapter Namen _vlanx_ , wobei X das VLAN ist, das dem logischen HNV-anbieternetzwerk (Transport) zugewiesen ist.

Die Konnektivität zwischen zwei Hyper-v-Hosts, die das logische HNV-anbieternetzwerk verwenden, kann durch einen Ping mit einem zusätzlichen Depot-Parameter (-c Y) erfolgen, wobei Y das tcpip-Netzwerk Depot ist, in dem die "phostvnics" erstellt werden. Dieses Depot kann durch Ausführen von Folgendes bestimmt werden:

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
> Die vNIC-Adapter für den PA-Host werden im Datenpfad nicht verwendet und verfügen daher nicht über eine IP-Adresse, die dem Adapter "vethernet (phostvnic)" zugewiesen ist.

Nehmen Sie beispielsweise an, dass die Hyper-V-Hosts 1 und 2 über die HNV-Anbieter-IP-Adressen verfügen:

|-Hyper-V-Host-|-PA IP-Adresse 1|-PA-IP-Adresse 2|
|---             |---            |---             |
|Host 1 | 10.10.182.64 | 10.10.182.65 |
|Host 2 | 10.10.182.66 | 10.10.182.67 |

Wir können mit dem folgenden Befehl ein Ping zwischen den beiden durchsetzen, um die Konnektivität des logischen HNV-Anbieters zu überprüfen.

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

*Remediation* Wiederherstellung Wenn der HNV-Anbieter Ping nicht funktioniert, überprüfen Sie die physische Netzwerk Konnektivität einschließlich der VLAN-Konfiguration. Die physischen NICs auf den einzelnen Hyper-V-Hosts sollten sich im trunk Modus befinden, ohne dass ein bestimmtes VLAN zugewiesen ist. Die vNIC des Verwaltungs Hosts sollte in das VLAN des logischen Verwaltungs Netzwerks isoliert werden.

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

#### <a name="check-mtu-and-jumbo-frame-support-on-hnv-provider-logical-network"></a>Überprüfen der MTU-und groß Frame-Unterstützung im logischen HNV-anbieternetzwerk

Ein weiteres häufiges Problem im logischen HNV-anbieternetzwerk besteht darin, dass für die physischen Netzwerkports und/oder Ethernet-Karten nicht ausreichend MTU konfiguriert ist, um den mehr Aufwand über die vxlan-Kapselung (oder nvgre) zu bewältigen. 
>[!NOTE]
> Einige Ethernet-Karten und Treiber unterstützen das neue * encapoverhead-Schlüsselwort, das automatisch vom Netzwerk Controller-Host-Agent auf den Wert 160 festgelegt wird. Dieser Wert wird dann dem Wert des * jumbopacket-Schlüssel Worts hinzugefügt, dessen Summe als Ankündigung der angekündigten MTU verwendet wird.
> z. b. * umcapoverhead = 160 und * jumbopacket = 1514 = > MTU = 1674b

```none
# Check whether or not your Ethernet card and driver support *EncapOverhead
PS C:\ > Test-EncapOverheadSettings

Verifying Physical Nic : <NIC> Ethernet Adapter #2
Physical Nic  <NIC> Ethernet Adapter #2 can support SDN traffic. Encapoverhead value set on the nic is  160
Verifying Physical Nic : <NIC> Ethernet Adapter
Physical Nic  <NIC> Ethernet Adapter can support SDN traffic. Encapoverhead value set on the nic is  160
```

Um zu testen, ob das logische HNV-anbieternetzwerk die größere MTU-Größe von End-to-End unterstützt, verwenden Sie das Cmdlet _Test-logicalnetworksupportsjumbopacket_ :
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

*Erungs*
* Passen Sie die MTU-Größe auf den physischen Switchports auf mindestens 1674b an (einschließlich 14B-Ethernet-Header und-Nachspann).
* Wenn Ihre NIC-Karte das encapoverhead-Schlüsselwort nicht unterstützt, passen Sie das Wort "jumbopacket" auf mindestens 1674b an.


#### <a name="check-tenant-vm-nic-connectivity"></a>Überprüfen der NIC-Konnektivität des Mandanten
Jede VM-NIC, die einer Gast-VM zugewiesen ist, verfügt über eine ca-PA-Zuordnung zwischen der privaten Kundenadresse (ca) und dem Speicherplatz der HNV-Anbieter Adresse (PA). Diese Zuordnungen werden in den ovsdb-Server Tabellen auf den einzelnen Hyper-V-Hosts gespeichert und können durch Ausführen des folgenden Cmdlets gefunden werden.

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
> Wenn die von Ihnen erwarteten ca-PA-Zuordnungen nicht für eine bestimmte Mandanten-VM ausgegeben werden, überprüfen Sie die VM-NIC und die IP-Konfigurations Ressourcen auf dem Netzwerk Controller mithilfe des Cmdlets _Get-networkcontrollernetworkinterface_ . Überprüfen Sie außerdem die eingerichteten Verbindungen zwischen dem NC-Host-Agent und den Netzwerk Controller Knoten.

Mit diesen Informationen kann ein Mandanten-VM-Ping jetzt vom Host mithilfe des _Test-virtualnetworkconnection_ -Cmdlets vom Netzwerk Controller initiiert werden.

## <a name="specific-troubleshooting-scenarios"></a>Spezifische Problem behandlungsszenarien

Die folgenden Abschnitte enthalten Anleitungen zur Problembehandlung für bestimmte Szenarien.

### <a name="no-network-connectivity-between-two-tenant-virtual-machines"></a>Keine Netzwerk Konnektivität zwischen zwei virtuellen Mandanten Computern

1.  Tenant Stellen Sie sicher, dass die Windows-Firewall auf virtuellen Mandanten Computern keinen Datenverkehr blockiert.  
2.  Tenant Überprüfen Sie, ob die IP-Adressen dem virtuellen Mandanten Computer zugewiesen wurden, indem Sie _ipconfig_ausführen. 
3.  Hoster Führen Sie " **Test-virtualnetworkconnection** " vom Hyper-V-Host aus, um die Konnektivität zwischen den beiden fraglichen virtuellen Mandanten Computern zu überprüfen. 

>[!NOTE]
>Die vsid verweist auf die virtuelle Subnetz-ID. Im Fall von vxlan ist dies die vxlan-Netzwerk Kennung (vni). Sie können diesen Wert ermitteln, indem Sie das Cmdlet **Get-pacamapping** ausführen.

#### <a name="example"></a>Beispiel

    $password = ConvertTo-SecureString -String "password" -AsPlainText -Force
    $cred = New-Object pscredential -ArgumentList (".\administrator", $password) 

Erstellen Sie ca-Ping zwischen "grünes Web-VM 1" mit senderca-IP-Adresse von 192.168.1.4 auf dem Host "sa18n30-2.SA18.nttest.Microsoft.com" mit der Mgmt-IP-Adresse 10.127.132.153 und listenerca IP von 192.168.1.5 erstellt, die beide an das virtuelle Subnetz (vsid) 4114 angefügt sind.

    Test-VirtualNetworkConnection -OperationId 27 -HostName sa18n30-2.sa18.nttest.microsoft.com -MgmtIp 10.127.132.153 -Creds $cred -VMName "Green Web VM 1" -VMNetworkAdapterName "Green Web VM 1" -SenderCAIP 192.168.1.4 -SenderVSID 4114 -ListenerCAIP 192.168.1.5 -ListenerVSID 4114

    Test-VirtualNetworkConnection at command pipeline position 1

Start des ca-Space-Pingtests Starten der Ablauf Verfolgungs Sitzung Ping an 192.168.1.5 erstellt erfolgreich von Adresse 192.168.1.4 RTT = 0 ms


Informationen zum Routing der Zertifizierungsstelle:

    Local IP: 192.168.1.4
    Local VSID: 4114
    Remote IP: 192.168.1.5
    Remote VSID: 4114
    Distributed Router Local IP: 192.168.1.1
    Distributed Router Local MAC: 40-1D-D8-B7-1C-06
    Local CA MAC: 00-1D-D8-B7-1C-05
    Remote CA MAC: 00-1D-D8-B7-1C-07
    Next Hop CA MAC Address: 00-1D-D8-B7-1C-07

Informationen zum PA-Routing:

    Local PA IP: 10.10.182.66
    Remote PA IP: 10.10.182.65

 <snip>...

4. Tenant Überprüfen Sie, ob für das virtuelle Subnetz oder die VM-Netzwerkschnittstellen keine verteilten Firewallrichtlinien angegeben sind, die den Datenverkehr blockieren würden.    

Fragen Sie die Netzwerk Controller-Rest-API in der Demo Umgebung unter sa18n30nc in der SA18.nttest.Microsoft.com-Domäne ab.

    $uri = "https://sa18n30nc.sa18.nttest.microsoft.com"
    Get-NetworkControllerAccessControlList -ConnectionUri $uri 

## <a name="look-at-ip-configuration-and-virtual-subnets-which-are-referencing-this-acl"></a>Sehen Sie sich die IP-Konfiguration und virtuelle Subnetze an, die auf diese ACL verweisen.

1. Hoster Führen Sie ``Get-ProviderAddress`` auf beiden Hyper-v-Hosts aus, die die beiden fraglichen Mandanten-VMs hosten, und führen Sie dann ``Test-LogicalNetworkConnection`` oder ``ping -c <compartment>`` vom Hyper-v-Host aus, um die Konnektivität im logischen HNV-anbieternetzwerk zu überprüfen
2.  Hoster Stellen Sie sicher, dass die MTU-Einstellungen auf den Hyper-v-Hosts und alle Layer-2-Geräte zwischen den Hyper-v-Hosts korrekt sind. Führen Sie ``Test-EncapOverheadValue`` auf allen fraglichen Hyper-V-Hosts aus. Überprüfen Sie außerdem, ob für alle Layer-2-Switches zwischen MTU mindestens 1674 Byte festgelegt sind, um den maximalen mehr Aufwand von 160 Bytes zu berücksichtigen.  
3.  Hoster Wenn keine PA-IP-Adressen vorhanden sind und/oder die ca-Konnektivität beschädigt ist, überprüfen Sie, ob die Netzwerk Richtlinie empfangen wurde. Führen Sie ``Get-PACAMapping`` aus, um zu überprüfen, ob die Kapselungs Regeln und ca-PA-Zuordnungen, die zum Erstellen von über Lagerungs Netzwerken erforderlich sind  
4.  Hoster Überprüfen Sie, ob der Netzwerk Controller-Host-Agent mit dem Netzwerk Controller verbunden ist. Führen Sie ``netstat -anp tcp |findstr 6640`` aus, um festzustellen, ob   
5.  Hoster Überprüfen Sie, ob die Host-ID in HKLM/mit der Instanz-ID der Server Ressourcen übereinstimmt, die die virtuellen Mandanten Computer hosten.  
6. Hoster Überprüfen Sie, ob die Port Profil-ID mit der Instanz-ID der VM-Netzwerkschnittstellen der virtuellen Mandanten Computer übereinstimmt.  

## <a name="logging-tracing-and-advanced-diagnostics"></a>Protokollierung, Ablauf Verfolgung und erweiterte Diagnose

In den folgenden Abschnitten finden Sie Informationen zur erweiterten Diagnose, Protokollierung und Ablauf Verfolgung.

### <a name="network-controller-centralized-logging"></a>Zentrale Netzwerk Controller Protokollierung 

Der Netzwerk Controller kann automatisch debuggerprotokolle erfassen und an einem zentralen Speicherort speichern. Die Protokoll Sammlung kann aktiviert werden, wenn Sie den Netzwerk Controller zum ersten Mal oder zu einem späteren Zeitpunkt bereitstellen. Die Protokolle werden vom Netzwerk Controller und vom Netzwerk Controller verwaltete Netzwerkelemente: Host Computer, Software Lastenausgleich (Software Load Balancer, SLB) und Gatewaycomputer erfasst. 

Diese Protokolle umfassen Debugprotokolle für den Netzwerk Controller Cluster, die Netzwerk Controller Anwendung, gatewayprotokolle, SLB, virtuelle Netzwerke und die verteilte Firewall. Wenn dem Netzwerk Controller ein neuer Host/SLB/Gateway hinzugefügt wird, wird die Protokollierung auf diesen Computern gestartet. Ebenso wird die Protokollierung auf diesen Computern beendet, wenn ein Host/SLB/Gateway vom Netzwerk Controller entfernt wird.

#### <a name="enable-logging"></a>Protokollierung aktivieren

Die Protokollierung wird automatisch aktiviert, wenn Sie den Netzwerk Controller Cluster mithilfe des Cmdlets **install-networkcontrollercluster** installieren. Standardmäßig werden die Protokolle lokal auf den Netzwerk Controller Knoten unter " *%systemdrive%\sdndiagnostics*" gesammelt. Es wird **dringend empfohlen** , diesen Speicherort in eine Remote Dateifreigabe (nicht lokal) zu ändern. 

Die Netzwerk Controller-Cluster Protokolle werden unter *%ProgramData%\Windows fabric\log\traces*gespeichert. Sie können einen zentralisierten Speicherort für die Protokoll Sammlung mit dem **diagnosticlogloations** -Parameter angeben. dabei wird empfohlen, dass es sich hierbei auch um eine Remote Dateifreigabe handelt. 

Wenn Sie den Zugriff auf diesen Speicherort einschränken möchten, können Sie die Zugriffs Anmelde Informationen mit dem **loglocationcredential** -Parameter angeben. Wenn Sie die Anmelde Informationen für den Zugriff auf den Protokoll Speicherort angeben, sollten Sie auch den Parameter " **fidentialverschlüsseltioncertificate** " angeben, der zum Verschlüsseln der lokal auf den Netzwerk Controller Knoten gespeicherten Anmelde Informationen verwendet wird.  

Mit den Standardeinstellungen wird empfohlen, dass Sie mindestens 75 GB freien Speicherplatz am zentralen Standort und 25 GB auf den lokalen Knoten (wenn kein zentraler Speicherort verwendet wird) für einen Netzwerk Controller Cluster mit drei Knoten verwenden.

#### <a name="change-logging-settings"></a>Protokollierungs Einstellungen ändern

Sie können die Protokollierungs Einstellungen jederzeit mithilfe des ``Set-NetworkControllerDiagnostic``-Cmdlets ändern. Die folgenden Einstellungen können geändert werden:

- **Zentralisierter Protokoll Speicherort**.  Mit dem ``DiagnosticLogLocation``-Parameter können Sie den Speicherort ändern, an dem alle Protokolle gespeichert werden.  
- **Anmelde Informationen für den Zugriff auf den Protokoll Speicherort**  Mit dem ``LogLocationCredential``-Parameter können Sie die Anmelde Informationen für den Zugriff auf den Protokoll Speicherort ändern.  
- **Wechseln Sie zur lokalen Protokollierung**.  Wenn Sie einen zentralisierten Speicherort zum Speichern von Protokollen bereitgestellt haben, können Sie sich auf den Netzwerk Controller Knoten mit dem ``UseLocalLogLocation``-Parameter wieder lokal anmelden (nicht empfohlen aufgrund von umfangreichen Speicherplatzanforderungen).  
- **Protokollierungs Bereich**.  Standardmäßig werden alle Protokolle gesammelt. Sie können den Bereich ändern, um nur Netzwerk Controller-Cluster Protokolle zu erfassen.  
- **Protokolliergrad**.  Der Standardprotokolliergrad ist "Information". Sie können den Wert in "Error", "Warning" oder "Verbose" ändern.  
- **Protokollierung der Zeit**.  Die Protokolle werden zirkulär gespeichert. Sie haben standardmäßig drei Tage Zeit, Daten zu protokollieren, unabhängig davon, ob Sie lokale Protokollierung oder zentrale Protokollierung verwenden. Sie können dieses Zeitlimit mit dem **logtimelimitindays** -Parameter ändern.  
- **Protokollieren der Größe**.  Standardmäßig verfügen Sie über eine maximale Größe von 75 GB Protokollierungs Daten, wenn Sie die zentralisierte Protokollierung und 25 GB bei Verwendung der lokalen Protokollierung verwenden. Sie können diesen Grenzwert mit dem **logsizelimitinmsb** -Parameter ändern.

#### <a name="collecting-logs-and-traces"></a>Erfassen von Protokollen und Ablauf Verfolgungen

VMM-bereit Stellungen verwenden standardmäßig die zentralisierte Protokollierung für den Netzwerk Controller. Der Speicherort der Dateifreigabe für diese Protokolle wird beim Bereitstellen der Netzwerk Controller-Dienst Vorlage angegeben.

Wenn kein Speicherort angegeben wurde, wird die lokale Protokollierung auf jedem Netzwerk Controller Knoten verwendet, wobei die Protokolle unter c:\windows\tracing\sdndiagnosticsgespeichert werden. Diese Protokolle werden mithilfe der folgenden Hierarchie gespeichert:

- CrashDumps
- Ncapplicationcrashdumps
- Ncapplicationlogs
- PerfCounters
- Sdndiagnostics
- Traces

Der Netzwerk Controller verwendet (Azure) Service Fabric. Bei der Behebung bestimmter Probleme sind möglicherweise Service Fabric Protokolle erforderlich. Diese Protokolle befinden sich auf jedem Netzwerk Controller Knoten unter "c:\programdata\microsoft\service Fabric".

Wenn ein Benutzer das _Debug-networkcontroller-_ Cmdlet ausgeführt hat, sind zusätzliche Protokolle auf jedem Hyper-V-Host verfügbar, der mit einer Server Ressource im Netzwerk Controller angegeben wurde. Diese Protokolle (und Ablauf Verfolgungen, sofern aktiviert) werden unter "c:\ncdiagnostics" beibehalten.

### <a name="slb-diagnostics"></a>SLB-Diagnose

#### <a name="slbm-fabric-errors-hosting-service-provider-actions"></a>SLBM Fabric-Fehler (hostingdienstanbieter-Aktionen)

1.  Überprüfen Sie, ob die Software Load Balancer Manager (SLBM) funktionsfähig ist und dass die Orchestrierungs Ebenen miteinander kommunizieren können: SLBM-> SLB MUX und SLBM-> SLB-Host-Agents. Führen Sie [dumpslbreststate](https://github.com/Microsoft/SDN/blob/master/Diagnostics/DumpSlbRestState.ps1) von einem beliebigen Knoten mit Zugriff auf den Rest-Endpunkt des Netzwerk Controllers aus.  
2.  Überprüfen Sie die *sdnslbmperf-* Indikatoren in Perfmon auf einem der Netzwerk Controller Knoten-VMS (vorzugsweise der primäre Netzwerk Controller Knoten-Get-networkcontrollerreplica):
    1.  Ist Load Balancer (lb)-Engine mit SLBM verbunden? (*SLBM lbengine-Konfigurationen Gesamt* > 0)  
    2.  Kennt SLBM zumindest seine eigenen Endpunkte? (*VIP-Endpunkte Gesamt* > = 2)  
    3.  Sind Hyper-V-Hosts (DIP) mit SLBM verbunden? (*HP Clients verbunden* = = num Server)   
    4.  Ist SLBM mit muxes verbunden? (*Muxes* , die == *muxes bei SLBM* - == *muxes* , die fehlerfrei sind, fehlerfrei sind = # SLB muxes VMS).  
3.  Stellen Sie sicher, dass der konfigurierte BGP-Router erfolgreich ein Peering mit der SLB-MUX  
    1.  Bei Verwendung von RRAS mit Remote Zugriff (d. h. mit dem virtuellen BGP-Computer):  
        1.  "Get-bgppeer" sollte verbunden anzeigen  
        2.  "Get-bgprouteinformation" sollte mindestens eine Route für die SLBM-Self-VIP anzeigen.  
    2.  Wenn Sie den Tor-Switch (Top-of-Rack) als BGP-Peer verwenden, lesen Sie die Dokumentation.  
        1.  Beispiel: # Show BGP instance  
4.  Überprüfen der *slbmuxperfcounters* -und *slbmux* -Leistungsindikatoren in Perfmon auf dem virtuellen SLB MUX-Computer
5.  Überprüfen des Konfigurations Status und der VIP-Bereiche in der Software Load Balancer Manager  
    1.  Get-networkcontrollerloadbalancerconfiguration-ConnectionUri < https://<FQDN or IP>| ConvertTo-JSON-Tiefe 8 (überprüfen Sie die VIP-Bereiche in IP-Pools, und stellen Sie sicher, dass sich die SLBM-Self-VIP (*loadbalanacermanageripaddress*) und alle Mandanten seitigen VIPs innerhalb dieser Bereiche befinden.)  
        1. Get-networkcontrollerippool-NetworkID "< Public/Private VIP Logical Network Resource ID >"-Subnetz TID "< Public/Private VIP-Ressourcen-ID des logischen Subnetzes >"-ResourceId "<IP Pool Resource Id>"-ConnectionUri $URI | ConvertTo-JSON-Tiefe 8 
    2.  Debug-networkcontrollerconfigurationstate-  

Wenn eine der obigen Überprüfungen fehlschlägt, wird der SLB-Status des Mandanten auch in einem Fehler Modus angezeigt.  

**Wiederherstellungs **  
Beheben Sie basierend auf den folgenden Diagnoseinformationen Folgendes:  
* Sicherstellen, dass SLB-Multiplexer verbunden sind  
  * Beheben von Zertifikats Problemen  
  * Beheben von Netzwerkverbindungsproblemen  
* Sicherstellen, dass BGP-peeringinformationen erfolgreich konfiguriert wurden  
* Stellen Sie sicher, dass die Host-ID in der Registrierung der Serverinstanz-ID in der Server Ressource entspricht (Referenz Anhang für *hostnotconnected* -Fehlercode  
* Protokolle erfassen  

#### <a name="slbm-tenant-errors-hosting-service-provider--and-tenant-actions"></a>SLBM-Mandanten Fehler (hostingdienstanbieter-und Mandanten Aktionen)

1.  Hoster Überprüfen Sie *Debug-networkcontrollerconfigurationstate* , um festzustellen, ob LoadBalancer-Ressourcen einen Fehlerzustand aufweisen. Versuchen Sie, das Problem zu verringern, indem Sie die Tabelle mit den Aktions Elementen im Anhang befolgen   
    1.  Überprüfen, ob ein VIP-Endpunkt vorhanden ist und Routen Ankündigungen  
    2.  Überprüfen Sie, wie viele DIP-Endpunkte für den VIP-Endpunkt ermittelt wurden.  
2.  Tenant Überprüfen, Load Balancer Ressourcen korrekt angegeben sind  
    1.  Überprüfen von DIP-Endpunkten, die in SLBM registriert sind, sind hostingmandanten-VMS, die den IP-Konfigurationen des LoadBalancer-Back-End-Adress Pools entsprechen  
3.  Hoster Wenn DIP-Endpunkte nicht erkannt oder verbunden werden:   
    1.  Überprüfen von *Debug-networkcontrollerconfigurationstate*  
        1.  Überprüfen Sie, ob der NC-und SLB-Host-Agent erfolgreich mit dem Netzwerk Controller-Ereignis Koordinator verbunden ist ``netstat -anp tcp |findstr 6640)``  
    2.  Überprüfen Sie " *HostID* " im *nchostagent* -Dienst "RegKey" (Verweis " *hostnotconnected* " im Anhang) entspricht der Instanz-ID der entsprechenden Server Ressource (``Get-NCServer |convertto-json -depth 8``).  
    3.  Überprüfen Sie die Port Profil-ID für den Port des virtuellen Computers mit der Instanz-ID der zugehörigen NIC-Ressource   
4.  [Hostinganbieter] Protokolle erfassen   

#### <a name="slb-mux-tracing"></a>SLB-MUX-Ablauf Verfolgung

Informationen aus den Software Load Balancer muxes können auch durch Ereignisanzeige bestimmt werden. 
1. Klicken Sie im Menü "Ereignisanzeige Ansicht" auf "analytische und Debugprotokolle anzeigen".
2. Navigieren Sie zu "Anwendungs-und Dienst Protokolle" > Microsoft > Windows > slbmuxdriver > Trace in Ereignisanzeige 
3. Klicken Sie mit der rechten Maustaste darauf, und wählen Sie Protokoll aktivieren aus.

>[!NOTE]
>Es wird empfohlen, diese Protokollierung für kurze Zeit zu aktivieren, während Sie versuchen, ein Problem zu reproduzieren.

### <a name="vfp-and-vswitch-tracing"></a>VFP-und Vswitch-Ablauf Verfolgung

Auf allen Hyper-V-Hosts, die eine Gast-VM hosten, die mit einem virtuellen Mandanten Netzwerk verbunden ist, können Sie eine VFP-Ablauf Verfolgung sammeln, um zu bestimmen, wo Probleme auftreten können.

```
netsh trace start provider=Microsoft-Windows-Hyper-V-VfpExt overwrite=yes tracefile=vfp.etl report=disable provider=Microsoft-Windows-Hyper-V-VmSwitch 
netsh trace stop
netsh trace convert .\vfp.etl ov=yes 
```
