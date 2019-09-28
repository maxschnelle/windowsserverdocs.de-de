---
title: Konfigurieren zusätzlicher HGS-Knoten
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 227f723b-acb2-42a7-bbe3-44e82f930e35
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 10/22/2018
ms.openlocfilehash: 5277a97f7f58d9d7edb1457cb363cb6ddf1d8b59
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403696"
---
# <a name="configure-additional-hgs-nodes"></a>Konfigurieren zusätzlicher HGS-Knoten

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

In Produktionsumgebungen sollten HGS in einem Cluster mit hoher Verfügbarkeit eingerichtet werden, um sicherzustellen, dass abgeschirmte VMS auch dann eingeschaltet werden können, wenn ein HGS-Knoten ausfällt. Für Testumgebungen sind keine sekundären HGS-Knoten erforderlich.

Verwenden Sie eine dieser Methoden, um HGS-Knoten hinzuzufügen, die für Ihre Umgebung am besten geeignet sind.

|                |                         |                              | 
|----------------|-------------------------|------------------------------|
|Neue HGS-Gesamtstruktur  | [Verwenden von PFX-Dateien](#dedicated-hgs-forest-with-pfx-certificates) | [Verwenden von Zertifikat Fingerabdrücken](#dedicated-hgs-forest-with-certificate-thumbprints) |
|Vorhandene geschützte Gesamtstruktur |  [Verwenden von PFX-Dateien](#existing-bastion-forest-with-pfx-certificates) | [Verwenden von Zertifikat Fingerabdrücken](#existing-bastion-forest-with-certificate-thumbprints) |

## <a name="prerequisites"></a>Erforderliche Komponenten

Stellen Sie sicher, dass jeder zusätzliche Knoten: 
- Hat dieselbe Hardware-und Softwarekonfiguration wie der primäre Knoten. 
- Ist mit dem gleichen Netzwerk verbunden wie die anderen HGS-Server
- Kann die anderen HGS-Server anhand Ihrer DNS-Namen auflösen

## <a name="dedicated-hgs-forest-with-pfx-certificates"></a>Dedizierte HGS-Gesamtstruktur mit PFX-Zertifikaten

1. Herauf Stufen des HGS-Knotens zu einem Domänen Controller
2. Initialisieren des HGS-Servers

### <a name="promote-the-hgs-node-to-a-domain-controller"></a>Herauf Stufen des HGS-Knotens zu einem Domänen Controller

[!INCLUDE [Promote to a domain controller](../../../includes/guarded-fabric-promote-domain-controller.md)] 

### <a name="initialize-the-hgs-server"></a>Initialisieren des HGS-Servers

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="dedicated-hgs-forest-with-certificate-thumbprints"></a>Dedizierte HGS-Gesamtstruktur mit Zertifikat Fingerabdrücken
 
1. Herauf Stufen des HGS-Knotens zu einem Domänen Controller
2. Initialisieren des HGS-Servers
3. Installieren der privaten Schlüssel für die Zertifikate

### <a name="promote-the-hgs-node-to-a-domain-controller"></a>Herauf Stufen des HGS-Knotens zu einem Domänen Controller

[!INCLUDE [Promote to a domain controller](../../../includes/guarded-fabric-promote-domain-controller.md)] 

### <a name="initialize-the-hgs-server"></a>Initialisieren des HGS-Servers

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

### <a name="install-the-private-keys-for-the-certificates"></a>Installieren der privaten Schlüssel für die Zertifikate

[!INCLUDE [Install private keys](../../../includes/guarded-fabric-install-private-keys.md)]

## <a name="existing-bastion-forest-with-pfx-certificates"></a>Vorhandene geschützte Gesamtstruktur mit PFX-Zertifikaten

1. Fügen Sie den Knoten der vorhandenen Domäne hinzu.
2. Erteilen Sie dem Computer Rechte zum Abrufen des GMSA-Kennworts und Ausführen von Install-ADServiceAccount.
3. Initialisieren des HGS-Servers

### <a name="join-the-node-to-the-existing-domain"></a>Fügen Sie den Knoten der vorhandenen Domäne hinzu.

1. Stellen Sie sicher, dass mindestens eine NIC auf dem Knoten für die Verwendung des DNS-Servers auf dem ersten HGS-Server konfiguriert ist.
2. Verknüpfen Sie den neuen HGS-Knoten mit derselben Domäne wie der erste HGS-Knoten. 

### <a name="grant-the-machine-rights-to-retrieve-gmsa-password-and-run-install-adserviceaccount"></a>Erteilen Sie dem Computer Rechte zum Abrufen des GMSA-Kennworts und Ausführen von Install-ADServiceAccount.

[!INCLUDE [Grant the machine rights to retrieve the group MSA](../../../includes/guarded-fabric-grant-machine-rights-to-retrieve-gmsa.md)] 

### <a name="initialize-the-hgs-server"></a>Initialisieren des HGS-Servers

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="existing-bastion-forest-with-certificate-thumbprints"></a>Vorhandene geschützte Gesamtstruktur mit Zertifikat Fingerabdruck

1. Fügen Sie den Knoten der vorhandenen Domäne hinzu.
2. Erteilen Sie dem Computer Rechte zum Abrufen des GMSA-Kennworts und Ausführen von Install-ADServiceAccount.
3. Initialisieren des HGS-Servers
4. Installieren der privaten Schlüssel für die Zertifikate

### <a name="join-the-node-to-the-existing-domain"></a>Fügen Sie den Knoten der vorhandenen Domäne hinzu.

1. Stellen Sie sicher, dass mindestens eine NIC auf dem Knoten für die Verwendung des DNS-Servers auf dem ersten HGS-Server konfiguriert ist.
2. Verknüpfen Sie den neuen HGS-Knoten mit derselben Domäne wie der erste HGS-Knoten. 

### <a name="grant-the-machine-rights-to-retrieve-gmsa-password-and-run-install-adserviceaccount"></a>Erteilen Sie dem Computer Rechte zum Abrufen des GMSA-Kennworts und Ausführen von Install-ADServiceAccount.

[!INCLUDE [Grant the machine rights to retrieve the group MSA](../../../includes/guarded-fabric-grant-machine-rights-to-retrieve-gmsa.md)] 

### <a name="initialize-the-hgs-server"></a>Initialisieren des HGS-Servers

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

Es dauert bis zu 10 Minuten, bis die Verschlüsselungs-und Signatur Zertifikate vom ersten HGS-Server auf diesen Knoten repliziert werden.

### <a name="install-the-private-keys-for-the-certificates"></a>Installieren der privaten Schlüssel für die Zertifikate

[!INCLUDE [Install private keys](../../../includes/guarded-fabric-install-private-keys.md)]

## <a name="configure-hgs-for-https-communications"></a>Konfigurieren von HGS für die HTTPS-Kommunikation

Wenn Sie HGS-Endpunkte mit einem SSL-Zertifikat sichern möchten, müssen Sie das SSL-Zertifikat auf diesem Knoten sowie alle anderen Knoten im HGS-Cluster konfigurieren.
SSL-Zertifikate *werden nicht* von HGS repliziert und müssen nicht die gleichen Schlüssel für jeden Knoten verwenden (d. h., Sie können für jeden Knoten unterschiedliche SSL-Zertifikate verwenden).

Wenn Sie ein SSL-Zertifikat anfordern, stellen Sie sicher, dass der voll qualifizierte Cluster Domänen Name `Get-HgsServer`(wie in der Ausgabe von gezeigt) entweder der allgemeine Antragsteller Name des Zertifikats ist oder als alternativer Antragsteller Name angegeben ist.
Wenn Sie ein Zertifikat von Ihrer Zertifizierungsstelle erhalten haben, können Sie HGS so konfigurieren, dass es mit [Set-hgsserver](https://technet.microsoft.com/itpro/powershell/windows/hgsserver/set-hgsserver)verwendet wird.

```powershell
$sslPassword = Read-Host -AsSecureString -Prompt "SSL Certificate Password"
Set-HgsServer -Http -Https -HttpsCertificatePath 'C:\temp\HgsSSLCertificate.pfx' -HttpsCertificatePassword $sslPassword
```

Wenn Sie das Zertifikat bereits im lokalen Zertifikat Speicher installiert haben und es per Fingerabdruck referenzieren möchten, führen Sie stattdessen den folgenden Befehl aus:

```powershell
Set-HgsServer -Http -Https -HttpsCertificateThumbprint 'A1B2C3D4E5F6...'
```

HGS macht immer die HTTP-und HTTPS-Ports für die Kommunikation verfügbar.
Das Entfernen der HTTP-Bindung in IIS wird nicht unterstützt. Sie können jedoch die Windows-Firewall oder andere netzwerkfirewalltechnologien verwenden, um die Kommunikation über Port 80 zu blockieren.

## <a name="decommission-an-hgs-node"></a>Außerbetriebsetzen eines HGS-Knotens

So setzen Sie einen HGS-Knoten außer Betrieb:

1. [Löschen Sie die HGS-Konfiguration](guarded-fabric-manage-hgs.md#clearing-the-hgs-configuration).

   Dadurch wird der Knoten aus dem Cluster entfernt und der Nachweis und die Schlüsselschutz Dienste deinstalliert. 
   Wenn es sich um den letzten Knoten im Cluster handelt, wird-Force benötigt, um anzugeben, dass der letzte Knoten entfernt und der Cluster in Active Directory zerstört werden soll. 
   
   Wenn HGS in einer geschützten Gesamtstruktur (Standard) bereitgestellt wird, ist dies der einzige Schritt. 
   Optional können Sie den Computer aus der Domäne entfernen und das GMSA-Konto aus Active Directory entfernen.

1. Wenn HGS eine eigene Domäne erstellt haben, sollten Sie auch [HGS deinstallieren](guarded-fabric-manage-hgs.md#clearing-the-hgs-configuration) , um den Beitritt zur Domäne zu entfernen und den Domänen Controller herabzusetzen.



## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Überprüfen der HGS-Konfiguration](guarded-fabric-verify-hgs-configuration.md)

