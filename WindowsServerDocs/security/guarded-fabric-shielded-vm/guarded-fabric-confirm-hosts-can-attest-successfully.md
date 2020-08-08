---
title: Bestätigen, dass geschützte Hosts bestätigen können
ms.topic: article
ms.assetid: 7485796b-b840-4678-9b33-89e9710fbbc7
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 09/25/2019
ms.openlocfilehash: 8c3f28b544db7a41c15c4f12b58c58c1f750cb54
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997506"
---
# <a name="confirm-guarded-hosts-can-attest"></a>Bestätigen, dass geschützte Hosts bestätigen können

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

Ein fabricadministrator muss bestätigen, dass Hyper-V-Hosts als geschützte Hosts ausgeführt werden können. Führen Sie die folgenden Schritte auf mindestens einem überwachten Host aus:

1. Wenn Sie die Hyper-v-Rolle und die Hyper-v-Unterstützung des Host-Überwachungs Diensts noch nicht installiert haben, installieren Sie diese mit dem folgenden Befehl:

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ```

2. Stellen Sie sicher, dass der Hyper-V-Host den DNS-Namen des HGS auflösen kann und über die Netzwerk Konnektivität zum Erreichen von Port 80 (oder 443, wenn Sie HTTPS einrichten) auf dem HGS-Server verfügt.

3. Konfigurieren Sie die Schlüsselschutz-und Nachweis-URLs des Hosts:

    - **Über Windows PowerShell**: Sie können die Schlüsselschutz-und Nachweis-URLs konfigurieren, indem Sie den folgenden Befehl in einer Windows PowerShell-Konsole mit erhöhten Rechten ausführen. &lt;Verwenden Sie für den FQDN &gt; den voll qualifizierten Domänen Namen (Fully Qualified Domain Name, FQDN) Ihres HGS-Clusters (z. b. HGS. Bastion. local), oder bitten Sie den HGS-Administrator, das Cmdlet **Get-hgsserver** auf dem HGS-Server auszuführen, um die URLs abzurufen.

        ```PowerShell
        Set-HgsClientConfiguration -AttestationServerUrl 'http://<FQDN>/Attestation' -KeyProtectionServerUrl 'http://<FQDN>/KeyProtection'
         ```

        Um einen Fall Back-HGS-Server zu konfigurieren, wiederholen Sie diesen Befehl, und geben Sie die Fall Back-URLs für die Schlüsselschutz-und Nachweis Dienste an. Weitere Informationen finden Sie unter [Fall Back Konfiguration](guarded-fabric-manage-branch-office.md#fallback-configuration).

    - **Über VMM**: Wenn Sie System Center 2016-Virtual Machine Manager (VMM) verwenden, können Sie die URLs für den Nachweis und den Schlüsselschutz in VMM konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren globaler HGS-Einstellungen](/system-center/vmm/guarded-deploy-host?view=sc-vmm-2019#configure-global-hgs-settings) in Bereitstellen von über **wachten Hosts in VMM**.

    >**Hinweise**
    > - Wenn der HGS-Administrator [https auf dem HGS-Server aktiviert](guarded-fabric-configure-hgs-https.md)hat, beginnen Sie mit den URLs `https://` .
    > - Wenn der HGS-Administrator HTTPS auf dem HGS-Server aktiviert und ein selbst signiertes Zertifikat verwendet hat, müssen Sie das Zertifikat in den Speicher vertrauenswürdiger Stamm Zertifizierungsstellen auf jedem Host importieren. Führen Sie hierzu den folgenden Befehl auf jedem Host aus:
       ```PowerShell
       Import-Certificate -FilePath "C:\temp\HttpsCertificate.cer" -CertStoreLocation Cert:\LocalMachine\Root
       ```
    > - Wenn Sie den HGS-Client für die Verwendung von HTTPS konfiguriert und TLS 1,0 systemwide deaktiviert haben, finden Sie in unserem [modernen TLS-Leitfaden](guarded-fabric-troubleshoot-hosts.md#modern-tls) Weitere Informationen.

4. Führen Sie den folgenden Befehl aus, um einen Nachweis Versuch auf dem Host zu initiieren und den Nachweis Status anzuzeigen:

    ```powershell
    Get-HgsClientConfiguration
    ```

    Die Ausgabe des Befehls gibt an, ob der Host den Nachweis überschritten hat und nun geschützt ist. Wenn `IsHostGuarded` nicht " **true**" zurückgibt, können Sie das HGS-Diagnosetool [Get-hgstrace](https://technet.microsoft.com/library/mt718831.aspx)ausführen, um dies zu untersuchen. Um die Diagnose auszuführen, geben Sie den folgenden Befehl in einer Windows PowerShell-Eingabeaufforderung mit erhöhten Rechten auf dem Host ein:

    ```powershell
    Get-HgsTrace -RunDiagnostics -Detailed
    ```

    > [!IMPORTANT]
    > Wenn Sie Windows Server 2019 oder Windows 10, Version 1809, verwenden und Code Integritäts Richtlinien verwenden, sollten Sie `Get-HgsTrace` einen Fehler für die aktive Diagnose der **Code Integritätsrichtlinie** zurückgeben.
    > Sie können dieses Ergebnis gefahrlos ignorieren, wenn es die einzige Fehlerdiagnose ist.

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Bereitstellen von abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)

## <a name="additional-references"></a>Weitere Verweise

- [Bereitstellen des Host-Überwachungsdiensts](guarded-fabric-deploying-hgs-overview.md)
- [Bereitstellen von abgeschirmten VMs](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)