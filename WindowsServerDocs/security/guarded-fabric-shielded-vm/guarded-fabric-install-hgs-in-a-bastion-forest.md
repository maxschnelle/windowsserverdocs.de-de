---
title: Host-Überwachungsdienst in einer vorhandenen geschützten Gesamtstruktur installieren
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 147610d9dcb36dfedab3aca11ee1a64731715519
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842221"
---
# <a name="install-hgs-in-an-existing-bastion-forest"></a>Host-Überwachungsdienst in einer vorhandenen geschützten Gesamtstruktur installieren 

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016


## <a name="join-the-hgs-server-to-the-existing-domain"></a>Fügen Sie den Host-Überwachungsdienst-Server mit der vorhandenen Domäne

In einer vorhandenen geschützten Gesamtstruktur muss der Root-Domäne-Host-Überwachungsdienst hinzugefügt werden. Verwenden Sie Server-Manager oder [Add-Computer](https://go.microsoft.com/fwlink/?LinkId=821564) verknüpfen Sie Ihr HGS-Server der Stammdomäne.

## <a name="add-the-hgs-server-role"></a>Fügen Sie die Host-Überwachungsdienst-Serverrolle hinzu.

Führen Sie alle Befehle in diesem Thema, in einer PowerShell-Sitzung mit erhöhten Rechten.

[!INCLUDE [Install the HGS server role](../../../includes/guarded-fabric-install-hgs-server-role.md)] 

Wenn Ihr Rechenzentrum eine sicheren geschützten Gesamtstruktur verfügt, in dem Sie Host-Überwachungsdienst Knoten beitreten möchten, gehen Sie wie folgt vor.
Sie können diese Schritte auch verwenden, 2 oder mehr unabhängigen HGS-Cluster zu konfigurieren, die der gleichen Domäne angehören.

## <a name="join-the-hgs-server-to-the-existing-domain"></a>Fügen Sie den Host-Überwachungsdienst-Server mit der vorhandenen Domäne

Verwenden Sie Server-Manager oder [Add-Computer](https://go.microsoft.com/fwlink/?LinkId=821564) die Host-Überwachungsdienst-Server auf die gewünschte Domäne zu verknüpfen.

## <a name="prepare-active-directory-objects"></a>Vorbereiten von Active Directory-Objekte

Erstellen Sie ein gruppenverwalteten Dienstkonto und 2-Sicherheitsgruppen.
Sie können die Clusterobjekte auch vorab bereitstellen, wenn das Konto, dem Sie Host-Überwachungsdienst mit Initialisieren nicht über die Berechtigung zum Erstellen von Computerobjekten in der Domäne verfügt.

## <a name="group-managed-service-account"></a>Gruppenverwalteten Dienstkontos

Die gruppenverwalteten Dienstkontos (gMSA) ist die Identität, die vom Host-Überwachungsdienst verwendet werden, abrufen und die Zertifikate verwenden. Verwendung [New-ADServiceAccount](https://technet.microsoft.com/itpro/powershell/windows/addsadministration/new-adserviceaccount) um ein gMSA zu erstellen.
Wenn dies die erste gruppenverwalteten Dienstkonten in der Domäne ist, müssen Sie einen Schlüsselverteilungsdienst-Stammschlüssel hinzufügen.

Jeder Host-Überwachungsdienst-Knoten müssen Zugriff auf das gMSA-Kennwort gewährt werden.
Die einfachste Möglichkeit hierzu besteht darin, eine Sicherheitsgruppe zu erstellen, die alle von Ihrem Host-Überwachungsdienst-Knoten enthält und gewähren Sie dieser Sicherheitsgruppe Zugriff zum Abrufen des gMSA-Kennworts.

Sie müssen Ihren HGS-Server neu starten, nach dem Hinzufügen einer Sicherheitsgruppe hinzu, um sicherzustellen, dass sie die neue Gruppenmitgliedschaft abruft.

```powershell
# Check if the KDS root key has been set up
if (-not (Get-KdsRootKey)) {
    # Adds a KDS root key effective immediately (ignores normal 10 hour waiting period)
    Add-KdsRootKey -EffectiveTime ((Get-Date).AddHours(-10))
}

# Create a security group for HGS nodes
$hgsNodes = New-ADGroup -Name 'HgsServers' -GroupScope DomainLocal -PassThru

# Add your HGS nodes to this group
# If your HGS server object is under an organizational unit, provide the full distinguished name instead of "HGS01"
Add-ADGroupMember -Identity $hgsNodes -Members "HGS01"

# Create the gMSA
New-ADServiceAccount -Name 'HGSgMSA' -DnsHostName 'HGSgMSA.yourdomain.com' -PrincipalsAllowedToRetrieveManagedPassword $hgsNodes
```

Das gruppenverwaltete Dienstkonto muss das Recht vor, Ereignisse im Sicherheitsprotokoll auf jedem Host-Überwachungsdienst-Server zu generieren.
Wenn Sie Gruppenrichtlinien, zum Zuweisen von Benutzerrechten zu konfigurieren verwenden, stellen Sie sicher, dass das gMSA-Konto die Berechtigungen der [generieren Ereignisse Entwickler eine Überwachungsberechtigung](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn221956%28v=ws.11%29) auf Ihren HGS-Servern.

> [!NOTE]
> Gruppenverwaltete Dienstkonten sind verfügbar ab der mit dem Windows Server 2012 Active Directory-Schema.
> Weitere Informationen finden Sie unter [gruppenverwalteten dienstkontoanforderungen](https://technet.microsoft.com/library/jj128431.aspx).

## <a name="jea-security-groups"></a>JEA-Sicherheitsgruppen

Beim Einrichten von Host-Überwachungsdienst bietet eine [Just Enough Administration (JEA)](https://aka.ms/JEAdocs) PowerShell-Endpunkt ist so konfiguriert, dass um Administratoren zum Verwalten von Host-Überwachungsdienst ohne vollständigen lokalen Administratorrechte zu ermöglichen.
Sie müssen keine JEA verwenden, um Host-Überwachungsdiensts zu verwalten, aber dennoch muss konfiguriert werden beim Ausführen der Initialize-HgsServer.
Die Konfiguration des JEA-Endpunkts besteht aus 2 Sicherheitsgruppen, die Ihren HGS-Administratoren und die Host-Überwachungsdienst Reviewer enthalten festlegen.
Benutzer, die Gruppe "Administratoren" angehören können hinzufügen, ändern oder Entfernen von Richtlinien auf dem Host-Überwachungsdienst; Prüfer können nur die aktuelle Konfiguration anzeigen.

Erstellen Sie 2 Sicherheitsgruppen für diese JEA-Gruppen, die mithilfe von Active Directory-Verwaltungstools oder [New-ADGroup](https://technet.microsoft.com/itpro/powershell/windows/addsadministration/new-adgroup).

```powershell
New-ADGroup -Name 'HgsJeaReviewers' -GroupScope DomainLocal
New-ADGroup -Name 'HgsJeaAdmins' -GroupScope DomainLocal
```

## <a name="cluster-objects"></a>Clusterobjekte

Wenn das Konto, das Sie verwenden, um das Einrichten des Host-Überwachungsdienst nicht über die Berechtigung zum Erstellen von neuen Computerobjekte in der Domäne verfügt, müssen Sie die Clusterobjekte vorab bereitstellen.
Diese Schritte werden erläutert [Vorabbereitstellen von Clustercomputerobjekten in Active Directory Domain Services](https://technet.microsoft.com/library/dn466519(v=ws.11).aspx).

Um Ihre erste HGS-Knoten einzurichten, müssen Sie einen Cluster Name-Objekt (CNO) und einem virtuellen Computer-Objekt (VCO) zu erstellen.
Das Clusternamenobjekt stellt den Namen des Clusters dar und wird hauptsächlich intern vom Failover-Clusterunterstützung verwendet.
Die VCO stellt den Host-Überwachungsdienst-Dienst, der auf den Cluster befindet und der Name der DNS-Server registriert werden.

> [!IMPORTANT]
> Der Benutzer, der ausgeführt wird `Initialize-HgsServer` erfordert **Vollzugriff** über das CNO und VCO-Objekte in Active Directory.

Um schnell Ihre CNO und VCO vorab bereitgestellt haben, müssen Sie Active Directory-Administrator die folgenden PowerShell-Befehle ausführen:

```powershell
# Create the CNO
$cno = New-ADComputer -Name 'HgsCluster' -Description 'HGS CNO' -Enabled $false -Passthru

# Create the VCO
$vco = New-ADComputer -Name 'HgsService' -Description 'HGS VCO' -Passthru

# Give the CNO full control over the VCO
$vcoPath = Join-Path "AD:\" $vco.DistinguishedName
$acl = Get-Acl $vcoPath
$ace = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $cno.SID, "GenericAll", "Allow"
$acl.AddAccessRule($ace)
Set-Acl -Path $vcoPath -AclObject $acl

# Allow time for your new CNO and VCO to replicate to your other Domain Controllers before continuing
```

## <a name="security-baseline-exceptions"></a>Ausnahmen zur Codezugriffssicherheit baseline

Wenn Sie Host-Überwachungsdienst in einer Umgebung mit hoher gesperrt bereitstellen, können bestimmte gruppenrichtlinieneinstellungen verhindern, dass Host-Überwachungsdienst normaler Betrieb.
Überprüfen Sie Ihre Gruppenrichtlinienobjekte für die folgenden Einstellungen, und befolgen Sie die Anweisungen aus, wenn Sie betroffen sind:

### <a name="network-logon"></a>Netzwerkanmeldung

**Richtlinienpfad ist:** Zuweisen von Computer Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten

**Richtlinienname:** Zugriff vom Netzwerk auf diesen Computer verweigern

**Erforderlicher Wert:** Stellen Sie sicher, dass der Wert keine netzwerkanmeldungen für alle lokalen Konten blockiert. Sie können jedoch problemlos lokale Administratorkonten, blockieren.

**Reason:** Failover-Clusterunterstützung, abhängig von einer nicht-Administrator lokalen Konto mit dem Namen CLIUSR zum Verwalten von Knoten im Cluster ab. Blockierende netzwerkanmeldung für diesen Benutzer wird verhindert, dass den Cluster ordnungsgemäß arbeiten.

### <a name="kerberos-encryption"></a>Kerberos Encryption

**Richtlinienpfad ist:** Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Sicherheitsoptionen

**Richtlinienname:** Netzwerksicherheit: Konfigurieren Sie für Kerberos zulässige Verschlüsselungstypen

**Aktion**: Wenn diese Richtlinie konfiguriert ist, müssen Sie das gMSA-Konto mit aktualisieren [Set-ADServiceAccount](https://docs.microsoft.com/powershell/module/addsadministration/set-adserviceaccount?view=win10-ps) nur die unterstützten Verschlüsselungsarten in dieser Richtlinie verwenden. Beispielsweise wenn Ihre Richtlinie nur AES128 lässt\_HMAC\_SHA1 und AES256\_HMAC\_SHA1, führen Sie `Set-ADServiceAccount -Identity HGSgMSA -KerberosEncryptionType AES128,AES256`.



## <a name="next-steps"></a>Nächste Schritte

- Die nächsten Schritte zum Einrichten von TPM-basierten Nachweis, finden Sie unter [initialisiert den Host-Überwachungsdienst-Cluster mithilfe von TPM-Modus in einer vorhandenen Gesamtstruktur der geschützten](guarded-fabric-initialize-hgs-tpm-mode-bastion.md).
- Die nächsten Schritte, um den schlüsselnachweis Host einzurichten, finden Sie unter [initialisieren den HGS-Cluster mithilfe von Schlüssel-Modus in einer vorhandenen Gesamtstruktur der geschützten](guarded-fabric-initialize-hgs-key-mode-bastion.md).
- Für die nächsten Schritte zum Einrichten der Admin-basierten nachweisen (in Windows Server-2019 veraltet) finden Sie unter [initialisiert den Host-Überwachungsdienst-Cluster mithilfe von AD-Modus in einer vorhandenen geschützten Gesamtstruktur](guarded-fabric-initialize-hgs-ad-mode-bastion.md).

