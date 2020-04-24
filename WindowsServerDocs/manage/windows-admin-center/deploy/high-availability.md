---
title: Bereitstellen von Windows Admin Center mit Hochverfügbarkeit
description: Bereitstellen von Windows Admin Center mit Hochverfügbarkeit (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 6ae7bd9ed7aee5835ac1f53b9e10879ad8824f52
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "71406942"
---
# <a name="deploy-windows-admin-center-with-high-availability"></a>Bereitstellen von Windows Admin Center mit Hochverfügbarkeit

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Du kannst Windows Admin Center in einem Failovercluster bereitstellen, um eine Hochverfügbarkeit für deinen Windows Admin Center-Gatewaydienst sicherzustellen. Die bereitgestellte Lösung ist eine Aktiv-Passiv-Lösung, bei der nur eine Instanz von Windows Admin Center aktiv ist. Wenn einer der Knoten im Cluster ausfällt, wechselt Windows Admin Center problemlos zu einem anderen Knoten, sodass die Server in der Umgebung problemlos weiter verwaltet werden können. 

[Weitere Informationen zu anderen Windows Admin Center-Bereitstellungsoptionen.](../plan/installation-options.md)

## <a name="prerequisites"></a>Voraussetzungen

- Ein Failovercluster mit mindestens zwei Knoten unter Windows Server 2016 oder 2019. [Weitere Informationen zum Bereitstellen eines Failoverclusters](../../../failover-clustering/failover-clustering-overview.md).
- Ein freigegebenes Clustervolume (CSV) für Windows Admin Center zum Speichern persistenter Daten, auf die von allen Knoten im Cluster zugegriffen werden kann. 10 GB sind für dein CSV ausreichend.
- Bereitstellungsskript für Hochverfügbarkeit aus der [Windows Admin Center HA-ZIP-Skriptdatei](https://aka.ms/WACHAScript). Lade die ZIP-Datei, die das Skript enthält, auf deinen lokalen Computer herunter, und kopiere das Skript dann nach Bedarf auf der Grundlage des nachfolgenden Leitfadens.
- Empfohlen, aber optional: eine signierte PFX-Zertifikatdatei und ein Kennwort. Das Zertifikat muss nicht bereits auf den Clusterknoten installiert sein, das Skript erledigt das für dich. Wenn du keins zur Verfügung stellst, generiert das Installationsskript ein selbstsigniertes Zertifikat, das nach 60 Tagen abläuft.

## <a name="install-windows-admin-center-on-a-failover-cluster"></a>Installieren von Windows Admin Center auf einem Failovercluster

1. Kopiere das Skript ```Install-WindowsAdminCenterHA.ps1``` auf einen Knoten in deinem Cluster. Lade die MSI-Datei von Windows Admin Center herunter oder kopiere es auf denselben Knoten.
2. Stelle über RDP eine Verbindung zum Knoten her, und führe das Skript ```Install-WindowsAdminCenterHA.ps1``` von diesem Knoten mit den folgenden Parametern aus:
    - `-clusterStorage`: Der lokale Pfad des freigegebenen Clustervolumes zum Speichern der Windows Admin Center-Daten.
    - `-clientAccessPoint`: Wähle einen Namen aus, der für den Zugriff auf Windows Admin Center verwendet wird. Wenn du z. B. ein Skript mit dem Parameter `-clientAccessPoint contosoWindowsAdminCenter` ausführst, greifst du auf den Windows Admin Center-Dienst zu, indem du `https://contosoWindowsAdminCenter.<domain>.com` besuchst.
    - `-staticAddress`: Optional. Mindestens eine statische Adresse für den allgemeinen Clusterdienst. 
    - `-msiPath`: Der Pfad für die MSI-Datei von Windows Admin Center.
    - `-certPath`: Optional. Der Pfad für eine PFX-Zertifikatdatei.
    - `-certPassword`: Optional. Ein SecureString-Kennwort für die in `-certPath` bereitgestellte PFX-Zertifikatdatei.
    - `-generateSslCert`: Optional. Wenn du kein signiertes Zertifikat bereitstellen möchtest, beziehe dieses Parameterflag ein, um ein selbstsigniertes Zertifikat zu generieren. Es ist zu beachten, dass die selbstsignierten Zertifikate nach 60 Tagen ablaufen.
    - `-portNumber`: Optional. Wenn kein Port angegeben ist, wird der Gatewaydienst an Port 443 (HTTPS) bereitgestellt. Gib diesen Parameter an, um einen anderen Port zu verwenden. Es ist zu beachten, dass bei Verwendung eines benutzerdefinierten Ports (alles außer 443) auf Windows Admin Center zugegriffen wird, indem du zu https://\<clientAccessPoint\>:\<port\> wechselst.

> [!NOTE]
> Das Skript ```Install-WindowsAdminCenterHA.ps1``` unterstützt die Parameter ```-WhatIf ``` und ```-Verbose```.

### <a name="examples"></a>Beispiele

#### <a name="install-with-a-signed-certificate"></a>Installieren mit einem signierten Zertifikat:

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

#### <a name="install-with-a-self-signed-certificate"></a>Installieren mit einem selbstsignierten Zertifikat:

```powershell
.\Install-WindowsAdminCenterHA.ps1 -clusterStorage "C:\ClusterStorage\Volume1" -clientAccessPoint "contoso-ha-gateway" -msiPath ".\WindowsAdminCenter.msi" -generateSslCert -Verbose
```

## <a name="update-an-existing-high-availability-installation"></a>Aktualisieren einer vorhandenen Hochverfügbarkeitsinstallation

Verwende dasselbe ```Install-WindowsAdminCenterHA.ps1```-Skript, um deine Hochverfügbarkeitsbereitstellung zu aktualisieren, ohne die Verbindungsdaten zu verlieren.

### <a name="update-to-a-new-version-of-windows-admin-center"></a>Aktualisieren auf eine neue Version von Windows Admin Center

Wenn eine neue Version von Windows Admin Center veröffentlicht wird, führe das Skript ```Install-WindowsAdminCenterHA.ps1``` einfach nur mit dem Parameter ```msiPath``` erneut aus:

```powershell
.\Install-WindowsAdminCenterHA.ps1 -msiPath '.\WindowsAdminCenter.msi' -Verbose
```

### <a name="update-the-certificate-used-by-windows-admin-center"></a>Aktualisieren des von Windows Admin Center verwendeten Zertifikats

Du kannst das von einer Hochverfügbarkeitsbereitstellung von Windows Admin Center verwendete Zertifikat jederzeit aktualisieren, indem du die PFX-Datei und das Kennwort des neuen Zertifikats angibst.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -certPath "cert.pfx" -certPassword $certPassword -Verbose
```

Es kann gleichzeitig mit der Aktualisierung der Windows Admin Center-Plattform mit einer neuen MSI-Datei auch das Zertifikat aktualisiert werden.

```powershell
$certPassword = Read-Host -AsSecureString
.\Install-WindowsAdminCenterHA.ps1 -msiPath ".\WindowsAdminCenter.msi" -certPath "cert.pfx" -certPassword $certPassword -Verbose
``` 

## <a name="uninstall"></a>Deinstallieren

Um die Hochverfügbarkeitsbereitstellung von Windows Admin Center von deinem Failovercluster zu deinstallieren, übergibst du den Parameter ```-Uninstall``` an das Skript ```Install-WindowsAdminCenterHA.ps1```.

```powershell
.\Install-WindowsAdminCenterHA.ps1 -Uninstall -Verbose
```

## <a name="troubleshooting"></a>Problembehandlung

Protokolle werden im temporären Ordner des CSV gespeichert (z. B. C:\ClusterStorage\Volume1\temp).