Wenn Sie eine PFX-Datei nicht für die Verschlüsselung und Signaturzertifikate auf dem ersten HGS-Server angegeben haben, wird nur der öffentliche Schlüssel mit diesem Server repliziert werden.
Sie müssen den privaten Schlüssel durch Importieren einer PFX-Datei mit dem privaten Schlüssel, in den lokalen Zertifikatspeicher oder, im Fall von HSM-gesicherten Schlüsseln, installieren den Softwareschlüsselspeicher-Anbieter konfigurieren und Ihre Zertifikate pro Ihres HSM-Herstellers zuordnen Anweisungen.

<!-- Appears in guarded-fabric-initialize-hgs-ad-mode-default.md and guarded-fabric-initialize-hgs-tpm-mode-default.md
-->