---
title: Bereitstellen geschützter Hosts
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 2379ca26-b32d-4055-8b4b-99d1f2df37e1
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 3b20a7eb2b5097d8ddb7381fd0304581ca4e6722
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845351"
---
# <a name="deploy-guarded-hosts"></a>Bereitstellen geschützter Hosts

>Gilt für: WindowsServer 2019, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die Themen in diesem Abschnitt beschreiben die Schritte, die ein fabricadministrator verwendet wird, so konfigurieren Sie Hyper-V-Hosts mit dem Host Guardian Service (HGS) funktioniert. Bevor Sie mindestens einen Knoten in diesen Schritten können die [HGS-Cluster eingerichtet werden muss](guarded-fabric-setting-up-the-host-guardian-service-hgs.md).

**Für TPM-vertrauenswürdiger Nachweis**:
1. [Konfigurieren der DNS-Struktur](guarded-fabric-configuring-fabric-dns.md): Beschreibt wie Sie eine DNS-Weiterleitung von der Fabric-Domäne mit der Host-Überwachungsdienst-Domäne einrichten.
2. [Erfassen von Host-Überwachungsdienst benötigte Informationen](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md): Enthält Informationen zum TPM-Bezeichner (auch als Platform-IDs bezeichnet) zu erfassen, erstellen eine codeintegritätsrichtlinie und erstellen Sie eine TPM-Baseline. Klicken Sie dann bieten Sie diese Informationen an dem HGS-Administrator zum Nachweis konfigurieren.
3. [Vergewissern Sie sich, überwachte Hosts nachweisen können](guarded-fabric-confirm-hosts-can-attest-successfully.md)

**Für den schlüsselnachweis Host**:
1. [Erstellen Sie einen Hostschlüssel](guarded-fabric-create-host-key.md#create-a-host-key): Beschreibt wie Sie eine DNS-Weiterleitung von der Fabric-Domäne mit der Host-Überwachungsdienst-Domäne einrichten.
2. [Fügen Sie den Hostschlüssel auf dem nachweisdienst](guarded-fabric-create-host-key.md#add-the-host-key-to-the-attestation-service): Enthält Informationen zum Einrichten einer Active Directory-Sicherheitsgruppe in der Domäne Fabric überwachten Hosts als Mitglieder dieser Gruppe hinzufügen aus, und geben diese Gruppen-ID für dem HGS-Administrator. 
3. [Vergewissern Sie sich, überwachte Hosts nachweisen können](guarded-fabric-confirm-hosts-can-attest-successfully.md)


**Für den Admin-vertrauenswürdiger Nachweis**:
1. [Konfigurieren der DNS-Struktur](guarded-fabric-configuring-fabric-dns.md): Beschreibt wie Sie eine DNS-Weiterleitung von der Fabric-Domäne mit der Host-Überwachungsdienst-Domäne einrichten.
2. [Erstellen einer Sicherheitsgruppe](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md): Enthält Informationen zum Einrichten einer Active Directory-Sicherheitsgruppe in der Domäne Fabric überwachten Hosts als Mitglieder dieser Gruppe hinzufügen aus, und geben diese Gruppen-ID für dem HGS-Administrator. 
3. [Vergewissern Sie sich, überwachte Hosts nachweisen können](guarded-fabric-confirm-hosts-can-attest-successfully.md)


## <a name="see-also"></a>Siehe auch

- [Bereitstellungsaufgaben für die geschützten Fabrics und abgeschirmte VMs](guarded-fabric-deploying-hgs-overview.md#deployment-tasks-for-guarded-fabrics-and-shielded-vms)
