---
title: Erstellen einer Antwortdatei für die BS-Spezialisierung
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 299aa38e-28d2-4cbe-af16-5b8c533eba1f
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 5717fcc9e1732b6273620e633c140c6df58ec8b7
ms.sourcegitcommit: 29ad32b9dea298a7fe81dcc33d2a42d383018e82
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65624657"
---
# <a name="create-os-specialization-answer-file"></a>Erstellen einer Antwortdatei für die BS-Spezialisierung

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Als Vorbereitung für die geschützte virtuelle Computer bereitstellen müssen Sie eine Betriebssystem-Spezialisierung-Antwortdatei erstellen. Auf Windows ist dies häufig als die Datei "unattend.xml" bezeichnet. Die **New-ShieldingDataAnswerFile** Windows PowerShell-Funktion können Sie dies tun. Sie können dann mithilfe der Antwortdatei, die Sie beim Erstellen aus einer Vorlage von VMs abgeschirmten mithilfe von System Center Virtual Machine Manager (oder jeder anderen fabriccontroller).

Allgemeine Richtlinien für die unbeaufsichtigte Installation von Dateien für abgeschirmte VMs, finden Sie unter [Erstellen einer Antwortdatei](guarded-fabric-tenant-creates-shielding-data.md#create-an-answer-file).
 
## <a name="downloading-the-new-shieldingdataanswerfile-function"></a>Die Funktion New-ShieldingDataAnswerFile herunterladen

Sie erhalten die **New-ShieldingDataAnswerFile** -Funktion aus der [PowerShell-Katalog](https://aka.ms/gftools). Wenn Ihr Computer über Internetkonnektivität verfügt, können Sie es in PowerShell mit dem folgenden Befehl installieren:

```powershell
Install-Module GuardedFabricTools -Repository PSGallery -MinimumVersion 1.0.0
```

Die `unattend.xml` Ausgabe kann in der geschützten Daten, zusammen mit zusätzlichen Elemente gepackt werden, damit, dass sie zum Erstellen abgeschirmter VMs aus Vorlagen verwendet werden kann.

Die folgenden Abschnitte zeigen die Funktionsparameter für die Verwendung einer `unattend.xml` Datei, die verschiedene Optionen enthält:

- [Grundlegende Windows-Antwortdatei](#basic-windows-answer-file)
- [Windows-Antwortdatei mit Domänenbeitritt](#windows-answer-file-with-domain-join)
- [Windows-Antwortdatei mit statischen IPv4-Adressen](#windows-answer-file-with-static-ipv4-addresses)
- [Windows-Antwortdatei mit dem benutzerdefinierten Gebietsschema](#windows-answer-file-with-a-custom-locale)
- [Einfache Linux-Antwortdatei](#basic-linux-answer-file)

## <a name="basic-windows-answer-file"></a>Grundlegende Windows-Antwortdatei

Die folgenden Befehle erstellen eine Windows-Antwortdatei, die einfach das Kennwort für das Administratorkonto und die Hostnamen festlegt.
Die Netzwerkadapter der virtuellen Computer DHCP zum Abrufen der IP-Adressen verwendet werden, und der virtuelle Computer wird nicht auf Active Directory-Domäne verknüpft werden.
Geben Sie bei Aufforderung zur Eingabe der Anmeldeinformationen eines Administrators den gewünschten Benutzernamen und das Kennwort ein.
Verwenden Sie "Administrator" für den Benutzernamen ein, wenn Sie das integrierte Administratorkonto konfigurieren möchten.

```powershell
$adminCred = Get-Credential -Message "Local administrator account"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred
```

## <a name="windows-answer-file-with-domain-join"></a>Windows-Antwortdatei mit Domänenbeitritt

Die folgenden Befehle erstellen eine Windows-Antwortdatei, die die abgeschirmte VM mit einer Active Directory-Domäne verknüpft.
Die VM-Netzwerkadapter werden DHCP verwendet, um IP-Adressen zu erhalten.

Die erste Eingabeaufforderung fragt die Kontoinformationen für den lokalen Administrator.
Verwenden Sie "Administrator" für den Benutzernamen ein, wenn Sie das integrierte Administratorkonto konfigurieren möchten.

Die zweite administratoranmeldeaufforderung fordert zur Eingabe von Anmeldeinformationen, die berechtigt sind, den Computer in Active Directory-Domäne einbinden.

Achten Sie darauf, dass Sie zum Ändern des Werts von der "-Domänenname" Parameter, um den vollqualifizierten Domänennamen des Active Directory-Domäne.

```powershell
$adminCred = Get-Credential -Message "Local administrator account"
$domainCred = Get-Credential -Message "Domain join credentials"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred -DomainName 'my.contoso.com' -DomainJoinCredentials $domainCred
```
## <a name="windows-answer-file-with-static-ipv4-addresses"></a>Windows-Antwortdatei mit statischen IPv4-Adressen

Die folgenden Befehle erstellen eine Windows-Antwortdatei, die statische IP-Adressen, die zum Zeitpunkt der Bereitstellung von der Fabric-Manager, z. B. System Center Virtual Machine Manager bereitgestellten verwendet.

Virtual Machine Manager bietet drei Komponenten an die statische IP-Adresse mit einer IP-Adresspool: IPv4-Adresse, IPv6-Adresse, Gateway-Adresse und DNS-Adresse. Wenn Sie möchten alle zusätzlichen Felder einbezogen werden oder eine benutzerdefinierte Netzwerkkonfiguration erforderlich, müssen Sie manuell bearbeiten, die Antwortdatei, die vom Skript erstellt.

Die folgenden Screenshots zeigen die IP-Adresspools, Sie in Virtual Machine Manager konfigurieren können. Diese Pools sind erforderlich, wenn Sie statische IP-Adresse verwenden möchten.

Die Funktion unterstützt derzeit nur einen DNS-Server. So sieht die DNS-Einstellungen würde folgendermaßen aussehen:

![Konfigurieren von DNS-Server mit statischen IP-pool](../media/Guarded-Fabric-Shielded-VM/guarded-host-unattend-static-ip-address-pool-dns-settings.png)

Hier ist Ihre Zusammenfassung für die statische IP-Adresspool erstellen würde folgendermaßen aussehen. Kurz gesagt, benötigen Sie nur eine Netzwerkroute, ein Gateway und ein DNS-Server -, und Sie müssen die IP-Adresse angeben.

![Zusammenfassung der Erstellung der statischen IP-Pools](../media/Guarded-Fabric-Shielded-VM/guarded-host-unattend-static-ip-address-pool-summary.png)

Sie müssen die Netzwerkadapter für den virtuellen Computer zu konfigurieren. Der folgende Screenshot zeigt, wo Sie festgelegt, dass die Konfiguration und wie Sie es und statische IP-Adresse zu wechseln.

![Konfigurieren der Hardware, um statische IP-Adresse zu verwenden.](../media/Guarded-Fabric-Shielded-VM/guarded-host-unattend-static-ip-address-pool-network-adapter-settings.png)

Anschließend können Sie die `-StaticIPPool` Parameter, um die statische IP-Elemente in der Antwortdatei einzuschließen. Die Parameter `@IPAddr-1@`, `@NextHop-1-1@`, und `@DNSAddr-1-1@` Antwort auf die Datei dann ersetzt werden durch die tatsächlichen Werte, die Sie in Virtual Machine Manager zum Zeitpunkt der Bereitstellung angegeben.

```powershell
$adminCred = Get-Credential -Message "Local administrator account"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred -StaticIPPool IPv4Address
```

## <a name="windows-answer-file-with-a-custom-locale"></a>Windows-Antwortdatei mit dem benutzerdefinierten Gebietsschema

Die folgenden Befehle erstellen eine Windows-Antwortdatei mit dem benutzerdefinierten Gebietsschema.

Geben Sie bei Aufforderung zur Eingabe der Anmeldeinformationen eines Administrators den gewünschten Benutzernamen und das Kennwort ein.
Verwenden Sie "Administrator" für den Benutzernamen ein, wenn Sie das integrierte Administratorkonto konfigurieren möchten.

```powershell
$adminCred = Get-Credential -Message "Local administrator account"
$domainCred = Get-Credential -Message "Domain join credentials"

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -AdminCredentials $adminCred -Locale es-ES
```

## <a name="basic-linux-answer-file"></a>Einfache Linux-Antwortdatei

Ab Windows Server-Version 1709, können Sie bestimmte Linux-Gastbetriebssysteme in abgeschirmte VMs ausführen.
Wenn Sie den System Center Virtual Machine Manager-Linux-Agent spezialisiert werden diese virtuellen Computer verwenden, kann das Cmdlet "New-ShieldingDataAnswerFile" kompatible Antwortdateien dafür erstellen.

In einem Linux-Antwortdatei enthalten Sie in der Regel die Root-Kennwort, Root-SSH-Schlüssel und optional auch statische IP-Pool-Informationen.
Ersetzen Sie den Pfad zu der öffentliche Hälfte Ihres SSH-Schlüssels, bevor Sie das folgende Skript ausführen.

```powershell
$rootPassword = Read-Host -Prompt "Root password" -AsSecureString

New-ShieldingDataAnswerFile -Path '.\ShieldedVMAnswerFile.xml' -RootPassword $rootPassword -RootSshKey '~\.ssh\id_rsa.pub'
```

## <a name="see-also"></a>Siehe auch

- [Bereitstellen von abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [Geschütztes Fabric und abgeschirmte VMs](guarded-fabric-and-shielded-vms-top-node.md)
