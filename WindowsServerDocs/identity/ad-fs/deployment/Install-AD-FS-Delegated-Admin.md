---
ms.assetid: 46725afe-8652-4cd7-928c-93b98f7fbae3
title: Erstellen einer AD FS Farm ohne Domänen Administrator Berechtigungen
description: Verwenden des install-adfsfarm-Cmdlets und-Skripts zum Erstellen einer AD FS-Farm mit delegierten Administrator Anmelde Informationen
author: billmath
ms.author: billmath
manager: daveba
ms.date: 04/01/2020
ms.topic: article
ms.openlocfilehash: 7dff0b19b4d8783dcd43344c6152be9d2c36441d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972187"
---
# <a name="creating-an-ad-fs-farm-without-domain-admin-privileges"></a>Erstellen einer AD FS Farm ohne Domänen Administrator Berechtigungen

>Gilt für: Windows Server 2019 und 2016

## <a name="overview"></a>Übersicht
Ab AD FS in Windows Server 2016 können Sie das Cmdlet Install-adfsfarm als lokalen Administrator auf dem Verbund Server ausführen, vorausgesetzt, dass Ihr Domänen Administrator Active Directory vorbereitet hat.  Das in diesem Artikel beschriebene Skript kann verwendet werden, um AD vorzubereiten.  Die Schritte lauten wie folgt:

1) Führen Sie als Domänen Administrator das Skript aus (oder erstellen Sie die Active Directory Objekte und Berechtigungen manuell).
2) Das Skript gibt ein AdminConfiguration-Objekt zurück, das den DN des neu erstellten AD-Objekts enthält.
3) Führen Sie auf dem Verbund Server das Cmdlet Install-adfsfarm aus, und melden Sie sich als lokaler Administrator an, und übergeben Sie das Objekt aus #2 obigen als AdminConfiguration-Parameter.

## <a name="assumptions"></a>Annahmen
- Condeso\localadmin ist ein integrierter Administrator auf dem Verbund Server, der nicht als Domänen Administrator angemeldet ist.
- Contoso\fssvcacct ist ein Domänen Konto, das als AD FS Dienst Konto verwendet wird.
- Contoso\fsgmsaacct $ ist ein GMSA-Konto, das als AD FS Dienst Konto verwendet wird.
- $svcCred ist die Anmelde Informationen des AD FS Dienst Kontos.
- $localAdminCred ist die Anmelde Informationen des lokalen Administrator Kontos (Non da) auf dem Verbund Server.

## <a name="using-a-domain-account-as-ad-fs-service-account"></a>Verwenden eines Domänen Kontos als AD FS-Dienst Konto
### <a name="prepare-ad"></a>Vorbereiten von AD
Führen Sie Folgendes als Domänen Administrator aus.
```
PS:\>$adminConfig=(.\New-AdfsDkmContainer.ps1 -ServiceAccount contoso\fssvcacct -AdfsAdministratorAccount contoso\localadmin)
```
### <a name="sample-output"></a>Beispielausgabe
```
$adminconfig.DkmContainerDN
CN=9530440c-bc84-4fe6-a3f9-8d60162a7bcf,CN=ADFS,CN=Microsoft,CN=Program Data,DC=contoso,DC=com
```
### <a name="create-the-ad-fs-farm"></a>Erstellen der AD FS-Farm
Führen Sie auf dem Verbund Server als lokaler Administrator den folgenden Befehl in einem PowerShell-Befehlsfenster mit erhöhten Rechten aus.

Wenn der Verbund Server Administrator nicht dieselbe PowerShell-Sitzung wie der oben genannte Domänen Administrator verwendet, erstellen Sie zunächst das adminconfig-Objekt mithilfe der Ausgabe der obigen Ausgabe neu.
```
PS:\>$adminConfig = @{"DKMContainerDn"="CN=9530440c-bc84-4fe6-a3f9-8d60162a7bcf,CN=ADFS,CN=Microsoft,CN=Program Data,DC=contoso,DC=com"}
```

Erstellen Sie als nächstes die Farm:
```
PS:\>$svcCred = (get-credential)
PS:\>$localAdminCred = (get-credential)
PS:\>Install-AdfsFarm -CertificateThumbprint 270D041785C579D75C1C981DA0F9C36ECFDB65E0 -FederationServiceName "fs.contoso.com" -ServiceAccountCredential $svcCred -Credential $localAdminCred -OverwriteConfiguration -AdminConfiguration $adminConfig -Verbose
```
## <a name="using-a-gmsa-as-the-ad-fs-service-account"></a>Verwenden eines GMSA als AD FS-Dienst Konto
### <a name="prepare-ad"></a>Vorbereiten von AD
```
PS:\>$adminConfig=(.\New-AdfsDkmContainer.ps1 -ServiceAccount contoso\FsGmsaAcct$ -AdfsAdministratorAccount contoso\localadmin)
```

### <a name="sample-output"></a>Beispielausgabe
```
$adminconfig.DkmContainerDN
CN=8065f653-af9d-42ff-aec8-56e02be4d5f3,CN=ADFS,CN=Microsoft,CN=Program Data,DC=contoso,DC=com
```

### <a name="create-the-ad-fs-farm"></a>Erstellen der AD FS-Farm
Führen Sie auf dem Verbund Server als lokaler Administrator den folgenden Befehl in einem PowerShell-Befehlsfenster mit erhöhten Rechten aus.

Wenn der Verbund Server Administrator nicht dieselbe PowerShell-Sitzung wie der oben genannte Domänen Administrator verwendet, erstellen Sie zunächst das adminconfig-Objekt mithilfe der Ausgabe der obigen Ausgabe neu.
```
PS:\>$adminConfig = @{"DKMContainerDn"="CN=8065f653-af9d-42ff-aec8-56e02be4d5f3,CN=ADFS,CN=Microsoft,CN=Program Data,DC=contoso,DC=com"}
```

Erstellen Sie als nächstes die Farm: Beachten Sie, dass dem lokalen Computer Konto und dem AD FS-Administrator Konto die Berechtigung zum Abrufen von Kennwort und delegieren an Konto Berechtigungen für das GMSA erteilt werden muss.
```
PS:\>$localadminobj = get-aduser "localadmin"
PS:\>$adfsnodecomputeracct = get-adcomputer "contoso_adfs_node"
PS:\>Set-ADServiceAccount -Identity fsgmsaacct -PrincipalsAllowedToRetrieveManagedPassword @( add=$localadmin.sid.value, $computeracct.sid.value) -PrincipalsAllowedToDelegateToAccount @( add=$localadmin.sid.value, $computeracct.sid.value)
PS:\>$localAdminCred = (get-credential)
PS:\>Install-AdfsFarm -CertificateThumbprint 270D041785C579D75C1C981DA0F9C36ECFDB65E0 -FederationServiceName "fs.contoso.com" -Credential $localAdminCred -GroupServiceAccountIdentifier "contoso\fsgmsaacct$" -OverwriteConfiguration -AdminConfiguration $adminConfig
```

## <a name="script-for-preparing-ad"></a>Skript für die Vorbereitung von AD
Das folgende PowerShell-Skript kann zum Ausführen der obigen Beispiele verwendet werden.

```
[CmdletBinding(SupportsShouldProcess=$true)]
param (
   [Parameter(Mandatory=$True)]
   [string]$ServiceAccount,
   [Parameter(Mandatory=$True)]
   [string]$AdfsAdministratorAccount
)

$ServiceAccountSplit = $ServiceAccount.Split("\");
if ($ServiceAccountSplit.Length -ne 2)
{
    Write-error "Specify the ServiceAccount identifier in 'domain\username' format"
    exit 1
}

$AdfsAdministratorAccountSplit = $AdfsAdministratorAccount.Split("\");
if ($AdfsAdministratorAccountSplit.Length -ne 2)
{
    Write-error "Specify the AdfsAdministratorAccount identifier in 'domain\username' format"
    exit 1
}

#######################################
## Verify AD module is installed
#######################################
$m = "ActiveDirectory"
if (Get-Module | Where-Object {$_.Name -eq $m})
{
    write-verbose "Module $m is already imported."
}
else
{
    if (Get-Module -ListAvailable | Where-Object {$_.Name -eq $m})
    {
        Import-Module $m -Verbose
    }
    else
    {
        write-error "Module $m was not imported, install the Active Directory RSAT package and retry."
        exit 1
    }
}

push-location ad:

#######################################
## Generate random DKM container name
## The OU Name is a randomly generated Guid
#######################################
[string]$guid = [Guid]::NewGuid()
write-verbose ("OU Name" + $guid)

$ouName = $guid
$initialPath = "CN=Microsoft,CN=Program Data," + (Get-ADDomain).DistinguishedName
$ouPath = "CN=ADFS," + $initialPath
$ou = "CN=" + $ouName + "," + $ouPath

#######################################
## Create DKM container and assign default ACE which allows adfs admin read access
#######################################

if ($pscmdlet.ShouldProcess("$ou", "Creating DKM container and assinging access"))
{
    Write-Verbose ("Creating organizational unit with DN: " + $ou)

    if ($AdfsAdministratorAccount.EndsWith("$"))
    {
        write-verbose "ADFS administrator account passed with $ suffix indicating a computer account"
        $userNameSplit = $AdfsAdministratorAccount.Split("\");
        $strSID = (Get-ADServiceAccount -Identity $userNameSplit[1]).SID
    }
    else
    {
        write-verbose "ADFS administrator account is a standard AD user"
        $objUser = New-Object System.Security.Principal.NTAccount($AdfsAdministratorAccount)
        $strSID = $objUser.Translate([System.Security.Principal.SecurityIdentifier])
    }

    if ($null -eq (Get-ADObject -Filter {distinguishedName -eq $ouPath}))
    {
        Write-Verbose ("First creating initial path " + $ouPath)
        New-ADObject -Name "ADFS" -Type Container -Path $initialPath
    }

    $acl = get-acl -Path $ouPath
    [System.DirectoryServices.ActiveDirectorySecurityInheritance]$adSecInEnum = [System.DirectoryServices.ActiveDirectorySecurityInheritance]::All
    $ace1 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"GenericRead","Allow",$adSecInEnum

    $acl.AddAccessRule($ace1)
    set-acl -Path $ouPath -AclObject $acl

    New-ADObject -Name $ouName -Type Container -Path $ouPath
}


#######################################
## Grant the following permission to the service account
# Read
# Create Child
# Write Owner
# Delete Tree
# Write DACL
# Write Property
#######################################
if ($ServiceAccount.EndsWith("$"))
{
    write-verbose "service account passed with $ suffix indicating a gMSA"
    $userNameSplit = $ServiceAccount.Split("\");
    $strSID = (Get-ADServiceAccount -Identity $userNameSplit[1]).SID
}
else
{
    write-verbose "service account is a standard AD user"
    $objUser = New-Object System.Security.Principal.NTAccount($ServiceAccount)
    $strSID = $objUser.Translate([System.Security.Principal.SecurityIdentifier])
}

if ($pscmdlet.ShouldProcess("$strSID", "Granting GenericRead, CreateChild, WriteOwner, DeleteTree, WriteDacl and WriteProperty"))
{
    [System.DirectoryServices.ActiveDirectorySecurityInheritance]$adSecInEnum = [System.DirectoryServices.ActiveDirectorySecurityInheritance]::All
    $ace1 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"GenericRead","Allow",$adSecInEnum
    $ace2 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"CreateChild","Allow",$adSecInEnum
    $ace3 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"WriteOwner","Allow",$adSecInEnum
    $ace4 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"DeleteTree","Allow",$adSecInEnum
    $ace5 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"WriteDacl","Allow",$adSecInEnum
    $ace6 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"WriteProperty","Allow",$adSecInEnum

    $acl = get-acl -Path $ou

    $acl.AddAccessRule($ace1)
    $acl.AddAccessRule($ace2)
    $acl.AddAccessRule($ace3)
    $acl.AddAccessRule($ace4)
    $acl.AddAccessRule($ace5)
    $acl.AddAccessRule($ace6)

    $acl.SetOwner($strSID)

    set-acl -Path $ou -AclObject $acl
}

#######################################
## Grant the following permission to the adfs admin account
# Read
# Create Child
# Write Owner
# Delete Tree
# Write DACL
# Write Property
#######################################

if ($AdfsAdministratorAccount.EndsWith("$"))
{
    write-verbose "ADFS administrator account passed with $ suffix indicating a gMSA"
    $userNameSplit = $AdfsAdministratorAccount.Split("\");
    $strSID = (Get-ADServiceAccount -Identity $userNameSplit[1]).SID
}
else
{
    write-verbose "ADFS administrator account is a standard AD user"
    $objUser = New-Object System.Security.Principal.NTAccount($AdfsAdministratorAccount)
    $strSID = $objUser.Translate([System.Security.Principal.SecurityIdentifier])
}

if ($pscmdlet.ShouldProcess("$strSID", "Granting GenericRead, CreateChild, WriteOwner, DeleteTree, WriteDacl and WriteProperty"))
{
    [System.DirectoryServices.ActiveDirectorySecurityInheritance]$adSecInEnum = [System.DirectoryServices.ActiveDirectorySecurityInheritance]::All
    $ace1 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"GenericRead","Allow",$adSecInEnum
    $ace2 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"CreateChild","Allow",$adSecInEnum
    $ace3 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"WriteOwner","Allow",$adSecInEnum
    $ace4 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"DeleteTree","Allow",$adSecInEnum
    $ace5 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"WriteDacl","Allow",$adSecInEnum
    $ace6 = New-Object System.DirectoryServices.ActiveDirectoryAccessRule $strSID,"WriteProperty","Allow",$adSecInEnum

    $acl = get-acl -Path $ou

    $acl.AddAccessRule($ace1)
    $acl.AddAccessRule($ace2)
    $acl.AddAccessRule($ace3)
    $acl.AddAccessRule($ace4)
    $acl.AddAccessRule($ace5)
    $acl.AddAccessRule($ace6)

    $acl.SetOwner($strSID)

    set-acl -Path $ou -AclObject $acl

    $adminConfig = @{"DKMContainerDn"=$ou}

    Write-Output $adminConfig
}

pop-location

```
