---
title: Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts
description: Dieses Thema behandelt das Bereitstellen eine Microsoft Software definierten Netzwerk (SDN)-Infrastruktur mithilfe von Skripts in Windows Server2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.service: virtual-network
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 5ba5bb37-ece0-45cb-971b-f7149f658d19
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4428ad73ab8933510d5a759ec4fa7377ea222ebd
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-a-software-defined-network-infrastructure-using-scripts"></a>Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Thema behandelt das Bereitstellen eine Microsoft Software definierten Netzwerk (SDN)-Infrastruktur mithilfe von Skripts. Die Infrastruktur umfasst einen mit hoher Verfügbarkeit (HA) Netzwerkcontroller, ein mit hoher Verfügbarkeit Software Load Balancer (SLB) / MUX, virtuelle Netzwerke und die zugehörigen Zugriffssteuerungslisten (ACLs). Darüber hinaus wird ein weiteres Skript eine mandantenarbeitslast Sie zur Bestätigung Ihrer SDN-Infrastruktur bereitgestellt.  
  
Wenn Sie Ihre mandantenarbeitsauslastungen außerhalb ihrer virtuellen Netzwerke kommunizieren möchten, können Sie zum Weiterleiten zwischen virtuellen und physischen Arbeitslasten SLB NAT-Regeln, Standort-zu-Standort-Gateway-Tunnel oder Layer-3-Weiterleitung festlegen.  
  
Sie können auch eine SDN-Infrastruktur mithilfe von Virtual Machine Manager (VMM) bereitstellen. Weitere Informationen finden Sie unter [richten Sie eine Software definierten Netzwerk (SDN)-Infrastruktur in VMM-Fabric](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-overview).  
  
## <a name="pre-deployment"></a>Vor der Bereitstellung  
  
> [!IMPORTANT]  
> Bevor Sie die Bereitstellung beginnen, müssen Sie planen und konfigurieren Ihren Hosts und physischen Netzwerkinfrastruktur. Weitere Informationen finden Sie unter [Planen einer Software definiert Netzwerkinfrastruktur](../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md).  
  
Alle Hyper-V-Hosts müssen Windows Server2016 installiert haben.  
  
## <a name="deployment-steps"></a>Zu den Bereitstellungsschritten  
Starten Sie durch die Konfiguration des Hyper-V-Hosts (physischen Servern) Hyper-V-Switch als auch IP-Adresszuweisung. Beliebige Speichertypen, die mit Hyper-V, gemeinsam genutzten oder lokalen kompatibel ist, kann verwendet werden.  
### <a name="install-host-networking"></a>Installieren von Host-Netzwerk  
1. Installieren Sie die neuesten Netzwerktreiber für Ihr NIC-Hardware verfügbar.  
2. Installieren der Hyper-V-Rolle auf allen Hosts (Weitere Informationen finden Sie unter [erste Schrittemit Hyper-V unter Windows Server2016](https://technet.microsoft.com/en-us/library/mt126159.aspx).   
  
   Ein Windows-PowerShellcommand an mit erhöhten Rechten:  
   ``Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart``  
    
    ein. Erstellen des virtuellen Hyper-V-Switch (verwenden Sie den gleichen Switch-Namen für alle Hosts. So: **SdnSwitch**). Konfigurieren Sie mindestens einen Netzwerkadapter oder, wenn Switch Embedded Teaming verwenden, konfigurieren Sie mindestens zwei Netzwerkadapter. Maximale eingehende Zuweisung erfolgt, wenn zwei NICs verwenden.  
 `` New-VMSwitch "<switch name>" -NetAdapterName "<NetAdapter1>" [, "<NetAdapter2>" -EnableEmbeddedTeaming $True] -AllowManagementOS $True``  
 
 >[!NOTE] 
 >Wenn Sie separate Management-NICs haben, können Sie die Schritte3 und 4 überspringen.

3. Finden Sie im Thema zur Planung ([Planen einer Software definiert Netzwerkinfrastruktur](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)) und arbeiten Sie mit Ihrem Netzwerkadministrator erhalten die VLAN-ID des VLAN-Management. Anfügen der Management-vNIC des neu erstellten virtuellen Switches für das Management VLAN. Dieser Schrittkann weggelassen werden, wenn Ihre Umgebung keine VLAN-Tags verwendet werden.  
 `` Set-VMNetworkAdapterIsolation -ManagementOS -IsolationMode Vlan -DefaultIsolationID <Management VLAN> -AllowUntaggedTraffic $True``  
 
4. Finden Sie im Thema zur Planung ([Planen einer Software definiert Netzwerkinfrastruktur](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)) und arbeiten Sie mit Ihrem Netzwerkadministrator entweder DHCP verwenden oder statische IP-Zuweisungen die vNIC Verwaltung des neu erstellten vSwitches eine IP-Adresse zuweisen. Das folgende Beispiel zeigt, wie Sie eine statische IP-Adresse zu erstellen und Zuweisen der Management-vNIC des vSwitches:  
 ``New-NetIPAddress -InterfaceAlias "vEthernet (<switch name>)" -IPAddress <IP> -DefaultGateway <Gateway IP> -AddressFamily IPv4 -PrefixLength <Length of Subnet Mask - for example: 24>``  
      
5. [Optional] Bereitstellen einer virtuellen Maschine zu Host Active Directory Domain Services ([installieren Sie Active Directory-Domänendienste (Stufe 100)](https://technet.microsoft.com/library/hh472162.aspx) und einen DNS-Server.  
   
    ein. Schließen Sie den virtuellen Computer von Active Directory und DNS-Server für das Management VLAN:
    
            Set-VMNetworkAdapterIsolation -VMName "<VM Name>" -Access -VlanId <Management VLAN> -AllowUntaggedTraffic $True  
   
   b. Installieren von Active Directory-Domänendienste und DNS.  
      >[!NOTE]
      >Netzwerkcontroller unterstützt sowohl Kerberos als auch x. 509-Zertifikate für die Authentifizierung. Dieses Handbuch verwendet beide Authentifizierungsmechanismen für unterschiedliche Zwecke (auch wenn nur eine erforderlich ist).  
        
6. Fügen Sie alle Hyper-V-Hosts zur Domäne hinzu. Vergewissern Sie sich den DNS-Server-Eintrag für den Netzwerkadapter, der IP-Adresse zugewiesen, die Netzwerk-Verwaltungspunkte an einen DNS-Server, der den Domänennamen aufgelöst werden können. Zum Beispiel:

        Set-DnsClientServerAddress -InterfaceAlias "vEthernet (<switch name>)" -ServerAddresses <DNS Server IP>  
   
   ein. Mit der rechten Maustaste **starten**, klicken Sie auf **System**, und klicken Sie dann auf **Einstellungen ändern**.  
   b. Klicken Sie auf **ändern**.  
   c. Klicken Sie auf **Domäne** und den Domänennamen angeben.  
   d. Klicken Sie auf **OK**.  
   e. Geben Sie Benutzername und Kennwort die Anmeldeinformationen des Benutzers bei entsprechender Aufforderung ein.  
   f. Starten Sie den Server neu.  
  
### <a name="validation"></a>Überprüfung  
Verwenden Sie die folgenden Schrittezum Überprüfen von diesem Host Netzwerk richtig eingerichtet ist.  
1. Stellen Sie sicher, dass die VM-Switch erfolgreich erstellt wurde:  
      
    ``Get-VMSwitch "<switch name>"``  
2. Stellen Sie sicher, dass die vNIC Management auf dem VM-Switch für die Verwaltung VLAN verbunden ist:  
    >[!NOTE]
    >Nur relevant, wenn Verwaltungs- und Mandanten-Datenverkehr dieselbe NIC Teilen    
      
    ``Get-VMNetworkAdapterIsolation -ManagementOS``  
3. Überprüfen, die alle Hyper-V-Hosts (und externen Management-Ressourcen, z.B.: DNS-Server) über Ping unter Verwendung der Verwaltung von IP-Adresse und/oder vollständig qualifizierten Domänennamen (FQDN) zugegriffen werden.   
      
   ``ping <Hyper-V Host IP>``  
   ``ping <Hyper-V Host FQDN>``  
4. Führen Sie den folgenden Befehl auf dem Host für die Bereitstellung aus, und geben Sie der vollqualifizierten Domänennamen der einzelnen Hyper-V-Hosts, um sicherzustellen, dass die Kerberos-Anmeldeinformationen verwendet, den Zugriff auf alle Server bereitgestellt.  
      
   ``winrm id -r:<Hyper-V Host FQDN>``  
      
### <a name="nano-installation-requirements-and-notes"></a>Anforderungen für die Installation von Nano und Notizen  
Wenn Sie Nano als Hyper-V-Hosts (physische Server) für die Bereitstellung verwenden, sind die folgenden zusätzlichen erforderlich:  
1. Alle Nano-Knoten müssen die DSC-Paket, das mit dem Language Pack installiert ist:  
   
   * Microsoft-NanoServer-DSC-Package.cab  
   * Microsoft-NanoServer-DSC-Package_en-us.cab
   
        ``dism /online /add-package /packagepath:<Path> /loglevel:4``  
2. Die Skripts SDN Express müssen von einem Nicht-Nano-Server (Windows Server Core oder Windows Server mit grafischer Benutzeroberfläche) ausgeführt werden. PowerShell-Workflows werden auf Nano nicht unterstützt.  
3.  Aufrufen der NorthBound-API von Netzwerkcontroller muss mithilfe von PowerShell oder NC-REST-Wrapper (die Invoke-WebRequest und Invoke-RestMethod abhängig) von einem Nicht-Nano-Host ausgeführt wird.  
   
         
### <a name="run-sdn-express-scripts"></a>Führen Sie Express SDN-Skripts  
  
1.  Die Installationsdateien befinden sich auf GitHub. Herunterladen die ZIP-Datei aus der [Microsoft-SDN-GitHub-Repository](https://github.com/Microsoft/SDN.git). Klicken Sie auf der Seite der Microsoft-SDN-Repository auf **Klon oder eine Download**, und klicken Sie dann auf **Download ZIP**.  
  
2.  Definieren Sie einen Computer als Bereitstellung-PC.  Dieser Computer muss Windows Server2016 ausgeführt werden. Erweitern Sie die ZIP-Datei und eine Kopie der **SDNExpress** Ordner auf dem Bereitstellungscomputer `C:\`Ordner.  
  
3.  Freigeben der `C:\SDNExpress`Ordner wie "**SDNExpress**" mit der Berechtigung für **jeder** auf **Lese-/Schreibzugriff**.  
  
4.  Navigieren Sie zu den `C:\SDNExpress`Ordner.

 Sie sehen die folgenden Ordner:  

|Name des Ordners|Beschreibung|  
|---------------|---------------|  
|AgentConf|Enthält neue Kopien von SDN-Host-Agent auf jedem Windows Server2016 Hyper-V-Host zum Programm Netzwerkrichtlinie verwendeten OVSDB-Schemas.|  
|Zertifikate|Temporärer freigegebenen Speicherort für die NC-Zertifikatdatei.|  
|Bilder|Leere, setzen Sie das Vhdx-Image von Windows Server2016 hier|  
|Tools|Dienstprogramme für die Problembehandlung und Debuggen.  Auf den Hosts und virtuellen Maschinen kopiert.  Es wird empfohlen, dass Sie den Netzwerkmonitor oder Wireshark hier platzieren, daher es möglich ist, falls erforderlich.|  
|Skripts|Bereitstellungsskripts.<br /><br />-   **SDNExpress.ps1**<br />    Bereitstellen, und konfigurieren das Fabric, einschließlich der virtuellen Maschinen im Netzwerk-Controller, SLB Mux-VMs, Gateway-Pools und Hyper-v-Gateway-VMs, die Pools entspricht.<br />-   **FabricConfig.psd1**<br />    Eine Datei Konfigurationsvorlage für das Skript SDNExpress.  Dies wird für Ihre Umgebung angepasst werden.<br />-   **SDNExpressTenant.ps1**<br />    Stellt eine Beispiel für Mandanten Arbeitslast auf einem virtuellen Netzwerk mit einem Lastenausgleich VIP bereit.<br />    Auch stellt eine oder mehrere Netzwerkverbindungen (IPsec-S2S-VPN-, GRE, L3) auf die Service-Anbieter-Edge-Gateways, der mit der zuvor erstellten Mandanten Arbeitslast verbunden sind. IPsec und GRE-Gateways sind über die entsprechende VIP-IP-Adresse und das weiterleitungsgateway L3-über den entsprechenden-Adresspool für die Konnektivität zur Verfügung.<br />    Dieses Skript kann verwendet werden, um die entsprechende Konfiguration mit der Option "Rückgängig" auch löschen.<br />-   **TenantConfig.psd1**<br />    Eine Vorlagenkonfigurationsdatei für Mandanten Arbeitsauslastung und S2S-Gateway-Konfiguration.<br />-   **SDNExpressUndo.ps1**<br />    Die Fabric-Umgebung bereinigt und wird es auf eine Anfangszustand zurückgesetzt.<br />-   **SDNExpressEnterpriseExample.ps1**<br />    Stellt eine oder mehrere Standort Unternehmensumgebungen mit einem Remote-Access-Gateway und (optional) eine entsprechende Enterprise virtuelle Computer pro Standort bereit. Die Enterprise-Gateways IPsec oder GRE eine Verbindung mit der entsprechenden VIP IP-Adresse des dienstanbietergateways der S2S-Tunnel herstellen. L3-Forwarding Gateway, die über die entsprechenden Peer-IP-Adresse hergestellt werden. <br />            Dieses Skript kann verwendet werden, um die entsprechende Konfiguration mit der Option "Rückgängig" auch löschen.<br />-   **EnterpriseConfig.psd1**<br />    Eine Vorlagenkonfigurationsdatei für die Unternehmens-Standort-zu-Standort-Gateway und Client-VM-Konfiguration.|  
|TenantApps|Dateien, die zum Bereitstellen von mandantenworkloads Beispiel verwendet werden.|  
  
5.  Überprüfen Sie, ob die Windows Server2016 VHDX-Datei die **Bilder** Ordner.  
  
6. Anpassen der SDNExpress\scripts\FabricConfig.psd1-Datei durch Ändern der **<< Ersetzen >>** Tags mit bestimmten Werten zum Anpassen Ihrer Lab-Infrastruktur einschließlich Hostnamen, Domänennamen, Benutzernamen und Kennwörter und Netzwerkinformationen für die Netzwerke im Thema Planen von Netzwerk aufgeführt.  
7. Erstellen Sie einen Hosteintrag A in DNS für die NetworkControllerRestName (FQDN) und NetworkControllerRestIP.  
8. Führen Sie das Skript als Benutzer mit Domänenadministrator-Anmeldeinformationen:  
      
    ``SDNExpress\scripts\SDNExpress.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  
      
9.  Um alle Vorgänge rückgängig zu machen, führen Sie den folgenden Befehl ein:  
      
    ``SDNExpress\scripts\SDNExpressUndo.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  
      
#### <a name="validation"></a>Überprüfung  
Vorausgesetzt, dass das Skript SDN Express abgeschlossen wurde ohne Fehler melden, können Sie den folgenden Schrittaus, um sicherzustellen, dass die fabricressourcen ordnungsgemäß bereitgestellt wurde und stehen für die Mandanten-Bereitstellung ausführen.  

- Verwendung [Diagnoseprogramm](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack) um sicherzustellen, dass es keine Fehler auf die fabricressourcen im Netzwerkcontroller.  
      
    ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller Rest Name>``  
        
   
### <a name="deploy-a-sample-tenant-workload-with-the-software-load-balancer"></a>Bereitstellen Sie eine Beispiel für die Mandanten-Arbeitslast mit des Software Load Balancers  
    
Nun, dass die Fabric-Ressourcen bereitgestellt wurden, können Sie Ihre SDN Bereitstellung End-to-End durch Bereitstellen einer Beispiel-Mandanten-Arbeitslast überprüfen. Diese Arbeitsauslastung Mandanten besteht aus zwei virtuellen Subnetz (Webebene und Datenbank-Ebene) über die Zugriffssteuerungsliste (ACL) Regeln, die Verwendung der SDN verteilten Firewall geschützt. Die Webebene virtuelle Subnetz ist über die Verwendung einer virtuellen IP-Adresse (VIP)-Adresse SLB/MUX verfügbar. Das Skript stellt zwei Web Ebene virtuelle Maschinen und eine Datenbank-Ebene virtuelle Maschine automatisch und verbindet diese in den virtuellen Subnetzen.  
  
1.  Anpassen der SDNExpress\scripts\TenantConfig.psd1-Datei durch Ändern der **<< Ersetzen >>** Tags mit bestimmten Werten (z.B.: VHD-Image Name, REST-Name des Domänencontrollers für Netzwerk, vSwitch Namen usw. wie zuvor in der Datei FabricConfig.psd1 definiert)  
2.  Führen Sie das Skript. Zum Beispiel:  
``SDNExpress\scripts\SDNExpressTenant.ps1 -ConfigurationDataFile TenantConfig.psd1 -Verbose``  
3.  Führen Sie die Konfiguration rückgängig machen, dasselbe Skript mit der **Rückgängig** Parameter. Zum Beispiel:  
``SDNExpress\scripts\SDNExpressTenant.ps1 -Undo -ConfigurationDataFile TenantConfig.psd1 -Verbose``  

#### <a name="validation"></a>Überprüfung  
Um zu überprüfen, dass die Mandanten-Bereitstellung erfolgreich war, führen Sie folgende Schritteaus:
1.  Melden Sie sich bei der Virtual Machine der Datenbank-Ebene, und versuchen Sie, die IP-Adresse eines Web-Ebene virtuellen Computer pingen (Stellen Sie sicher, dass Windows-Firewall im Web Ebene virtuelle Computer ausgeschaltet ist).  
2.  Überprüfen Sie die Controller-Mandanten-Netzwerkressourcen auf Fehler. Führen Sie Folgendes auf jedem Hyper-V-Host mit Layer-3-Konnektivität mit dem Netzwerkcontroller:  
      
    ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller REST Name>``
3. Um sicherzustellen, dass das Lastenausgleichsmodul ordnungsgemäß ausgeführt wird, führen Sie Folgendes auf jedem Hyper-V-Host:
    
        wget <VIP IP address>/unique.htm -disablekeepalive -usebasicparsing
   
   Wo `<VIP IP address>`der Webebene VIP-IP-Adresse, die Sie in der Datei TenantConfig.psd1 konfiguriert ist. Suchen Sie nach der `VIPIP`in TenantConfig.psd1 Variablen.

   Führen Sie dieses Mal verschachteln zum Wechseln zwischen den verfügbaren DIP Lastenausgleich finden Sie unter. Sie können dieses Verhalten mit einem Webbrowser auch verfolgen. Navigieren Sie zu `<VIP IP address>/unique.htm`. Schließen Sie den Browser, und öffnen Sie eine neue Instanz, und navigieren Sie erneut. Die blauen Seiten und grüne alternativen, außer wenn der Browser die Seite werden zwischengespeichert, bevor ein Timeout für der Cache wird angezeigt.