---
title: Bereitstellen eines Windows Admin Center-Gateways in Azure
description: Bereitstellen eines Windows Admin Center-Gateways in Azure
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 1da4df284febbf18b5796322868451c45ab247ab
ms.sourcegitcommit: 7c7fc443ecd0a81bff6ed6dbeeaf4f24582ba339
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2019
ms.locfileid: "74903932"
---
# <a name="deploy-windows-admin-center-in-azure"></a>Bereitstellen des Windows Admin Centers in Azure

## <a name="deploy-using-script"></a>Mithilfe von Skript bereitstellen

Sie können [Deploy-WACAzVM. ps1](https://aka.ms/deploy-wacazvm) herunterladen, das Sie von [Azure Cloud Shell](https://shell.azure.com) ausführen, um ein Windows Admin Center-Gateway in Azure einzurichten. Mit diesem Skript kann die gesamte Umgebung, einschließlich der Ressourcengruppe, erstellt werden.

[Wechseln Sie zu manuelle Bereitstellungs Schritte.](#deploy-manually-on-an-existing-azure-virtual-machine)

### <a name="prerequisites"></a>Voraussetzungen

* Richten Sie Ihr Konto in [Azure Cloud Shell](https://shell.azure.com)ein. Wenn Sie Cloud Shell zum ersten Mal verwenden, werden Sie aufgefordert, ein Azure Storage-Konto mit Cloud Shell zuzuordnen oder zu erstellen.
* Navigieren Sie in einem **PowerShell** -Cloud Shell zu Ihrem Basisverzeichnis: ```PS Azure:\> cd ~```
* Wenn Sie die ```Deploy-WACAzVM.ps1``` Datei hochladen möchten, ziehen Sie Sie per Drag & amp; Drop vom lokalen Computer an eine beliebige Stelle im Cloud Shell Fenster.

Wenn Sie Ihr eigenes Zertifikat angeben:

* Laden Sie das Zertifikat in [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-whatis)hoch. Erstellen Sie zunächst einen Schlüssel Tresor im Azure-Portal, und laden Sie dann das Zertifikat in den Schlüssel Tresor hoch. Alternativ können Sie das Azure-Portal verwenden, um ein Zertifikat für Sie zu generieren.

### <a name="script-parameters"></a>Skriptparameter

* **Resourcegroupname** -[Zeichenfolge] gibt den Namen der Ressourcengruppe an, in der die VM erstellt wird.

* **Name** -[Zeichenfolge] gibt den Namen des virtuellen Computers an.

* **Credential** -[PSCredential] gibt die Anmelde Informationen für den virtuellen Computer an.

* **Msipath** -[Zeichenfolge] gibt den lokalen Pfad der MSI-Datei des Windows Admin Centers an, wenn Windows Admin Center auf einer vorhandenen VM bereitgestellt wird. Standardmäßig wird die Version von https://aka.ms/WACDownload, sofern nicht ausgelassen.

* **Vaultname** -[String] gibt den Namen des Schlüssel Tresors an, der das Zertifikat enthält.

* **CertName** -[Zeichenfolge] gibt den Namen des Zertifikats an, das für die MSI-Installation verwendet werden soll.

* **Generatess lcert** -[Switch] true, wenn die MSI ein selbst signiertes SSL-Zertifikat generieren soll.

* **PortNumber** -[int] gibt die SSL-Portnummer für den Windows Admin Center-Dienst an. Der Standardwert ist 443, wenn ausgelassen.

* **OpenPorts** -[int []] gibt die geöffneten Ports für den virtuellen Computer an.

* **Location** -[Zeichenfolge] gibt den Speicherort des virtuellen Computers an.

* **Size** -[Zeichenfolge] gibt die Größe des virtuellen Computers an. Der Standardwert ist "Standard_DS1_v2".

* **Image** -[Zeichenfolge] gibt das Image des virtuellen Computers an. Der Standardwert ist "Win2016Datacenter".

* **Virtualnetworkname** -[Zeichenfolge] gibt den Namen des virtuellen Netzwerks für den virtuellen Computer an.

* **SubnetName** -[Zeichenfolge] gibt den Namen des Subnetzes für die VM an.

* **Securitygroupname** -[String] gibt den Namen der Sicherheitsgruppe für die VM an.

* **Publicipaddressname** -[Zeichenfolge] gibt den Namen der öffentlichen IP-Adresse für den virtuellen Computer an.

* **Installwaconly** -[Switch] wird auf "true" festgelegt, wenn WAC auf einem bereits vorhandenen virtuellen Azure-Computer installiert werden soll.

Es gibt zwei verschiedene Optionen für die Bereitstellung der MSI und das Zertifikat, das für die MSI-Installation verwendet wird. Die MSI kann entweder von aka.ms/WACDownload heruntergeladen werden, oder wenn die Bereitstellung auf einem vorhandenen virtuellen Computer erfolgen soll, kann der Dateipfad einer MSI-Datei lokal auf dem virtuellen Computer angegeben werden. Das Zertifikat befindet sich entweder in Azure Key Vault oder ein selbst signiertes Zertifikat wird von der MSI generiert.

### <a name="script-examples"></a>Skript Beispiele

Definieren Sie zunächst allgemeine Variablen, die für die Parameter des Skripts erforderlich sind.

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

#### <a name="example-1-use-the-script-to-deploy-wac-gateway-on-a-new-vm-in-a-new-virtual-network-and-resource-group-use-the-msi-from-akamswacdownload-and-a-self-signed-cert-from-the-msi"></a>Beispiel 1: Verwenden Sie das Skript zum Bereitstellen eines WAC-Gateways auf einem neuen virtuellen Computer in einem neuen virtuellen Netzwerk und einer neuen Ressourcengruppe. Verwenden Sie die MSI aus aka.ms/WACDownload und ein selbst signiertes Zertifikat aus der MSI.

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

#### <a name="example-2-same-as-1-but-using-a-certificate-from-azure-key-vault"></a>Beispiel 2: wie #1, aber das Verwenden eines Zertifikats aus Azure Key Vault.

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

#### <a name="example-3-using-a-local-msi-on-an-existing-vm-to-deploy-wac"></a>Beispiel 3: Verwenden einer lokalen MSI auf einem vorhandenen virtuellen Computer zum Bereitstellen von WAC

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

### <a name="requirements-for-vm-running-the-windows-admin-center-gateway"></a>Anforderungen an den virtuellen Computer, der das Windows Admin Center-Gateway ausgeführt

Port 443 (HTTPS) muss geöffnet sein.
Mithilfe der für das Skript definierten Variablen können Sie den folgenden Code in Azure Cloud Shell verwenden, um die Netzwerk Sicherheitsgruppe zu aktualisieren:

```powershell
$nsg = Get-AzNetworkSecurityGroup -Name $SecurityGroupName -ResourceGroupName $ResourceGroupName
$newNSG = Add-AzNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name ssl-rule -Description "Allow SSL" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 443
Set-AzNetworkSecurityGroup -NetworkSecurityGroup $newNSG
```

### <a name="requirements-for-managed-azure-vms"></a>Anforderungen an verwaltete Azure-VMS

Port 5985 (WinRM über HTTP) muss geöffnet sein und über einen aktiven Listener verfügen.
Sie können den Code unten in Azure Cloud Shell verwenden, um die verwalteten Knoten zu aktualisieren. ```$ResourceGroupName``` und ```$Name``` verwenden dieselben Variablen wie das Bereitstellungs Skript, aber Sie müssen die ```$Credential``` verwenden, die für die von Ihnen verwaltete VM spezifisch sind.

```powershell
Enable-AzVMPSRemoting -ResourceGroupName $ResourceGroupName -Name $Name
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any} -Credential $Credential
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {winrm create winrm/config/Listener?Address=*+Transport=HTTP} -Credential $Credential
```

## <a name="deploy-manually-on-an-existing-azure-virtual-machine"></a>Manuelles Bereitstellen auf einem vorhandenen virtuellen Azure-Computer

Installieren Sie vor der Installation des Windows Admin Centers auf der gewünschten Gateway-VM ein SSL-Zertifikat für die HTTPS-Kommunikation, oder Sie können ein selbst signiertes Zertifikat verwenden, das vom Windows Admin Center generiert wurde. Sie erhalten jedoch eine Warnung, wenn Sie versuchen, eine Verbindung über einen Browser herzustellen, wenn Sie die letztere Option auswählen. Sie können diese Warnung in Microsoft Edge umgehen, indem Sie auf > Details klicken, um auf **der Webseite zu** navigieren, oder in Chrome auf **> Erweitert klicken, um zu [Webseite] zu**wechseln. Es wird empfohlen, nur selbst signierte Zertifikate für Testumgebungen zu verwenden.

> [!NOTE]
> Diese Anweisungen gelten für die Installation von unter Windows Server mit Desktop Darstellung, nicht für eine Server Core-Installation. 

1. [Laden Sie Windows Admin Center](https://aka.ms/windowsadmincenter) auf Ihren lokalen Computer herunter.

2. Stellen Sie eine Remote Desktop Verbindung mit dem virtuellen Computer her, kopieren Sie die MSI von Ihrem lokalen Computer, und fügen Sie Sie in die VM ein.

3. Doppelklicken Sie auf die MSI-Installation, um die Installation zu starten, und befolgen Sie die Anweisungen im Assistenten. Bedenken Sie dabei Folgendes:

   - Standardmäßig verwendet das Installationsprogramm den empfohlenen Port 443 (HTTPS). Wenn Sie einen anderen Port auswählen möchten, müssen Sie auch diesen Port in der Firewall öffnen. 

   - Wenn Sie bereits ein SSL-Zertifikat auf der VM installiert haben, stellen Sie sicher, dass Sie diese Option auswählen und den Fingerabdruck eingeben.

4. Starten Sie den Windows Admin Center-Dienst (Ausführen von C:/Programme/Windows Admin Center/SME. exe).

[Erfahren Sie mehr über das Bereitstellen von Windows Admin Center.](../deploy/install.md)

### <a name="configure-the-gateway-vm-to-enable-https-port-access"></a>Konfigurieren der Gateway-VM zum Aktivieren des HTTPS-Port Zugriffs: 

1. Navigieren Sie im Azure-Portal zu ihrer VM, und wählen Sie **Netzwerk**aus. 

2. Wählen Sie **Regel für eingehenden Port hinzufügen** und unter **Dienst**die Option **https** 

> [!NOTE]
> Wenn Sie einen anderen Port als den Standardwert 443 ausgewählt haben, wählen Sie unter Dienst die Option **Benutzer** definiert aus, und geben Sie den Port ein, den Sie in Schritt 3 unter **Port Bereiche** 

### <a name="accessing-a-windows-admin-center-gateway-installed-on-an-azure-vm"></a>Zugreifen auf ein auf einer Azure-VM installiertes Windows Admin Center-Gateway

An diesem Punkt sollten Sie in der Lage sein, über einen modernen Browser (Microsoft Edge oder Chrome) auf dem lokalen Computer auf das Windows Admin Center zuzugreifen, indem Sie zum DNS-Namen Ihrer Gateway-VM navigieren. 

> [!NOTE]
> Wenn Sie einen anderen Port als 443 ausgewählt haben, können Sie auf das Windows Admin Center zugreifen, indem Sie zu https://\<DNS-Namen Ihres virtuellen Computers\>:\<benutzerdefinierter Port\>

Wenn Sie versuchen, auf Windows Admin Center zuzugreifen, werden Sie vom Browser zur Eingabe von Anmelde Informationen aufgefordert, um auf den virtuellen Computer zuzugreifen, auf dem Windows Admin Center installiert ist. Hier müssen Sie die Anmelde Informationen eingeben, die sich in der lokalen Benutzergruppe oder der lokalen Gruppe "Administratoren" des virtuellen Computers befinden. 

Um andere virtuelle Computer im vnet hinzuzufügen, stellen Sie sicher, dass WinRM auf den virtuellen Ziel Computern ausgeführt wird, indem Sie Folgendes in PowerShell oder über die Eingabeaufforderung auf der Ziel-VM ausführen: `winrm quickconfig`

Wenn Sie nicht der Azure-VM angehören, verhält sich der virtuelle Computer wie ein Server in der Arbeitsgruppe. Daher müssen Sie sicherstellen, dass Sie das [Windows Admin Center in einer Arbeitsgruppe verwenden](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup).