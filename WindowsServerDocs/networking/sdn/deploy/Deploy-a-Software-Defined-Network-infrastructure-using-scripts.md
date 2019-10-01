---
title: Bereitstellen einer Software definierten Netzwerkinfrastruktur mithilfe von Skripts
description: In diesem Thema wird beschrieben, wie Sie eine Microsoft-Sdn-Infrastruktur (Software Defined Network) mithilfe von Skripts in Windows Server 2016 bereitstellen.
manager: dougkim
ms.prod: windows-server
ms.service: virtual-network
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 5ba5bb37-ece0-45cb-971b-f7149f658d19
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: 29013827d0cde0447c48afa7a42551760ab9e940
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355995"
---
# <a name="deploy-a-software-defined-network-infrastructure-using-scripts"></a>Bereitstellen einer Software-Defined Networking-Infrastruktur mithilfe von Skripts

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema stellen Sie eine Microsoft-Sdn-Infrastruktur (Software Defined Network) mithilfe von Skripts bereit. Die Infrastruktur umfasst einen hochverfügbaren Netzwerk Controller (ha), eine SLB-/Mux (HA Software Load Balancer), virtuelle Netzwerke und zugehörige Access Control Listen (ACLs). Darüber hinaus stellt ein weiteres Skript eine Mandanten Arbeitsauslastung bereit, damit Sie Ihre Sdn-Infrastruktur überprüfen können.  

Wenn Sie möchten, dass Ihre mandantenworkloads außerhalb Ihrer virtuellen Netzwerke kommunizieren, können Sie SLB-NAT-Regeln, Site-to-Site-gatewaytunnel oder Layer-3-Weiterleitung einrichten, um zwischen virtuellen und physischen Workloads zu leiten.  

Sie können auch eine Sdn-Infrastruktur mithilfe von Virtual Machine Manager (VMM) bereitstellen. Weitere Informationen finden Sie unter [Einrichten einer Sdn-Infrastruktur (Software Defined Network) im VMM-Fabric](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-overview).  


## <a name="pre-deployment"></a>Vor der Bereitstellung  

> [!IMPORTANT]  
> Bevor Sie mit der Bereitstellung beginnen, müssen Sie Ihre Hosts und die physische Netzwerkinfrastruktur planen und konfigurieren. Weitere Informationen finden Sie unter [Planen einer Software-Defined Networking-Infrastruktur](../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md).  

Auf allen Hyper-V-Hosts muss Windows Server 2016 installiert sein.  

## <a name="deployment-steps"></a>Bereitstellungsschritte  
Beginnen Sie, indem Sie den virtuellen Hyper-v-Switch und die IP-Adresszuweisung für Hyper-v-Hosts konfigurieren. Jeder Speichertyp, der mit Hyper-V, Shared oder local kompatibel ist, kann verwendet werden.  

### <a name="install-host-networking"></a>Installieren von Host Netzwerken  

1. Installieren Sie die neuesten Netzwerktreiber, die für Ihre NIC-Hardware verfügbar sind.  
2. Installieren Sie die Hyper-v-Rolle auf allen Hosts (Weitere Informationen finden [Siehe Erste Schritte mit Hyper-v Windows Server 2016](https://docs.microsoft.com/windows-server/virtualization/hyper-v/get-started/Get-started-with-Hyper-V-on-Windows).   

   ```PowerShell
   Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart
   ```  

3. Erstellen Sie den virtuellen Hyper-V-Switch.<p>Verwenden Sie den gleichen Switchnamen für alle Hosts, z. b. **sdnswitch**. Konfigurieren Sie mindestens einen Netzwerkadapter, oder konfigurieren Sie bei Verwendung von Set mindestens zwei Netzwerkadapter. Die maximale eingehende Verteilung erfolgt bei Verwendung von zwei NICs.  

   ```PowerShell
   New-VMSwitch "<switch name>" -NetAdapterName "<NetAdapter1>" [, "<NetAdapter2>" -EnableEmbeddedTeaming $True] -AllowManagementOS $True
   ```  
   >[!TIP] 
   >Sie können die Schritte 4 und 5 überspringen, wenn Sie über separate Verwaltungs-NICs verfügen.

3. Informationen zum Abrufen der VLAN-ID des Verwaltungs-VLANs finden Sie im Thema zur Planung ([Planen einer Software-Defined Network-Infrastruktur](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)) und zusammenarbeiten mit Ihrem Netzwerkadministrator. Fügen Sie die Verwaltungs-vNIC des neu erstellten virtuellen Switches dem Verwaltungs-VLAN hinzu. Dieser Schritt kann ausgelassen werden, wenn in Ihrer Umgebung keine VLAN-Tags verwendet werden.  

   ```PowerShell
   Set-VMNetworkAdapterIsolation -ManagementOS -IsolationMode Vlan -DefaultIsolationID <Management VLAN> -AllowUntaggedTraffic $True
   ```  

4. Informationen zum Zuweisen einer IP-Adresse zur Verwaltungs-vNIC des neu erstellten vSwitches finden Sie im Thema zur Planung ([Planen einer Software-Defined Network-Infrastruktur](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)) und zusammenarbeiten mit Ihrem Netzwerkadministrator. Im folgenden Beispiel wird gezeigt, wie eine statische IP-Adresse erstellt und der Verwaltungs-vNIC des Vswitch zugewiesen wird:  

   ```PowerShell
   New-NetIPAddress -InterfaceAlias "vEthernet (<switch name>)" -IPAddress <IP> -DefaultGateway <Gateway IP> -AddressFamily IPv4 -PrefixLength <Length of Subnet Mask - for example: 24>
   ```  

5. Optionale Stellen Sie eine virtuelle Maschine auf dem Host Active Directory Domain Services bereit ([Installieren Sie Active Directory Domain Services (Stufe 100)](https://technet.microsoft.com/library/hh472162.aspx) und einen DNS-Server.  

    a. Verbinden Sie den virtuellen Computer für den Active Directory/DNS-Server mit dem Verwaltungs-VLAN:

       ```PowerShell
       Set-VMNetworkAdapterIsolation -VMName "<VM Name>" -Access -VlanId <Management VLAN> -AllowUntaggedTraffic $True  
       ```   

   b. Installieren Sie Active Directory Domain Services und DNS.  

   >[!NOTE]
   >Der Netzwerk Controller unterstützt Kerberos-und X. 509-Zertifikate für die Authentifizierung. In diesem Leitfaden werden beide Authentifizierungsmechanismen für verschiedene Zwecke verwendet (es ist jedoch nur eine erforderlich).  

6. Verknüpfen Sie alle Hyper-V-Hosts mit der Domäne. Stellen Sie sicher, dass der DNS-Server Eintrag für den Netzwerkadapter mit einer dem Verwaltungs Netzwerk zugewiesenen IP-Adresse auf einen DNS-Server verweist, der den Domänen Namen auflösen kann. 

   ```PowerShell   
   Set-DnsClientServerAddress -InterfaceAlias "vEthernet (<switch name>)" -ServerAddresses <DNS Server IP>  
   ```

   a. Klicken Sie mit der rechten Maustaste auf **Start**, klicken Sie auf **System**und dann auf **Einstellungen ändern**.  
   b. Klicken Sie auf **Ändern**.  
   c. Klicken Sie auf **Domäne** , und geben Sie den Domänen Namen  
   d. Klicken Sie auf **OK**.  
   e. Geben Sie bei entsprechender Aufforderung den Benutzernamen und das Kennwort ein.  
   f. Starten Sie den Server neu.  

### <a name="validation"></a>Überprüfung  
Mithilfe der folgenden Schritte können Sie überprüfen, ob das Host Netzwerk ordnungsgemäß eingerichtet ist.  

1. Stellen Sie sicher, dass der virtuelle Computer erfolgreich erstellt wurde:  

   ```PowerShell
   Get-VMSwitch "<switch name>"
   ```  

2. Vergewissern Sie sich, dass die Verwaltungs-vNIC auf dem VM-Switch mit dem Verwaltungs-VLAN verbunden ist:  

   >[!NOTE]
   >Nur relevant, wenn der Verwaltungs-und Mandanten Datenverkehr dieselbe NIC gemeinsam verwenden.    

   ```PowerShell
   Get-VMNetworkAdapterIsolation -ManagementOS
   ```

3. Überprüfen Sie alle Hyper-V-Hosts und externen Verwaltungsressourcen, z. b. DNS-Server.<p>Stellen Sie sicher, dass Sie über Ping über ihre Verwaltungs-IP-Adresse und/oder den voll qualifizierten Domänen Namen (FQDN) zugänglich sind.   

   ``ping <Hyper-V Host IP>``  
   ``ping <Hyper-V Host FQDN>``  

4. Führen Sie den folgenden Befehl auf dem Bereitstellungs Host aus, und geben Sie den FQDN jedes Hyper-V-Hosts an, um sicherzustellen, dass die verwendeten Kerberos-Anmelde Informationen Zugriff auf alle Server bieten.  

   ``winrm id -r:<Hyper-V Host FQDN>``  

### <a name="nano-installation-requirements-and-notes"></a>Nano-Installationsanforderungen und-Hinweise  

Wenn Sie nano als Hyper-V-Hosts (physische Server) für die Bereitstellung verwenden, müssen die folgenden zusätzlichen Anforderungen erfüllt sein:  

1. Alle Nano-Knoten müssen das DSC-Paket mit dem Language Pack installiert haben:  

   - Microsoft-NanoServer-DSC-Package. cab  
   - Microsoft-NanoServer-DSC-Package_en-US. cab

     ``dism /online /add-package /packagepath:<Path> /loglevel:4``  

2. Die Sdn Express-Skripts müssen von einem nicht-Nano-Host (Windows Server Core oder Windows Server w/GUI) ausgeführt werden. PowerShell-Workflows werden unter Nano nicht unterstützt.  

3. Das Aufrufen der Northbound-API des Netzwerk Controllers mithilfe von PowerShell oder NC-Rest-Wrapper (die auf "aufrufen-WebRequest" und "aufrufen-restmethod" basieren) muss von einem nicht-Nano-Host aus erfolgen.  


### <a name="run-sdn-express-scripts"></a>Ausführen von Sdn Express-Skripts  

1. Wechseln Sie zum [Microsoft Sdn GitHub-Repository](https://github.com/Microsoft/SDN.git) für die Installationsdateien.

2. Laden Sie die Installationsdateien aus dem Repository auf den angegebenen Bereitstellungs Computer herunter. Klicken Sie auf **Klonen oder herunterladen** und dann auf **ZIP herunterladen**.  

   >[!NOTE]
   >Auf dem angegebenen Bereitstellungs Computer muss Windows Server 2016 oder höher ausgeführt werden.

3. Erweitern Sie die ZIP-Datei, und kopieren Sie den Ordner **sdnexpress** in den Ordner `C:\` des Bereitstellungs Computers.  

4. Geben Sie den Ordner "`C:\SDNExpress`" als "**sdnexpress**" mit der Berechtigung an, **Lese-/Schreibzugriff** **zu erhalten** .  

5. Navigieren Sie zum Ordner "`C:\SDNExpress`".<p>Die folgenden Ordner werden angezeigt:  


   | Ordnername |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   |-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |  Agentconf  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   Enthält neue Kopien von ovsdb-Schemas, die vom Sdn-Host-Agent auf jedem Windows Server 2016 Hyper-V-Host zum Programmieren der Netzwerk Richtlinie verwendet werden.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |    Zertifikate    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         Temporärer frei gegebener Speicherort für die NC-Zertifikat Datei.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |   Abbilder    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         Leer, platzieren Sie Ihr Windows Server 2016 vhdx-Abbild hier.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |    Tools    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            Dienstprogramme für Problembehandlung und Debuggen.  Auf die Hosts und virtuellen Maschinen kopiert.  Es wird empfohlen, dass Sie hier Netzwerkmonitor oder wireshark platzieren, damit es bei Bedarf verfügbar ist.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
   |   Scripts   | Bereitstellungs Skripts.<br /><br />-   **sdnexpress. ps1**<br />    Stellt das Fabric bereit und konfiguriert es, einschließlich der virtuellen Computer des Netzwerk Controllers, der virtuellen SLB MUX-Computer, der gatewaypools und der virtuellen HNV-Gateway-Computer, die den Pools entsprechen.<br />-   **fabricconfig. psd1**<br />    Eine Konfigurationsdatei Vorlage für das sdnexpress-Skript.  Dies wird für Ihre Umgebung angepasst.<br />-   **sdnexpresstenant. ps1**<br />    Stellt eine Beispiel-Mandanten Arbeitsauslastung in einem virtuellen Netzwerk mit einer VIP mit Lastenausgleich bereit.<br />    Außerdem wird von eine oder mehrere Netzwerkverbindungen (IPSec S2S VPN, GRE, L3) auf den Edge-Gateways des Dienstanbieters bereitgestellt, die mit der zuvor erstellten Mandanten Arbeitsauslastung verbunden sind. Die IPSec-und GRE-Gateways sind für Konnektivität über die entsprechende VIP-IP-Adresse und das L3-Weiterleitungs Gateway über den entsprechenden Adresspool verfügbar.<br />    Dieses Skript kann auch verwendet werden, um die entsprechende Konfiguration mit einer Option zum Rückgängigmachen zu löschen.<br />-   **tenantconfig. psd1**<br />    Eine Vorlagen Konfigurationsdatei für die Mandanten Arbeitsauslastung und die S2S-Gatewaykonfiguration.<br />-   **sdnexpressundo. ps1**<br />    Bereinigt die Fabric-Umgebung und setzt Sie auf den Startzustand zurück.<br />-   **sdnexpressenterpriseexample. ps1**<br />    Stellt eine oder mehrere Unternehmens Standort Umgebungen mit einem Remote Zugriffs Gateway und (optional) einem entsprechenden virtuellen Unternehmens Computer pro Standort bereit. Die IPSec-oder GRE Enterprise-Gateways verbinden sich mit der entsprechenden VIP-IP-Adresse des Dienstanbieter Gateways, um die S2S-Tunnel einzurichten. Das L3-Weiterleitungs Gateway verbindet sich über die entsprechende Peer-IP-Adresse. <br />            Dieses Skript kann auch verwendet werden, um die entsprechende Konfiguration mit einer Option zum Rückgängigmachen zu löschen.<br />-   **enterpriseconfig. psd1**<br />    Eine Vorlagen Konfigurationsdatei für das Standort-zu-Standort-Gateway für Unternehmen und die Konfiguration der Client-VM. |
   | Tenantapps  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             Zum Bereitstellen von Beispiel-mandantenworkloads verwendete Dateien.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

   ---

6. Vergewissern Sie sich, dass sich die vhdx-Datei von Windows Server 2016 im Ordner **Images** befindet.  

7. Passen Sie die Datei "sdnexpress\script\fabricconfig.psd1" an, indem Sie die **< < ersetzen > >** Tags durch bestimmte Werte an Ihre Lab-Infrastruktur anpassen, einschließlich Hostnamen, Domänen Namen, Benutzernamen und Kenn Wörter sowie Netzwerkinformationen für das Netzwerke, die im Thema Planning Network aufgeführt sind.  

8. Erstellen Sie einen Host a-Datensatz in DNS für networkcontrollerrestname (vollständig) und networkcontrollerrestip.  

9. Führen Sie das Skript als Benutzer mit Anmelde Informationen des Domänen Administrators aus:  

   ``SDNExpress\scripts\SDNExpress.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  

10. Um alle Vorgänge rückgängig zu machen, führen Sie den folgenden Befehl aus:  

    ``SDNExpress\scripts\SDNExpressUndo.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  

#### <a name="validation"></a>Überprüfung  

Vorausgesetzt, dass das Sdn Express-Skript bis zum Abschluss ausgeführt wurde, ohne Fehler zu melden, können Sie den folgenden Schritt ausführen, um sicherzustellen, dass die fabricressourcen ordnungsgemäß bereitgestellt und für die Mandanten Bereitstellung  

Verwenden Sie [Diagnosetools](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack) , um sicherzustellen, dass keine Fehler in Fabric-Ressourcen im Netzwerk Controller vorhanden sind.  

   ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller Rest Name>``  


### <a name="deploy-a-sample-tenant-workload-with-the-software-load-balancer"></a>Bereitstellen einer Beispiel-Mandanten Arbeitsauslastung mit dem Software Load Balancer  

Nachdem nun Fabric-Ressourcen bereitgestellt wurden, können Sie die End-to-End-Bereitstellung Ihrer Sdn-Bereitstellung überprüfen Diese Mandanten Arbeitsauslastung besteht aus zwei virtuellen Subnetzen (webetier-und Datenbankebene), die über Access Control List-Regeln (ACL) mithilfe der verteilten Sdn-Firewall geschützt sind. Der Zugriff auf das virtuelle Subnetz der webeebene erfolgt über SLB/MUX mithilfe einer virtuellen IP-Adresse (VIP). Das Skript stellt automatisch zwei virtuelle Computer der webeebene und einen virtuellen Computer der Datenbankebene bereit und verbindet diese mit den virtuellen Subnetzen.  

1.  Passen Sie die Datei sdnexpress\script\tenantconfig.psd1 an, indem Sie die **< < ersetzen > >** Tags durch bestimmte Werte ändern (z. b.: VHD-Abbild Name, Netzwerk Controller-Rest-Name, Name des vswitchs usw., wie zuvor in der Datei fabricconfig. psd1 definiert)  

2.  Führen Sie das Skript aus. Zum Beispiel:  

    ``SDNExpress\scripts\SDNExpressTenant.ps1 -ConfigurationDataFile TenantConfig.psd1 -Verbose``  

3.  Um die Konfiguration rückgängig zu machen, führen Sie das gleiche Skript mit dem Parameter **Rückgängig** aus. Zum Beispiel:  

    ``SDNExpress\scripts\SDNExpressTenant.ps1 -Undo -ConfigurationDataFile TenantConfig.psd1 -Verbose``  

#### <a name="validation"></a>Überprüfung  

Gehen Sie folgendermaßen vor, um zu überprüfen, ob die Mandanten Bereitstellung erfolgreich war:

1. Melden Sie sich bei dem virtuellen Computer der Datenbankebene an, und versuchen Sie, die IP-Adresse eines der virtuellen Computer der webeebene zu pingen. (stellen Sie sicher, dass die Windows-Firewall auf virtuellen Computern der  

2. Überprüfen Sie die Netzwerk Controller-Mandanten Ressourcen auf Fehler. Führen Sie auf jedem Hyper-V-Host mit Layer-3-Konnektivität mit dem Netzwerk Controller Folgendes aus:  

   ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller REST Name>``

3. Um zu überprüfen, ob der Load Balancer ordnungsgemäß ausgeführt wird, führen Sie auf jedem Hyper-V-Host Folgendes aus:

   ``wget <VIP IP address>/unique.htm -disablekeepalive -usebasicparsing``

   Dabei ist `<VIP IP address>` die IP-Adresse der webeebene, die Sie in der Datei "tenantconfig. psd1" konfiguriert haben. 

   >[!TIP]
   >Suchen Sie in "tenantconfig. psd1" nach der Variablen "`VIPIP`".

   Führen Sie diese mehrerer-Zeiten aus, um den Lasten Ausgleichs Schalter zwischen den verfügbaren Dips anzuzeigen. Dieses Verhalten können Sie auch mithilfe eines Webbrowsers beobachten. Wechseln Sie zu `<VIP IP address>/unique.htm`. Schließen Sie den Browser, öffnen Sie eine neue Instanz, und suchen Sie dann erneut. Die blaue Seite und die grüne Seite werden angezeigt, es sei denn, der Browser speichert die Seite vor dem Timeout des Caches zwischen.

---