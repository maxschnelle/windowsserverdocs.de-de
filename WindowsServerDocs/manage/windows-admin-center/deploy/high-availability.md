---
title: Bereitstellen des Windows Admin Centers mit hoher Verfügbarkeit
description: Bereitstellen des Windows Admin Centers mit hoher Verfügbarkeit (Project Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 6ae7bd9ed7aee5835ac1f53b9e10879ad8824f52
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406942"
---
# <a name="deploy-windows-admin-center-with-high-availability"></a>Bereitstellen des Windows Admin Centers mit hoher Verfügbarkeit

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Sie können das Windows Admin Center in einem Failovercluster bereitstellen, um Hochverfügbarkeit für Ihren Windows Admin Center-Gatewaydienst bereitzustellen. Die bereitgestellte Lösung ist eine Aktiv/Passiv-Lösung, bei der nur eine Instanz von Windows Admin Center aktiv ist. Wenn einer der Knoten im Cluster ausfällt, führt das Windows Admin Center ein ordnungsgemäßes Failover zu einem anderen Knoten durch, sodass Sie die Server in Ihrer Umgebung nahtlos weiter verwalten können. 

[Erfahren Sie mehr über andere Bereitstellungs Optionen für Windows Admin Center.](../plan/installation-options.md)

## <a name="prerequisites"></a>Erforderliche Komponenten

- Ein Failovercluster mit mindestens zwei Knoten unter Windows Server 2016 oder 2019. [Erfahren Sie mehr über das Bereitstellen eines Failoverclusters](../../../failover-clustering/failover-clustering-overview.md).
- Ein frei gegebenes Cluster Volume (CSV) für Windows Admin Center zum Speichern von persistenten Daten, auf die von allen Knoten im Cluster zugegriffen werden kann. 10 GB sind für Ihr CSV ausreichend.
- Hoch Verfügbarkeits Bereitstellungs Skript aus der [Windows Admin Center-ZIP-Datei](https://aka.ms/WACHAScript)für Hochverfügbarkeit. Laden Sie die ZIP-Datei mit dem Skript auf Ihren lokalen Computer herunter, und kopieren Sie das Skript basierend auf den nachfolgenden Anleitungen nach Bedarf.
- Empfohlen, aber optional: ein signiertes Zertifikat. pfx & Kennwort. Sie müssen das Zertifikat nicht bereits auf den Cluster Knoten installiert haben. das Skript führt dies für Sie aus. Wenn Sie keinen angeben, generiert das Installationsskript ein selbst signiertes Zertifikat, das nach 60 Tagen abläuft.

## <a name="install-windows-admin-center-on-a-failover-cluster"></a>Installieren des Windows Admin Centers auf einem Failovercluster

1. Kopieren Sie das Skript ```Install-WindowsAdminCenterHA.ps1``` auf einen Knoten in Ihrem Cluster. Laden Sie die MSI-Datei des Windows Admin Centers herunter, oder kopieren Sie Sie auf denselben Knoten.
2. Stellen Sie über RDP eine Verbindung mit dem Knoten her, und führen Sie das Skript ```Install-WindowsAdminCenterHA.ps1``` von diesem Knoten mit den folgenden Parametern aus:
    - `-clusterStorage`: der lokale Pfad des freigegebenes Clustervolume, in dem die Daten des Windows Admin Centers gespeichert werden sollen.
    - `-clientAccessPoint`: Wählen Sie einen Namen aus, den Sie für den Zugriff auf das Windows Admin Center verwenden werden. Wenn Sie z. b. das Skript mit dem Parameter `-clientAccessPoint contosoWindowsAdminCenter` ausführen, greifen Sie auf den Windows Admin Center-Dienst zu, indem Sie `https://contosoWindowsAdminCenter.<domain>.com` besuchen.
    - `-staticAddress`: Optional. Eine oder mehrere statische Adressen für den generischen Cluster Dienst. 
    - `-msiPath`: Der Pfad für die MSI-Datei des Windows Admin Centers.
    - `-certPath`: Optional. Der Pfad für eine PFX-Zertifikat Datei.
    - `-certPassword`: Optional. Ein SecureString-Kennwort für das in `-certPath` angegebene Zertifikat. pfx
    - `-generateSslCert`: Optional. Wenn Sie kein signiertes Zertifikat angeben möchten, fügen Sie dieses parameterflag ein, um ein selbst signiertes Zertifikat zu generieren. Beachten Sie, dass das selbst signierte Zertifikat in 60 Tagen abläuft.
    - `-portNumber`: Optional. Wenn Sie keinen Port angeben, wird der Gatewaydienst über Port 443 (HTTPS) bereitgestellt. Wenn Sie einen anderen Port verwenden möchten, geben Sie in diesem Parameter an. Beachten Sie Folgendes: Wenn Sie einen benutzerdefinierten Port verwenden (alles außer 443), greifen Sie auf das Windows Admin Center zu, indem Sie zu https://\<clientaccesspoint @ no__t-1: \<Port @ no__t-3 wechseln.

> [!NOTE]
> Das Skript "```Install-WindowsAdminCenterHA.ps1```" unterstützt ```-WhatIf ```-und ```-Verbose```-Parameter.

### <a name="examples"></a>Beispiele

#### <a name="install-with-a-signed-certificate"></a>Installieren mit einem signierten Zertifikat:

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

#### <a name="install-with-a-self-signed-certificate"></a>Installieren mit einem selbst signierten Zertifikat:

```powershell
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -generateSslCert -Verbose
```

## <a name="update-an-existing-high-availability-installation"></a>Aktualisieren einer vorhandenen hoch Verfügbarkeits Installation

Verwenden Sie das gleiche ```Install-WindowsAdminCenterHA.ps1```-Skript, um Ihre ha-Bereitstellung zu aktualisieren, ohne die Verbindungsdaten zu verlieren.

### <a name="update-to-a-new-version-of-windows-admin-center"></a>Aktualisieren auf eine neue Version von Windows Admin Center

Wenn eine neue Version von Windows Admin Center veröffentlicht wird, führen Sie das Skript ```Install-WindowsAdminCenterHA.ps1``` einfach erneut mit dem Parameter "```msiPath```" aus:

```powershell
.\Install-WindowsAdminCenterHA.ps1 -msiPath '.\WindowsAdminCenter.msi' -Verbose
```

### <a name="update-the-certificate-used-by-windows-admin-center"></a>Aktualisieren des vom Windows Admin Center verwendeten Zertifikats

Sie können das Zertifikat, das von einer ha-Bereitstellung von Windows Admin Center verwendet wird, jederzeit aktualisieren, indem Sie die PFX-Datei und das Kennwort des neuen Zertifikats bereitstellen.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

Sie können das Zertifikat auch aktualisieren, wenn Sie die Windows Admin Center-Plattform mit einer neuen MSI-Datei aktualisieren.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
``` 

## <a name="uninstall"></a>Deinstallieren

Wenn Sie die ha-Bereitstellung von Windows Admin Center aus Ihrem Failovercluster deinstallieren möchten, übergeben Sie den ```-Uninstall```-Parameter an das ```Install-WindowsAdminCenterHA.ps1```-Skript.

```powershell
.\Install-WindowsAdminCenterHA.ps1 -Uninstall -Verbose
```

## <a name="troubleshooting"></a>Problembehandlung

Protokolle werden im temporären Ordner des CSV gespeichert (z. b. "c:\clusterstorage\volume1\temp").