---
title: Bereitstellen eines Windows Admin Center-Gateways in Azure
description: Wie Sie ein Windows Admin Center-Gateway in Azure bereitstellen
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: a3fa1838096d910505faf9a2c5bd819b3a256fe2
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280419"
---
# <a name="deploy-windows-admin-center-in-azure"></a>Bereitstellen von Windows Admin Center in Azure

## <a name="deploy-using-script"></a>Bereitstellen mithilfe von Skripts

Sie können [bereitstellen – WACAzVM.ps1](https://aka.ms/deploy-wacazvm) das Ausführen von [Azure Cloud Shell](https://shell.azure.com) zum Einrichten eines Windows Admin Center-Gateways in Azure. Dieses Skript kann die gesamte Umgebung, einschließlich der Ressourcengruppe erstellen.

[Fahren Sie mit Schritten zur manuellen Bereitstellung](#deploy-manually-on-an-existing-azure-virtual-machine)

### <a name="prerequisites"></a>Vorraussetzungen

* Einrichten Ihres Kontos in [Azure Cloud Shell](https://shell.azure.com). Wenn dies zum ersten Mal verwenden Cloud Shell ist, werden Sie aufgefordert werden zugeordnet, oder erstellen ein Azure Storage-Konto mit Cloud Shell.
* In einem **PowerShell** Cloud Shell, navigieren Sie zu Ihrem Basisverzeichnis: ```PS Azure:\> cd ~```
* Zum Hochladen der ```Deploy-WACAzVM.ps1``` Datei, Drag & drop auf dem lokalen Computer an einem beliebigen Standort in der Cloud Shell-Fensters.

Wenn Sie Ihr eigenes Zertifikat angeben:

* Hochladen des Zertifikats auf [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis). Erstellen eines schlüsseltresors im Azure-Portal zunächst, laden Sie das Zertifikat in den schlüsseltresor hoch. Alternativ können Sie Azure-Portal, um ein Zertifikat für Sie generieren.

### <a name="script-parameters"></a>Skriptparameter

* **ResourceGroupName** -[String] Gibt den Namen der Ressourcengruppe, in dem der virtuelle Computer erstellt werden.

* **Namen** -[String] Gibt den Namen des virtuellen Computers.

* **Anmeldeinformationen** -[PSCredential] Gibt die Anmeldeinformationen für den virtuellen Computer an.

* **MSI-Pfad** -[String] Gibt den lokalen Pfad, der die MSI-Datei für Windows Admin Center an, bei der Bereitstellung von Windows Admin Center auf einem vorhandenen virtuellen Computer. Standardmäßig die Version von http://aka.ms/WACDownload Wenn nicht angegeben.

* **VaultName** -[String] Gibt den Namen des schlüsseltresors, den das Zertifikat enthält.

* **CertName** -[String] Gibt den Namen des Zertifikats, das für die MSI-Installation verwendet werden.

* **GenerateSslCert** -[Schalter] True, wenn die MSI-Datei ein selbst signiertes Ssl-Zertifikat generiert werden sollen.

* **PortNumber** -[Int] Gibt an, die Ssl-Portnummer für den Windows Admin Center-Dienst. Der Standardwert ist 443, wenn nicht angegeben.

* **OpenPorts** -[Int []] Gibt die offenen Ports für den virtuellen Computer an.

* **Speicherort** -[String] Gibt den Speicherort des virtuellen Computers.

* **Größe** -[String] Gibt die Größe des virtuellen Computers an. Der Standardwert ist "Standard_DS1_v2", wenn nicht angegeben.

* **Image** -[String] Gibt an, das Image des virtuellen Computers. Der Standardwert ist "Win2016Datacenter", wenn nicht angegeben.

* **VirtualNetworkName** -[String] Gibt den Namen des virtuellen Netzwerks für den virtuellen Computer.

* **SubnetName** -[String] Gibt den Namen des Subnetzes für den virtuellen Computer.

* **SecurityGroupName** -[String] Gibt den Namen der Sicherheitsgruppe für den virtuellen Computer.

* **PublicIpAddressName** -[String] Gibt den Namen der öffentlichen IP-Adresse für den virtuellen Computer.

* **InstallWACOnly** -[Schalter] auf "true" festgelegt, wenn WAC auf einer bereits vorhandenen Azure-VM installiert werden soll.

Es gibt 2 unterschiedliche Optionen für die MSI-Datei zum Bereitstellen und das Zertifikat für die MSI-Installation verwendet. Die MSI-Datei kann entweder aka.ms/WACDownload heruntergeladen werden, oder wenn einem vorhandenen virtuellen Computer bereitstellen, kann der "FilePath" des eine MSI-Datei lokal auf dem virtuellen Computer zugewiesen werden. Das Zertifikat finden Sie in beiden Azure-Schlüsseltresor oder ein selbst signiertes Zertifikat durch die MSI-Datei generiert werden.

### <a name="script-examples"></a>Beispiele für Skripts

Definieren Sie zuerst die allgemeine Variablen, die für die Parameter des Skripts erforderlich.

```PowerShell
$ResourceGroupName = "wac-rg1" 
$VirtualNetworkName = "wac-vnet"
$SecurityGroupName = "wac-nsg"
$SubnetName = "wac-subnet"
$VaultName = "wac-key-vault"
$CertName = "wac-cert"
$Location = "westus"
$PublicIpAddressName = "wac-public-ip"
$Size = "Standard_D4s_v3"
$Image = "Win2016Datacenter"
$Credential = Get-Credential
```

#### <a name="example-1-use-the-script-to-deploy-wac-gateway-on-a-new-vm-in-a-new-virtual-network-and-resource-group-use-the-msi-from-akamswacdownload-and-a-self-signed-cert-from-the-msi"></a>Beispiel 1: Verwenden Sie das Skript WAC Gateway auf einer neuen VM in eine neue virtuelle Netzwerk und Ressourcengruppe bereitstellen. Verwenden Sie die MSI-Datei aus aka.ms/WACDownload und ein selbstsigniertes Zertifikat aus der MSI-Datei.

```PowerShell
$scriptParams = @{
    ResourceGroupName = $ResourceGroupName
    Name = "wac-vm1"
    Credential = $Credential
    VirtualNetworkName = $VirtualNetworkName
    SubnetName = $SubnetName
    GenerateSslCert = $true
}
./Deploy-WACAzVM.ps1 @scriptParams
```

#### <a name="example-2-same-as-1-but-using-a-certificate-from-azure-key-vault"></a>Beispiel 2: Identisch mit #1, aber mit einem Zertifikat aus Azure Key Vault.

```PowerShell
$scriptParams = @{
    ResourceGroupName = $ResourceGroupName
    Name = "wac-vm2"
    Credential = $Credential
    VirtualNetworkName = $VirtualNetworkName
    SubnetName = $SubnetName
    VaultName = $VaultName
    CertName = $CertName
}
./Deploy-WACAzVM.ps1 @scriptParams
```

#### <a name="example-3-using-a-local-msi-on-an-existing-vm-to-deploy-wac"></a>Beispiel 3: Verwenden einen lokalen MSI-Datei auf einer vorhandenen VM WAC bereitstellen.

```PowerShell
$MsiPath = "C:\Users\<username>\Downloads\WindowsAdminCenter<version>.msi"
$scriptParams = @{
    ResourceGroupName = $ResourceGroupName
    Name = "wac-vm3"
    Credential = $Credential
    MsiPath = $MsiPath
    InstallWACOnly = $true
    GenerateSslCert = $true
}
./Deploy-WACAzVM.ps1 @scriptParams
```

### <a name="requirements-for-vm-running-the-windows-admin-center-gateway"></a>Anforderungen für die virtuellen Computer mit dem Gateway Windows Admin Center

Port 443 (HTTPS) muss geöffnet sein.
Verwenden die gleichen Variablen, die für das Skript definiert, können Sie den folgenden Code in Azure Cloud Shell verwenden, um die Netzwerksicherheitsgruppe zu aktualisieren:

```powershell
$nsg = Get-AzNetworkSecurityGroup -Name $SecurityGroupName -ResourceGroupName $ResourceGroupName
$newNSG = Add-AzNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name ssl-rule -Description "Allow SSL" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 443
Set-AzNetworkSecurityGroup -NetworkSecurityGroup $newNSG
```

### <a name="requirements-for-managed-azure-vms"></a>Anforderungen für verwaltete Azure-VM

Port 5985 (WinRM über HTTP) muss geöffnet und einen aktiven Listener.
In Azure Cloud Shell können den folgenden Code Sie um die verwalteten Knoten zu aktualisieren. ```$ResourceGroupName``` und ```$Name``` die gleichen Variablen als das Bereitstellungsskript verwenden, aber Sie benötigen, verwenden Sie die ```$Credential``` spezifisch für den virtuellen Computer Sie verwalten.

```powershell
Enable-AzVMPSRemoting -ResourceGroupName $ResourceGroupName -Name $Name
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any} -Credential $Credential
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {winrm create winrm/config/Listener?Address=*+Transport=HTTP} -Credential $Credential
```

## <a name="deploy-manually-on-an-existing-azure-virtual-machine"></a>Manuell auf vorhandenen virtuellen Azure-Computer bereitstellen

Vor der Installation von Windows Admin Center auf Ihre gewünschte Gateway-VM, installieren ein SSL-Zertifikat für HTTPS-Kommunikation verwenden oder Sie können auch ein selbstsigniertes Zertifikat generiert, die von Windows Admin Center verwenden. Allerdings erhalten Sie eine Warnung, beim Herstellen einer Verbindung über einen Browser, wenn Sie letztere Option auswählen. Sie können diese Warnung in Microsoft Edge umgehen, indem Sie auf **Details > Fahren Sie mit der Webseite** oder, in Chrome müssen dazu **erweitert > Fahren Sie mit [Webseite]** . Es wird empfohlen, dass Sie selbstsignierte Zertifikate nur für testumgebungen verwenden.

> [!NOTE]
> Diese Anweisungen gelten für die Installation unter Windows Server mit Desktopdarstellung und nicht auf einer Server Core-Installation. 

1. [Download Windows Admin Center](https://aka.ms/windowsadmincenter) auf dem lokalen Computer.

2. Eine Remotedesktopverbindung mit dem virtuellen Computer herzustellen, und klicken Sie dann die MSI-Datei von Ihrem lokalen Computer kopieren, und fügen Sie den virtuellen Computer.

3. Doppelklicken Sie auf die MSI-Datei, um die Installation zu beginnen, und befolgen Sie die Anweisungen im Assistenten. Achten Sie darauf, dass die folgenden:

   - Standardmäßig verwendet das Installationsprogramm den empfohlene Port 443 (HTTPS). Wenn Sie einen anderen Port auswählen möchten, beachten Sie, dass Sie diesen Port in Ihrer Firewall öffnen müssen. 

   - Wenn Sie bereits ein SSL-Zertifikat auf dem virtuellen Computer installiert haben, stellen Sie sicher, Sie wählen diese Option aus, und geben Sie den Fingerabdruck.

4. Starten Sie den Windows Admin Center-Dienst (c: / Program Dateien/Windows-Administrator Center/sme.exe ausgeführt)

[Weitere Informationen finden Sie Informationen zum Bereitstellen von Windows Admin Center.](../deploy/install.md)

### <a name="configure-the-gateway-vm-to-enable-https-port-access"></a>Konfigurieren Sie die Gateway-VM, um Zugriff auf HTTPS-Ports zu aktivieren: 

1. Navigieren Sie zu Ihrem virtuellen Computer im Azure-Portal, und wählen **Networking**. 

2. Wählen Sie **hinzufügen eingehender Portregel** , und wählen Sie **HTTPS** unter **Service**. 

> [!NOTE]
> Wenn Sie einen anderen Port als der Standardwert 443 ausgewählt haben, wählen Sie **benutzerdefinierte** unter Dienst, und geben Sie den Port, die Sie ausgewählt, klicken Sie in Schritt 3 unter haben **Port Bereiche**. 

### <a name="accessing-a-windows-admin-center-gateway-installed-on-an-azure-vm"></a>Zugreifen auf ein Windows Admin Center-Gateway auf einer Azure-VM installiert

An diesem Punkt sollten Sie durch Navigieren zu den DNS-Namen des Gateways des virtuellen Computers Windows Admin Center in einem modernen Browser (Edge oder Chrome) auf dem lokalen Computer zugreifen können. 

> [!NOTE]
> Wenn Sie einen anderen Port als 443 ausgewählt haben, können Sie Windows Admin Center zugreifen, navigieren Sie zu https://\<DNS-Namen Ihres virtuellen Computers\>:\<benutzerdefinierten Port\>

Wenn Sie versuchen, Windows Admin Center zugreifen, fordert der Browser zur Eingabe von Anmeldeinformationen auf dem virtuellen Computer, auf dem Windows Admin Center installiert ist. Hier müssen Sie Anmeldeinformationen eingeben, die in der lokalen Benutzer oder die Gruppe "lokale Administratoren" des virtuellen Computers sind. 

Um andere VMs im VNet hinzufügen möchten, stellen Sie sicher, dass WinRM auf dem Ziel-VMs durch Ausführen des folgenden Befehls in PowerShell oder die Eingabeaufforderung auf dem virtuellen Zielcomputer ausgeführt wird: `winrm quickconfig`

Wenn Sie mit der Azure-VM domänenverknüpfung nicht getan haben, der virtuellen Computer verhält sich wie ein Server in einer Arbeitsgruppe, damit Sie sicherstellen, dass Sie berücksichtigen müssen [mithilfe von Windows Admin Center in einer Arbeitsgruppe](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup).