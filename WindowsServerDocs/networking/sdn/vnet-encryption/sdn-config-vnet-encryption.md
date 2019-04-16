---
title: Konfigurieren Sie die Verschlüsselung für ein virtuelles Netzwerk
description: Dieses Thema enthält Informationen zur virtuellen Netzwerk-Verschlüsselung für die Software Defined Networking in Windows Server
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 378213f5-2d59-4c9b-9607-1fc83f8072f1
ms.author: pashort
author: grcusanz
ms.openlocfilehash: 7d1de535e7758793e5ddaa7eeefada0aa55d3328
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-encryption-for-a-virtual-subnet"></a>Konfigurieren Sie die Verschlüsselung für ein virtuelles Subnetz

>Gilt für: Windows Server

Dieses Thema enthält die folgenden Abschnitte, in denen Sie die erforderlichen Schrittezum Aktivieren der Verschlüsselung auf einem virtuellen Netzwerk beschrieben.

- [Erstellen das Verschlüsselungszertifikat](#bkmk_Certificate)
- [Erstellen die Zertifikat-Anmeldeinformationen](#bkmk_credential)
- [Konfigurieren eines virtuellen Netzwerks für die Verschlüsselung](#bkmk_vnet)

## <a name="bkmk_Certificate"></a>Erstellen das Verschlüsselungszertifikat
Ein Verschlüsselungszertifikat muss auf jedem Host installiert werden, in denen Verschlüsselung verwendet werden soll.  Sie können für alle Mandanten ein Zertifikat verwenden oder ein eindeutiges Zertifikat pro Mandant generieren, falls erforderlich.

Schritt1: Erstellen des Zertifikats

    $subjectName = "EncryptedVirtualNetworks"
    $cryptographicProviderName = "Microsoft Base Cryptographic Provider v1.0";
    [int] $privateKeyLength = 1024;
    $sslServerOidString = "1.3.6.1.5.5.7.3.1";
    $sslClientOidString = "1.3.6.1.5.5.7.3.2";
    [int] $validityPeriodInYear = 5;

    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"
    $name.Encode("CN=" + $SubjectName, 0)

    #Generate Key
    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"
    $key.ProviderName = $cryptographicProviderName
    $key.KeySpec = 1 #X509KeySpec.XCN_AT_KEYEXCHANGE
    $key.Length = $privateKeyLength
    $key.MachineContext = 1
    $key.ExportPolicy = 0x2 #X509PrivateKeyExportFlags.XCN_NCRYPT_ALLOW_EXPORT_FLAG 
    $key.Create()

    #Configure Eku
    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"
    $serverauthoid.InitializeFromValue($sslServerOidString)
    $clientauthoid = new-object -com "X509Enrollment.CObjectId.1"
    $clientauthoid.InitializeFromValue($sslClientOidString)
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"
    $ekuoids.add($serverauthoid)
    $ekuoids.add($clientauthoid)
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"
    $ekuext.InitializeEncode($ekuoids)

    # Set the hash algorithm to sha512 instead of the default sha1
    $hashAlgorithmObject = New-Object -ComObject X509Enrollment.CObjectId
    $hashAlgorithmObject.InitializeFromAlgorithmName( $ObjectIdGroupId.XCN_CRYPT_HASH_ALG_OID_GROUP_ID, $ObjectIdPublicKeyFlags.XCN_CRYPT_OID_INFO_PUBKEY_ANY, $AlgorithmFlags.AlgorithmFlagsNone, "SHA512")


    #Request Certificate
    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"

    $cert.InitializeFromPrivateKey(2, $key, "")
    $cert.Subject = $name
    $cert.Issuer = $cert.Subject
    $cert.NotBefore = (get-date).ToUniversalTime()
    $cert.NotAfter = $cert.NotBefore.AddYears($validityPeriodInYear);
    $cert.X509Extensions.Add($ekuext)
    $cert.HashAlgorithm = $hashAlgorithmObject
    $cert.Encode()

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"
    $enrollment.InitializeFromRequest($cert)
    $certdata = $enrollment.CreateRequest(0)
    $enrollment.InstallResponse(2, $certdata, 0, "")

Nach dem Ausführen der oben sehen Sie ein neues Zertifikat in den persönlichen Speicher des Computers an, dem Sie das Skript ausgeführt haben:

    PS D:\> dir cert:\\localmachine\my


    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\my

    Thumbprint                                Subject
    ----------                                -------
    84857CBBE7A1C851A80AE22391EB2C39BF820CE7  CN=MyNetwork
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks

Schritt2: Exportieren Sie das Zertifikat in eine Datei, die, der Sie zwei Kopien des Zertifikats, eine mit dem privaten Schlüssel und eine ohne benötigen.

    $subjectName = "EncryptedVirtualNetworks"
    $cert = Get-ChildItem cert:\localmachine\my | ? {$_.Subject -eq "CN=$subjectName"}
    [System.io.file]::WriteAllBytes("c:\$subjectName.pfx", $cert.Export("PFX", "secret"))
    Export-Certificate -Type CERT -FilePath "c:\$subjectName.cer" -cert $cert

Nach dem Ausführen der oben genannten müssen Sie jetzt zwei Dateien.  Diese müssen auf jedem Hyper-V-Hosts installiert werden.

    PS C:\> dir c:\$subjectname.*


        Directory: C:\


    Mode                LastWriteTime         Length Name
    ----                -------------         ------ ----
    -a----        9/22/2017   4:54 PM            543 EncryptedVirtualNetworks.cer
    -a----        9/22/2017   4:54 PM           1706 EncryptedVirtualNetworks.pfx

Schritt3: Installieren auf einem Hyper-V-Host

    $server = "Server01"

    $subjectname = "EncryptedVirtualNetworks"
    copy c:\$SubjectName.* \\$server\c$
    invoke-command -computername $server -ArgumentList $subjectname,"secret" {
        param (
            [string] $SubjectName,
            [string] $Secret
        )
        $certFullPath = "c:\$SubjectName.cer"

        # create a representation of the certificate file
        $certificate = new-object System.Security.Cryptography.X509Certificates.X509Certificate2
        $certificate.import($certFullPath){$_}

        # import into the store
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("Root", "LocalMachine")
        $store.open("MaxAllowed")
        $store.add($certificate)
        $store.close()

        $certFullPath = "c:\$SubjectName.pfx"
        $certificate = new-object System.Security.Cryptography.X509Certificates.X509Certificate2
        $certificate.import($certFullPath, $Secret, "MachineKeySet,PersistKeySet")

        # import into the store
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My", "LocalMachine")
        $store.open("MaxAllowed")
        $store.add($certificate)
        $store.close()

        # Important: Remove the certficate files when finished
        remove-item C:\$SubjectName.cer
        remove-item C:\$SubjectName.pfx
    }    

Wiederholen Sie für jeden Server in Ihrer Umgebung.  Sie verfügen jetzt über ein Zertifikat in den Stamm und Shop jedem Hyper-V-Host installiert

Sie können die Installation des Zertifikats überprüfen, überprüfen Sie den Inhalt der mein und Root-Zertifikatspeicher:

    PS C:\> enter-pssession Server1

    [Server1]: PS C:\> get-childitem cert://localmachine/my,cert://localmachine/root | ? {$_.Subject -eq "CN=EncryptedVirtualNetworks"}

    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\my

    Thumbprint                                Subject
    ----------                                -------
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks


    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\root

    Thumbprint                                Subject
    ----------                                -------
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks

Notieren Sie den Fingerabdruck, da Sie sie benötigen für das Erstellen des Zertifikats Credential-Objekts in den Netzwerk-Controller.

## <a name="bkmk_Certificate"></a>Erstellen die Zertifikat-Anmeldeinformationen

Wenn das Zertifikat auf jedem Hyper-V-Host an den Netzwerkcontroller angeschlossen erfolgreich installiert wurde, können Sie den Netzwerk-Controller, um es verwenden zu konfigurieren.

Sie müssen ein Anmeldeinformationsobjekt erstellen, das den Fingerabdruck des Zertifikats enthält.  Sie müssen dies von einem Computer, müssen Sie die Netzwerk-Controller-PowerShell-Module installiert.

    # Replace with thumbprint from your certificate
    $thumbprint = "5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6"  
    
    # Replace with your Network Controller URI
    $uri = "https://nc.contoso.com"

    Import-module networkcontroller
    
    $credproperties = new-object Microsoft.Windows.NetworkController.CredentialProperties
    $credproperties.Type = "X509Certificate"
    $credproperties.Value = $thumbprint
    New-networkcontrollercredential -connectionuri $uri -resourceid "EncryptedNetworkCertificate" -properties $credproperties -force

Sie können diese Anmeldeinformationen für jeden verschlüsselte virtuelle Netwokr wiederverwenden oder bereitstellen und verwenden Sie ein eindeutiges Zertifikat für jeden Mandanten können.

## <a name="bkmk_Certificate"></a>Konfigurieren eines virtuellen Netzwerks für die Verschlüsselung

Dieser Schrittsetzt voraus, Sie haben bereits ein virtuelles Netzwerk "Mein Netzwerk" erstellt und enthält mindestens ein virtuelles Subnetz.  Informationen zum Erstellen von virtuellen Netzwerken finden Sie unter [erstellen, löschen oder aktualisieren virtueller Mandantennetzwerke](../Manage/Create,-Delete,-or-Update-Tenant-Virtual-Networks.md).

Schritt1: Abrufen der Objekte virtuellen Netzwerk und die Anmeldeinformationen aus dem Netzwerkcontroller

    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "MyNetwork"
    $certcred = Get-NetworkControllerCredential -ConnectionUri $uri -ResourceId "EncryptedNetworkCertificate"

Schritt2: Hinzufügen eines Verweises auf die Zertifikat-Anmeldeinformationen und Aktivieren der Verschlüsselung für die einzelnen Subnetze.

    $vnet.properties.EncryptionCredential = $certcred

    # Replace the Subnets index with the value corresponding to the subnet you want encrypted.  
    # Repeat for each subnet where encryption is needed
    $vnet.properties.Subnets[0].properties.EncryptionEnabled = $true

Schritt3: Schalten Sie das aktualisierte virtuelle Netzwerkobjekt in den Netzwerkcontroller

    New-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId $vnet.ResourceId -Properties $vnet.Properties -force

Sobald dies abgeschlossen ist, sind keine weiteren Schritteerforderlich.  Alle virtuellen Computer, die zurzeit verbunden ist, und alle virtuellen Computer, der später mit dem oben genannten Subnetz verbunden ist, müssen den Datenverkehr automatisch verschlüsselt, bei der Kommunikation mit einem anderen virtuellen Computer im gleichen Subnetz.


