---
title: Upgrade eines überwachten Fabric auf Windows Server 2019
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 11/21/2018
ms.openlocfilehash: 50e35939031a74173fb031cf963af97bf8bb6dba
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856353"
---
# <a name="upgrade-a-guarded-fabric-to-windows-server-2019"></a>Upgrade eines überwachten Fabric auf Windows Server 2019

> Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Artikel werden die Schritte beschrieben, die erforderlich sind, um ein vorhandenes geschütztes Fabric von Windows Server 2016, Windows Server Version 1709 oder Windows Server Version 1803 auf Windows Server 2019 zu aktualisieren.

## <a name="whats-new-in-windows-server-2019"></a>Neuerungen in Windows Server 2019

Wenn Sie ein überwachtes Fabric unter Windows Server 2019 ausführen, können Sie mehrere neue Features nutzen:

Der **Host Schlüssel** Nachweis ist unser neuester Nachweis Modus, der so konzipiert ist, dass abgeschirmte VMS leichter ausgeführt werden können, wenn Ihre Hyper-V-Hosts nicht über TPM 2,0-Geräte verfügen, die für den TPM-Nachweis verfügbar sind. Der Host Schlüssel Nachweis verwendet Schlüsselpaare zum Authentifizieren von Hosts mit HGS, sodass Hosts nicht mit einer Active Directory Domäne verknüpft werden müssen, wodurch die AD-Vertrauensstellung zwischen HGS und der Unternehmens Gesamtstruktur entfällt und die Anzahl der geöffneten Firewallports reduziert wird. Der Host Schlüssel Nachweis ersetzt Active Directory Nachweis, der in Windows Server 2019 als veraltet markiert ist.

**V2** -Nachweis Version: zur Unterstützung von Host Schlüssel Nachweis und neuen Features in Zukunft haben wir die Versionierung in HGS eingeführt. Eine Neuinstallation von HGS unter Windows Server 2019 führt dazu, dass der Server einen v2-Nachweis durchführt. Dies bedeutet, dass der Host Schlüssel Nachweis für Windows Server 2019-Hosts unterstützt wird und noch v1-Hosts unter Windows Server 2016 unterstützt werden. Direkte Upgrades auf 2019 verbleiben bei Version v1, bis Sie v2 manuell aktivieren. Die meisten Cmdlets verfügen jetzt über den Parameter "-hgsversion", mit dem Sie angeben können, ob Sie mit Legacy-oder modernen Nachweis Richtlinien arbeiten möchten.

**Unterstützung für abgeschirmte Linux-VMs** : Hyper-V-Hosts unter Windows Server 2019 können abgeschirmte Linux-VMs ausführen. Während sich seit Windows Server, Version 1709, abgeschirmte VMS von Linux befinden, ist Windows Server 2019 die erste langfristige Wartung der Kanal Version, um Sie zu unterstützen.

**Verbesserungen bei Filialen** : Wir haben das Ausführen von abgeschirmten VMs in Zweigstellen mit Unterstützung für abgeschirmte Offline-VMS und Fall Back Konfigurationen auf Hyper-V-Hosts vereinfacht.

**TPM-Host Bindung** : für die sichersten Workloads, bei denen eine abgeschirmte VM nur auf dem ersten Host ausgeführt werden soll, auf dem Sie erstellt wurde, können Sie die VM nun mithilfe des TPM des Hosts an diesen Host binden. Dies eignet sich am besten für Arbeitsstationen mit privilegiertem Zugriff und nicht für allgemeine Rechenzentrums Workloads, die zwischen Hosts migriert werden müssen.

## <a name="compatibility-matrix"></a>Kompatibilitätsmatrix

Bevor Sie das geschützte Fabric auf Windows Server 2019 aktualisieren, sollten Sie die folgende Kompatibilitäts Matrix überprüfen, um festzustellen, ob Ihre Konfiguration unterstützt wird.

|  | WS2016-HGS | WS2019-HGS|
|---|---|---|
|**WS2016 Hyper-V-Host** | Unterstützt | Unterstützt<sup>1</sup>|
|**WS2019 Hyper-V-Host** | Nicht unterstützt<sup>2</sup> | Unterstützt|

<sup>1</sup> Windows Server 2016-Hosts können nur Windows Server 2019 HGS-Server mithilfe des v1-Nachweis Protokolls belegen. Neue Features, die exklusiv im v2-Nachweis Protokoll verfügbar sind, einschließlich des Host Schlüssel Nachweis, werden für Windows Server 2016-Hosts nicht unterstützt.

<sup>2</sup> Microsoft kennt ein Problem, das verhindert, dass Windows Server 2019-Hosts, die den TPM-Nachweis verwenden, erfolgreich auf einem Windows Server 2016 HGS-Server getestet werden. Diese Einschränkung wird in einem zukünftigen Update für Windows Server 2016 behoben werden.

## <a name="upgrade-hgs-to-windows-server-2019"></a>Aktualisieren von HGS auf Windows Server 2019

Es wird empfohlen, das Upgrade Ihres HGS-Clusters auf Windows Server 2019 durchzuführen, bevor Sie ein Upgrade für Ihre Hyper-V-Hosts durchführen, um sicherzustellen, dass alle Hosts, ob Sie Windows Server 2016 oder 2019 ausführen, erfolgreich bestätigt werden können.

Wenn Sie Ihren HGS-Cluster aktualisieren, müssen Sie einen Knoten temporär aus dem Cluster entfernen, während er aktualisiert wird. Dadurch wird die Kapazität Ihres Clusters reduziert, um auf Anforderungen von ihren Hyper-V-Hosts zu reagieren. Dies kann zu langsamen Reaktionszeiten oder Dienst Ausfällen für Ihre Mandanten führen. Stellen Sie sicher, dass Sie über genügend Kapazität verfügen, um Ihre Nachweis-und schlüsselfreigabe Anforderungen zu verarbeiten, bevor Sie ein Upgrade für einen HGS

Um Ihr HGS-Cluster zu aktualisieren, führen Sie die folgenden Schritte auf jedem Knoten des Clusters, jeweils jeweils einem Knoten aus:

1.  Entfernen Sie den HGS-Server aus Ihrem Cluster durch Ausführen von `Clear-HgsServer` an einer PowerShell-Eingabeaufforderung mit erhöhten Rechten. Mit diesem Cmdlet werden der replizierte HGS-Speicher, die HGS-Websites und der Knoten aus dem Failovercluster entfernt.
2.  Wenn es sich bei dem HGS-Server um einen Domänen Controller (Standardkonfiguration) handelt, müssen Sie `adprep /forestprep` ausführen und `adprep /domainprep` auf dem ersten Knoten ausführen, der aktualisiert wird, um die Domäne für ein Betriebssystem Upgrade vorzubereiten. Weitere Informationen finden Sie in der [Active Directory Domain Services Upgradedokumentation](https://docs.microsoft.com/windows-server/identity/ad-ds/deploy/upgrade-domain-controllers#supported-in-place-upgrade-paths) .
3.  Führen Sie ein direktes Upgrade auf Windows Server 2019 [aus](../../get-started-19/install-upgrade-migrate-19.md) .
4.  Führen Sie [Initialize-hgsserver](guarded-fabric-configure-additional-hgs-nodes.md) aus, um den Knoten wieder zum Cluster hinzuzufügen.

Nachdem alle Knoten auf Windows Server 2019 aktualisiert wurden, können Sie optional die HGS-Version auf v2 aktualisieren, um neue Features wie den Host Schlüssel Nachweis zu unterstützen.

```powershell
Set-HgsServerVersion  v2
```

## <a name="upgrade-hyper-v-hosts-to-windows-server-2019"></a>Aktualisieren von Hyper-V-Hosts auf Windows Server 2019

Bevor Sie ein Upgrade für Ihre Hyper-v-Hosts auf Windows Server 2019 durchführen, stellen Sie sicher, dass Ihr HGS-Cluster bereits auf Windows Server 2019 aktualisiert wurde und Sie alle virtuellen Computer vom Hyper-v-Server verschoben haben.

1.  Wenn Sie Windows Defender-Anwendungs Steuerungs Code-Integritäts Richtlinien auf dem Server verwenden (immer bei der Verwendung des TPM-Nachweis), stellen Sie sicher, dass die Richtlinie entweder im Überwachungsmodus oder deaktiviert ist, bevor Sie versuchen, den Server zu aktualisieren. [Erfahren Sie, wie Sie eine WDac-Richtlinie deaktivieren](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/disable-windows-defender-application-control-policies)
2.  Befolgen Sie die Anweisungen im [Windows Server-upgradeinhalt](../../upgrade/upgrade-overview.md) , um Ihren Host auf Windows Server 2019 zu aktualisieren. Wenn Ihr Hyper-V-Host Teil eines Failoverclusters ist, können Sie ein paralleles [Upgrade des Cluster Betriebssystems](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md)in Erwägung gezogen.
3.  Testen Sie Ihre Windows Defender-Anwendungs Steuerungs Richtlinie, [und aktivieren](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/audit-windows-defender-application-control-policies) Sie Sie erneut, wenn Sie vor dem Upgrade eine aktiviert haben.
4.  Führen Sie `Get-HgsClientConfiguration` aus, um zu überprüfen, ob **ishostbewacht = true**ist. Dies bedeutet, dass der Host erfolgreich mit Ihrem HGS-Server übergeben wird.
5.  Wenn Sie einen TPM-Nachweis verwenden, müssen Sie [die TPM-Baseline oder die Code Integritätsrichtlinie](guarded-fabric-add-host-information-for-tpm-trusted-attestation.md) nach dem Upgrade erneut erfassen, um den Nachweis zu erfüllen.
6.  Erneutes Ausführen von abgeschirmten VMS auf dem Host

## <a name="switch-to-host-key-attestation"></a>Zum Host Schlüssel Nachweis wechseln

Führen Sie die folgenden Schritte aus, wenn Sie zurzeit Active Directory basierten Nachweis ausführen und ein Upgrade auf den Host Schlüssel Nachweis durchführen möchten. Beachten Sie, dass der Active Directory basierte Nachweis in Windows Server 2019 veraltet ist und in einer zukünftigen Version möglicherweise entfernt wird.

1.  Stellen Sie sicher, dass der HGS-Server im v2-Nachweis Modus betrieben wird, indem Sie den folgenden Befehl ausführen. Vorhandene v1-Hosts werden auch dann weiterhin überzeugen, wenn der HGS-Server auf v2 aktualisiert wird.

    ```powershell
    Set-HgsServerVersion v2
    ```

2.  [Generieren Sie Host Schlüssel](guarded-fabric-create-host-key.md) von jedem ihrer Hyper-V-Hosts, und registrieren Sie Sie bei HGS. Da sich HGS weiterhin im Active Directory Modus befindet, wird eine Warnung angezeigt, dass die neuen Host Schlüssel nicht sofort wirksam werden. Dies ist beabsichtigt, da Sie nicht in den Host Schlüssel Modus wechseln möchten, bis alle Hosts erfolgreich mit Host Schlüsseln bestätigt werden.

3.  Nachdem die Host Schlüssel für jeden Host registriert wurden, können Sie HGS so konfigurieren, dass der Host Schlüssel Nachweis Modus verwendet wird:

    ```powershell
    Set-HgsServer -TrustHostKey
    ```

    Wenn Sie Probleme mit dem Host Schlüssel Modus haben und auf Active Directory basierten Nachweis zurückkehren müssen, führen Sie den folgenden Befehl auf HGS aus:

    ```powershell
    Set-HgsServer -TrustActiveDirectory
    ```