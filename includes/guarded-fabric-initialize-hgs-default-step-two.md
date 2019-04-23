Suchen Sie Ihr HGS-Überwachungsdienst-Zertifikate. Sie benötigen ein Signaturzertifikat und ein Verschlüsselungszertifikat clientkonfigurationsobjekt des Host-Überwachungsdienst-Clusters.
Die einfachste Möglichkeit zum Angeben der Zertifikate auf dem Host-Überwachungsdienst ist eine kennwortgeschützte PFX-Datei für jedes Zertifikat zu erstellen, die die öffentlichen und privaten Schlüssel enthält. Wenn Sie HSM-gesicherten Schlüsseln oder andere nicht exportierbare Zertifikate verwenden, stellen Sie sicher, dass das Zertifikat in den Zertifikatspeicher des lokalen Computers installiert ist, bevor Sie fortfahren.
Weitere Informationen, welche Zertifikate verwenden können, finden Sie unter [Abrufen von Zertifikaten für die Host-Überwachungsdienst](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-obtain-certs).

<!-- Appears in guarded-fabric-initialize-hgs-ad-mode-default.md and guarded-fabric-initialize-hgs-tpm-mode-default.md
-->