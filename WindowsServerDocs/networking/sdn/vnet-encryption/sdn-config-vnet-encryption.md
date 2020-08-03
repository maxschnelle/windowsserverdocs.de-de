---
title: Konfigurieren der Verschlüsselung für eine Virtual Network
description: Die Verschlüsselung virtueller Netzwerke ermöglicht die Verschlüsselung des Datenverkehrs von virtuellen Netzwerken zwischen virtuellen Computern, die in Subnetzen, die als "Verschlüsselung aktiviert" gekennzeichnet sind, miteinander kommunizieren.
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 378213f5-2d59-4c9b-9607-1fc83f8072f1
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/08/2018
ms.openlocfilehash: 11ec399ab9c63b27711b19987c6e070b47545fdd
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87520229"
---
# <a name="configure-encryption-for-a-virtual-subnet"></a>Konfigurieren der Verschlüsselung für ein virtuelles Subnetz

>Gilt für: Windows Server

Die Verschlüsselung virtueller Netzwerke ermöglicht die Verschlüsselung des Datenverkehrs von virtuellen Netzwerken zwischen virtuellen Computern, die in Subnetzen, die als "Verschlüsselung aktiviert" gekennzeichnet sind, miteinander kommunizieren. Sie nutzt auch Datagram Transport Layer Security (DTLS) im virtuellen Subnetz, um Pakete zu verschlüsseln. DTLS schützt vor Abhörversuchen, Manipulation und Fälschung durch jeden, der Zugriff auf das physische Netzwerk hat.

Die Verschlüsselung virtueller Netzwerke erfordert Folgendes:
- Auf jedem der Sdn-aktivierten Hyper-V-Hosts sind Verschlüsselungs Zertifikate installiert.
- Ein Anmelde Informationen-Objekt im Netzwerk Controller, das auf den Fingerabdruck des Zertifikats verweist.
- Die Konfiguration der einzelnen virtuellen Netzwerke enthält Subnetze, für die eine Verschlüsselung erforderlich ist.

Wenn Sie die Verschlüsselung in einem Subnetz aktivieren, wird der gesamte Netzwerk Datenverkehr in diesem Subnetz zusätzlich zu sämtlichen Verschlüsselung auf Anwendungsebene, die möglicherweise auch stattfindet, automatisch verschlüsselt.  Datenverkehr zwischen Subnetzen, auch wenn Sie als verschlüsselt gekennzeichnet ist, wird automatisch unverschlüsselt gesendet. Sämtlicher Datenverkehr, der die Grenze des virtuellen Netzwerks überschreitet, wird auch unverschlüsselt gesendet.

>[!NOTE]
>Bei der Kommunikation mit einem anderen virtuellen Computer im gleichen Subnetz, unabhängig davon, ob er zu einem späteren Zeitpunkt verbunden oder verbunden ist, wird der Datenverkehr automatisch verschlüsselt.

>[!TIP]
>Wenn Sie Anwendungen darauf beschränken müssen, nur im verschlüsselten Subnetz zu kommunizieren, können Sie Access Control Listen (ACLs) nur verwenden, um die Kommunikation innerhalb des aktuellen Subnetzes zuzulassen. Weitere Informationen finden [Sie unter Verwenden von Access Control Listen (ACLs) zum Verwalten des Netzwerk Datenverkehrs Flusses des Daten](https://docs.microsoft.com/windows-server/networking/sdn/manage/use-acls-for-traffic-flow)Centers.


## <a name="step-1-create-the-encryption-certificate"></a>Schritt 1: Erstellen des Verschlüsselungs Zertifikats
Auf jedem Host muss ein Verschlüsselungs Zertifikat installiert sein. Sie können das gleiche Zertifikat für alle Mandanten verwenden oder für jeden Mandanten ein eindeutiges Zertifikat generieren.

1.  Generieren des Zertifikats

    ```
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
    ```

    Nach dem Ausführen des Skripts wird im eigenen Speicher ein neues Zertifikat angezeigt:

    ```
    PS D:\> dir cert:\\localmachine\my
    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\my

    Thumbprint                                Subject
    ----------                                -------
    84857CBBE7A1C851A80AE22391EB2C39BF820CE7  CN=MyNetwork
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks
    ```

1. Exportieren Sie das Zertifikat in eine Datei.<p>Sie benötigen zwei Kopien des Zertifikats, eines mit dem privaten Schlüssel und eines ohne.

    ```
   $subjectName = "EncryptedVirtualNetworks"
   $cert = Get-ChildItem cert:\localmachine\my | ? {$_.Subject -eq "CN=$subjectName"}
   [System.io.file]::WriteAllBytes("c:\$subjectName.pfx", $cert.Export("PFX", "secret"))
   Export-Certificate -Type CERT -FilePath "c:\$subjectName.cer" -cert $cert
    ```

3. Installieren Sie die Zertifikate auf den einzelnen Hyper-v-Hosts.

    ```
    PS C:\> dir c:\$subjectname.*

    Directory: C:\

    Mode                LastWriteTime         Length Name
    ----                -------------         ------ ----
    -a----        9/22/2017   4:54 PM            543 EncryptedVirtualNetworks.cer
    -a----        9/22/2017   4:54 PM           1706 EncryptedVirtualNetworks.pfx
    ```

1. Installieren von auf einem Hyper-V-Host

    ```
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
        $certificate.import($certFullPath)

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

        # Important: Remove the certificate files when finished
        remove-item C:\$SubjectName.cer
        remove-item C:\$SubjectName.pfx
    }
    ```

5. Wiederholen Sie diesen Vorgang für jeden Server in Ihrer Umgebung.<p>Wenn Sie sich für jeden Server wiederholen, sollten Sie über ein Zertifikat verfügen, das im Stammverzeichnis und im Speicher jedes Hyper-V-Hosts installiert ist.

6. Überprüfen Sie die Installation des Zertifikats.<p>Überprüfen Sie die Zertifikate, indem Sie den Inhalt des Zertifikats "My" und "root" überprüfen:

    ```
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
    ```

7. Notieren Sie sich den Fingerabdruck.<p>Sie müssen den Fingerabdruck notieren, da Sie ihn benötigen, um das Zertifikat Anmelde Informationen-Objekt im Netzwerk Controller zu erstellen.

## <a name="step-2-create-the-certificate-credential"></a>Schritt 2: Erstellen der Zertifikat Anmelde Informationen

Nachdem Sie das Zertifikat auf allen Hyper-V-Hosts installiert haben, die mit dem Netzwerk Controller verbunden sind, müssen Sie den Netzwerk Controller jetzt für die Verwendung konfigurieren.  Zu diesem Zweck müssen Sie ein Anmelde Informationsobjekt erstellen, das den Zertifikat Fingerabdruck des Computers enthält, auf dem die PowerShell-Module für den Netzwerk Controller installiert sind.

```
///Replace with the thumbprint from your certificate
$thumbprint = "5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6"

$uri = "https://nc.contoso.com"

///Replace with your Network Controller URI
Import-module networkcontroller

$credproperties = new-object Microsoft.Windows.NetworkController.CredentialProperties
$credproperties.Type = "X509Certificate"
$credproperties.Value = $thumbprint
New-networkcontrollercredential -connectionuri $uri -resourceid "EncryptedNetworkCertificate" -properties $credproperties -force
```

> [!TIP]
> Sie können diese Anmelde Informationen für jedes verschlüsselte virtuelle Netzwerk wieder verwenden, oder Sie können ein eindeutiges Zertifikat für jeden Mandanten bereitstellen und verwenden.

## <a name="step-3-configuring-a-virtual-network-for-encryption"></a>Schritt 3: Konfigurieren einer Virtual Network für die Verschlüsselung

Bei diesem Schritt wird davon ausgegangen, dass Sie bereits einen virtuellen Netzwerknamen "Mein Netzwerk" erstellt haben und mindestens ein virtuelles Subnetz enthält.  Weitere Informationen zum Erstellen virtueller Netzwerke finden Sie unter [erstellen, löschen oder Aktualisieren von virtuellen Mandanten Netzwerken](../Manage/Create,-Delete,-or-Update-Tenant-Virtual-Networks.md).

>[!NOTE]
>Bei der Kommunikation mit einem anderen virtuellen Computer im gleichen Subnetz, unabhängig davon, ob er zu einem späteren Zeitpunkt verbunden oder verbunden ist, wird der Datenverkehr automatisch verschlüsselt.

1.  Rufen Sie die Virtual Network-und Anmelde Informationsobjekte vom Netzwerk Controller ab:

    ```
    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "MyNetwork"
    $certcred = Get-NetworkControllerCredential -ConnectionUri $uri -ResourceId "EncryptedNetworkCertificate"
    ```

2.  Fügen Sie einen Verweis auf die Zertifikat Anmelde Informationen hinzu, und aktivieren Sie die Verschlüsselung in einzelnen Subnetzen:

    ```
    $vnet.properties.EncryptionCredential = $certcred

    # Replace the Subnets index with the value corresponding to the subnet you want encrypted.
    # Repeat for each subnet where encryption is needed
    $vnet.properties.Subnets[0].properties.EncryptionEnabled = $true
    ```

3.  Fügen Sie das aktualisierte Virtual Network Objekt in den Netzwerk Controller ein:

    ```
    New-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId $vnet.ResourceId -Properties $vnet.Properties -force
    ```

*Herzlichen Glückwunsch!* * Sie sind fertig, nachdem Sie diese Schritte abgeschlossen haben.
