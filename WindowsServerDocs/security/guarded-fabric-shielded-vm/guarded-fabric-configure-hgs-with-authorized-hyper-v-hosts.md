---
title: Bereitstellen geschützter Hosts
ms.prod: windows-server
ms.topic: article
ms.assetid: 2379ca26-b32d-4055-8b4b-99d1f2df37e1
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 0f678172d397ff61fd336b7c844d43f77bea7fad
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856833"
---
# <a name="deploy-guarded-hosts"></a>Bereitstellen geschützter Hosts

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


## <a name="see-also"></a>Siehe auch

- [Bereitstellungs Aufgaben für geschützte Fabrics und abgeschirmte VMS](guarded-fabric-deploying-hgs-overview.md#deployment-tasks-for-guarded-fabrics-and-shielded-vms)
