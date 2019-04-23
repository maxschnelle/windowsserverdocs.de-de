Alternativ können Sie einen Fingerabdruck angeben, wenn Sie Ihr eigenes Zertifikat verwenden möchten. Dies kann nützlich sein, wenn ein Zertifikat auf mehreren Computern freigeben, oder verwenden ein Zertifikat an einem TPM noch ein HSM gebunden werden soll. Hier ist ein Beispiel zum Erstellen eines TPM-Bound-Zertifikats (der verhindert, dass der private Schlüssel gestohlen und auf einem anderen Computer verwendet und erfordert nur ein TPM 1.2):

```powersehll
$tpmBoundCert = New-SelfSignedCertificate -Subject “Host Key Attestation ($env:computername)” -Provider “Microsoft Platform Crypto Provider”
Set-HgsClientHostKey -Thumbprint $tpmBoundCert.Thumbprint
```


<!-- Appears in set-up-hgs-for-always-encrypted-in-sql-server.md and guarded-fabric-create-host-key.md
-->