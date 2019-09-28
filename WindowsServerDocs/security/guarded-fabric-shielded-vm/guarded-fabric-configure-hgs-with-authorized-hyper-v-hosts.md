---
title: Bereitstellen geschützter Hosts
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 2379ca26-b32d-4055-8b4b-99d1f2df37e1
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: bc79d13b4dda96cd3e760958a6310276d2c45bae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386753"
---
# <a name="deploy-guarded-hosts"></a>Bereitstellen geschützter Hosts

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

In den Themen in diesem Abschnitt werden die Schritte beschrieben, die ein Fabric-Administrator zum Konfigurieren von Hyper-V-Hosts für die Verwendung mit dem Host-Überwachungsdienst (HGS) durchführt. Bevor Sie diese Schritte ausführen können, muss mindestens ein Knoten im [HGS-Cluster eingerichtet werden](guarded-fabric-setting-up-the-host-guardian-service-hgs.md).

**Für TPM-Trusted Nachweis**:
1. [Konfigurieren des Fabric-DNS](guarded-fabric-configuring-fabric-dns.md): Erläutert, wie Sie eine DNS-Weiterleitung von der Fabric-Domäne zur HGS-Domäne einrichten.
2. [Erfassungs Informationen, die für HGS erforderlich](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)sind: Erläutert, wie TPM-IDs (auch als Platt Form Bezeichner bezeichnet) erfasst, eine Code Integritätsrichtlinie erstellt und eine TPM-Baseline erstellt wird. Anschließend geben Sie diese Informationen für den HGS-Administrator an, um den Nachweis zu konfigurieren.
3. [Bestätigen, dass geschützte Hosts bestätigen können](guarded-fabric-confirm-hosts-can-attest-successfully.md)

**Für Host Schlüssel**Nachweis:
1. [Erstellen eines Host Schlüssels](guarded-fabric-create-host-key.md#create-a-host-key): Erläutert, wie Sie eine DNS-Weiterleitung von der Fabric-Domäne zur HGS-Domäne einrichten.
2. [Fügen Sie den Host Schlüssel zum Nachweis Dienst hinzu](guarded-fabric-create-host-key.md#add-the-host-key-to-the-attestation-service): Erläutert das Einrichten einer Active Directory Sicherheitsgruppe in der Fabric-Domäne, das Hinzufügen von überwachten Hosts als Mitglieder dieser Gruppe und das Bereitstellen dieser Gruppen-ID für den HGS-Administrator. 
3. [Bestätigen, dass geschützte Hosts bestätigen können](guarded-fabric-confirm-hosts-can-attest-successfully.md)


**Für admin-Trusted Nachweis**:
1. [Konfigurieren des Fabric-DNS](guarded-fabric-configuring-fabric-dns.md): Erläutert, wie Sie eine DNS-Weiterleitung von der Fabric-Domäne zur HGS-Domäne einrichten.
2. [Erstellen Sie eine Sicherheitsgruppe](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md): Erläutert das Einrichten einer Active Directory Sicherheitsgruppe in der Fabric-Domäne, das Hinzufügen von überwachten Hosts als Mitglieder dieser Gruppe und das Bereitstellen dieser Gruppen-ID für den HGS-Administrator. 
3. [Bestätigen, dass geschützte Hosts bestätigen können](guarded-fabric-confirm-hosts-can-attest-successfully.md)


## <a name="see-also"></a>Siehe auch

- [Bereitstellungs Aufgaben für geschützte Fabrics und abgeschirmte VMS](guarded-fabric-deploying-hgs-overview.md#deployment-tasks-for-guarded-fabrics-and-shielded-vms)
