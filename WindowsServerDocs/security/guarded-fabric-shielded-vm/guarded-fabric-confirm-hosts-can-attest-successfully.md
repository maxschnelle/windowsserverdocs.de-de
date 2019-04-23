---
title: Vergewissern Sie sich, überwachte Hosts nachweisen können
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 7485796b-b840-4678-9b33-89e9710fbbc7
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 02/05/2019
ms.openlocfilehash: 6b67208176b426f52d3c5106f8de09ad334d3b01
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829531"
---
# <a name="confirm-guarded-hosts-can-attest"></a>Vergewissern Sie sich, überwachte Hosts nachweisen können 

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016


Ein fabricadministrator muss, um sicherzustellen, dass die Hyper-V-Hosts als überwachten Hosts ausgeführt werden können. Führen Sie die folgenden Schritte aus, auf mindestens einen bewachten Host:

1.  Wenn Sie die Hyper-V-Rolle und das Feature für Hyper-V-Unterstützung für Host-Überwachungsdiensts noch nicht installiert haben, installieren Sie sie mit dem folgenden Befehl ein:

        Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart

2.  Stellen Sie sicher, die Hyper-V-Host den HGS DNS-Namen auflösen kann, und verfügt über eine Netzwerkverbindung zum Erreichen von Port 80 (oder 443, wenn Sie HTTPS eingerichtet) auf dem Host-Überwachungsdienst-Server.

2.  Konfigurieren des Hosts Schlüsselschutz und Nachweis-URLs:

    - **Mithilfe von Windows PowerShell**: Sie können den Schutz der Schlüssel und die Nachweis URLs konfigurieren, durch den folgenden Befehl in einer Windows PowerShell-Konsole mit erhöhten Rechten ausführen. Für &lt;FQDN&gt;, verwenden Sie den vollständig qualifizierten Domänennamen (FQDN) des Host-Überwachungsdienst-Clusters (z. B. hgs.bastion.local, oder bitten Sie den HGS-Administrator zum Ausführen der **Get-HgsServer** Cmdlet auf dem Host-Überwachungsdienst-Server zum Abrufen der URLs).

        `Set-HgsClientConfiguration -AttestationServerUrl 'http://<FQDN>/Attestation' -KeyProtectionServerUrl 'http://<FQDN>/KeyProtection'`

        Um einen fallback-Host-Überwachungsdienst-Server konfigurieren, wiederholen Sie diesen Befehl aus, und geben Sie die fallback-URLs für den Schlüsselschutz und Nachweis. Weitere Informationen finden Sie unter [Fallbackkonfiguration](guarded-fabric-manage-branch-office.md#fallback-configuration). 

    - **Über VMM**: Bei Verwendung von System Center 2016 – Virtual Machine Manager (VMM) können Sie die Nachweis- und Schlüsselschutz-URLs für Schlüssel in VMM konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren globaler HGS-Einstellungen](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-hosts#configure-global-hgs-settings) in **Bereitstellen von überwachten Hosts in VMM**.
    
    >**Hinweise**
    > - Wenn der HGS-Administrator [HTTPS auf dem Host-Überwachungsdienst-Server aktiviert](guarded-fabric-configure-hgs-https.md), beginnen Sie die URLs mit `https://`.
    > - Wenn der HGS-Administrator HTTPS auf dem Host-Überwachungsdienst-Server aktiviert und ein selbstsigniertes Zertifikat verwendet, müssen Sie das Zertifikat in den Speicher "Vertrauenswürdige Stammzertifizierungsstellen" auf jedem Host zu importieren. Zu diesem Zweck führen Sie den folgenden Befehl auf jedem Host aus:<br>
        `Import-Certificate -FilePath "C:\temp\HttpsCertificate.cer" -CertStoreLocation Cert:\LocalMachine\Root`
    
3.  Um ein Nachweis Versuch, auf dem Host zu initiieren und Anzeigen des nachweisstatus, führen Sie den folgenden Befehl aus:

        Get-HgsClientConfiguration

    Die Ausgabe des Befehls gibt an, ob der Host Nachweis übergeben und ist jetzt geschützt. Wenn `IsHostGuarded` keinen zurückgibt **"true"**, Sie können das Host-Überwachungsdienst-Diagnosetool ausführen [Get-HgsTrace](https://technet.microsoft.com/library/mt718831.aspx), um zu untersuchen. Geben Sie den folgenden Befehl in einer Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten auf dem Host, um die Diagnose:

        Get-HgsTrace -RunDiagnostics -Detailed

    > [!IMPORTANT]
    > Wenn Sie Windows Server-2019 oder Windows 10, Version 1809 verwenden und die anwendungssteuerungscode-Integritätsrichtlinien, verwenden `Get-HgsTrace` möglicherweise einen Fehler für zurück der **Code Integrity Richtlinie aktiv** Diagnose.
    > Sie können dieses Ergebnis gefahrlos ignorieren, bei dem nur fehlgeschlagene Diagnose.

## <a name="next-step"></a>Nächster Schritt

>[!div class="nextstepaction"]
[Bereitstellen von abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)

## <a name="see-also"></a>Siehe auch

- [Bereitstellen des Host-Überwachungsdienst (Host-Überwachungsdienst)](guarded-fabric-deploying-hgs-overview.md)
- [Bereitstellen von abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)

