---
title: Upgrade eines überwachten Fabric auf Windows Server 2019
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 11/21/2018
ms.openlocfilehash: 39974806c02e55b37d3d16748c4ca0e3f361ee45
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284110"
---
# <a name="upgrade-a-guarded-fabric-to-windows-server-2019"></a>Upgrade eines überwachten Fabric auf Windows Server 2019

> Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieser Artikel beschreibt die erforderlichen Schritte zum Aktualisieren eines vorhandenen geschützten Fabrics von Windows Server 2016, Windows Server, Version 1709 oder Windows Server-Version 1803 auf Windows Server-2019.

## <a name="whats-new-in-windows-server-2019"></a>Neuigkeiten in Windows Server 2019

Wenn Sie ein geschütztes Fabric für Windows Server-2019 ausführen, können Sie mehrere neue Funktionen nutzen:

**Hosten von Schlüsselnachweis** ist unsere neuesten nachweismodus, erleichtern es, die abgeschirmte VMs ausführen, wenn Hyper-V-Hosts nicht über TPM 2.0-Geräte, die für den TPM-Nachweis verfügbar verfügen soll. Host-Schlüsselnachweis verwendet Schlüsselpaare, um einen Host mit Host-Überwachungsdienst bietet die Anforderung für Hosts mit einer Active Directory-Domäne verknüpft werden die AD-Vertrauensstellung zwischen Host-Überwachungsdienst und der Unternehmensgesamtstruktur zu eliminieren und Reduzierung der Anzahl von Firewallports öffnen zu authentifizieren. Host-Schlüsselnachweis ersetzt die Active Directory-Nachweis, die in Windows Server-2019 veraltet ist.

**Nachweis v2-Version** - Host-Schlüsselnachweis und neue Funktionen in der Zukunft unterstützen wir haben die Versionierung für Host-Überwachungsdienst eingeführt. Eine neue Installation von Host-Überwachungsdienst auf Windows Server-2019 führt auf dem Server, die mit v2-Nachweis, was bedeutet es Host schlüsselnachweis für 2019 für Windows Server-Hosts unterstützt wird, und nach wie vor die v1-Hosts unter Windows Server 2016 unterstützen. Bei Version v1 wird ein direktes Upgrades auf 2019 bleibt, bis Sie manuell, v2 aktivieren. Die meisten Cmdlets haben jetzt einen HgsVersion - Parameter, mit dem Sie angeben, wenn Sie mit älteren oder moderne Nachweis Richtlinien arbeiten möchten.

**Unterstützung für Linux abgeschirmte VMs** -Hyper-V-Hosts, die mit Windows Server-2019 können ausführen abgeschirmte Linux-VMs. Abgeschirmten Linux-VMs waren seit Windows Server-Version 1709, Windows Server-2019 ist die erste Wartungskanal für Long-Term-Version, zu deren Unterstützung.

**Branch Office Verbesserungen** – wir machen es einfacher, zum Ausführen geschützter VMs in Zweigstellen mit Unterstützung für offline-abgeschirmte VMs und Konfigurationen für Hyper-V-Hosts.

**TPM-Bindung durch Host** – für die meisten Workloads Sie möchten eine abgeschirmte VM nur auf den ersten Host ausgeführt sichere, bei denen es erstelltes, aber keine anderen war, können Sie nun den virtuellen Computer für diesen Host mithilfe des Hosts TPM binden. Dies ist am besten verwendet für Arbeitsstationen mit privilegiertem Zugriff und Zweigstellen, anstatt der allgemeinen Datacenter-Workloads, die die zwischen Hosts migriert werden müssen.

## <a name="compatibility-matrix"></a>Matrix der sperrenkompatibilität

Überprüfen Sie die folgenden Kompatibilitätsmatrix, um festzustellen, ob Ihre Konfiguration unterstützt wird, vor dem upgrade von Ihr geschützten Fabrics auf Windows Server-2019.

|  | WS2016 HGS | WS2019 HGS|
|---|---|---|
|**WS2016 Hyper-V Host** | Unterstützt | Unterstützt<sup>1</sup>|
|**WS2019 Hyper-V Host** | Nicht unterstützte<sup>2</sup> | Unterstützt|

<sup>1</sup> Windows Server 2016-Hosts können nur für Windows Server 2019 HGS-Servern, die über die v1-nachweisprotokoll bestätigen. Neue Features, die in das nachweisprotokoll v2, einschließlich Schlüsselnachweis Host, ausschließlich verfügbar sind, werden für Windows Server 2016-Hosts nicht unterstützt.

<sup>2</sup> besteht ein bekanntes Problem verhindert 2019 für Windows Server-Hosts, die TPM-Nachweis von bestätigen erfolgreich für einen Windows Server 2016-Host-Überwachungsdienst-Server verwenden. Diese Einschränkung wird in einem zukünftigen Update für Windows Server 2016 behoben.

## <a name="upgrade-hgs-to-windows-server-2019"></a>Aktualisieren von Host-Überwachungsdienst auf Windows-Server 2019

Es wird empfohlen, aktualisieren Ihren HGS-Cluster auf Windows Server-2019, vor dem upgrade auf die Hyper-V-Hosts, um sicherzustellen, dass alle Hosts, fortfahren können, ob sie Windows Server 2016 oder 2019, ausgeführt werden, erfolgreich zu bestätigen.

Aktualisieren Ihren HGS-Cluster erfordert, dass Sie vorübergehend entfernen einen Knoten aus dem Cluster zu einem Zeitpunkt während des Upgrades ist. Dies reduziert die Kapazität des Clusters zum Reagieren auf Anforderungen von den Hyper-V-Hosts und kann zu langsamen Reaktionszeiten kommt oder Ausfälle von Betriebssystemdiensten für Ihren Mandanten. Stellen Sie sicher, dass Sie ausreichenden Kapazität für Ihre Nachweis und die wichtigsten Release-Anforderungen zu verarbeiten, vor dem Upgrade eines HGS-Servers verfügen.

Um Ihren HGS-Cluster zu aktualisieren, führen Sie die folgenden Schritte auf jedem Knoten des Clusters, einen Knoten zu einem Zeitpunkt:

1.  Entfernen Sie den HGS-Server aus dem Cluster mit `Clear-HgsServer` in einer PowerShell-Eingabeaufforderung mit erhöhten Rechten. Dieses Cmdlet entfernt die Host-Überwachungsdienst replizierte Speicher, Host-Überwachungsdienst-Websites und Knoten aus dem Failovercluster.
2.  Wenn Sie Ihr HGS-Server ein Domänencontroller (Standardkonfiguration) ist, müssen Sie ausführen `adprep /forestprep` und `adprep /domainprep` auf dem ersten Knoten, die gerade aktualisiert wird, um die Domäne für ein Betriebssystemupgrade vorzubereiten. Finden Sie unter den [Active Directory Domain Services-upgradedokumentation](https://docs.microsoft.com/windows-server/identity/ad-ds/deploy/upgrade-domain-controllers#supported-in-place-upgrade-paths) für Weitere Informationen.
3.  Führen Sie eine [in-Place-Aktualisierung](../../get-started-19/install-upgrade-migrate-19.md) auf Windows Server-2019.
4.  Führen Sie [Initialize-HgsServer](guarded-fabric-configure-additional-hgs-nodes.md) auf die Knoten zum Cluster hinzuzufügen.

Sobald alle Knoten auf Windows Server-2019 aktualisiert wurden, können Sie optional die Host-Überwachungsdienst-Version auf v2 zur Unterstützung neuer Features wie z. B. Schlüsselnachweis Host aktualisieren.

```powershell
Set-HgsServerVersion  v2
```

## <a name="upgrade-hyper-v-hosts-to-windows-server-2019"></a>Aktualisieren von Hyper-V-Hosts Windows Server-2019

Bevor Sie den Hyper-V-Hosts Windows Server-2019 aktualisieren, stellen Sie sicher, dass es sich bei Ihrem Host-Überwachungsdienst-Cluster auf Windows Server-2019 bereits aktualisiert wird und dass Sie alle virtuellen Computer vom Hyper-V-Server verschoben haben.

1.  Wenn Sie Windows Defender Application Control anwendungssteuerungscode-Integritätsrichtlinien auf dem Server (immer der Fall bei Verwendung von TPM-Nachweis) verwenden, stellen Sie sicher, dass die Richtlinie befindet sich entweder in der Überwachungsmodus aktiviert oder deaktiviert werden, bevor Sie versuchen, den Server zu aktualisieren. [Erfahren Sie, wie eine WDAC-Richtlinie deaktivieren](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/disable-windows-defender-application-control-policies)
2.  Befolgen Sie die Anweisungen in der [Windows Server-Upgrade-Center](http://aka.ms/upgradecenter) Hosts an, um Windows Server-2019 zu aktualisieren. Wenn Ihre Hyper-V-Host Teil eines Failoverclusters ist, sollten Sie eine [Cluster Operating System Rolling Upgrade](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md).
3.  [Testen und reaktivieren Sie](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/audit-windows-defender-application-control-policies) Ihre Windows Defender Application Control-Richtlinie, wenn Sie einen vor dem Upgrade aktiviert haben.
4.  Führen Sie `Get-HgsClientConfiguration` überprüft, ob **IsHostGuarded = True**, d. h. des Hosts Nachweis mit dem HGS-Server erfolgreich übergeben wird.
5.  Wenn Sie TPM-Nachweis verwenden, müssen Sie möglicherweise auf [erfassen Sie die Integrität-Richtlinie für den TPM Baseline oder den Code erneut](guarded-fabric-add-host-information-for-tpm-trusted-attestation.md) nach dem Upgrade auf einen Nachweis erbringen.
6.  Start ausführen abgeschirmter VMs auf dem Host wieder!

## <a name="switch-to-host-key-attestation"></a>Wechseln Sie zum Hosten von den Schlüsselnachweis

Führen Sie die folgenden Schritte aus, wenn Sie Active Directory-basierten Nachweis derzeit ausgeführt werden und auf dem Host Schlüsselnachweis aktualisieren möchten. Beachten Sie, dass die Active Directory-basierten Nachweis ist in Windows Server-2019 veraltet und kann in einer zukünftigen Version entfernt werden.

1.  Stellen Sie sicher, dass Ihr HGS-Server mithilfe des folgenden Befehls in v2-nachweismodus ausgeführt wird. Vorhandenen v1-Hosts werden fortgesetzt, bestätigen Sie, selbst wenn der HGS-Server auf v2 aktualisiert wird.

    ```powershell
    Set-HgsServerVersion v2
    ```

2.  [Host-Schlüssel generieren](guarded-fabric-create-host-key.md) aller Ihrer Hyper-V-hosts, und registrieren Sie ihn beim Host-Überwachungsdienst. Da die Host-Überwachungsdiensts dennoch im Active Directory-Modus betrieben wird, erhalten Sie eine Warnung, dass der neue Hostschlüssel nicht sofort wirksam werden. Dies ist beabsichtigt und, da Sie nicht möchten, so ändern in Host-Modus-Taste, bis alle Hosts erfolgreich mit Hostschlüssel nachweisen kann.

3.  Nachdem der Host-Schlüssel für jeden Host registriert wurden, können Sie HGS für die Verwendung der Host den schlüsselnachweis-Modus konfigurieren:

    ```powershell
    Set-HgsServer -TrustHostKey
    ```

    Wenn Sie schwierigkeiten mit dem Host-Schlüssel-Modus ausführen und die zu Active Directory-basierten Nachweis zurückkehren müssen, führen Sie den folgenden Befehl auf dem Host-Überwachungsdienst:

    ```powershell
    Set-HgsServer -TrustActiveDirectory
    ```