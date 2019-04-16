---
title: Bereitstellen von Windows Admin Center Gateway in Azure
description: Bereitstellen von Windows Admin Center Gateway in Azure
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: af766c2e0502d9fe633cae42d999db5cbffc32c8
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296922"
---
# Bereitstellen von Windows Admin Center in Azure

## Bereitstellung mit Skripts

Sie können [Bereitstellen WACAzVM.ps1](https://aka.ms/deploy-wacazvm) herunterladen, die über [Azure-Cloud-Shell](https://shell.azure.com) zum Einrichten von Windows Admin Center Gateway in Azure ausgeführt wird. Dieses Skript kann die gesamte Umgebung, einschließlich der Ressourcengruppe erstellen.

[Zum manuellen Bereitstellungsschritte springen](#deploy-manually-on-an-existing-azure-virtual-machine)

### Voraussetzungen

* Richten Sie Ihr Konto in [Azure-Cloud-Shell](https://shell.azure.com). Wenn dies zum ersten Mal verwenden Cloud-Shell ist, werden Sie aufgefordert zugeordnet, oder erstellen ein Azure-Speicherkonto mit Cloud-Shell.
* Navigieren Sie in einer **PowerShell** -Cloud-Shell zu Ihrem Basisverzeichnis: ```PS Azure:\> cd ~```
* Hochladen der ```Deploy-WACAzVM.ps1``` Datei, Drag & drop aus dem lokalen Computer an eine beliebige Stelle im Cloud-Shell-Fenster.

Wenn Ihr eigenes Zertifikat angeben:

* Laden Sie das Zertifikat auf [Azure dem Schlüsseltresor](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis). Erstellen Sie eine wichtige Tresor im Azure-Portal zunächst, das Zertifikat in den wichtigsten Tresor hoch. Alternativ können Sie Azure-Portal verwenden, um ein Zertifikat zu generieren.

### Skriptparameter

* **ResourceGroupName** - [String] Gibt den Namen der Ressourcengruppe, in denen die VM erstellt wird.

* **Name** - [String] Gibt den Namen des virtuellen Computers.

* **Credential** - [PSCredential] Gibt die Anmeldeinformationen für den virtuellen Computer an.

* **Image** - [String] Gibt den lokalen Pfad des Windows Admin Center MSI-Datei, bei der Bereitstellung von Windows Admin Center auf einer vorhandenen VM. Verwendet die Version von http://aka.ms/WACDownload Wenn nicht angegeben.

* **VaultName** - [String] Gibt den Namen des Schlüssel Depots mit dem Zertifikat.

* **CertName** - [String] Gibt den Namen des Zertifikats für MSI-Installation verwendet werden.

* **GenerateSslCert** - [Switch] "true", wenn einem selbstsignierten signierte Ssl-Zertifikat von die MSI-Datei generiert werden sollen.

* **PortNumber** - [Int] Gibt die Ssl-Portnummer für den Windows Admin Center-Dienst. Die Standardeinstellung ist 443, wenn nicht angegeben.

* **OpenPorts** - [Int []] Gibt die offene Ports für den virtuellen Computer an.

* **Speicherort** : [String] Gibt den Speicherort des virtuellen Computers.

* **Größe** - [String] Gibt die Größe des virtuellen Computers. Der Standardwert ist "Standard_DS1_v2", wenn nicht angegeben.

* **Bild** - [String] Gibt das Bild des virtuellen Computers. Der Standardwert ist "Win2016Datacenter", wenn nicht angegeben.

* **VirtualNetworkName** - [String] Gibt den Namen des virtuellen Netzwerks für den virtuellen Computer.

* **SubnetName** - [String] Gibt den Namen des Subnetzes für den virtuellen Computer.

* **SecurityGroupName** - [String] Gibt den Namen der Sicherheitsgruppe ein, für den virtuellen Computer.

* **PublicIpAddressName** - [String] Gibt den Namen der öffentliche IP-Adresse für den virtuellen Computer.

* **InstallWACOnly** - [Switch] Satz auf "true", wenn WAC auf einer bereits vorhandenen Azure-VM installiert werden soll.

Es gibt 2 verschiedene Optionen für die MSI-Datei zum Bereitstellen und das Zertifikat für MSI-Installation verwendet. MSI-Datei kann entweder von aka.ms/WACDownload heruntergeladen werden, oder wenn auf einer vorhandenen VM bereitstellen, Filepath von eine MSI-Datei lokal auf dem virtuellen Computer gewährt werden kann. Das Zertifikat kann in beiden Azure dem Schlüsseltresor gefunden werden, oder die MSI-Datei ein selbstsigniertes Zertifikat generiert werden.

### Beispiele für Skripts

Zuerst definieren Sie gängige Variablen, die für die Parameter des Skripts erforderlich.

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

#### Beispiel 1: Verwenden Sie das Skript WAC-Gateway auf einem neuen virtuellen Computer in einer neuen virtuellen Netzwerk und Ressourcen Gruppe bereitstellen. Verwenden Sie die MSI-Datei aus aka.ms/WACDownload und ein selbstsigniertes Zertifikat aus der MSI-Datei.

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

#### Beispiel 2: Identisch mit #1, jedoch mit einem Zertifikat Azure dem Schlüsseltresor.

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

#### Beispiel 3: Verwenden einer lokalen MSI auf einer vorhandenen VM WAC bereitstellen.

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

### Anforderungen für das Windows Admin Center Gateway-VM

Port 443 (HTTPS) muss geöffnet sein.
Verwenden die gleichen Variablen für Skript definiert, können den folgenden Code in Azure-Cloud-Shell Sie um die Netzwerk-Sicherheitsgruppe zu aktualisieren:

```powershell
$nsg = Get-AzNetworkSecurityGroup -Name $SecurityGroupName -ResourceGroupName $ResourceGroupName
$newNSG = Add-AzNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name ssl-rule -Description "Allow SSL" -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * -DestinationPortRange 443
Set-AzNetworkSecurityGroup -NetworkSecurityGroup $newNSG
```

### Anforderungen für verwalteten Azure-VM

Port 5985 (WinRM über HTTP) muss geöffnet sein und einen aktiven Listener haben.
Sie können den folgenden Code in Azure-Cloud-Shell verwenden, die verwalteten Knoten zu aktualisieren. ```$ResourceGroupName``` und ```$Name``` verwenden Sie die gleichen Variablen als das Bereitstellungsskript, aber Sie müssen verwenden, die ```$Credential``` speziell für den virtuellen Computer Sie verwalten.

```powershell
Enable-AzVMPSRemoting -ResourceGroupName $ResourceGroupName -Name $Name
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {Set-NetFirewallRule -Name WINRM-HTTP-In-TCP-PUBLIC -RemoteAddress Any} -Credential $Credential
Invoke-AzVMCommand -ResourceGroupName $ResourceGroupName -Name $Name -ScriptBlock {winrm create winrm/config/Listener?Address=*+Transport=HTTP} -Credential $Credential
```

## Bereitstellen von manuell auf vorhandenen Azure virtuellen Computer

Vor der Installation von Windows Admin Center auf das gewünschte VM-Gateway, können installieren ein SSL-Zertifikat für HTTPS-Kommunikation zu verwenden, oder Sie ein selbstsigniertes Zertifikat generiert von Windows Admin Center verwenden. Allerdings erhalten Sie eine Warnung, beim Herstellen einer Verbindung über einen Browser, wenn Sie die letztere Option auswählen. Sie können diese Warnung in Edge auf **Details > fahren Sie mit der Webseite** oder in Chrome, umgehen, durch die Auswahl der **erweiterten > weiter zu [Webseite]**. Es wird empfohlen, dass Sie nur Verwendung selbstsignierter Zertifikate für Test-Umgebungen.

> [!NOTE]
> Diese Anweisungen gelten für die Installation auf Windows Server mit Desktop Experience, nicht auf Server Core-Installationsoption. 

1. [Herunterladen von Windows Admin Center](https://aka.ms/windowsadmincenter) auf Ihrem lokalen Computer.

2. Stellen Sie eine Remotedesktopverbindung in den virtuellen Computer her und kopieren Sie die MSI-Datei aus Ihrem lokalen Computer, und fügen Sie in den virtuellen Computer.

3. Doppelklicken Sie auf die MSI-Datei, um die Installation zu beginnen, und folgen Sie den Anweisungen im Assistenten. Beachten Sie Folgendes:

   - Standardmäßig verwendet der Installer die empfohlenen Port 443 (HTTPS). Wenn Sie einen anderen Port auswählen möchten, beachten Sie, dass Sie auf diesem Port in Ihrer Firewall sowie zu öffnen. 

   - Wenn Sie bereits ein SSL-Zertifikat auf dem virtuellen Computer installiert haben, sicherzustellen, dass Sie diese Option auswählen, und geben Sie den Fingerabdruck.

4. Starten Sie den Windows Admin Center-Dienst (führen Sie "c:" / Program Dateien/Windows Admin Center/sme.exe)

[Weitere Informationen zum Bereitstellen von Windows Admin Center.](../deploy/install.md)

### Konfigurieren Sie das Gateway VM HTTPS-Port-Zugriff zu aktivieren: 

1. Navigieren Sie zu einem virtuellen Computer im Azure-Portal, und wählen Sie die **Netzwerke**. 

2. Wählen Sie **eingehende Portregel hinzufügen** und **HTTPS** **-Dienstes**. 

> [!NOTE]
> Wenn Sie einen Port als der Standard 443 ausgewählt haben, wählen Sie **benutzerdefinierte** unter Dienste, und geben Sie den Port, die, den Sie in Schritt 3 unter **Portbereichen**ausgewählt haben. 

### Zugriff auf ein Windows Admin Center-Gateway auf Azure-VM installiert

An dieser Stelle sollten Sie Windows Admin Center über einen modernen Browser (Edge oder Chrome) auf Ihrem lokalen Computer zugreifen, durch die Navigation auf den DNS-Namen Ihres Gateways VM sein. 

> [!NOTE]
> Wenn Sie einen anderen Port als 443 ausgewählt haben, können Sie Windows Admin Center zugreifen, durch die Navigation auf https://\<DNS Namen Ihrer VM\>:\<custom port\>

Wenn Sie versuchen, Windows Admin Center zugreifen, fordert der Browser zur Eingabe der Anmeldeinformationen auf dem virtuellen Computer, auf dem Windows Admin Center installiert ist. Hier müssen Sie Anmeldeinformationen eingeben, die lokalen Benutzer und der lokalen Administratorgruppe des virtuellen Computers sind. 

Um fügen Sie weitere virtuelle Computer in der vnet angefügt wird, stellen Sie sicher, dass WinRM auf den Ziel-VMs ausgeführt wird, indem Sie Folgendes in PowerShell- oder die auf den Ziel-VM ausführen: `winrm quickconfig`

Wenn Sie die Azure-VM Domäne nicht geschehen, verhält sich die VM wie einem Server in einer Arbeitsgruppe, daher müssen Sie sicherstellen, dass Sie für die [Verwendung von Windows Admin Center in einer Arbeitsgruppe](../support/troubleshooting.md#using-windows-admin-center-in-a-workgroup)berücksichtigen.