---
title: Konfigurieren der Verschlüsselung für ein virtuelles Netzwerk
description: Verschlüsselung des virtuellen Netzwerks ermöglicht die Verschlüsselung der virtuellen Netzwerkdatenverkehr zwischen virtuellen Computern, die miteinander kommunizieren, in Subnetzen, die als "Verschlüsselung aktiviert."
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 378213f5-2d59-4c9b-9607-1fc83f8072f1
ms.author: pashort
author: shortpatti
ms.date: 08/08/2018
ms.openlocfilehash: d2c09c83a227c5a75ff5b1b39b2ef6d1286bbfc8
ms.sourcegitcommit: cd12ace92e7251daaa4e9fabf1d8418632879d38
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2019
ms.locfileid: "66501564"
---
# <a name="configure-encryption-for-a-virtual-subnet"></a>Konfigurieren der Verschlüsselung für ein virtuelles Subnetz

>Gilt für: Windows Server

Verschlüsselung des virtuellen Netzwerks können für die Verschlüsselung von virtuellen Netzwerkdatenverkehr zwischen virtuellen Computern, die in Subnetzen, die als "Verschlüsselung aktiviert." gekennzeichnet miteinander kommunizieren Es nutzt auch Datagram Transport Layer Security (DTLS) im virtuellen Subnetz, um Pakete zu verschlüsseln. DTLS schützt vor Abhörversuchen, Manipulation und Fälschung durch jeden, der Zugriff auf das physische Netzwerk hat.

Verschlüsselung für virtuelle Netzwerke sind erforderlich:
- Verschlüsselungszertifikate, die auf jedem der SDN-fähige Hyper-V-Hosts installiert werden.
- Ein Objekt mit Anmeldeinformationen in den Netzwerkcontroller verweisen auf den Fingerabdruck des Zertifikats.
- Konfiguration auf alle virtuellen Netzwerke enthalten, Subnetze, die Verschlüsselung erforderlich ist.

Nach Aktivieren der Verschlüsselung in einem Subnetz wird neben jeder Verschlüsselung auf Anwendungsebene, die auch ausgeführt werden kann, automatisch alle Netzwerkdatenverkehr innerhalb dieses Subnetzes verschlüsselt.  Datenverkehr, der zwischen Subnetzen, überschreitet, auch wenn markiert als verschlüsselte, wird automatisch unverschlüsselt gesendet. Jeglicher Datenverkehr, der die Begrenzung des virtuellen Netzwerks überschreitet, ruft auch unverschlüsselt gesendet.

>[!NOTE]
>Bei der Kommunikation mit einem anderen virtuellen Computer im gleichen Subnetz, ob die derzeit verbundene oder zu einem späteren Zeitpunkt, den Datenverkehr verbundene ruft automatisch verschlüsselt.

>[!TIP]
>Wenn Sie nur im Subnetz verschlüsselte Kommunikation zwischen Anwendungen einschränken müssen, können Sie die Zugriffssteuerungslisten (ACLs) verwenden, nur um die Kommunikation im aktuellen Subnetz zuzulassen. Weitere Informationen finden Sie unter [verwenden Zugriffssteuerungslisten (ACLs) zum Verwalten von Datencenter-Netzwerk fließt der Datenverkehr](https://docs.microsoft.com/windows-server/networking/sdn/manage/use-acls-for-traffic-flow).


## <a name="step-1-create-the-encryption-certificate"></a>Schritt 1 Erstellen Sie das Verschlüsselungszertifikat
Jeder Host muss ein Verschlüsselungszertifikat installiert haben. Sie können verwenden das gleiche Zertifikat für alle Mandanten oder generieren ein eindeutiges Element für jeden Mandanten. 

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

Nachdem das Skript ausgeführt, ein neues Zertifikat angezeigt wird, der My-Zertifikatspeicher:

    PS D:\> dir cert:\\localmachine\my


    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\my

    Thumbprint                                Subject
    ----------                                -------
    84857CBBE7A1C851A80AE22391EB2C39BF820CE7  CN=MyNetwork
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks

2. Exportieren des Zertifikats in eine Datei an.<p>Sie benötigen zwei Kopien des Zertifikats, mit dem privaten Schlüssel und eine ohne.

```
   $subjectName = "EncryptedVirtualNetworks"
   $cert = Get-ChildItem cert:\localmachine\my | ? {$_.Subject -eq "CN=$subjectName"}
   [System.io.file]::WriteAllBytes("c:\$subjectName.pfx", $cert.Export("PFX", "secret"))
   Export-Certificate -Type CERT -FilePath "c:\$subjectName.cer" -cert $cert
```

3. Installieren Sie die Zertifikate auf jedem hyper-V-Hosts 

   PS: C:\> Dir c:\$subjectname.*


~~~
    Directory: C:\


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        9/22/2017   4:54 PM            543 EncryptedVirtualNetworks.cer
-a----        9/22/2017   4:54 PM           1706 EncryptedVirtualNetworks.pfx
~~~

4. Installieren auf einem Hyper-V-host

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

5. Wiederholen Sie für jeden Server in Ihrer Umgebung.<p>Nach dem für jeden Server wiederholen, benötigen Sie ein Zertifikat in den Stammseiten und my-Zertifikatspeicher der einzelnen Hyper-V-Hosts installiert. 

6. Überprüfen Sie die Installation des Zertifikats ein.<p>Überprüfen Sie die Zertifikate den Inhalt der meine und die Stamm-Zertifikatsspeicher:

   PS C:\> Geben Sie-Pssession-Server1

~~~
[Server1]: PS C:\> get-childitem cert://localmachine/my,cert://localmachine/root | ? {$_.Subject -eq "CN=EncryptedVirtualNetworks"}

PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\my

Thumbprint                                Subject
----------                                -------
5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks


PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\root

Thumbprint                                Subject
----------                                -------
5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks
~~~

7. Notieren Sie den Fingerabdruck.<p>Sie müssen sich den Fingerabdruck, Sie brauchen ihn zum Erstellen des Zertifikat-Credential-Objekts im Netzwerkcontroller.

## <a name="step-2-create-the-certificate-credential"></a>Schritt 2 Erstellen Sie die Zertifikatanmeldeinformationen

Nach der Installation des Zertifikats auf jedem Hyper-V-Host mit Netzwerkcontroller verbunden, müssen Sie jetzt den Netzwerkcontroller für dessen Verwendung konfigurieren.  Zu diesem Zweck müssen Sie ein Anmeldeinformationsobjekt mit den Fingerabdruck des Zertifikats auf dem Computer mit der installierten Network Controller PowerShell-Module erstellen. 


    # Replace with thumbprint from your certificate
    $thumbprint = "5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6"  

    # Replace with your Network Controller URI
    $uri = "https://nc.contoso.com"

    Import-module networkcontroller

    $credproperties = new-object Microsoft.Windows.NetworkController.CredentialProperties
    $credproperties.Type = "X509Certificate"
    $credproperties.Value = $thumbprint
    New-networkcontrollercredential -connectionuri $uri -resourceid "EncryptedNetworkCertificate" -properties $credproperties -force

>[!TIP]
>Sie können diese Anmeldeinformationen für jede verschlüsselte virtuelle Netzwerk wiederverwenden, oder Sie bereitstellen und ein eindeutiges Zertifikat für jeden Mandanten verwenden können.


## <a name="step-3-configuring-a-virtual-network-for-encryption"></a>Schritt 3 Konfigurieren eines virtuellen Netzwerks für die Verschlüsselung

Dieser Schritt setzt voraus, Sie haben bereits einen virtuellen Netzwerknamen "My Network" erstellt und enthält mindestens ein virtuelles Subnetz.  Informationen zum Erstellen von virtueller Netzwerks finden Sie unter [erstellen, löschen oder aktualisieren virtueller Mandantennetzwerke](../Manage/Create,-Delete,-or-Update-Tenant-Virtual-Networks.md).

>[!NOTE]
>Bei der Kommunikation mit einem anderen virtuellen Computer im gleichen Subnetz, ob die derzeit verbundene oder zu einem späteren Zeitpunkt, den Datenverkehr verbundene ruft automatisch verschlüsselt.

1.  Das virtuelle Netzwerk und die Anmeldeinformationen-Objekte aus dem Netzwerkcontroller abrufen

    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "MyNetwork" $certcred = Get-NetworkControllerCredential -ConnectionUri $uri -ResourceId "EncryptedNetworkCertificate"

2.  Hinzufügen eines Verweises auf das Zertifikat für die Anmeldeinformationen ein, und Aktivieren der Verschlüsselung in einzelnen Subnetzen

    $vnet.properties.EncryptionCredential = $certcred

    # <a name="replace-the-subnets-index-with-the-value-corresponding-to-the-subnet-you-want-encrypted"></a>Ersetzen Sie den Index für die Subnetze, durch den Wert für das Subnetz, die verschlüsselt werden sollen.  
    # <a name="repeat-for-each-subnet-where-encryption-is-needed"></a>Wiederholen Sie für jedes Subnetz, in denen Verschlüsselung erforderlich ist
    $vnet.properties.Subnets[0].properties.EncryptionEnabled = $true

3.  Fügen Sie das aktualisierte virtuelle Netzwerkobjekt in den Netzwerkcontroller

    New-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId $vnet.ResourceId -Properties $vnet.Properties -force


_**Herzlichen Glückwunsch!** _ Sie sind fertig, nachdem Sie diese Schritte abgeschlossen haben. 


## <a name="next-steps"></a>Nächste Schritte



