---
title: Sicherheitseinstellungen für virtuelle Computer der Generation 1 für Hyper-V
description: Beschreibt die Sicherheitseinstellungen, die im Hyper-V-Manager für virtuelle Maschinen der Generation 1 verfügbar sind.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f8f8c569-8b74-4c19-876e-1c7d00cce308
author: larsiwer
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: ceb3c2628546815f9b0af35946e173f4276130d2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392791"
---
# <a name="generation-1-virtual-machine-security-settings"></a>Sicherheitseinstellungen für virtuelle Computer der Generation 1

>Gilt für: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Verwenden Sie die Sicherheitseinstellungen für den virtuellen Computer der Generation 1 im Hyper-V-Manager, um die Daten und den Zustand eines virtuellen Computers zu schützen.

## <a name="encryption-support-settings-in-hyper-v-manager"></a>Verschlüsselungs Unterstützungs Einstellungen in Hyper-V-Manager

Sie können zum Schutz der Daten und des Zustands des virtuellen Computers beitragen, indem Sie die folgende Verschlüsselungs Unterstützungs Option auswählen.

- **Verschlüsseln von Zustands-und Migrations Datenverkehr für virtuelle Computer** : verschlüsselt den gespeicherten Zustand der virtuellen Maschine beim Schreiben auf den Datenträger und den Datenverkehr für die Live Migration.

Um diese Option zu aktivieren, müssen Sie ein Schlüsselspeicher Laufwerk für den virtuellen Computer hinzufügen.

## <a name="key-storage-drive-in-hyper-v-manager"></a>Schlüsselspeicher Laufwerk im Hyper-V-Manager

Ein Schlüsselspeicher Laufwerk stellt dem virtuellen Computer ein kleines Laufwerk bereit, damit ein BitLocker-Schlüssel gespeichert wird. Dies ermöglicht es dem virtuellen Computer, seinen Betriebssystem Datenträger zu verschlüsseln, ohne dass ein virtualisierter Trusted Platform Module (TPM)-Chip erforderlich ist. Der Inhalt des Schlüsselspeicher Laufwerks wird mithilfe einer Schlüssel Schutzvorrichtung verschlüsselt. Die Schlüssel Schutzvorrichtung autorisiert den Hyper-V-Host, den virtuellen Computer auszuführen. Der Inhalt des Schlüsselspeicher Laufwerks und der Schlüssel Schutzvorrichtung werden als Teil des Lauf Zeit Zustands der virtuellen Maschine gespeichert.

Um den Inhalt des Schlüsselspeicher Laufwerks zu entschlüsseln und den virtuellen Computer zu starten, muss der Hyper-V-Host wie folgt lauten:

- Teil eines autorisierten geschützten Fabrics für diesen virtuellen Computer oder
- Sie müssen den privaten Schlüssel von einem der Wächter des virtuellen Computers haben.

Weitere Informationen zu geschützten Fabrics finden Sie im Abschnitt Introducing abgeschirmte VMS ( [Sicherheit und](../../../security/Security-and-Assurance.md)Sicherheit).

Sie können einem leeren Slot auf einem der IDE-Controller des virtuellen Computers ein Schlüsselspeicher Laufwerk hinzufügen. Klicken Sie hierzu auf **Schlüsselspeicher Laufwerk hinzufügen** , um dem ersten freien IDE-Controller Slot dieses virtuellen Computers ein Schlüsselspeicher Laufwerk hinzuzufügen.

## <a name="see-also"></a>Siehe auch

- [Sicherheitseinstellungen für virtuelle Computer der Generation 2 im Hyper-V-Manager](Generation-2-virtual-machine-security-settings-for-hyper-v.md)
- [Sicherheit und Zuverlässigkeit](../../../security/Security-and-Assurance.md)