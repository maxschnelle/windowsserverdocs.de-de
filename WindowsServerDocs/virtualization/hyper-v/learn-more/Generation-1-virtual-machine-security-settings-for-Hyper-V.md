---
title: Sicherheitseinstellungen für virtuelle Computer der 1. Generation für Hyper-V
description: Beschreibt die Sicherheitseinstellungen, die im Hyper-V-Manager für virtuelle Computer der 1. Generation verfügbar sind
ms.topic: article
ms.assetid: f8f8c569-8b74-4c19-876e-1c7d00cce308
ms.author: benarm
author: BenjaminArmstrong
ms.date: 10/04/2016
ms.openlocfilehash: d7076056462e7fa3e822c49abfb37278f5ea3482
ms.sourcegitcommit: dd1fbb5d7e71ba8cd1b5bfaf38e3123bca115572
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90745995"
---
# <a name="generation-1-virtual-machine-security-settings"></a>Sicherheitseinstellungen für virtuelle Computer der 1. Generation

>Gilt für: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Verwenden Sie die Sicherheitseinstellungen für virtuelle Computer der 1. Generation im Hyper-V-Manager, um die Daten und den Status eines virtuellen Computers zu schützen.

## <a name="encryption-support-settings-in-hyper-v-manager"></a>Einstellungen für die Verschlüsselungsunterstützung in Hyper-V-Manager

Sie können den Schutz von Daten und Status des virtuellen Computers unterstützen, indem Sie die folgende Option für die Verschlüsselungsunterstützung auswählen.

- **Encrypt State and VM migration traffic** (Status- und VM-Migrationsdatenverkehr verschlüsseln): Verschlüsselt den gespeicherten Status des virtuellen Computers beim Schreiben auf den Datenträger und den Datenverkehr bei der Livemigration.

Um diese Option zu aktivieren, müssen Sie ein Schlüsselspeicher-Laufwerk für den virtuellen Computer hinzufügen.

## <a name="key-storage-drive-in-hyper-v-manager"></a>Schlüsselspeicher-Laufwerk im Hyper-V-Manager

Ein Schlüsselspeicher-Laufwerk stellt dem virtuellen Computer ein kleines Laufwerk zur Verfügung, auf dem ein BitLocker-Schlüssel gespeichert werden kann. Dieses ermöglicht es dem virtuellen Computer, seinen Betriebssystem-Datenträger zu verschlüsseln, ohne dazu einen virtuellen TPM-Chip (Trusted Platform Module) zu benötigen. Der Inhalt des Schlüsselspeicher-Laufwerks wird mithilfe einer Schlüsselschutzvorrichtung verschlüsselt. Die Schlüsselschutzvorrichtung autorisiert den Hyper-V-Host, den virtuellen Computer auszuführen. Sowohl der Inhalt des Schlüsselspeicher-Laufwerks als auch die Schlüsselschutzvorrichtung werden als Teil des Laufzeitzustands des virtuellen Computers gespeichert.

Um die Inhalte des Schlüsselspeicher-Laufwerks zu entschlüsseln und den virtuellen Computer zu starten, muss eine der folgenden Bedingungen auf den Hyper-V-Host zutreffen:

- Er muss Teil einer autorisierten geschützten Fabric für diesen virtuellen Computer sein oder
- Über den privaten Schlüssel eines der Wächter des virtuellen Computers verfügen.

Weitere Informationen zu geschützten Fabrics erhalten Sie im Abschnitt zur Einführung in abgeschirmte VMs in [Sicherheit und Zusicherung](../../../security/Security-and-Assurance.yml).

Sie können einem leeren Steckplatz auf einem der IDE-Controller des virtuellen Computers ein Schlüsselspeicher-Laufwerk hinzufügen. Klicken Sie dazu auf **Schlüsselspeicher-Laufwerk hinzufügen**, um dem ersten freien Steckplatz auf dem IDE-Controller des virtuellen Computers ein Schlüsselspeicher-Laufwerk hinzuzufügen.

## <a name="additional-references"></a>Weitere Verweise

- [Sicherheitseinstellungen für virtuelle Computer der 2. Generation in Hyper-V-Manager](Generation-2-virtual-machine-security-settings-for-hyper-v.md)
- [Sicherheit und Zuverlässigkeit](../../../security/Security-and-Assurance.yml)