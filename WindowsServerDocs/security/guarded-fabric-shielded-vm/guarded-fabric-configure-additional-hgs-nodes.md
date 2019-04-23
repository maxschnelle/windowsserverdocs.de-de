---
title: Konfigurieren zusätzlicher HGS-Knoten
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 227f723b-acb2-42a7-bbe3-44e82f930e35
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 10/22/2018
ms.openlocfilehash: a89337457cc71ffee78e3f73fecc2262f1fb38e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855201"
---
# <a name="configure-additional-hgs-nodes"></a>Konfigurieren zusätzlicher HGS-Knoten

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In produktionsumgebungen sollte Host-Überwachungsdienst in einem Cluster mit hochverfügbarkeit eingerichtet werden, um sicherzustellen, dass geschützte VMs auf unterstützt werden können, selbst wenn ein Host-Überwachungsdienst-Knoten ausfällt. Host-Überwachungsdienst Sekundärknoten sind für testumgebungen geeignet jedoch, nicht erforderlich.

Verwenden Sie eine der folgenden Methoden zum Hinzufügen von Host-Überwachungsdienst-Knoten, wie am besten für Ihre Umgebung geeignet ist.

|                |                         |                              | 
|----------------|-------------------------|------------------------------|
|Neuen Host-Überwachungsdienst-Gesamtstruktur  | [Verwenden die PFX-Dateien](#dedicated-hgs-forest-with-pfx-certificates) | [Anstelle des Zertifikatfingerabdrucks](#dedicated-hgs-forest-with-certificate-thumbprints) |
|Vorhandene geschützten Gesamtstruktur |  [Verwenden die PFX-Dateien](#existing-bastion-forest-with-pfx-certificates) | [Anstelle des Zertifikatfingerabdrucks](#existing-bastion-forest-with-certificate-thumbprints) |

## <a name="prerequisites"></a>Vorraussetzungen

Stellen Sie sicher, dass jeder zusätzliche Knoten: 
- Hat die gleiche Hardware und Software-Konfiguration wie der primäre Knoten 
- Mit dem gleichen Netzwerk wie die anderen HGS-Server verbunden ist
- Die anderen HGS-Server können durch ihre DNS-Namen aufgelöst werden.

## <a name="dedicated-hgs-forest-with-pfx-certificates"></a>Dedizierte Host-Überwachungsdienst-Gesamtstruktur mit der PFX-Zertifikate

1. Den Host-Überwachungsdienst-Knoten zu einem Domänencontroller heraufstufen
2. Initialisieren Sie den Host-Überwachungsdienst-server

### <a name="promote-the-hgs-node-to-a-domain-controller"></a>Den Host-Überwachungsdienst-Knoten zu einem Domänencontroller heraufstufen

[!INCLUDE [Promote to a domain controller](../../../includes/guarded-fabric-promote-domain-controller.md)] 

### <a name="initialize-the-hgs-server"></a>Initialisieren Sie den Host-Überwachungsdienst-server

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="dedicated-hgs-forest-with-certificate-thumbprints"></a>Dedizierte Host-Überwachungsdienst-Gesamtstruktur mit Fingerabdrücke für clusterzertifikat
 
1. Den Host-Überwachungsdienst-Knoten zu einem Domänencontroller heraufstufen
2. Initialisieren Sie den Host-Überwachungsdienst-server
3. Installieren Sie die privaten Schlüssel für die Zertifikate

### <a name="promote-the-hgs-node-to-a-domain-controller"></a>Den Host-Überwachungsdienst-Knoten zu einem Domänencontroller heraufstufen

[!INCLUDE [Promote to a domain controller](../../../includes/guarded-fabric-promote-domain-controller.md)] 

### <a name="initialize-the-hgs-server"></a>Initialisieren Sie den Host-Überwachungsdienst-server

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

### <a name="install-the-private-keys-for-the-certificates"></a>Installieren Sie die privaten Schlüssel für die Zertifikate

[!INCLUDE [Install private keys](../../../includes/guarded-fabric-install-private-keys.md)]

## <a name="existing-bastion-forest-with-pfx-certificates"></a>Vorhandene geschützten Gesamtstruktur mit der PFX-Zertifikate

1. Fügen Sie den Knoten mit der vorhandenen Domäne
2. Erteilen Sie Computer Rechte zum Abrufen von gMSA-Kennwort und zum Ausführen von Install-ADServiceAccount
3. Initialisieren Sie den Host-Überwachungsdienst-server

### <a name="join-the-node-to-the-existing-domain"></a>Fügen Sie den Knoten mit der vorhandenen Domäne

1. Stellen Sie sicher, dass mindestens eine Netzwerkkarte auf dem Knoten für die Verwendung von des DNS-Servers auf dem ersten HGS-Server konfiguriert ist.
2. Verknüpfen Sie den neuen Knoten für den Host-Überwachungsdienst, mit der gleichen Domäne wie Ihre ersten Knoten für den Host-Überwachungsdienst. 

### <a name="grant-the-machine-rights-to-retrieve-gmsa-password-and-run-install-adserviceaccount"></a>Erteilen Sie Computer Rechte zum Abrufen von gMSA-Kennwort und zum Ausführen von Install-ADServiceAccount

[!INCLUDE [Grant the machine rights to retrieve the group MSA](../../../includes/guarded-fabric-grant-machine-rights-to-retrieve-gmsa.md)] 

### <a name="initialize-the-hgs-server"></a>Initialisieren Sie den Host-Überwachungsdienst-server

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

## <a name="existing-bastion-forest-with-certificate-thumbprints"></a>Vorhandene geschützten Gesamtstruktur mit Fingerabdrücke für clusterzertifikat

1. Fügen Sie den Knoten mit der vorhandenen Domäne
2. Erteilen Sie Computer Rechte zum Abrufen von gMSA-Kennwort und zum Ausführen von Install-ADServiceAccount
3. Initialisieren Sie den Host-Überwachungsdienst-server
4. Installieren Sie die privaten Schlüssel für die Zertifikate

### <a name="join-the-node-to-the-existing-domain"></a>Fügen Sie den Knoten mit der vorhandenen Domäne

1. Stellen Sie sicher, dass mindestens eine Netzwerkkarte auf dem Knoten für die Verwendung von des DNS-Servers auf dem ersten HGS-Server konfiguriert ist.
2. Verknüpfen Sie den neuen Knoten für den Host-Überwachungsdienst, mit der gleichen Domäne wie Ihre ersten Knoten für den Host-Überwachungsdienst. 

### <a name="grant-the-machine-rights-to-retrieve-gmsa-password-and-run-install-adserviceaccount"></a>Erteilen Sie Computer Rechte zum Abrufen von gMSA-Kennwort und zum Ausführen von Install-ADServiceAccount

[!INCLUDE [Grant the machine rights to retrieve the group MSA](../../../includes/guarded-fabric-grant-machine-rights-to-retrieve-gmsa.md)] 

### <a name="initialize-the-hgs-server"></a>Initialisieren Sie den Host-Überwachungsdienst-server

[!INCLUDE [Initialize the HGS server](../../../includes/guarded-fabric-initialize-hgs-on-the-node.md)] 

Es dauert bis zu 10 Minuten für die Verschlüsselung und Signaturzertifikate aus den ersten Host-Überwachungsdienst-Server auf diesem Knoten repliziert.

### <a name="install-the-private-keys-for-the-certificates"></a>Installieren Sie die privaten Schlüssel für die Zertifikate

[!INCLUDE [Install private keys](../../../includes/guarded-fabric-install-private-keys.md)]

## <a name="configure-hgs-for-https-communications"></a>Konfigurieren von Host-Überwachungsdienst für HTTPS-Kommunikation

Wenn Sie Host-Überwachungsdienst-Endpunkte mit dem ein SSL-Zertifikat schützen möchten, müssen Sie das SSL-Zertifikat auf diesem Knoten als auch alle anderen Knoten im Cluster-Host-Überwachungsdienst konfigurieren.
SSL-Zertifikate *nicht* von Host-Überwachungsdienst repliziert und müssen nicht für jeden Knoten die gleichen Schlüssel verwenden (d. h. Sie können ein andere SSL-Zertifikate für jeden Knoten haben).

Wenn Sie ein SSL-Zertifikat anfordern, stellen Sie sicher mit der Cluster vollständig qualifizierten Domänennamen (wie gezeigt in der Ausgabe des `Get-HgsServer`) ist entweder der allgemeine Antragstellername des Zertifikats oder einen alternativen DNS-Namen enthalten.
Wenn Sie ein Zertifikat von Ihrer Zertifizierungsstelle erhalten haben, können Sie konfigurieren, dass HGS für die Verwendung zusammen mit [Set-HgsServer](https://technet.microsoft.com/itpro/powershell/windows/hgsserver/set-hgsserver).

```powershell
$sslPassword = Read-Host -AsSecureString -Prompt "SSL Certificate Password"
Set-HgsServer -Http -Https -HttpsCertificatePath 'C:\temp\HgsSSLCertificate.pfx' -HttpsCertificatePassword $sslPassword
```

Wenn Sie bereits das Zertifikat im lokalen Zertifikatspeicher installiert, und es durch Fingerabdruck verweisen möchten, führen Sie stattdessen den folgenden Befehl aus:

```powershell
Set-HgsServer -Http -Https -HttpsCertificateThumbprint 'A1B2C3D4E5F6...'
```

Host-Überwachungsdienst wird immer die HTTP- und HTTPS-Ports für die Kommunikation verfügbar machen.
Es ist nicht unterstützt, die die HTTP-Bindung in IIS zu entfernen, aber Sie die Windows-Firewall oder andere Netzwerk-Firewall-Technologien verwenden können, um die Kommunikation über Port 80 blockiert.

## <a name="decommission-an-hgs-node"></a>Außerbetriebsetzung eines Host-Überwachungsdienst-Knotens

Einen Host-Überwachungsdienst-Knoten außer Betrieb genommen werden:

1. [Deaktivieren Sie die Konfiguration des Host-Überwachungsdienst](guarded-fabric-manage-hgs.md#clearing-the-hgs-configuration).

   Dadurch wird der Knoten aus dem Cluster entfernt und deinstalliert den Nachweis- und Schlüsselschutz-Dienste. 
   Wenn sie den letzten Knoten im Cluster ist, - Force ist erforderlich, um anzugeben, Sie möchten, entfernen Sie den letzten Knoten, und entfernen Sie den Cluster in Active Directory. 
   
   Wenn in einer geschützten Gesamtstruktur (Standard), Host-Überwachungsdienst, das ist der einzige Schritt bereitgestellt wird. 
   Sie können optional den Computer aus der Domäne entfernen und entfernen das gMSA-Konto aus Active Directory.

1. Wenn HGS eine eigenen Domäne erstellt haben, sollten Sie auch [Deinstallieren von Host-Überwachungsdienst](guarded-fabric-manage-hgs.md#clearing-the-hgs-configuration) entfernen die Domäne und zu Herabstufung des Domänencontrollers.



## <a name="next-step"></a>Nächster Schritt

>[!div class="nextstepaction"]
[Überprüfen Sie die Konfiguration des Host-Überwachungsdienst](guarded-fabric-verify-hgs-configuration.md)

