---
title: Generation 1 VM-Sicherheitseinstellungen für Hyper-V
description: Beschreibt die Sicherheitseinstellungen, die in Hyper-V-Manager für virtuelle Maschinen der Generation 1 verfügbar sind
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f8f8c569-8b74-4c19-876e-1c7d00cce308
author: larsiwer
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 73cc2e45367d448aa736644e4a3bc02d3670fc6c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447913"
---
# <a name="generation-1-virtual-machine-security-settings"></a>Generation 1 VM-Sicherheitseinstellungen

>Gilt für: WindowsServer 2016 wird Microsoft Hyper-V Server 2016, WindowsServer 2019, Microsoft Hyper-V-Server 2019

Verwenden Sie die Sicherheitseinstellungen der Generation 1 VM im Hyper-V-Manager, zum Schutz der Daten und des Status eines virtuellen Computers.

## <a name="encryption-support-settings-in-hyper-v-manager"></a>Unterstützung der verschlüsselungseinstellungen im Hyper-V-Manager

Sie können die Daten und Status des virtuellen Computers zu schützen, indem Sie die folgenden Verschlüsselung Supportoption auswählen.

- **Verschlüsseln von Status und die VM-Migration-Traffic** -Status der virtuellen Maschine gespeichert verschlüsselt, wenn sie auf dem Datenträger und der live Migration-Traffic geschrieben werden.

Um diese Option aktivieren, müssen Sie ein Laufwerk Speichern von Schlüsseln für den virtuellen Computer hinzufügen.

## <a name="key-storage-drive-in-hyper-v-manager"></a>In Hyper-V-Manager-Schlüsselspeicher-Laufwerk

Ein Laufwerk Speichern von Schlüsseln bietet ein kleines Laufwerk mit dem virtuellen Computer für einen BitLocker-Schlüssel gespeichert werden. Dadurch wird der virtuelle Computer der Betriebssystem-Datenträger zu verschlüsseln, ohne dass einen virtualisierte Trusted Platform Module (TPM)-Chip. Der Inhalt des Laufwerks Schlüsselspeicher werden mithilfe einer Schlüsselschutzvorrichtung verschlüsselt. Der Schlüsselschutzvorrichtung Authories Hyper-V-Host, auf dem virtuellen Computer ausgeführt werden soll. Die Inhalte der das Speichern von Schlüsseln-Laufwerk und die Schlüsselschutzvorrichtung werden als Teil des Laufzeitstatus des virtuellen Computers gespeichert.

Zum Entschlüsseln der Inhalt des Laufwerks Schlüsselspeicher und den virtuellen Computer starten, muss der Hyper-V-Host sein:

- Teil einer autorisierten geschütztes Fabric für diese virtuelle Maschine, oder
- Haben Sie den privaten Schlüssel aus einem der Überwachungen des virtuellen Computers an.

Weitere Informationen zu geschützten Fabrics finden Sie im Abschnitt Einführung in abgeschirmte VMs in [Sicherheit und Zusicherungen](../../../security/Security-and-Assurance.md).

Sie können ein Laufwerk Speichern von Schlüsseln an einem leeren Steckplatz eines der VM IDE-Controller hinzufügen. Zu diesem Zweck klicken Sie auf **hinzufügen Schlüssel Speicherlaufwerk** ein Schlüsselspeicher-Laufwerk mit dem ersten kostenlose IDE-Controller-Steckplatz dieses virtuellen Computers hinzufügen.

## <a name="see-also"></a>Siehe auch

- [Generation 2 VM-Sicherheitseinstellungen in Hyper-V-manager](Generation-2-virtual-machine-security-settings-for-hyper-v.md)
- [Sicherheit und Zuverlässigkeit](../../../security/Security-and-Assurance.md)