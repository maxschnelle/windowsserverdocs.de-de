---
title: Sicherheitseinstellungen für virtuelle Computer der 2. Generation für Hyper-V
description: Beschreibt die Sicherheitseinstellungen, die im Hyper-V-Manager für virtuelle Computer der Generation 2 verfügbar sind
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 06ab4f5f-6b8e-4058-8108-76785aa93d4c
author: larsiwer
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 7eb867529d38ab21ee21c19f92c89ed4128b0ea4
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "80860803"
---
# <a name="generation-2-virtual-machine-security-settings-for-hyper-v"></a>Sicherheitseinstellungen für virtuelle Computer der 2. Generation für Hyper-V

>Gilt für: Windows Server 2016, Microsoft Hyper-V Server 2016, Windows Server 2019, Microsoft Hyper-V Server 2019

Verwenden Sie die Sicherheitseinstellungen für virtuelle Computer im Hyper-V-Manager, um die Daten und den Status eines virtuellen Computers zu schützen. Sie können virtuelle Computer vor Untersuchung, Diebstahl und Manipulation in Form von Malware, die auf dem Host ausgeführt wird, oder durch Administratoren des Rechenzentrums schützen. Das Maß an Sicherheit, das Sie erzielen können, hängt von der verwendeten Hardware, der Generation des virtuellen Computers und davon ab, ob Sie den als Host-Überwachungsdienst bezeichneten Dienst eingerichtet haben, der Hosts zum Starten von abgeschirmten virtuellen Computern autorisiert.  

Der Host-Überwachungsdienst ist eine neue Rolle in Windows Server 2016. Er identifiziert legitime Hyper-V-Hosts und erlaubt ihnen das Ausführen eines bestimmten virtuellen Computers. Im Normalfall werden Sie den Host-Überwachungsdienst für ein Rechenzentrum einrichten. Sie können aber auch einen abgeschirmten virtuellen Computer für die lokale Ausführung erstellen, ohne einen Host-Überwachungsdienst einzurichten. Später können Sie den abgeschirmten virtuellen Computer an eine Host Guardian Fabric verteilen.  

Wenn Sie den Host-Überwachungsdienst nicht eingerichtet haben oder ihn im lokalen Modus auf dem Hyper-V-Host ausführen und der Host über den Wächterschlüssel des Besitzers des virtuellen Computers verfügt, können Sie die in diesem Thema beschriebenen Einstellungen ändern.   Ein Besitzer eines Wächterschlüssels ist eine Organisation, die einen privaten oder öffentlichen Schlüssel erstellt und freigibt, sodass sich alle mit diesem Schlüssel erstellten virtuellen Computer in ihrem Besitz befinden.  

Informationen dazu, wie Sie die Sicherheit Ihrer virtuellen Computer mithilfe des Host-Überwachungsdiensts steigern können, finden Sie in den folgenden Ressourcen.  

- [„Harden the Fabric: Protecting Tenant Secrets in Hyper-V“ (Absichern der Fabric: Schützen geheimer Mandantendaten in Hyper-V) (Ignite-Video)](https://go.microsoft.com/fwlink/?LinkId=746379)
- [Geschützte Fabric und abgeschirmte VMs](https://go.microsoft.com/fwlink/?LinkId=746381)

## <a name="secure-boot-setting-in-hyper-v-manager"></a>Secure Boot-Einstellung im Hyper-V-Manager  

Secure Boot ist ein Feature, das für virtuelle Computer der 2. Generation verfügbar ist und die Ausführung von nicht autorisierter Firmware, nicht autorisierten Betriebssystemen oder nicht autorisierten UEFI-Treibern (Unified Extensible Firmware Interface, auch als Options-ROMS bezeichnet) zu verhindern hilft. Secure Boot ist standardmäßig aktiviert. Sie können secure Boot mit virtuellen Computer der 2. Generation verwenden, auf denen Windows- oder Linux-Distritutionsbetriebssysteme ausgeführt werden.  

Die in der folgenden Tabelle beschriebenen Vorlagen beziehen sich auf die Zertifikate, die Sie benötigen, um die Integrität des Hostprozesses zu überprüfen.  

|Vorlagenname|Beschreibung|  
|-----------------|---------------|  
|Microsoft Windows|Aktivieren Sie diese Option, um einen sicheren Systemstart des virtuellen Computers für ein Windows-Betriebssystem festzulegen.|  
|Microsoft UEFI-Zertifizierungsstelle|Aktivieren Sie diese Option, um einen sicheren Systemstart des virtuellen Computers für ein Linux-Verteilungsbetriebssystem festzulegen.|  
|Abgeschirmte Open Source-VM|Diese Vorlage wird für den sicheren Systemstart von [Linux-basierten abgeschirmten VMs](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-create-a-linux-shielded-vm-template) verwendet.|

Weitere Informationen finden Sie in den folgenden Themen.  

- [Sicherheitsübersicht für Windows 10](https://docs.microsoft.com/windows/security/threat-protection/overview-of-threat-mitigations-in-windows-10)  
- [Soll ich in Hyper-V einen virtuellen Computer der 1. oder der 2. Generation erstellen?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)  
- [Virtuelle Linux- und FreeBSD Computer unter Hyper-V](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)  

## <a name="encryption-support-settings-in-hyper-v-manager"></a>Einstellungen für die Verschlüsselungsunterstützung in Hyper-V-Manager

Sie können den Schutz von Daten und Status des virtuellen Computers unterstützen, indem Sie die folgenden Optionen für die Verschlüsselungsunterstützung auswählen.  

- **Trusted Platform Module aktivieren**: Diese Einstellung stellt auf Ihrem virtuellen Computer einen virtualisierten TPM-Chip (Trusted Platform Module) zur Verfügung. Dies ermöglicht es dem Gast, den Datenträger des virtuellen Computers mithilfe von BitLocker zu verschlüsseln.
  - Wenn auf Ihrem Hyper-V-Host Windows 10 1511 ausgeführt wird, müssen Sie den isolierten Benutzermodus aktivieren. 
- **Encrypt State and VM migration traffic** (Status- und VM-Migrationsdatenverkehr verschlüsseln): Verschlüsselt den Datenverkehr für den gespeicherten Status und die Livemigration des virtuellen Computers.

### <a name="enable-isolated-user-mode"></a>Isolierten Benutzermodus aktivieren

Wenn Sie **Trusted Platform Module aktivieren** auf Hyper-V-Hosts auswählen, die Windows-Versionen vor Windows 10 Anniversary Update ausführen, müssen Sie den isolierten Benutzermodus aktivieren. Auf Hyper-V-Hosts, die Windows Server 2016 oder Windows 10 Anniversary Update oder höher ausführen, ist dieser Schritt nicht erforderlich.

Der isolierte Benutzermodus ist die Laufzeitumgebung, die Sicherheitsanwendungen innerhalb des virtuellen abgesicherten Modus auf dem Hyper-V-Host hostet. Der virtuelle abgesicherte Modus wird verwendet, um den Status des virtuellen TPM-Chips zu schützen.  

Um den isolierten Benutzermodus auf Hyper-V-Hosts zu aktivieren, die frühere Versionen von Windows 10 ausführen,  

1.  Öffnen Sie die Windows PowerShell als Administrator.  

2.  Führen Sie die folgenden Befehle aus:  

    ```  
    Enable-WindowsOptionalFeature -Feature IsolatedUserMode -Online  
    New-Item -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Force  
    New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Name EnableVirtualizationBasedSecurity -Value 1 -PropertyType DWord -Force  

    ```  

Sie können einen virtuellen Computer mit aktiviertem virtuellem TPM auf jeden Host migrieren, der Windows Server 2016 oder Windows 10, Build 10586 oder höher, ausführt. Wenn Sie sie auf einen anderen Host migrieren, können Sie sie möglicherweise nicht starten. Sie müssen die Schlüsselschutzvorrichtung für den betreffenden virtuellen Computer aktualisieren, um den neuen Host zur Ausfühung des virtuellen Computers zu autorisieren. Weitere Informationen finden Sie unter [Geschützte Fabric und abgeschirmte VMs](https://go.microsoft.com/fwlink/?LinkId=746381) und [Systemanforderungen für Hyper-V unter Windows Server](../System-requirements-for-Hyper-V-on-Windows.md).  

## <a name="security-policy-in-hyper-v-manager"></a>Sicherheitsrichtlinie in Hyper-V-Manager  
Um bessere Sicherheit virtueller Computer zu erreichen, verwenden Sie die Option **Enable Shielding** (Abschottung aktivieren), um Managementfeatures wie Konsolenverbindungen, PowerShell Direct und bestimmte Integrationskomponenten zu deaktivieren. Wenn Sie diese Option aktivieren, werden die Optionen **Secure Boot**, **Trusted Platform Module aktivieren** und **Status- und VM-Migrationsdatenverkehr verschlüsseln** aktiviert und durchgesetzt.   

Sie können einen abgeschirmten virtuellen Computer lokal ausführen, ohne einen Host-Überwachungsdienst einzurichten. Wenn Sie sie auf einen anderen Host migrieren, können Sie sie möglicherweise nicht starten. Sie müssen die Schlüsselschutzvorrichtung für den betreffenden virtuellen Computer aktualisieren, um den neuen Host zur Ausfühung des virtuellen Computers zu autorisieren. Weitere Informationen finden Sie unter [Geschützte Fabric und abgeschirmte VMs](https://go.microsoft.com/fwlink/?LinkId=746381).  

Weitere Informationen zur Sicherheit in Windows Server finden Sie unter [Sicherheit und Zusicherungen](../../../security/Security-and-Assurance.md).  
