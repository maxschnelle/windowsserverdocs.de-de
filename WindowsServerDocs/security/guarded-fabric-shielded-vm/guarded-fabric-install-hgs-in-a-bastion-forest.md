---
title: Installieren von HGS in einer vorhandenen geschützten Gesamtstruktur
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: 358fae9a9ee477537d3ee929ff81920175d58298
ms.sourcegitcommit: 5344adcf9c0462561a4f9d47d80afc1d095a5b13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/18/2020
ms.locfileid: "90766413"
---
# <a name="install-hgs-in-an-existing-bastion-forest"></a>Installieren von HGS in einer vorhandenen geschützten Gesamtstruktur

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016


## <a name="join-the-hgs-server-to-the-existing-domain"></a>Fügen Sie den HGS-Server der vorhandenen Domäne hinzu.

In einer vorhandenen geschützten Gesamtstruktur müssen HGS der Stamm Domäne hinzugefügt werden. Verwenden Sie Server-Manager oder [Add-Computer](https://go.microsoft.com/fwlink/?LinkId=821564) , um den HGS-Server mit der Stamm Domäne zu verknüpfen.

## <a name="add-the-hgs-server-role"></a>Hinzufügen der HGS-Server Rolle

Führen Sie alle Befehle in diesem Thema in einer PowerShell-Sitzung mit erhöhten Rechten aus.

[!INCLUDE [Install the HGS server role](../../../includes/guarded-fabric-install-hgs-server-role.md)]

Wenn Ihr Rechenzentrum über eine sichere geschützte Gesamtstruktur verfügt, der Sie HGS-Knoten beitreten möchten, führen Sie die folgenden Schritte aus.
Sie können diese Schritte auch verwenden, um zwei oder mehr unabhängige HGS-Cluster zu konfigurieren, die mit derselben Domäne verknüpft sind.

## <a name="join-the-hgs-server-to-the-existing-domain"></a>Fügen Sie den HGS-Server der vorhandenen Domäne hinzu.

Verwenden Sie Server-Manager oder [Add-Computer](https://go.microsoft.com/fwlink/?LinkId=821564) , um die HGS-Server mit der gewünschten Domäne zu verknüpfen.

## <a name="prepare-active-directory-objects"></a>Vorbereiten von Active Directory Objekten

Erstellen Sie ein Gruppen verwaltetes Dienst Konto und zwei Sicherheitsgruppen.
Sie können die Cluster Objekte auch vorab bereitstellen, wenn das Konto, mit dem Sie HGS initialisieren, nicht über die Berechtigung zum Erstellen von Computer Objekten in der Domäne verfügt.

## <a name="group-managed-service-account"></a>Gruppenverwaltetes Dienstkonto

Das Gruppen verwaltete Dienst Konto (Group Managed Service Account, GMSA) ist die Identität, die von HGS zum Abrufen und Verwenden der Zertifikate verwendet wird. Verwenden Sie [New-ADServiceAccount](/powershell/module/addsadministration/new-adserviceaccount?view=win10-ps) , um ein GMSA zu erstellen.
Wenn dies das erste GMSA in der Domäne ist, müssen Sie einen Schlüssel Verteilungsdienst-Stamm Schlüssel hinzufügen.

Jedem HGS-Knoten muss der Zugriff auf das GMSA-Kennwort gestattet werden.
Die einfachste Möglichkeit, dies zu konfigurieren, besteht darin, eine Sicherheitsgruppe zu erstellen, die alle Ihre HGS-Knoten enthält, und dieser Sicherheitsgruppe Zugriff zu gewähren, um das GMSA-Kennwort abzurufen.

Sie müssen den HGS-Server neu starten, nachdem Sie ihn einer Sicherheitsgruppe hinzugefügt haben, um sicherzustellen, dass er die neue Gruppenmitgliedschaft erhält.

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

Das GMSA benötigt das Recht, Ereignisse im Sicherheitsprotokoll auf jedem HGS-Server zu generieren.
Wenn Sie Gruppenrichtlinie verwenden, um die Zuweisung von Benutzerrechten zu konfigurieren, stellen Sie sicher, dass dem GMSA-Konto die [Berechtigung Audit-Ereignisse generieren](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn221956%28v=ws.11%29) auf Ihren HGS-Servern erteilt wird.

> [!NOTE]
> Gruppen verwaltete Dienst Konten sind ab dem Windows Server 2012-Active Directory Schema verfügbar.
> Weitere Informationen finden Sie unter [Gruppen verwaltete Dienst Kontoanforderungen](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj128431(v=ws.11)).

## <a name="jea-security-groups"></a>Jea-Sicherheitsgruppen

Wenn Sie HGS einrichten, wird ein Jea-PowerShell-Endpunkt [(Just Enough Administration)](/powershell/scripting/learn/remoting/jea/overview) konfiguriert, um Administratoren das Verwalten von HGS ohne volle lokale Administratorrechte zu ermöglichen.
Sie müssen Jea nicht zum Verwalten von HGS verwenden, aber es muss beim Ausführen von Initialize-hgsserver weiterhin konfiguriert werden.
Die Konfiguration des Jea-Endpunkts besteht aus dem Festlegen von zwei Sicherheitsgruppen, die ihre HGS-Administratoren und HGS-Reviewer enthalten.
Benutzer, die der Administrator Gruppe angehören, können Richtlinien auf HGS hinzufügen, ändern oder entfernen. Reviewer können die aktuelle Konfiguration nur anzeigen.

Erstellen Sie zwei Sicherheitsgruppen für diese Jea-Gruppen, indem Sie Active Directory Admin Tools oder [New-adgroup](/powershell/module/addsadministration/new-adgroup?view=win10-ps)verwenden.

```powershell
New-ADGroup -Name 'HgsJeaReviewers' -GroupScope DomainLocal
New-ADGroup -Name 'HgsJeaAdmins' -GroupScope DomainLocal
```

## <a name="cluster-objects"></a>Clusterobjekte

Wenn das Konto, das Sie zum Einrichten von HGS verwenden, nicht über die Berechtigung zum Erstellen neuer Computer Objekte in der Domäne verfügt, müssen Sie die Cluster Objekte vorab bereitstellen.
Diese Schritte werden unter vorab Bereitstellen von [Cluster Computer Objekten in Active Directory Domain Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn466519(v=ws.11))erläutert.

Zum Einrichten des ersten HGS-Knotens müssen Sie ein Cluster Namen Objekt (CNO) und ein virtuelles Computer Objekt (VCO) erstellen.
Das CNO stellt den Namen des Clusters dar und wird hauptsächlich intern vom Failoverclustering verwendet.
VCO stellt den HGS-Dienst dar, der sich auf dem Cluster befindet, und ist der Name, der beim DNS-Server registriert ist.

> [!IMPORTANT]
> Der Benutzer, der ausführen wird, `Initialize-HgsServer` muss die **vollständige Kontrolle** über die CNO-und VCO-Objekte in Active Directory haben.

Wenn Sie CNO und VCO schnell vorab bereitstellen möchten, müssen Sie über einen Active Directory Administrator die folgenden PowerShell-Befehle ausführen:

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

## <a name="security-baseline-exceptions"></a>Sicherheitsbaseline-Ausnahmen

Wenn Sie HGS in einer stark gesperrten Umgebung bereitstellen, können bestimmte Gruppenrichtlinie Einstellungen verhindern, dass HGS ordnungsgemäß funktionieren.
Überprüfen Sie die Gruppenrichtlinie Objekte auf die folgenden Einstellungen, und befolgen Sie die Anweisungen, wenn Sie betroffen sind:

### <a name="network-logon"></a>Netzwerk Anmeldung

**Richtlinien Pfad:** Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten

**Richtlinien Name:** Zugriff vom Netzwerk auf diesen Computer verweigern

**Erforderlicher Wert:** Stellen Sie sicher, dass der Wert keine Netzwerk Anmeldungen für alle lokalen Konten blockiert. Lokale Administrator Konten können jedoch problemlos blockiert werden.

**Grund:** Failoverclustering basiert auf einem lokalen Konto mit dem Namen cliusr, das nicht Administrator ist, um Cluster Knoten zu verwalten. Durch das Blockieren der Netzwerk Anmeldung für diesen Benutzer wird verhindert, dass der Cluster ordnungsgemäß funktioniert.

### <a name="kerberos-encryption"></a>Kerberos-Verschlüsselung

**Richtlinien Pfad:** Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Sicherheitsoptionen

**Richtlinien Name:** Netzwerksicherheit: Konfigurieren der für Kerberos zulässigen Verschlüsselungstypen

**Aktion**: Wenn diese Richtlinie konfiguriert ist, müssen Sie das GMSA-Konto mit " [Set-ADServiceAccount](/powershell/module/addsadministration/set-adserviceaccount?view=win10-ps) " aktualisieren, sodass nur die unterstützten Verschlüsselungstypen in dieser Richtlinie verwendet werden. Wenn Ihre Richtlinie beispielsweise nur AES128 \_ HMAC \_ SHA1 und AES256 \_ HMAC \_ SHA1 zulässt, sollten Sie Ausführen `Set-ADServiceAccount -Identity HGSgMSA -KerberosEncryptionType AES128,AES256` .



## <a name="next-steps"></a>Nächste Schritte

- Die nächsten Schritte zum Einrichten eines TPM-basierten Nachweis finden Sie unter [Initialisieren des HGS-Clusters mit dem TPM-Modus in einer vorhandenen](guarded-fabric-initialize-hgs-tpm-mode-bastion.md)geschützten Gesamtstruktur.
- Die nächsten Schritte zum Einrichten des Host Schlüssel-Attestation finden Sie unter [Initialisieren des HGS-Clusters mithilfe des Schlüssel Modus in einer vorhandenen](guarded-fabric-initialize-hgs-key-mode-bastion.md)geschützten Gesamtstruktur.
- Die nächsten Schritte zum Einrichten des Administrator basierten Nachweis (in Windows Server 2019 veraltet) finden Sie unter [Initialisieren des HGS-Clusters mit dem AD-Modus in einer vorhandenen](guarded-fabric-initialize-hgs-ad-mode-bastion.md)geschützten Gesamtstruktur.