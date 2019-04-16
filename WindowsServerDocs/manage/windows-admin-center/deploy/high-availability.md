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
ms.sourcegitcommit: 802a7bd537cab22893abb7e6657c4be90346ef88
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/23/2019
ms.locfileid: "9025032"
---
# Bereitstellen von Windows Admin Center mit hoher Verfügbarkeit

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

Sie können Windows Admin Center in einem Failovercluster zur Bereitstellung von hoher Verfügbarkeit für Ihren Windows Admin Center Gateway-Dienst bereitstellen. Bereitgestellte Lösung ist eine Lösung aktiv / passiv, in denen nur eine Instanz von Windows Admin Center aktiv ist. Wenn einer der Knoten im Cluster ein Fehler auftritt, Failover Windows Admin Center problemlos auf einen anderen Knoten abgemeldet nahtlos, die Server in Ihrer Umgebung zu verwalten. 

[Informationen Sie zu anderen Bereitstellungsoptionen Windows Admin Center.](../plan/installation-options.md)

## Voraussetzungen

- Ein Failovercluster mit 2 oder mehr Knoten unter Windows Server 2016 oder 2019. [Erfahren Sie mehr über die Bereitstellung von einem Failovercluster](../../../failover-clustering/failover-clustering-overview.md).
- Einem freigegebenen Clustervolume (CSV) für Windows Admin Center zum Speichern von Daten, die alle Knoten im Cluster zugegriffen werden kann. 10 GB wird für Ihre CSV ausreichen.
- Skript für hohe Verfügbarkeit der Bereitstellung von [Windows Admin Center HA Skript Zip-Datei](https://aka.ms/WACHAScript). Laden Sie die ZIP-Datei mit dem Skript auf Ihrem lokalen Computer und kopieren Sie das Skript nach Bedarf anhand der folgenden Anleitung.
- Empfohlene, aber optional: ein signiertes Zertifikat PFX & Kennwort. Sie müssen das Zertifikat auf den Clusterknoten bereits installiert haben – das Skript ausführen, die für Sie. Wenn Sie nicht bereitgestellt wird, generiert das Installationsskript ein selbstsigniertes Zertifikat, das nach 60 Tagen abgelaufen ist.

## Installieren von Windows Admin Center auf einem Failovercluster

1. Kopieren der ```Install-WindowsAdminCenterHA.ps1``` Skript auf einem Knoten im Cluster festzulegen. Laden Sie oder kopieren Sie die Windows Admin Center MSI-Datei mit dem gleichen Knoten.
2. Eine Verbindung mit dem Knoten über RDP und führen Sie die ```Install-WindowsAdminCenterHA.ps1``` Skript aus, mit den folgenden Parametern:
    - `-clusterStorage`: den lokalen Pfad des Cluster Shared Volume, dass Windows Admin Center-Daten gespeichert.
    - `-clientAccessPoint`: Wählen Sie einen Namen, mit denen Sie Windows Admin Center zugreifen. Beispielsweise, wenn Sie das Skript mit der Parameter auszuführen `-clientAccessPoint contosoWindowsAdminCenter`, werden Sie auf den Windows Admin Center-Dienst zugreifen, Vorsichtsmaßnahmen `https://contosoWindowsAdminCenter.<domain>.com`
    - `-staticAddress`: Optional. Eine oder mehrere statische Adressen für den allgemeinen Cluster-Dienst. 
    - `-msiPath`: Der Pfad für die Windows Admin Center MSI-Datei.
    - `-certPath`: Optional. Der Pfad für ein Zertifikat PFX-Datei.
    - `-certPassword`: Optional. Ein SecureString Kennwort für das Zertifikat PFX-Datei finden Sie unter `-certPath`
    - `-generateSslCert`: Optional. Wenn Sie kein Zertifikats bereitstellen möchten, fügen Sie dieses Flag Parameter, um ein selbstsigniertes Zertifikat zu generieren. Beachten Sie, dass das selbstsignierte Zertifikat innerhalb von 60 Tagen ablaufen.
    - `-portNumber`: Optional. Wenn Sie einen Port angeben, wird der Gatewaydienst auf Port 443 (HTTPS) bereitgestellt. Um verwenden ein anderen Port angeben in dieser Parameter. Beachten Sie, wenn Sie einen benutzerdefinierten Port (nichts neben 443) verwenden, Sie das Windows Admin Center zugreifen müssen, indem https://\<clientAccessPoint\>:\<port\> soll.

> [!NOTE]
> Die ```Install-WindowsAdminCenterHA.ps1``` Skript unterstützt ```-WhatIf ``` und ```-Verbose``` Parameter

### Beispiele

#### Installieren Sie ein Zertifikat:

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

#### Installieren Sie ein selbstsigniertes Zertifikat:

```powershell
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -generateSslCert -Verbose
```

## Aktualisieren einer vorhandenen Installations für hohe Verfügbarkeit

Verwenden Sie dieselben ```Install-WindowsAdminCenterHA.ps1``` Skript, um Ihre Bereitstellung HOCHVERFÜGBARKEITSLÖSUNGEN zu aktualisieren, ohne Verlust von Daten für Ihre.

### Aktualisieren Sie auf eine neue Version von Windows Admin Center

Wenn eine neue Version von Windows Admin Center veröffentlicht wird, führen Sie einfach die ```Install-WindowsAdminCenterHA.ps1``` Skript erneut mit nur die ```msiPath``` Parameter:

```powershell
.\Install-WindowsAdminCenterHA.ps1 -msiPath '.\WindowsAdminCenter.msi' -Verbose
```

### Aktualisieren Sie das Zertifikat zum von Windows Admin Center

Sie können das Zertifikat von einer HOCHVERFÜGBARKEITSLÖSUNGEN Bereitstellung von Windows Admin Center zu einem beliebigen Zeitpunkt durch die Bereitstellung von PFX-Datei für das neue Zertifikat zum Aktualisieren und und das Kennwort.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

Sie können das Zertifikat auch zur gleichen Zeit aktualisieren die Plattform Windows Admin Center mit einer neuen MSI-Datei zu aktualisieren.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
``` 

## Deinstallieren

Um die HOCHVERFÜGBARKEITSLÖSUNGEN Bereitstellung von Windows Admin Center aus den Failovercluster zu deinstallieren, übergeben Sie die ```-Uninstall``` Parameter, um die ```Install-WindowsAdminCenterHA.ps1``` Skript.

```powershell
.\Install-WindowsAdminCenterHA.ps1 -Uninstall -Verbose
```

## Fehlerbehebung

Protokolle werden in der temporäre Ordner, der im CSV-Format (z. B. C:\ClusterStorage\Volume1\temp) gespeichert.