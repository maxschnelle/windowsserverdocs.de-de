---
title: Unterstützte Windows 10-Sicherheitskonfigurationen für Remote Desktop Services VDI
description: Enthält Informationen zu unterstützten Konfigurationen für Windows 10-VDI mit RDS unter Windows Server 2016.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 10/27/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8f164f5d-a498-4f91-a12f-3e01d554f810
author: lizap
manager: dongill
ms.openlocfilehash: ff890150dcea30c425267dcaae9b1bdbc6d78b8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820081"
---
# <a name="supported-windows-10-security-configurations-for-remote-desktop-services-vdi"></a>Unterstützte Windows 10-Sicherheitskonfigurationen für Remote Desktop Services VDI

> Gilt für: Windows Server 2016

Windows 10 und Windows Server 2016 müssen neue Schutzebenen, die in das Betriebssystem zur ausführlicheren Schutz gegen sicherheitsverletzungen helfen, Angriffe zu blockieren, und verbessern die Sicherheit der VMs, Anwendungen und Daten erstellt.

> [!NOTE]
> Überprüfen Sie die [Remote Desktop Services unterstützt die Konfigurationsinformationen](rds-supported-config.md).

Die folgende Tabelle zeigt die neuen Features in einer VDI-Bereitstellung über RDS unterstützt werden

|  VDI-Auflistungstyp               |  In einem Pool zusammengefasste verwaltet |  Persönliche verwaltet |  Nicht verwaltete in einem Pool zusammengefasste                                     |  Nicht verwaltete personal                                    |
|-------------------------------------|------------------|--------------------|--------------------------------------------------------|--------------------------------------------------------|
| [Credential Guard](https://technet.microsoft.com/itpro/windows/keep-secure/credential-guard)                    | Ja              | Ja                | Ja                                                    | Ja                                                    |
| [Device Guard](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)                        | Ja              | Ja                | Ja                                                    | Ja                                                    |
| [Remote Credential Guard](https://technet.microsoft.com/itpro/windows/keep-secure/remote-credential-guard)             | Nein               | Nein                 | Nein                                                     | Nein                                                     |
| [Geschützte & Verschlüsselung unterstützte VMs](../../security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms.md) | Nein               | Nein                 | Die Verschlüsselung unterstützt virtuelle Computer mit zusätzlicher Konfiguration | Die Verschlüsselung unterstützt virtuelle Computer mit zusätzlicher Konfiguration |

## <a name="remote-credential-guard"></a>Remote Credential Guard:

Remote Credential Guard ist nur für direkte Verbindungen mit den Zielcomputern und nicht für diejenigen über Remote Desktop Connection Broker und RD-Gateway unterstützt.
> [!NOTE]
> Wenn Sie einen Verbindungsbroker in einer Umgebung mit Einzel-Instanz, und den Namen des Computers mit dem DNS-Namen übereinstimmt, können Sie Remote Credential Guard, verwenden können, obwohl dies wird nicht unterstützt.

## <a name="shielded-vms-and-encryption-supported-vms"></a>Abgeschirmte virtuelle Computer und Verschlüsselung unterstützte VMs: 

- Abgeschirmte VMs werden in Remote Desktop Services VDI nicht unterstützt. 

Für die Nutzung von Verschlüsselung unterstützte VMs:
- Verwenden Sie eine nicht verwaltete Sammlung und einer Bereitstellung Technologie außerhalb der Prozess der sammlungserstellung Remote Desktop Services, um die virtuellen Computer bereitzustellen. 
- Benutzerprofil-Datenträger werden nicht unterstützt, da sie differenzielle Datenträger benötigen 

