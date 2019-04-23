---
title: Bereitstellen von Windows Admin Center mit hoher Verfügbarkeit
description: Bereitstellen von Windows Admin Center mit hoher Verfügbarkeit (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: a0062230dd3d9e9c52aa317f87e06b0e84507dc4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861061"
---
# <a name="deploy-windows-admin-center-with-high-availability"></a>Bereitstellen von Windows Admin Center mit hoher Verfügbarkeit

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Sie können Windows Admin Center in einem Failovercluster für hohe Verfügbarkeit für Ihren Windows Admin Center-Gateway-Dienst bereitstellen. Bereitgestellte Lösung ist eine Aktiv / Passiv-Lösung, in denen nur eine Instanz des Windows Admin Center aktiv ist. Wenn einer der Knoten im Cluster ausfällt, ein Windows Admin Center ordnungsgemäß Failover auf einen anderen Knoten können Sie weiterhin die Server in Ihrer Umgebung problemlos verwalten. 

[Informationen Sie zu anderen Bereitstellungsoptionen Windows Admin Center.](../plan/installation-options.md)

## <a name="prerequisites"></a>Vorraussetzungen

- Ein Failovercluster mit 2 oder mehr Knoten auf Windows Server 2016 oder 2019. [Weitere Informationen zum Bereitstellen eines Failoverclusters](../../../failover-clustering/failover-clustering-overview.md).
- Ein freigegebenes Clustervolume (CSV) für Windows Admin Center zum Speichern persistenter Daten, die von allen Knoten im Cluster zugegriffen werden kann. 10 GB jedoch reicht für Ihrer CSV-Datei aus.
- Hohe Verfügbarkeit-Bereitstellungsskript aus [Windows Admin Center HA Skript Zip-Datei](https://aka.ms/WACHAScript). Laden Sie die ZIP-Datei mit dem Skript auf Ihren lokalen Computer herunter, und kopieren Sie das Skript nach Bedarf basierend auf der Anleitung unten.
- Empfohlen aber optional: ein signiertes Zertifikat-PFX und Kennwort. Sie müssen nicht bereits das Zertifikat auf den Clusterknoten installiert haben: das Skript wird für Sie funktionieren. Wenn Sie nicht bereitgestellt wird, generiert das Installationsskript ein selbst signiertes Zertifikat, die nach 60 Tagen abläuft.

## <a name="install-windows-admin-center-on-a-failover-cluster"></a>Installieren Sie Windows Admin Center auf einem Failovercluster

1. Kopieren der ```Install-WindowsAdminCenterHA.ps1``` Skript auf einen Knoten in Ihrem Cluster. Herunterladen Sie, oder kopieren Sie die MSI-Datei Windows Admin Center auf demselben Knoten.
2. Eine Verbindung herstellen, auf den Knoten über RDP und führen Sie die ```Install-WindowsAdminCenterHA.ps1``` Skripts von diesem Knoten mit den folgenden Parametern:
    - `-clusterStorage`: der lokale Pfad, der das freigegebene Clustervolume zum Speichern von Daten von Windows Admin Center.
    - `-clientAccessPoint`: Wählen Sie einen Namen, die Sie verwenden, um Windows Admin Center zugreifen. Angenommen, Sie führen das Skript mit dem Parameter `-clientAccessPoint contosoWindowsAdminCenter`, greifen auf den Dienst Windows Admin Center finden Sie unter `https://contosoWindowsAdminCenter.<domain>.com`
    - `-staticAddress`: Optional. Eine oder mehrere statische Adressen für den generischen Clusterdienst. 
    - `-msiPath`: Der Pfad für die MSI-Datei von Windows Admin Center.
    - `-certPath`: Optional. Der Pfad für eine Zertifikat-PFX-Datei.
    - `-certPassword`: Optional. Ein SecureString-Kennwort für die Zertifikat-PFX-Datei im bereitgestellten `-certPath`
    - `-generateSslCert`: Dies ist optional. Wenn Sie kein signiertes Zertifikat bereitstellen möchten, schließen Sie dieses Flag Parameter, um ein selbstsigniertes Zertifikat zu generieren. Beachten Sie, dass das selbstsignierte Zertifikat in 60 Tagen ablaufen wird.
    - `-portNumber`: Optional. Wenn Sie keinen Port angeben, wird der Gateway-Dienst auf Port 443 (HTTPS) bereitgestellt. Verwendung von ein anderen Port geben Sie in diesem Parameter. Beachten Sie, dass wenn Sie einen benutzerdefinierten Port (alles, was zusätzlich zu Port 443) verwenden, Sie die Windows Admin Center zugreifen müssen, indem Sie zu https://\<ClientAccessPoint\>:\<Port\>.

> [!NOTE]
> Die ```Install-WindowsAdminCenterHA.ps1``` Skript unterstützt ```-WhatIf ``` und ```-Verbose``` Parameter

### <a name="examples"></a>Beispiele

#### <a name="install-with-a-signed-certificate"></a>Installieren Sie mit einem signierten Zertifikat:

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

#### <a name="install-with-a-self-signed-certificate"></a>Installieren Sie mit der ein selbstsigniertes Zertifikat:

```powershell
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -generateSslCert -Verbose
```

## <a name="update-an-existing-high-availability-installation"></a>Aktualisieren einer vorhandenen Installation für hohe Verfügbarkeit

Verwenden Sie den gleichen ```Install-WindowsAdminCenterHA.ps1``` Skript zum Aktualisieren Ihrer HA-Bereitstellung, der ohne Datenverlust für Ihre Verbindung.

### <a name="update-to-a-new-version-of-windows-admin-center"></a>Aktualisieren Sie auf eine neue Version von Windows Admin Center

Wenn eine neue Version von Windows Admin Center veröffentlicht wird, führen Sie einfach die ```Install-WindowsAdminCenterHA.ps1``` Skript erneut mit der nur die ```msiPath``` Parameter:

```powershell
.\Install-WindowsAdminCenterHA.ps1 -msiPath '.\WindowsAdminCenter.msi' -Verbose
```

### <a name="update-the-certificate-used-by-windows-admin-center"></a>Aktualisieren Sie das Zertifikat ein, die Windows Admin Center

Sie können das Zertifikat von einer HA-Bereitstellung von Windows Admin Center zu einem beliebigen Zeitpunkt verwendet werden, durch die Bereitstellung von PFX-Datei des neuen Zertifikats aktualisieren und und das Kennwort.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

Sie können auch das Zertifikat zur gleichen Zeit aktualisieren, die Sie die Windows Admin Center-Plattform durch eine neue MSI-Datei aktualisieren.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
``` 

## <a name="uninstall"></a>Deinstallieren

Um die HA-Bereitstellung von Windows Admin Center über den Failovercluster zu deinstallieren, übergeben die ```-Uninstall``` Parameter, um die ```Install-WindowsAdminCenterHA.ps1``` Skript.

```powershell
.\Install-WindowsAdminCenterHA.ps1 -Uninstall -Verbose
```

## <a name="troubleshooting"></a>Problembehandlung

Protokolle werden im temporären Ordner der CSV-Datei (z. B. C:\ClusterStorage\Volume1\temp) gespeichert.