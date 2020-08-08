---
title: Bereitstellen überwachter Hosts
ms.topic: article
ms.assetid: 2379ca26-b32d-4055-8b4b-99d1f2df37e1
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: d69ce87349e7714a1aaf1bb0cc03fb9a145da12e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87966137"
---
# <a name="deploy-guarded-hosts"></a>Bereitstellen überwachter Hosts

>Gilt für: Windows Server 2019, Windows Server (halbjährlicher Kanal), Windows Server 2016

In den Themen in diesem Abschnitt werden die Schritte beschrieben, die ein Fabric-Administrator zum Konfigurieren von Hyper-V-Hosts für die Verwendung mit dem Host-Überwachungsdienst (HGS) durchführt. Bevor Sie diese Schritte ausführen können, muss mindestens ein Knoten im [HGS-Cluster eingerichtet werden](guarded-fabric-setting-up-the-host-guardian-service-hgs.md).

**Für TPM-Trusted Nachweis**:
1. [Konfigurieren des Fabric-DNS](guarded-fabric-configuring-fabric-dns.md): erläutert, wie Sie eine DNS-Weiterleitung von der Fabric-Domäne zur HGS-Domäne einrichten.
2. [Von HGS benötigte Erfassungs Informationen](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md): erläutert, wie TPM-IDs (auch als Platt Form Bezeichner bezeichnet) erfasst, eine Code Integritätsrichtlinie erstellt und eine TPM-Baseline erstellt wird. Anschließend geben Sie diese Informationen für den HGS-Administrator an, um den Nachweis zu konfigurieren.
3. [Bestätigen, dass geschützte Hosts bestätigen können](guarded-fabric-confirm-hosts-can-attest-successfully.md)

**Für Host Schlüssel**Nachweis:
1. [Erstellen eines Host Schlüssels](guarded-fabric-create-host-key.md#create-a-host-key): erläutert, wie Sie eine DNS-Weiterleitung von der Fabric-Domäne zur HGS-Domäne einrichten.
2. [Hinzufügen des Host Schlüssels zum Nachweis Dienst](guarded-fabric-create-host-key.md#add-the-host-key-to-the-attestation-service): erläutert das Einrichten einer Active Directory Sicherheitsgruppe in der Fabric-Domäne, das Hinzufügen von überwachten Hosts als Mitglieder dieser Gruppe und das Bereitstellen dieser Gruppen-ID für den HGS-Administrator.
3. [Bestätigen, dass geschützte Hosts bestätigen können](guarded-fabric-confirm-hosts-can-attest-successfully.md)


**Für admin-Trusted Nachweis**:
1. [Konfigurieren des Fabric-DNS](guarded-fabric-configuring-fabric-dns.md): erläutert, wie Sie eine DNS-Weiterleitung von der Fabric-Domäne zur HGS-Domäne einrichten.
2. [Erstellen einer Sicherheitsgruppe](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md): erläutert, wie Sie eine Active Directory Sicherheitsgruppe in der Fabric-Domäne einrichten, überwachte Hosts als Mitglieder dieser Gruppe hinzufügen und diese Gruppen-ID dem HGS-Administrator bereitstellen.
3. [Bestätigen, dass geschützte Hosts bestätigen können](guarded-fabric-confirm-hosts-can-attest-successfully.md)


## <a name="additional-references"></a>Weitere Verweise

- [Bereitstellungs Aufgaben für geschützte Fabrics und abgeschirmte VMS](guarded-fabric-deploying-hgs-overview.md#deployment-tasks-for-guarded-fabrics-and-shielded-vms)
