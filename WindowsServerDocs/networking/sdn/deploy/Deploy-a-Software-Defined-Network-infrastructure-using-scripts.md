---
title: Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts
description: In diesem Thema wird beschrieben, wie eine Software Defined Network (SDN) von Microsoft-Infrastruktur mithilfe von Skripts in Windows Server 2016 bereitstellen wird.
manager: dougkim
ms.prod: windows-server-threshold
ms.service: virtual-network
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 5ba5bb37-ece0-45cb-971b-f7149f658d19
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: ce88659f6065ddd0957b95831a4e3065f09dc9e9
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446372"
---
# <a name="deploy-a-software-defined-network-infrastructure-using-scripts"></a>Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema stellen Sie eine Software Defined Network (SDN) von Microsoft-Infrastruktur mithilfe von Skripts bereit. Die Infrastruktur umfasst einen hoher Verfügbarkeit (HA) vom Netzwerkcontroller, einen HA Software Load Balancer (SLB) / MUX, virtuelle Netzwerke und die zugehörigen Zugriffssteuerungslisten (ACLs). Darüber hinaus stellt ein weiteres Skript eine mandantenarbeitslast Sie zur Überprüfung Ihrer SDN-Infrastruktur.  

Wenn Sie die arbeitsauslastungen Ihrer Mandanten außerhalb von ihren virtuellen Netzwerken kommunizieren möchten, können Sie die SLB-NAT-Regeln, Standort-zu-Standort-Gateway-Tunnel oder Layer-3-Weiterleitung zum Weiterleiten von zwischen virtuellen und physischen Workloads einrichten.  

Sie können auch eine SDN-Infrastruktur mit Virtual Machine Manager (VMM) bereitstellen. Weitere Informationen finden Sie unter [richten Sie eine Infrastruktur (Software Defined Network, SDN) im VMM-Fabric](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-overview).  


## <a name="pre-deployment"></a>Vor der Bereitstellung  

> [!IMPORTANT]  
> Vor der Bereitstellung, müssen Sie planen und konfigurieren Sie Ihren Hosts und der physischen Netzwerkinfrastruktur. Weitere Informationen finden Sie unter [Planen einer Software-Defined Networking-Infrastruktur](../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md).  

Alle Hyper-V-Hosts müssen Windows Server 2016 installiert haben.  

## <a name="deployment-steps"></a>Bereitstellungsschritte  
Zunächst konfigurieren die Hyper-V-Hosts (physische Server) Hyper-V virtual Switch und IP-Adresszuweisung. Jeder Storage-Typ, der mit Hyper-V, freigegebenen oder lokalen kompatibel ist, kann verwendet werden.  

### <a name="install-host-networking"></a>Installieren Sie Hostnetzwerk  

1. Installieren Sie die neuesten Netzwerktreiber für die NIC-Hardware zur Verfügung.  
2. Installieren der Hyper-V-Rolle auf allen Hosts (Weitere Informationen finden Sie unter [erste Schritte mit Hyper-V unter Windows Server 2016](https://docs.microsoft.com/windows-server/virtualization/hyper-v/get-started/Get-started-with-Hyper-V-on-Windows).   

   ```PowerShell
   Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart
   ```  

3. Erstellen Sie den virtuellen Hyper-V-Switch.<p>Verwenden Sie den gleichen Parameternamen für alle Hosts, z. B. **SdnSwitch**. Konfigurieren Sie mindestens einen Netzwerkadapter oder, wenn SET zu verwenden, konfigurieren Sie mindestens zwei Netzwerkadapter. Maximale Zuweisung von eingehenden tritt auf, wenn Sie zwei Netzwerkkarten verwenden.  

   ```PowerShell
   New-VMSwitch "<switch name>" -NetAdapterName "<NetAdapter1>" [, "<NetAdapter2>" -EnableEmbeddedTeaming $True] -AllowManagementOS $True
   ```  
   >[!TIP] 
   >Sie können die Schritte 4 und 5 überspringen, wenn Sie separate Management NICs verfügen.

3. Im Thema zur Planung finden Sie unter ([Planen einer Software Defined Networking-Infrastruktur](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)) und das Arbeiten mit Ihrem Netzwerkadministrator die VLAN-ID des VLAN Management zu erhalten. Fügen Sie die vNIC Verwaltung des neu erstellten virtuellen Switches, mit dem Management-VLAN. Dieser Schritt kann ausgelassen werden, wenn Ihre Umgebung keine VLAN-Tags verwendet.  

   ```PowerShell
   Set-VMNetworkAdapterIsolation -ManagementOS -IsolationMode Vlan -DefaultIsolationID <Management VLAN> -AllowUntaggedTraffic $True
   ```  

4. Im Thema zur Planung finden Sie unter ([Planen einer Software Defined Networking-Infrastruktur](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)) und das Arbeiten mit Ihrem Netzwerkadministrator verwenden Sie entweder DHCP oder statischen IP-Adresszuweisungen die vNIC Verwaltung des neu erstellten IP-Adresse zuweisen vSwitch. Im folgende Beispiel veranschaulicht das Erstellen einer statischen IP-Adresse und der vNIC Verwaltung des vSwitches zuweisen:  

   ```PowerShell
   New-NetIPAddress -InterfaceAlias "vEthernet (<switch name>)" -IPAddress <IP> -DefaultGateway <Gateway IP> -AddressFamily IPv4 -PrefixLength <Length of Subnet Mask - for example: 24>
   ```  

5. [Optional] Bereitstellen eines virtuellen Computers zum Hosten von Active Directory Domain Services ([Install Active Directory Domain Services (Stufe 100)](https://technet.microsoft.com/library/hh472162.aspx) und einen DNS-Server.  

    a. Verbinden Sie die Active Directory-/DNS-Server-VM mit dem Management-VLAN:

       ```PowerShell
       Set-VMNetworkAdapterIsolation -VMName "<VM Name>" -Access -VlanId <Management VLAN> -AllowUntaggedTraffic $True  
       ```   

   b. Installieren von Active Directory-Domänendienste und DNS.  

   >[!NOTE]
   >Die Netzwerkcontroller unterstützt sowohl Kerberos als auch x. 509-Zertifikate für die Authentifizierung. Dieses Handbuch verwendet beide Authentifizierungsmechanismen für unterschiedliche Zwecke, (obwohl nur eine erforderlich ist).  

6. Verknüpfen Sie alle Hyper-V-Hosts mit der Domäne. Vergewissern Sie sich den DNS-Server-Eintrag für den Netzwerkadapter, der IP-Adresse zugewiesen, der Netzwerk-Verwaltungspunkt mit einem DNS-Server, der den Domänennamen auflösen können. 

   ```PowerShell   
   Set-DnsClientServerAddress -InterfaceAlias "vEthernet (<switch name>)" -ServerAddresses <DNS Server IP>  
   ```

   a. Mit der rechten Maustaste **starten**, klicken Sie auf **System**, und klicken Sie dann auf **Change Settings**.  
   b. Klicken Sie auf **Ändern**.  
   c. Klicken Sie auf **Domäne** und den Domänennamen angeben.  
   d. Klicken Sie auf **OK**.  
   e. Geben Sie Namen und das Kennwort die Anmeldeinformationen des Benutzers bei Aufforderung ein.  
   f. Starten Sie den Server neu.  

### <a name="validation"></a>Überprüfung  
Verwenden Sie die folgenden Schritte aus, um zu überprüfen, Host, Netzwerk ordnungsgemäß installiert wurde.  

1. Stellen Sie sicher, dass die VM-Switch erfolgreich erstellt wurde:  

   ```PowerShell
   Get-VMSwitch "<switch name>"
   ```  

2. Stellen Sie sicher, dass die vNIC Management auf dem VM-Switch mit dem Management-VLAN verbunden ist:  

   >[!NOTE]
   >Nur relevant, wenn Verwaltungs- und Mandanten-Datenverkehr dieselbe NIC Teilen    

   ```PowerShell
   Get-VMNetworkAdapterIsolation -ManagementOS
   ```

3. Überprüfen Sie alle Hyper-V-Hosts und -Verwaltung externer Ressourcen, z. B. DNS-Server.<p>Stellen Sie sicher, dass sie über Ping mithilfe ihrer Verwaltungs-IP-Adresse bzw. den vollständig qualifizierten Domänennamen (FQDN) zugegriffen werden kann.   

   ``ping <Hyper-V Host IP>``  
   ``ping <Hyper-V Host FQDN>``  

4. Führen Sie den folgenden Befehl auf dem Bereitstellungshost aus, und geben Sie der FQDN der einzelnen Hyper-V-Hosts, um sicherzustellen, dass die Kerberos-Anmeldeinformationen, die zum Zugriff auf alle Server bereitstellt.  

   ``winrm id -r:<Hyper-V Host FQDN>``  

### <a name="nano-installation-requirements-and-notes"></a>Nano-Installationsanforderungen und Anmerkungen zu dieser Version  

Wenn Sie Nano als Hyper-V-Hosts (physische Server) für die Bereitstellung verwenden, gelten folgende zusätzliche Anforderungen:  

1. Alle Nano-Knoten müssen das DSC-Paket, die mit dem Language Pack installiert ist:  

   - Microsoft-NanoServer-DSC-Package.cab  
   - Microsoft-NanoServer-DSC-Package_en-us.cab

     ``dism /online /add-package /packagepath:<Path> /loglevel:4``  

2. Die Skripts mit SDN Express müssen von einem nicht-Nano-Host (Windows Server Core oder Windows Server mit grafischer Benutzeroberfläche) ausgeführt werden. PowerShell-Workflows werden auf Nano nicht unterstützt.  

3. Die NorthBound-API von Netzwerkcontroller aufrufen muss mithilfe von PowerShell oder der NC-REST-Wrapper (mit Invoke-WebRequest "und" Invoke-RestMethod abhängen) von einem nicht-Nano-Host ausgeführt werden.  


### <a name="run-sdn-express-scripts"></a>Ausführen von Skripts mit SDN Express  

1. Wechseln Sie zu der [Microsoft SDN GitHub-Repository](https://github.com/Microsoft/SDN.git) für die Installationsdateien.

2. Herunterladen der Installationsdateien aus dem Repository auf dem Bereitstellungscomputer der angegebenen. Klicken Sie auf **Klonen oder herunterladen** , und klicken Sie dann auf **Download ZIP**.  

   >[!NOTE]
   >Die angegebene Bereitstellungscomputer muss WindowsServer 2016 oder höher ausgeführt werden.

3. Erweitern Sie die Zip-Datei, und kopieren die **SDNExpress** Ordner auf des Bereitstellungscomputer `C:\` Ordner.  

4. Freigabe der `C:\SDNExpress` Ordner wie "**SDNExpress**" mit der Berechtigung für **jeder** zu **Lese-/Schreibzugriff**.  

5. Navigieren Sie zu der `C:\SDNExpress` Ordner.<p>Sie finden Sie in den folgenden Ordnern:  


   | Ordnername |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   |-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |  AgentConf  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   Enthält neue Exemplare OVSDB Schemas, die von den SDN-Host-Agent auf jedem Windows Server 2016 Hyper-V-Host zum Programm Netzwerkrichtlinie verwendet.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |    Zertifikate    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         Temporärer freigegebenen Speicherort für die NC-Zertifikatsdatei.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |   Abbilder    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         Leere, setzen Sie hier Ihre Vhdx-Abbild von Windows Server 2016                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |    Tools    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            Dienstprogramme für die Problembehandlung und Debuggen.  Für die Hosts und virtuelle Computer kopiert.  Es wird empfohlen, dass Sie den Netzwerkmonitor oder Wireshark hier platzieren, damit sie bei Bedarf verfügbar ist.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
   |   Scripts   | Bereitstellungsskripts.<br /><br />-   **SDNExpress.ps1**<br />    Bereitgestellt wird, und konfiguriert das Fabric, einschließlich der virtuellen Maschinen von des Netzwerkcontrollers, virtuellen SLB Mux-Maschinen, Gateway-Pools und der HNV-Gateway virtuellen Computer, die für die Empfangsfunktionen.<br />-   **FabricConfig.psd1**<br />    Eine Datei Konfigurationsvorlage für das Skript SDNExpress.  Dies wird für Ihre Umgebung angepasst werden.<br />-   **SDNExpressTenant.ps1**<br />    Stellt eine mandantenarbeitslast Beispiel, in einem virtuellen Netzwerk eine Lastenausgleich-VIP-Adresse bereit.<br />    Auch stellt ein oder mehr Netzwerkverbindungen (IPSec-S2S-VPN, GRE, L3) bereit, auf den Service-Anbieter Edge-Gateways, die mit der zuvor erstellten mandantenarbeitslast verbunden sind. Die IPSec- und GRE-Gateways sind über die entsprechenden VIP-IP-Adresse und der L3-weiterleitungs-Gateway für Verbindungen verfügbar, über die entsprechenden-Adresspool.<br />    Dieses Skript kann zum Löschen der entsprechenden Konfigurations mit einer Rückgängig-Option auch verwendet werden.<br />-   **TenantConfig.psd1**<br />    Eine Vorlage-Konfigurationsdatei für Workloads von Mandanten und S2S-Gateway-Konfiguration.<br />-   **SDNExpressUndo.ps1**<br />    Bereinigt die Fabric-Umgebung, und klicken Sie auf einen Anfangszustand zurückgesetzt wird.<br />-   **SDNExpressEnterpriseExample.ps1**<br />    Stellt eine oder mehrere Standort unternehmensumgebungen mit einem Remote-Access-Gateway und (optional) eine entsprechende Enterprise-VM pro Standort bereit. Die IPSec oder GRE-Enterprise-Gateways eine Verbindung mit der entsprechenden VIP-IP-Adresse des dienstanbietergateways die S2S-Tunnel herstellen. Der L3-Gateway weitergeleitet, die über die entsprechenden Peer-IP-Adresse hergestellt werden. <br />            Dieses Skript kann zum Löschen der entsprechenden Konfigurations mit einer Rückgängig-Option auch verwendet werden.<br />-   **EnterpriseConfig.psd1**<br />    Eine Vorlage-Konfigurationsdatei für den Enterprise-Standort-zu-Standort-Gateway und die Client-VM-Konfiguration. |
   | TenantApps  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             Dateien, die zum Bereitstellen von mandantenworkloads Beispiel verwendet werden.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

   ---

6. Überprüfen Sie, ob die Windows Server 2016-VHDX-Datei die **Images** Ordner.  

7. Anpassen die Datei SDNExpress\scripts\FabricConfig.psd1 durch Ändern der **<< Ersetzen >>** Tags mit bestimmten Werten Ihrer Lab-Infrastruktur, einschließlich von Hostnamen, Domänennamen, Benutzernamen und Kennwörtern, anpassen und Informationen zum Netzwerk für die Netzwerke, die im Thema Planen von Netzwerk aufgeführt.  

8. Erstellen Sie einen Host A-Eintrag im DNS für die NetworkControllerRestName (FQDN) und NetworkControllerRestIP.  

9. Führen Sie das Skript als Benutzer mit Domänenadministrator-Anmeldeinformationen:  

   ``SDNExpress\scripts\SDNExpress.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  

10. Wenn alle Vorgänge rückgängig machen möchten, führen Sie den folgenden Befehl aus:  

    ``SDNExpress\scripts\SDNExpressUndo.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  

#### <a name="validation"></a>Überprüfung  

Vorausgesetzt, dass das Skript mit SDN Express bis zum Abschluss ausgeführt, ohne Fehler meldet, können Sie den folgenden Schritt aus, um sicherzustellen, dass Fabric-Ressourcen wurden ordnungsgemäß bereitgestellt und stehen für die mandantenbereitstellung durchführen.  

Verwendung [Diagnosetools](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack) um sicherzustellen, dass auf jedem Fabric-Ressourcen im Netzwerkcontroller keine Fehler vorhanden sind.  

   ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller Rest Name>``  


### <a name="deploy-a-sample-tenant-workload-with-the-software-load-balancer"></a>Bereitstellen einer beispielworkload eine Mandanten mit den Software Load balancer  

Nun, dass Fabric-Ressourcen bereitgestellt wurden, können Sie Ihre SDN-Bereitstellung End-to-End durch Bereitstellen einer beispielworkload eine Mandanten überprüfen. Diese Mandanten-arbeitsauslastung besteht aus zwei virtuelle Subnetze (Web- und Datenbankebene) über die Zugriffssteuerungsliste (ACL)-Regeln, die mit der verteilte SDN-Firewall geschützt. Die Webschicht-Subnetz ist über die SLB/MUX-unter Verwendung einer virtuellen IP-Adresse (VIP) Adresse zugänglich. Das Skript wird automatisch bereitgestellt werden, zwei virtuelle Computer der Webebene und eine virtuelle Maschine für eine Datenbank-Ebene und verbindet diese mit den virtuellen Subnetzen.  

1.  Anpassen die Datei SDNExpress\scripts\TenantConfig.psd1 durch Ändern der **<< Ersetzen >>** Tags mit bestimmten Werten (z. B.: VHD-Image-Name, netzwerkcontrollername REST, vSwitch Namen usw. wie zuvor in der Datei FabricConfig.psd1 definiert)  

2.  Führen Sie das Skript ein. Zum Beispiel:  

    ``SDNExpress\scripts\SDNExpressTenant.ps1 -ConfigurationDataFile TenantConfig.psd1 -Verbose``  

3.  Führen Sie die Konfiguration rückgängig machen, die das gleiche Skript mit dem **Rückgängig** Parameter. Zum Beispiel:  

    ``SDNExpress\scripts\SDNExpressTenant.ps1 -Undo -ConfigurationDataFile TenantConfig.psd1 -Verbose``  

#### <a name="validation"></a>Überprüfung  

Um zu überprüfen, dass die mandantenbereitstellung erfolgreich war, führen Sie folgende Schritte aus:

1. Melden Sie sich bei den virtuellen Datenbankcomputer Tarif und pingen Sie die IP-Adresse eines der virtuellen Computer der Webebene (Stellen Sie sicher, dass die Windows-Firewall im virtuellen Computer der Webebene deaktiviert ist).  

2. Überprüfen Sie die Controller-Mandanten-Netzwerkressourcen für alle Fehler an. Führen Sie den folgenden von jedem Hyper-V-Host mit Layer-3-Konnektivität und den Netzwerkcontroller:  

   ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller REST Name>``

3. Um sicherzustellen, dass der Load Balancer ordnungsgemäß ausgeführt wird, führen Sie den folgenden von jedem Hyper-V-Host aus:

   ``wget <VIP IP address>/unique.htm -disablekeepalive -usebasicparsing``

   wo `<VIP IP address>` der Webebene VIP-IP-Adresse, die Sie in der Datei TenantConfig.psd1 konfiguriert ist. 

   >[!TIP]
   >Suchen Sie nach der `VIPIP` TenantConfig.psd1 Variable.

   Führen Sie diese mehreren Male auf, um den Lastenausgleich zwischen den verfügbaren DIPs wechseln, finden Sie unter. Sie können dieses Verhalten mithilfe eines Webbrowsers auch beobachten. Wechseln Sie zu `<VIP IP address>/unique.htm`. Schließen Sie den Browser und öffnen Sie eine neue Instanz, und navigieren Sie erneut. Sehen Sie die Seite "Blau" und die grüne Seite alternativen, außer wenn der Browser die Seite zwischenspeichert, bevor das Zeitlimit für des Caches.

---